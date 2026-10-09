# Reltroner LMS — Phase 3A-03C-2D Identity Provisioning Architecture Decision Record

**ADR ID:** `ADR-LMS-KC-001`  
**Version:** `review-candidate-1`  
**Date:** 2026-10-09 (Asia/Jakarta)  
**Review outcome:** `RECOMMENDED FOR SIGN-OFF / DESIGN REVIEW COMPLETE`  
**Governance status:** `NOT HUMAN-RATIFIED; NOT IMPLEMENTED; NO PRODUCTION MUTATION`  
**Parent phase:** `3A — Integration Discovery`; preceding evidence `3A-03C-2D-1 — ACCEPTED (read-only discovery)`  
**Next conditional gates:** ADR sign-off as part of 3A; 3B for versioned contract/tests; Phase 4 for controlled Keycloak provisioning.

## 0. What this ADR decides—and does not decide

The proposed logical identity architecture is explicit enough for architect/human sign-off and Phase 3B configuration specification. It does **not** authorize provisioning, migration, token retrieval, changing existing Keycloak objects, or making a production claim of security readiness. Runtime efficacy is proven only by future test evidence. The service-to-service workload assertion, audit reconciliation, frontend cutover and revocation freshness require separate ADRs and cannot be silently treated as accepted by this record.

**Decision shorthand:** `dedicated browser clients + lms-api resource client/roles + explicit audience + explicitly scope-limited access-token capabilities + preserve HRM unchanged + fail closed`.

## 1. Authoritative sources and pinned evidence

| Class | Evidence/source | Conclusion |
|---|---|---|
| Frozen logical contract | `Reltroner/progress-documentation/lms/logical-service-boundary-api-contract.md`, blob `cf089b8df4b5ccb1761b504ffae662a0053bf03e` | Binding issuer, browser clients, audience, capability namespace, Keycloak authority, no frontend authorization authority |
| Frozen placement contract | `Reltroner/progress-documentation/lms/master-infrastructure-placement-contract.md`, blob `b899761c9e833f9fa567055801b9ba0834ed56eb` | Independent origins; no broad subdomain session requirement; public Gateway/private services |
| Engineering ledger | `Reltroner/progress-documentation/lms/engineering-end-to-end-progress-ledger.md`, blob `866cc8c3b126ee6fae0cab8ac5160552cf41ad4a` | 3A read-only, 3B/4 future stage gates, 19 capabilities, explicit threats and negative tests |
| Backend implementation | `Reltroner/LMS-BE@e30a61780994d85671cbf079e6b9ce899b3fe837` | Six independent Laravel app foundations; empty domain `routes/api.php`; Gateway CORS allowlists two frontends |
| Frontend source | `Reltroner/LMS-FE@f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7` | `.env.example` legacy issuer/client; UX-only `student` default in `auth-roles.ts`; production FE env not verified |
| E-2A 03:27:37 UTC | read-only SQL | `reltroner` realm enabled; `lms-user`, `lms-admin`, `lms-api`, `lms-reltroner` absent within that realm |
| E-2B 03:31:11 UTC | read-only SQL + user Admin Console | `master=7` clients; `reltroner=8`; 8 client IDs agree between SQL/GUI; no LMS-like client cross-realm except unrelated `reltroner-realm` on master |
| E-2C 03:49:29 UTC | read-only SQL + GUI | 6 realm roles, 17 scopes, 37 mappers; shared `roles` scope: realm roles, client roles and audience resolve |
| E-2D1 04:00:59 UTC | read-only SQL | HRM clients each 12 scope associations; each `full_scope_allowed=false`, `public_client=false`; no directly attached protocol mappers |
| Issuer probe 03:07 UTC | external OIDC metadata via production VPS | exact canonical `iss=https://auth.reltroner.com/realms/reltroner`, discovery HTTP 200 |

**Observed existing roles:** `default-roles-reltroner`, `demo_user`, `production_user`, `service_account`, `offline_access`, `uma_authorization`; none grants the LMS capabilities by itself. **Observed HRM-specific scopes:** `hrm-demo-identity`, `hrm-production-identity`. **Unverified:** live LMS tokens (clients absent), installed Keycloak version, HRM effective token claim samples, current FE production OIDC env.

## 2. Decision drivers and exclusions

Drivers: conform to 20 infrastructure and 24 logical frozen invariants; independent public learner/admin trust contexts; avoid access-token privilege escalation; do not alter HRM; deterministic and testable `aud`, `azp` and role claims; easy rollback and no additional paid infrastructure; preserve Keycloak as identity authority.

Exclusions: Keycloak user/password/MFA replacement, browser-held Keycloak Admin credentials, new IAM product, shared LMS user database, changing built-in `roles` mapper or realm-wide defaults, changing existing `hrm-web`/`hrm-demo-web`, and new LMS admin role-edit privileges before audited adapter release.

## 3. Chosen target architecture (RECOMMENDED)

### 3.1 Three identities

| Identity | Purpose | Recommended properties | Explicit prohibitions |
|---|---|---|---|
| `lms-user` | Browser OAuth client for `https://lms.reltroner.com` | Public OIDC; standard Authorization Code ON; PKCE **S256 required**; exact callback `https://lms.reltroner.com/auth/callback`; dedicated allowed origin | client secret in browser; implicit grant; password/direct grants; service accounts; admin capability in learner access token |
| `lms-admin` | Browser OAuth client for `https://lms-admin.reltroner.com` | Independent public OIDC; code+PKCE S256; callback `https://lms-admin.reltroner.com/auth/callback`; dedicated allowed origin; `Full Scope Allowed=false` | admin entitlement by virtue of client ID; wildcard redirects; client secret; broad origin/cookie sharing |
| `lms-api` | OIDC resource identity + owner of 19 API capability client roles | Dedicated OIDC resource-server client; target `aud=lms-api`; no interactive browser flow or password grant; service accounts OFF initially | treating this client as a third learner surface; Keycloak Admin APIs exposed to frontend |

For **both** browser clients: `Full Scope Allowed=false`, explicitly restricted role scope mappings, no implicit/direct/resource-owner-password flows, service accounts OFF. Disable unneeded scopes such as `offline_access` until a specific use case/review proves necessary. Enforce exact redirects and web origins; add dev origins only in documented nonproduction settings, never wildcard production origins. OIDC RP-initiated logout URIs require exact review, not guessed. Confirm settings against the installed Keycloak version before configuration.

In newer Keycloak documentation `Full Scope Allowed` is marked deprecated, but disabling broad role visibility and explicitly specifying role scope mappings remains the security objective. Do not change global client policies solely for LMS without separately evaluating HRM impact.

### 3.2 Audience mechanism (chosen candidate)

**Choose an explicit, dedicated audience mapper** in an LMS-only OIDC client scope, proposed name `lms-api-audience`. Configure it to include `lms-api` in the **access token** of both LMS browser clients; link it as a **DEFAULT client scope only to** `lms-user` and `lms-admin`. Do not attach to HRM clients, realm-default scope template, or the built-in `roles` scope. Do not emit unnecessary audience into ID tokens.

Why: the built-in `audience resolve` mapper only derives `aud` when relevant client roles are effectively available. Even a user with zero granted LMS capabilities must be possible to authenticate without an inconsistent audience result; authorization must subsequently deny protected operations with 403. Dedicated mapper makes the intended resource audience stable independent of role assignments.

Accept string or array `aud` as permitted by JWT, but require membership/equality to exact `lms-api`; extra audiences never confer LMS privilege. The presence of audience is **not** an authorization decision. Validate authorized client separately.

### 3.3 Capability roles and claim contract (chosen candidate)

Exact **19** capability names are created as `lms-api` **client roles** (not realm roles and not ad hoc server constants). External protected API evaluates only explicit allowed values from the **access-token** claim `resource_access["lms-api"].roles` after cryptographic checks. This claim location is an implementation contract candidate; runtime example-token evaluation is a mandatory provisioning acceptance gate.

**6 Learning:**

- `learning.enrollment.read.self`
- `learning.enrollment.create.self`
- `learning.progress.read.self`
- `learning.progress.write.self`
- `learning.bookmark.read.self`
- `learning.bookmark.write.self`

**4 Mentorship:**

- `mentorship.offering.read`
- `mentorship.booking.read.self`
- `mentorship.booking.create.self`
- `mentorship.booking.cancel.self`

**2 Knowledge/Assistant:** `knowledge.search`, `assistant.use`.

**7 Admin:** `admin.principal.read`, `admin.principal.role.manage`, `admin.mentorship.read`, `admin.mentorship.manage`, `admin.learning.read`, `admin.learning.override`, `admin.audit.read`.

The 19 roles are a **namespace**, not 19 roles granted to every LMS account. A user's assignments and the client's allowed role scope mappings must both permit a capability. No role or claim inferred from `student`, `instructor`, `admin`, `production_user`, `demo_user`, `service_account` or frontend `RoleGate` may substitute for backend capability verification.

### 3.4 Effective scope isolation (chosen candidate)

Candidate dedicated client scopes:

| Scope name | Linked to | Assignment | Scope and content |
|---|---|---|---|
| `lms-api-audience` | `lms-user`, `lms-admin` | DEFAULT | Access-token Audience mapper for `lms-api` ONLY |
| `lms-learner-capabilities` | `lms-user` ONLY | DEFAULT | Explicit role scope mappings for the **12** nonadmin capabilities, subject to per-user role assignment |
| `lms-admin-capabilities` | `lms-admin` ONLY | DEFAULT | Explicit role scope mappings for **7** admin capabilities, subject to per-user role assignment |

Use the existing Keycloak `roles` mapper behavior to render effective client roles into `resource_access`, **without editing the shared built-in scope**. On both clients, turn off Full Scope Allowed and verify effective role scope mapping intersection in the *Evaluate* tab. Ensure no dedicated LMS scope is added as a realm default or to any HRM client. Check whether a scope with role scope mappings is omitted for users without matching roles and what effect that has on intended tokens.

Admin flows requiring particular nonadmin APIs require an **explicit contract-approved addition** of exactly the needed capability to admin scope; don't pregrant all learner actions just for convenience. Instructor privileged workflows live on admin origin but receive only the permissions needed. Public catalog and permitted guest offerings do not require granting an authenticated capability to every anonymous visitor; guest behavior is independently decided at endpoint layer.

**Allowed does not mean assigned:** A client-scoped role cannot enter an access token unless the subject is actually assigned that role (or inherits it through an explicitly approved group/composite mechanism). Avoid realm default roles that autoassign LMS admin; never grant `admin.*` by account registration.

### 3.5 Expected sanitized access-token claim shape (ILLUSTRATIVE, NOT OBSERVED)

Learner authorized for reading progress:

```json
{
  "iss": "https://auth.reltroner.com/realms/reltroner",
  "aud": ["lms-api"],
  "azp": "lms-user",
  "sub": "<redacted-test-subject>",
  "exp": 0,
  "resource_access": {
    "lms-api": {
      "roles": ["learning.progress.read.self"]
    }
  }
}
```

Here `exp: 0` is a **redacted placeholder**, not a sample valid token. Do not copy as live test fixture; validators require a future valid timestamp and signature. An authorized admin token similarly has `azp=lms-admin` plus actual assigned `admin.*` capability, **not** implied all 7 admin capabilities. No client secret, raw JWT, session cookie, private/public key material, user email or real subject ID belongs in handoff logs.

### 3.6 Gateway policy: deterministic checks

For every protected `/api/v1` operation: trusted issuer + JWKS signature with algorithm allowlist; token is access token of an accepted type/profile (verify actual Keycloak issued format; do **not** assume `typ=at+jwt` without evidence); `exp`, `nbf` if present and time tolerance bounded; `aud` contains `lms-api`; valid `azp` in approved browser client allowlist; required explicit `resource_access.lms-api.roles` capability. For admin operations add mandatory `azp=lms-admin`; nonadmin routes apply approved route/client allowlists rather than assuming universal client access. Missing capability => deny, do not default to student. Derive principal ID from signed `sub`. Enforce resource-owner checks **within owning service**, not solely Gateway.

Classification candidate: missing/invalid/expired token -> `401` with safe Problem Details; authenticated principal with insufficient rights/client context -> `403`; distinguish infrastructure/key fetch unavailable from invalid identity without fail-open. Exact final HTTP error taxonomy remains the Phase 3A API schema/3B contract gate; never invent successes.

No direct browser request to private Learning/Mentorship/Knowledge/Assistant/Audit services. CORS allowlist is **browser access behavior**, not a substitute for authentication/authorization. Maintain host-scoped credentials; avoid `Domain=.reltroner.com` cookies.

### 3.7 Internal service trust is explicitly NOT decided here

Gateway-to-service calls require authenticated **workload caller identity** AND a signed, short-lived, recipient- and operation-bound principal delegation. Service must validate caller, principal context and domain ownership. `X-Principal-ID`, `X-Roles`, `X-Permissions` or loopback alone are unacceptable. Assistant-to-domain delegation must be audience-bound. Token transport format, signing keys, replay control, clock skew, revocation, rotation and service-caller allowlists remain `ADR-LMS-INTERNAL-TRUST` **OPEN**; no silent adoption of a specific signing algorithm or key.

### 3.8 Role administration boundary

`PATCH /api/v1/admin/principals/{principal_id}/roles` cannot ship based on client provisioning alone. It requires the approved restricted Keycloak Admin API adapter (least privilege), authorization of the initiating principal, durable audit intent/outcome, retry/reconcile for ambiguous Keycloak result, prevention of self-escalation if required, and regressions. Never edit Keycloak database directly or share admin credentials with browser. This is `ADR-LMS-ADMIN-ROLE-OPERATIONS` OPEN.

## 4. Alternatives considered

| Candidate | Decision | Reason |
|---|---|---|
| One shared browser client for learner/admin | REJECT | Inconsistent with frozen separate-browser-client invariant and weak separation |
| Realm `production_user` as LMS permission | REJECT | Identity class is not app capability; risks privilege confusion |
| `lms-api` roles under client-role namespace | PREFERRED | Exact capability mapping and Keycloak resource identity, limited role scope |
| `audience resolve` alone | NOT PRIMARY | `aud` changes with effective role grants; more conditional behavior to prove |
| Explicit dedicated audience mapper for both LMS clients | PREFERRED | Predictable `aud=lms-api`; avoids changing shared scope |
| Change built-in `roles`/realm default scopes for LMS | REJECT | Potential impact to HRM clients in shared realm |
| Realm role for `student` implies all learner capabilities | REJECT | Fail-closed capabilities required; role-persona not authority |
| Bypass Keycloak and implement LMS passwords | REJECT | Violates frozen identity authority |
| Provision all now | REJECT FOR PHASE 3A | Read-only discovery gate, not runtime change authorization |

## 5. Threat, negative, and compatibility acceptance matrix

Every row: **SPECIFIED / NOT EXECUTED**. Tests require pinned environment, user role fixture, sanitized claim shape, actual request, status/result, timestamp and reviewer.

| Test ID | Condition / attempt | Required result |
|---|---|---|
| KC-T01 | `lms-user` authorization code without S256 PKCE | Reject |
| KC-T02 | `lms-admin` authorization code without S256 PKCE | Reject |
| KC-T03 | Implicit/password/direct access grant attempted against LMS clients | Reject |
| KC-T04 | Redirect to sibling, wildcard, unregistered or HTTP production URL | Reject |
| KC-T05 | Public browser clients contain secret/service account privilege | Reject config |
| KC-T06 | Legitimate learner access token | Correct `iss`, `aud=lms-api`, `azp=lms-user`, only actual permitted roles |
| KC-T07 | Legitimate admin with one allowed capability | `azp=lms-admin`, only granted admin capabilities; no blanket all-admin |
| KC-T08 | Same authorized admin subject authenticates via `lms-user` | No admin capability in learner-client access token |
| KC-T09 | Learner signs in through `lms-admin` and requests admin API | Deny 403; client name not permission |
| KC-T10 | Wrong `aud`, valid signature | Deny before domain call |
| KC-T11 | Wrong `azp`, valid signature/audience/capability | Deny per route client policy |
| KC-T12 | ID token passed as access token | Reject |
| KC-T13 | Forged/untrusted-signature, wrong issuer, expired token | Reject |
| KC-T14 | Missing capability / subject no roles | Deny; no default `student` privilege |
| KC-T15 | Client is allowed to expose a role but subject not granted role | No role in token; deny request |
| KC-T16 | `lms-user` allowed scope accidentally includes `admin.*` | Deployment BLOCKED |
| KC-T17 | LMS audience scope linked to `hrm-web` or `hrm-demo-web` | Deployment BLOCKED |
| KC-T18 | Guest offering endpoint accessed without token | Only as explicitly allowed by route policy; protected endpoints reject |
| KC-T19 | Cross-user learning/booking resource ID | Deny by service ownership rule |
| KC-T20 | Replayed/spoofed internal delegation | Reject in independent internal trust gate |
| KC-T21 | JWT JWKS rotation, missing key, Keycloak outage | Fail closed with documented cache/outage policy |
| KC-T22 | Capability revoked while old token remains valid | Enforced freshness/revocation policy; do not claim instant effect absent mechanism |
| KC-T23 | HRM scope assignment/mapper/role export before and after provisioning | Diff exactly zero for existing HRM objects |
| KC-T24 | HRM existing auth/login and authorization regression | PASS before and after rollout |
| KC-T25 | Keycloak role-admin mutation ambiguous result | No false success; durable audit/reconciliation (separate gate) |
| KC-T26 | Ingress token contains CORS-approved origin but no capability | Reject; CORS not authorization |
| KC-T27 | Realm default roles or shared `roles` mapper mutated | Deployment BLOCKED without separate contract authorization |
| KC-T28 | Actual `resource_access.lms-api.roles` and `aud` evaluated for both clients using test identities | Match schema and allowlist; no HRM-specific role/claim leakage |
| KC-T29 | Optional `offline_access` scope requested without authorization | No unintended offline access |
| KC-T30 | Revocation/missing-claim and request-ID error response | Sanitized Problem Details; no tokens/stack traces |

**Hard preproduction blockers:** KC-T06..T17, KC-T21, KC-T23, KC-T24, KC-T28 and any route-relevant negative tests. Full release acceptance additionally depends on all mandatory domain/service tests and separately signed ADRs.

## 6. Rollout/rollback order — for future approved Phase 4 ONLY

0. Complete review and accept this ADR as part of 3A; version config specification and test harness in 3B. Do NOT make live changes from this document alone.
1. During approved change window: verify installed Keycloak version, Admin Console permissions, production env, issuer/JWKS, HRM effective behavior; prepare access-controlled backup/export securely (never paste exported secrets) and tested restore/rollback method; capture scoped redacted baseline including HRM role/scope associations.
2. With approved Keycloak Admin API/GUI or reviewed automation, create a **new** disabled/unexposed `lms-api` resource client as appropriate; disable unneeded grants/service accounts; create **exactly 19** client roles; no global default grants.
3. Create dedicated `lms-api-audience`, `lms-learner-capabilities`, `lms-admin-capabilities` scopes; enforce exact role scope mappings; no HRM bindings and no mutation of default templates.
4. Create `lms-user` and `lms-admin`, strict public/code/S256/redirect/origin settings; explicitly disable unwanted flows, offline grants, Full Scope Allowed; attach only correct LMS-specific scopes.
5. Use Keycloak Client Scopes -> Evaluate with synthetic/nonproduction test identities and test role assignments; inspect **redacted claim structure only**; confirm audience and client-context isolation, including admin principal via learner client.
6. Compare HRM configuration scoped diff to frozen baseline and run HRM regression tests. If any HRM drift or client permissions mismatch: stop; disable/remove only newly created LMS entities with dependency-aware rollback; never wipe realm or HRM clients; follow documented backup restore procedure if necessary.
7. Only after Gateway JWT validation, internal auth, API tests and domain authorization are green, enable controlled FE OIDC cutover with independent learner/admin deployment and rollback; no production token accepted by unverified domain handler.
8. Evidence-based promotion and human approval: SHA, immutable config export hash (redacted), timestamp, actor, test results, before/after differences and rollback rehearsals.

**No package upgrade, OS reboot, DNS/TLS change, Keycloak mutation, Laravel code write, database migration, role assignment or production test-user creation is authorized by Phase 3A.**

## 7. RACI / decision owner and immutable constraints

| Deliverable/role | Decision ownership |
|---|---|
| Target identity contract and canonical requirements | Frozen Phase 0C/1 contracts; not subject to unilateral change |
| Design recommendation and threat analysis | ChatGPT architecture reviewer (this ADR) |
| Ratification / accepted ADR | User/project owner explicit approval after review |
| Keycloak provisioning implementation | Authorized operator in later controlled Phase 4 change window |
| Backend token validator and tests | IDE coding agent after accepted 3B spec/change scope; independently reviewed |
| HRM compatibility | Existing HRM production contract + observed baseline, no implicit modifications |
| Release readiness | Product DoD evidence reviewers, not inferred from source existence |

## 8. Unresolved dependencies (not blockers to design review; blockers to release as applicable)

| Ref | Remaining question | Completion evidence | Gate |
|---|---|---|---|
| KC-OPEN-01 | Exact installed Keycloak version and feature/UI semantics | version probe + admin UI screenshots, sanitized | Pre-implementation |
| KC-OPEN-02 | `lms-api` resource client exact flags/automation schema | reviewed config fixture and later Evaluate claims | 3B specification/Phase 4 |
| KC-OPEN-03 | Effective role scope algorithm and no HRM claim leakage | synthetic test token claim-shape matrix | Phase 4 |
| KC-OPEN-04 | Actual FE deployed OIDC env and separate admin-origin implementation | read-only CI/Cloudflare env metadata, no secrets | Frontend cutover |
| KC-OPEN-05 | Internal workload identity and delegated-principal assertion | separate signed ADR + forged/replay tests | Phase 4 |
| KC-OPEN-06 | Revocation freshness and JWKS outage rotation | explicit SLO/policy and negative tests | Phase 4 |
| KC-OPEN-07 | Restricted admin Keycloak adapter / audit uncertain outcome | separate signed ADR + reconciliation | Before role PATCH release |
| KC-OPEN-08 | Final error taxonomy/schema | OpenAPI + provider/consumer tests | Phase 3B |

## 9. Final review decision

- `3A-03C-2D-1`: **DISCOVERY ACCEPTED** (user-provided SQL/GUI evidence).
- `ADR-LMS-KC-001`: **RECOMMENDED FOR HUMAN SIGN-OFF**. The above identity provisioning design is internally consistent with the pinned frozen contracts on the reviewed requirements. Independent implementation and live token proof are not available, so **not** implementation-accepted.
- `3A-03C-2D`: **ARCHITECTURAL REVIEW COMPLETED; SIGN-OFF PENDING**.
- `3A`: **IN PROGRESS**; subsequent persistence/event, catalog and final DoD/traceability gates remain.
- `3B`: **NOT AUTHORIZED**.
- Production Keycloak/HRM/Gateway/FE modification: **NOT AUTHORIZED**.

## 10. Primary technical references

- Keycloak official Server Administration Guide: https://www.keycloak.org/docs/26.8.0/server_admin/ (role scope mappings, audience mapper and Client Scopes Evaluate; **not** evidence that this is installed runtime version).
- OAuth 2.0 Security Best Current Practice: https://www.rfc-editor.org/rfc/rfc9700
- JWT Best Current Practices: https://www.rfc-editor.org/rfc/rfc8725
- JWT Access Token Profile: https://www.rfc-editor.org/rfc/rfc9068 (token type/profile compatibility must be tested rather than assumed).
- Frozen GitHub contracts and user-supplied runtime evidence listed in §1.

---

_Extracted without semantic changes from historical combined source `reltroner-lms-phase3a-03c-2d-provisioning-adr-review-20261009.md` (blob `c2296c0c3e142843dd8a986570dea2e850958e36`). Review candidate, **NOT owner-ratified**. Do not infer production implementation._
