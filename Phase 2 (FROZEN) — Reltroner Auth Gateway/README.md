# 🔐 Reltroner Auth Gateway — Phase 2 (FROZEN)

**Project:** `reltroner-app-main`  
**Role:** Authentication Gateway  
**Identity Provider (IdP):** Keycloak  
**Phase Status:** ✅ **FROZEN** (Completed, Stable, and Archived)

---

## 📌 Phase Objective (Non-Negotiable)

**Phase 2 is not about building an authentication system.**  
It is about proving a **gateway pattern**.

Phase 2 exists **only** to prove that:

- Laravel **does not perform local authentication**
- Laravel acts purely as an **Auth Gateway**
- **All authentication authority belongs to Keycloak**
- Laravel only:
  - receives an `authorization_code`
  - exchanges it for tokens (`access_token`, `id_token`)
  - creates a **gateway session**
  - protects routes via middleware

> **Keycloak is the source of truth.  
> Laravel is a controlled gateway.**

---

## ❌ Explicitly Out of Scope (Phase 2)

Phase 2 **does not include**:

- ❌ User database design
- ❌ Laravel Auth guards
- ❌ Breeze / Fortify login flows
- ❌ Roles, permissions, RBAC
- ❌ Token persistence
- ❌ Multi-tenant logic
- ❌ Production hardening

Any appearance of these is considered **scope leakage**.

---

## 🧱 Architecture Overview

```

Browser
↓
reltroner-app (Laravel Gateway)
↓ redirect
Keycloak (Identity Provider)
↓ callback (authorization_code)
reltroner-app
↓ token exchange
Session Gateway Created
↓
Protected Dashboard

```

### Core Principle

```

Laravel   = Gateway
Keycloak  = Source of Truth

```

---

## 🔁 Authentication Flow (Detailed)

### 1️⃣ Entry Point
```

GET /
→ redirect → /dashboard

```

---

### 2️⃣ Gateway Protection
```

/dashboard
→ EnsureSSOAuthenticated middleware
→ redirect → /sso/login

```

---

### 3️⃣ Redirect to Keycloak
```

/sso/login
→ redirect to:
/realms/{realm}/protocol/openid-connect/auth

```

---

### 4️⃣ Authorization Code Callback
```

/sso/callback?code=XXXX

```

Laravel performs:
- validation of `code`
- exchange `code → access_token (+ id_token)`
- session creation

---

### 5️⃣ Authenticated Access
```

session(sso_authenticated === true)
→ dashboard allowed

````

---

## 🔑 Session Gateway Design

Session is **minimal and intentional**:

```php
session([
    'sso_authenticated' => true,
    'access_token'      => '...',
    'id_token'          => '...', // optional
]);
````

**There is deliberately:**

* no users table
* no passwords
* no guards
* no local identity

---

## 🛡 Middleware — `EnsureSSOAuthenticated`

```php
if (!session('sso_authenticated')) {
    return redirect()->route('sso.login');
}
```

### Registration (Kernel Alias)

```php
protected $middlewareAliases = [
    'sso' => \App\Http\Middleware\EnsureSSOAuthenticated::class,
];
```

This middleware defines the **gateway boundary**.

---

## 🚪 Logout Strategy (SSO-Correct)

Logout must invalidate **both**:

* Laravel gateway session
* Keycloak SSO session

```php
Route::get('/logout', function () {
    Session::flush();

    return redirect(
        config('services.keycloak.base_url')
        . '/realms/' . config('services.keycloak.realm')
        . '/protocol/openid-connect/logout'
        . '?redirect_uri=' . urlencode(url('/'))
    );
})->name('logout');
```

This preserves **SSO correctness**.

---

## 🧨 Major Bugs Encountered & Resolved

### 🧨 Bug #1 — Database Session Crash

**Error**

```
SQLSTATE[HY000] [2002] No connection could be made
```

**Root Cause**

```
SESSION_DRIVER=database
```

**Why It Failed**

* No database is intended for Phase 2

**Fix**

```
SESSION_DRIVER=file
```

---

### 🧨 Bug #2 — Missing Socialite Services Config

**Error**

```
Missing services entry for keycloak.client_secret
```

**Root Cause**

* Partial Socialite config
* Conflict with manual OIDC design

**Fix**

* Removed Socialite from runtime
* Switched to **manual OAuth2 flow**

---

### 🧨 Bug #3 — Middleware Alias Not Registered

**Error**

```
Target class [sso] does not exist
```

**Root Cause**

* Middleware created but not aliased

**Fix**

```php
protected $middlewareAliases = [
    'sso' => EnsureSSOAuthenticated::class,
];
```

---

### 🧨 Bug #4 — Phantom Route Reference in View

**Error**

```
Route [keycloak.logout] not defined
```

**Root Cause**

* Legacy route referenced in view

**Fix**

* Replaced with gateway `/logout`
* Cleared route & view cache

---

## 🧪 Current State Verification

| Component               | Status |
| ----------------------- | ------ |
| Keycloak Login          | ✅      |
| Authorization Code Flow | ✅      |
| Token Exchange          | ✅      |
| Session Gateway         | ✅      |
| Middleware Protection   | ✅      |
| Dashboard Access        | ✅      |
| Logout (SSO-correct)    | ✅      |
| No Database Dependency  | ✅      |

---

## 🟢 Phase 2 Status

```
PHASE 2 — AUTH GATEWAY
STATUS: 🔒 FROZEN
```

* Stable
* Deterministic
* Minimal
* Enterprise-correct

No further changes are allowed in this phase.

---

## 🚀 Next Phase (Not Implemented Yet)

### Phase 3 — SSO Consumer (`finance.reltroner.com`)

Planned scope:

* Token validation
* JWT introspection
* Trust `reltroner-app` as Auth Gateway
* **No direct Keycloak login**
* Zero duplication of auth logic

---

## 🧠 Final Note

Phase 2 **intentionally stops before complexity**.

This architecture mirrors:

* enterprise SSO gateways
* zero-trust entry points
* modular ERP ecosystems

If reviewed by a senior engineer,
**the architectural intent is immediately clear.**

---

**Author:** Reltroner
**Phase:** Auth Gateway — Phase 2
**Status:** 🔒 Frozen & Archived
