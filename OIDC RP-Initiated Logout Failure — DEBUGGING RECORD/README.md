# 🧾 DEBUGGING RECORD

# OIDC RP-Initiated Logout Failure

**Project:** Reltroner ERP Gateway
**Phase:** 2 (FROZEN)
**Layer:** Auth Gateway → OIDC (Keycloak)
**Severity:** Medium (Flow-Breaking)
**Security Impact:** None
**Status:** ✅ Resolved
**Architecture Integrity:** Preserved

---

# I. Executive Summary

Logout flow failed with:

```
Invalid redirect uri
```

Keycloak returned:

```
HTTP 400
```

The failure:

* Did NOT compromise authentication
* Did NOT affect signing logic
* Did NOT affect trust boundaries
* Did NOT affect Phase 3 or Finance module

Root cause was:

> Literal mismatch between `post_logout_redirect_uri` and Keycloak whitelist.

This was a protocol-level compliance issue, not a security defect.

---

# II. Symptom Overview

When user clicked logout:

* Browser remained on page
* Keycloak displayed error page
* Network tab showed:

```
GET /realms/reltroner/protocol/openid-connect/logout → 400
```

Laravel log showed:

```
LOGOUT CONTROLLER EXECUTED
Logout redirect target {"post_logout_redirect_uri":"http://app.reltroner.test:8000/logged-out"}
```

However, actual request differed.

---

# III. Root Cause Analysis (Sequential)

---

## Step A — Middleware Suspicion ❌

Initially suspected:

* Middleware interception
* Session auto-refresh
* Breeze conflict

Findings:

* Logout controller executed
* Redirect issued
* No guard interference
* Laravel not acting as auth authority

Conclusion:

Middleware not responsible.

---

## Step B — Route Conflict ❌

Executed:

```bash
php artisan route:list | findstr logout
```

Found Breeze route override:

```
POST logout → Auth\AuthenticatedSessionController@destroy
```

### Fix

Explicit override after `auth.php` registration:

```php
Route::post('/logout', [SSOController::class, 'logout'])
    ->name('logout');
```

Route conflict resolved.

However, 400 error persisted.

---

## Step C — Network Inspection ✅ (Turning Point)

Browser DevTools → Network → Logout request

Observed:

```
post_logout_redirect_uri=http://app.reltroner.test:8000/logout
```

Keycloak whitelist contained:

```
http://app.reltroner.test:8000/logged-out
```

OIDC requires:

> Exact literal string match.

Mismatch caused rejection.

---

# IV. Definitive Root Cause

Controller used:

```php
'post_logout_redirect_uri' => route('logout'),
```

Which resolved to:

```
/logout
```

Keycloak whitelist expected:

```
/logged-out
```

OIDC RP-Initiated Logout specification mandates exact match.

No wildcard.
No prefix tolerance.
No partial match.

---

# V. Phase-Compliant Fix

## Controller Correction

```php
$postLogoutRedirect = route('logged.out');

$query = http_build_query([
    'id_token_hint'            => $idToken,
    'post_logout_redirect_uri' => $postLogoutRedirect,
    'client_id'                => config('services.keycloak.client_id'),
]);
```

---

## Route Addition

```php
Route::get('/logged-out', [SSOController::class, 'loggedOut'])
    ->name('logged.out');
```

---

## Keycloak Whitelist

Already contained:

```
http://app.reltroner.test:8000/logged-out
```

No Keycloak change required.

---

# VI. Corrected Execution Flow

```
POST /logout
↓
SSOController@logout
↓
Redirect → Keycloak logout endpoint
↓
Keycloak validates id_token_hint
↓
Keycloak validates post_logout_redirect_uri (exact match)
↓
Redirect → /logged-out
↓
Laravel invalidates session
↓
Redirect → /sso/login
```

---

# VII. Architectural Integrity Check

### Phase 2 (Auth Gateway)

✔ Laravel not auth authority
✔ Minimal session semantics
✔ No guard introduced

---

### Phase 3 (SSO → Finance)

✔ Signing algorithm untouched
✔ HS256 TTL untouched
✔ Trust boundary intact

---

### Phase 4 (Finance UI)

✔ No controller modification
✔ No route contract change
✔ No Blade modification

---

# VIII. Senior-Level Lessons

1. OIDC logout requires exact URI literal match.
2. Route names are not redirect URIs.
3. Always inspect actual network query string.
4. Backend log output ≠ actual outbound request.
5. SSO debugging must prioritize browser network trace.

---

# IX. Final Status

```
LOGOUT FLOW
STATUS: STABLE
OIDC COMPLIANT: YES
ARCHITECTURAL VIOLATION: NONE
FREEZE STATUS: INTACT
```

---

---

# 🧾 DEBUGGING RECORD

# ID Token Verification Failure (Clock Skew)

**Project:** Reltroner ERP Gateway
**Phase:** 2 (FROZEN)
**Layer:** OIDC ID Token Verification
**Severity:** High (Authentication Blocking)
**Security Impact:** None
**Status:** ✅ Resolved
**Architecture Integrity:** Preserved

---

# I. Executive Summary

Login failed during callback.

Error:

```
Cannot handle token with iat prior to 2026-03-03T07:13:03+00:00
```

Root cause:

> Clock skew between Laravel host and Keycloak container.

This was not:

* A JWT signature failure
* A cryptographic defect
* A claim validation bug
* A Keycloak misconfiguration

It was:

> Distributed system time synchronization variance.

---

# II. Error Meaning

JWT claim:

```
iat (issued at)
```

Laravel server time differed slightly from Keycloak time.

Firebase/php-jwt default tolerance:

```
0 seconds
```

Even 1-second drift can cause rejection.

---

# III. Root Cause

Keycloak container time:

```
T1
```

Laravel (Windows host) time:

```
T2
```

T1 ≠ T2.

JWT library rejected token because:

```
iat > server_time
```

Strict validation triggered.

---

# IV. Why This Is Critical

Without clock tolerance:

* Docker environments fail
* CI pipelines fail
* Multi-node cluster fail
* Distributed systems unstable

Clock skew tolerance is standard OIDC best practice.

---

# V. Location of Fix

File:

```
app/Services/SSO/KeycloakIdentityService.php
```

Method:

```php
verifyIdToken(string $idToken)
```

---

# VI. Phase-Safe Correction

Before decoding:

```php
JWT::$leeway = 60;
```

Then:

```php
$decoded = JWT::decode(
    $idToken,
    JWK::parseKeySet($jwks)
);
```

---

# VII. Why 60 Seconds?

* Industry standard
* Safe margin
* Does not weaken signature validation
* Does not alter exp validation logic
* Does not alter issuer/audience
* Does not modify TTL

It only tolerates distributed clock drift.

---

# VIII. Corrected Method (Stable Version)

```php
public function verifyIdToken(string $idToken): array
{
    try {

        // Clock skew tolerance (distributed system safety)
        JWT::$leeway = 60;

        $jwks = $this->fetchJwks();

        $decoded = JWT::decode(
            $idToken,
            JWK::parseKeySet($jwks)
        );

        $payload = (array) $decoded;

        $this->validateClaims($payload);

        return $payload;

    } catch (Exception $e) {
        Log::error('ID Token verification failed', [
            'error' => $e->getMessage(),
        ]);

        throw new Exception('Invalid ID token.');
    }
}
```

---

# IX. Architectural Compliance

### Phase 2

✔ Laravel still not identity authority
✔ Cryptographic verification preserved
✔ No bypass introduced

---

### Phase 3

✔ HS256 internal signing untouched
✔ TTL untouched
✔ Gateway trust untouched

---

### Phase 4

✔ No UI modification
✔ No routing modification

---

# X. Security Analysis

Leeway does NOT:

* Skip signature verification
* Skip issuer validation
* Skip audience validation
* Skip expiration validation

It only:

> Adjusts iat/nbf boundary tolerance.

Security boundary remains intact.

---

# XI. Principal-Level Insight

This was not:

* A Laravel bug
* A Keycloak bug
* A JWT bug

It was:

> Distributed system time synchronization assumption failure.

The correct solution:

* Minimal
* Standard-compliant
* Phase-safe
* Architecture-preserving

---

# XII. Final Status

```
ID TOKEN VERIFICATION
STATUS: STABLE
CLOCK SKEW HANDLED: YES
DISTRIBUTED SAFE: YES
ARCHITECTURE INTACT: YES
FREEZE STATUS: PRESERVED
```

---

Both incidents are now formally documented and governance-compliant.

No freeze revoke required.
No trust boundary change introduced.
System remains architecturally stable.
