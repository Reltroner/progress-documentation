# 🧾 OFFICIAL DEBUG REPORT

# OpenSSL RSA Failure in `KeycloakIdentityServiceTest`

**Project:** Reltroner Gateway

**Subsystem:** SSO → JWT Verification → OpenSSL

**Severity:** High (Cryptographic Blocking Failure)

**Impact:** Test suite blocked (JWT signing & verification unusable)

**Status:** ✅ Fully Resolved

**Methodology:** Principal Engineer Layered Isolation Strategy

**Architecture Integrity:** Preserved

**Repository:** [https://github.com/Reltroner/reltroner-app-main](https://github.com/Reltroner/reltroner-app-main)

---

# I. Executive Summary

`KeycloakIdentityServiceTest` failed due to **three distinct failures occurring sequentially across different architectural layers**, each producing similar cryptographic error messages.

The failures were:

1. OpenSSL 3 provider not activated (Environment Layer)
2. Corrupted private key in test fixture (Data Integrity Layer)
3. Algorithm mismatch between encode and decode (Contract Layer)

Because all three surfaced as cryptographic validation errors, the issue initially appeared as a single systemic crypto failure.

In reality:

> Three separate defects
> Three separate layers
> One misleading symptom

---

# II. Initial Symptom

Running:

```bash
php artisan test
```

Produced failure:

```
Tests\Domain\SSO\KeycloakIdentityServiceTest
```

Primary error:

```
DomainException: OpenSSL unable to validate key
```

Stack trace location:

```
vendor/firebase/php-jwt/src/JWT.php:272
openssl_pkey_get_private($key)
```

---

# III. Misleading Indicators

The error originated inside `firebase/php-jwt`, which could falsely imply:

* JWT library defect ❌
* Laravel defect ❌
* JWK parsing defect ❌

Actual classification:

> Crypto engine-level failure.

Framework was not the root cause.

---

# IV. Debugging Methodology Applied

Instead of trial-and-error key rotation or code rewrites, the following strategy was applied:

> Stop modifying application code.
> Stop rotating keys randomly.
> Audit by isolation layer.

Layer isolation order:

1. Crypto engine
2. Key integrity
3. JWT algorithm contract
4. Application service logic

---

# V. PHASE 1 — OpenSSL Isolation (Outside Laravel)

## Objective

Validate OpenSSL behavior independently from Laravel and JWT.

## Implementation

Created folder:

```
crypto-debug/
```

Test script executed:

```php
openssl_pkey_new()
openssl_pkey_export()
openssl_pkey_get_private()
```

## Result

```
openssl_pkey_export(): Cannot get key from parameter 1
openssl_pkey_get_details(): Argument must be OpenSSLAsymmetricKey, false given
```

Interpretation:

> RSA key generation failing at engine level.

Conclusion:

Problem existed before Laravel and before JWT.

---

# VI. PHASE 2 — OpenSSL Environment Audit

Command:

```bash
php --ri openssl
```

Output:

```
OpenSSL support => enabled
OpenSSL Library Version => OpenSSL 3.0.15
Openssl default config => C:\Program Files\Common Files\SSL/openssl.cnf
```

Critical issue:

Config path did not exist.

---

# 🎯 Root Cause #1 — OpenSSL 3 Provider Not Activated

OpenSSL 3 uses a provider-based architecture.

Without valid configuration:

* Extension shows as enabled
* Provider not activated
* RSA algorithm unavailable
* Crypto calls silently fail

This was an environment misconfiguration.

---

# VII. PHASE 3 — Provider Activation Fix

Created minimal config:

`crypto-debug/openssl_local.cnf`

```ini
openssl_conf = openssl_init

[openssl_init]
providers = provider_sect

[provider_sect]
default = default_sect

[default_sect]
activate = 1
```

Set environment variable:

```powershell
setx OPENSSL_CONF "C:\laragon\www\reltroner-app-main\crypto-debug\openssl_local.cnf" /M
```

Restarted terminal.

Verification:

```bash
php --ri openssl
```

Isolation script re-run:

```
object(OpenSSLAsymmetricKey)#1 (0) {}
```

Crypto engine confirmed operational.

---

# VIII. PHASE 4 — Key Integrity Audit

After engine repair, error persisted.

Inspection revealed:

* Private key embedded via heredoc
* Key truncated
* Base64 block incomplete
* Not valid 2048-bit RSA

Error reproduced:

```
OpenSSL unable to validate key
```

---

# 🎯 Root Cause #2 — Corrupted Private Key

Failure shifted from engine-level to data integrity-level.

Problem was:

> Invalid RSA test fixture.

---

# IX. PHASE 5 — Deterministic Key Strategy

Removed heredoc key usage.

Generated valid keys via isolation layer:

```
crypto-debug/private.pem
crypto-debug/public.pem
```

Copied to:

```
tests/Fixtures/
```

Updated test:

```php
file_get_contents(base_path('tests/Fixtures/private.pem'))
```

Benefits:

* No CRLF issues
* No invisible characters
* No truncation
* Deterministic formatting
* Clear separation of test data

---

# X. PHASE 6 — Algorithm Contract Violation

After key correction, new error appeared:

```
UnexpectedValueException: Incorrect key for this algorithm
```

Investigation revealed:

Encode:

```
RS256
```

Decode:

```
HS256
```

---

# 🎯 Root Cause #3 — Algorithm Mismatch

HS256 = Symmetric HMAC
RS256 = Asymmetric RSA

Token signed with RS256 cannot be verified with HS256.

This was a contract violation.

---

# XI. Final Correction

Changed:

```php
new Key($publicKey, 'HS256')
```

To:

```php
new Key($publicKey, 'RS256')
```

---

# XII. Final Result

```
Tests: 39 passed
Assertions: 88
Duration: 2.89s
```

Full cryptographic compliance restored.

---

# XIII. Root Cause Summary

| Layer       | Issue                               | Type           |
| ----------- | ----------------------------------- | -------------- |
| Environment | OpenSSL 3 provider not activated    | Configuration  |
| Data        | Private key corrupted               | Integrity      |
| Contract    | Algorithm mismatch (RS256 vs HS256) | Implementation |

Three independent issues.
One shared symptom.

---

# XIV. Final System State

SSO layer now:

* RSA-based
* OpenSSL provider-configured
* Deterministic file-based key fixtures
* Strict RS256 contract
* Fully passing test suite
* Isolation debug strategy documented

---

# XV. Permanent Safeguards

1. `OPENSSL_CONF` permanently configured.
2. All crypto tests use file-based fixtures.
3. No heredoc private keys permitted.
4. Encode/decode algorithm explicitly enforced.
5. `crypto-debug/` retained for isolation diagnostics.
6. Recommendation: execute crypto tests in Linux CI for environment parity.

---

# XVI. Engineering Lessons

### 1️⃣ OpenSSL "enabled" does not mean RSA usable.

Provider activation determines algorithm availability.

---

### 2️⃣ Always isolate crypto outside framework first.

Framework-level debugging misleads if engine is broken.

---

### 3️⃣ Never use heredoc for RSA private keys.

Use file fixtures for determinism and clarity.

---

### 4️⃣ Multi-layer failures can mimic a single defect.

Layered isolation prevents debugging loops and architectural overcorrection.

---

# XVII. Governance Conclusion

This incident:

* Did not affect production runtime
* Did not weaken cryptographic guarantees
* Did not alter trust boundaries
* Did not require architecture revision

Resolution preserved:

* SSO design
* JWT verification integrity
* RS256 contract enforcement
* Deterministic test behavior

---

**Status:** CLOSED
**Crypto Engine:** Healthy
**Test Suite:** Stable
**Architecture:** Intact
**Freeze Impact:** None
