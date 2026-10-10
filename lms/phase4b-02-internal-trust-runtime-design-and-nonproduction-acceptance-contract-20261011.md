# Reltroner LMS — Phase 4B-02 Internal Trust Runtime Design & Nonproduction Acceptance Contract

> **Work order:** `LMS-P4B-02-DESIGN-20261011`  
> **Status:** **DESIGN CANDIDATE / OWNER REVIEW PENDING / CODE & RUNTIME NOT AUTHORIZED**. Owner instructed immediate design mapping before coding.  
> **Scope:** exact current six-service middleware map, OIDC-vs-workload identity contract, Redis replay/loss failure model, test matrix, acceptance and conditional next implementation plan. **Documentation-only**.  
> **GitHub evidence pins:** `Reltroner/LMS-BE/main=617dadc0d0d627071d713ceb729df6658202b43e`, `Reltroner/LMS-FE/main=eb01a4d2c924299b929aebf0f4826b94cf341fc6`, `Reltroner/progress-documentation/main=183372371b3a40a0349ac390848911273ccd2361` at design start, 2026-10-11 Asia/Jakarta. Do not assume those SHAs remain current later.  
> **Mandatory sources:** [Canonical README §7 clarity policy](./README.md), [FROZEN Phase 0C physical](./master-infrastructure-placement-contract.md), [FROZEN Phase 1 logical/API](./logical-service-boundary-api-contract.md), [ADR-LMS-TRUST-001 owner-ratified NONPROD DESIGN](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md), [identity provisioning ADR candidate](./adr-lms-kc-001-identity-provisioning-review-candidate.md), [4B-01 G03 E36](./phase4b-01-g03-adr-status-source-alignment-work-order-20261011.md), and the source-pinned contracts listed below.

## 1. Clarity-first introduction: what is being designed and why?

A **gateway** is the public entrance to LMS APIs, like a building reception desk; **middleware** is a series of security checkpoints before a request reaches a domain controller; **OIDC** is the protocol by which Keycloak authenticates a human; **workload assertion** is proof a microservice caller is trusted; **delegation assertion** is separately verified proof of the specific end-user, operation and capabilities the caller may represent; **Redis replay guard** prevents using a previously accepted signed request token twice. Authorization is enforced in **backend services**, not by hiding frontend UI.

**Goal:** For every initial user-bound call `Browser -> Gateway -> Learning`, the Gateway must independently verify the user's OIDC **access** token; the Learning service must independently authenticate the **calling workload**, validate **signed scoped end-user delegation**, enforce operation/recipient/client/capability/ownership binding and atomically reject repeated assertions **BEFORE any side effects**. For machine-only operations, workload authentication remains mandatory and there must be **no fabricated end-user**. The system must deny when a needed safety dependency is down or unknown.

**Current scope:** This is a versioned **design/acceptance candidate**. It does not implement new routes, middleware, Keycloak clients, signing keys, Redis keys, database roles, Nginx routing, worker processes or infrastructure. An acceptance matrix and an executable implementation are different artifacts; don't mark a test PASS until run against a real nonproduction HTTP flow.

## 2. Exact source-to-runtime middleware and route inventory (observed, NOT inferred)

At accepted BE `main` SHA `617dadc...`, inspected all six `services/{gateway,learning,mentorship,knowledge,assistant,audit}/bootstrap/app.php`, `routes/api.php`, their `app/Http/Middleware` directories, `routes/health.php` and feature-test directories.

| Service | Public/API role (frozen) | Middleware app directory, observed | Bootstrap and routing state | Trust implementation gap |
|---|---|---|---|---|
| `gateway` | Only **public** LMS API ingress; OIDC validation and caller signing | `RequestIdMiddleware.php` only | `RequestIdMiddleware::class` prepended; `api.php` contains only `<?php`; `/health/live`, `/health/ready` mapped; Laravel CORS middleware **not removed** in bootstrap | No OIDC/JWKS verifier, caller assertion signer, scoped delegation signer, service routing or business authz routes observed |
| `learning` | Private enrollment/progress/bookmarks owner | `RequestIdMiddleware.php` only | Same health and empty business API, but `HandleCors::class` removed | No private signed workload/delegation verifier, jti reservation, resource ownership enforcement |
| `mentorship` | Private offerings/booking owner | `RequestIdMiddleware.php` only | Same private CORS removal/empty API | No same service trust, booking/idempotency domain enforcement |
| `knowledge` | Private knowledge/search owner | `RequestIdMiddleware.php` only | Same private CORS removal/empty API | No same service trust/ACL enforcement |
| `assistant` | Private AI orchestration owner | `RequestIdMiddleware.php` only | Same private CORS removal/empty API | No same service trust, tool invocation capability gates |
| `audit` | Private audit/projection owner | `RequestIdMiddleware.php` only | Same private CORS removal/empty API | No same service trust/privileged mutation gate |

**Additional observed baseline:** Each `RequestIdMiddleware` accepts a syntactically valid incoming `X-Request-ID` UUID or generates one, attaches `request_id` and echoes it on response. This is **trace correlation, not authentication and not a trusted principal**. Each service has `HealthController.php` and a Problem Details response/error mapping; current `/health/ready` returns a static `ok` and **does not validate Redis replay readiness**. Feature tests exercise health, CORS/isolation, failure boundary and service surface; no trust-verifier middleware class is listed in the observed directories. Six `routes/api.php` files each have the same 6-byte PHP opening tag, **zero defined business routes in those files**.

**Observation scope limitation:** This is a direct GitHub directory/source inventory, not a completed local Laravel `route:list` execution, runtime web request, or full proof no alternative code is elsewhere. Don't claim an HTTP `404` against an unimplemented route proves authorization denial.

## 3. Source contract boundaries, ownership, and first integration slice

**Frozen public surface:** exactly 26 external operation method+path contracts and 19 capability names in BE `contracts/openapi/v1/openapi.json` and `contracts/authz/operation-policy.json`; 4 owned PostgreSQL DBs; no direct public access to five domain services. `GET /api/v1/learning/enrollments` = **API-02**, owner Learning, required client `lms-user`, capability `learning.enrollment.read.self`, actor binding `SIGNED_SUB_AND_RESOURCE_OWNER`. `GET /api/v1/me` = API-01 Gateway-only safe principal projection without invented extra capability. The initial provider path should be exercised with an isolated **test-only** representative route or approved API-02 integration skeleton, not introduced as a new public business route silently. Exact path allocation must be checked before coding.

**Example acceptance flow (PROPOSED implementation wiring; behavior must comply with frozen rules):**

```text
Browser (lms-user) -- Keycloak access JWT --> Gateway [only public API ingress]
  1. RequestId/correlation + strict ingress limits (not a trusted user header)
  2. Keycloak OIDC bearer JWT verifier: trusted issuer/JWKS/kid, aud=lms-api,
     exp/nbf, azp=lms-user, exact authorized capability and safe principal
     [OIDC signing-algorithm allowlist currently BLOCKED pending independent decision]
  3. Operation policy/owner and route-level authorization (API-02)
  4. Sign separate scoped workload identity + user delegation assertions
  5. Private HTTP JSON to Learning; never forward browser JWT as workload credential
                    |
                    v
Learning [loopback/private-only; no public DNS/interface]
  6. RequestId -> private boundary -> signed caller service verifier
  7. Independently validate signed end-user delegation for user-bound API-02
  8. Cross-assertion caller/recipient/operation/request_id/sub/capability consistency
  9. Redis atomic one-time jti reservations, including all relevant assertion proofs
 10. Authz capability intersection and owner-bound query (deny cross-user access)
 11. Only now dispatch authorized handler, then audit safely
```

**Machine-only service calls:** require verifiable caller workload identity, exact service/operation allowlist and **explicitly classified machine-only operation**, not an empty or forged user delegation. Do not create new permissions or service-only routes without a reviewed contract. Both private network routing and signed assertions are mandatory layers, never interchangeable.

**Authentication vs authorization:** invalid/missing signature, unknown `kid`, wrong issuer/audience/expired proof -> authentication denial; valid identity but insufficient capability/owner/operation -> authorization denial. A signed internal assertion is not permission to bypass resource ownership, administrative separation or audit obligations.

## 4. Binding identity and trust design vs proposals requiring decision

| Aspect | Status of authority | Exact contract / rejection rule |
|---|---|---|
| Human OIDC issuer | **FROZEN** | `https://auth.reltroner.com/realms/reltroner`; `aud=lms-api`; browser clients `lms-user` and `lms-admin`; access JWT only; no frontend role fallbacks |
| Keycloak OIDC signing algorithm(s) | **BLOCKED / NOT DETERMINED FROM REAL KEYCLOAK EVIDENCE** | BE source sentinel `BLOCKED_PENDING_SIGNED_3B02_CRYPTO_PARAMETER_ADR` is **not** Ed25519 runtime authorization. Need owner-approved distinct effective `alg`, JWKS trust and rotation observation; do not hard-code guessed RS256/EdDSA |
| Internal assertion algorithm/profile | **ADR-LMS-TRUST-001 RATIFIED — DESIGN ONLY** | JWS Compact EdDSA/Ed25519, protected `alg=EdDSA`, pinned per-caller `kid` registry, no token-header `jku/x5u`; private keys never in source |
| Identity/claim binding | **ADR RATIFIED** | `iss=lms-internal-trust`, `aud=lms-internal-services`, caller/recipient, operation, `request_id`, `principal_sub`, intersection of approved capability set and token-granted capabilities |
| JWS timestamp and rotation | **ADR RATIFIED** | `iat/nbf/exp` required, `exp-iat<=60s`, skew max 5s, rotation overlap max 180s, emergency revoked key immediately denied |
| Replay store | **ADR RATIFIED — DESIGN ONLY** | CSPRNG-produced `jti` with >=128-bit entropy; atomic one-use `SET NX PX` equivalent before side effects; TTL >= remaining exp plus skew; fail closed on unavailable/indeterminate store; outage/reset quarantine >=65s **after verified recovery** |
| Two independently validated logical proofs | **ADR RATIFIED** | Workload caller proof + signed scoped delegation for a user-bound operation. **Single combined synthetic JWS fixture does not fulfill real dual verification** |
| Exact on-wire two-assertion encoding/type/domain separation | **OWNER DESIGN DECISION REQUIRED (D02-01)** | Candidate: two independent JWS Compact tokens with distinct protected `typ`, independent `jti`, key scopes, explicit cross-binding and distinct HTTP header names. Do **not** treat these proposed header/type literals as frozen or let an IDE silently alter the original schema |
| Redis-loss detection/recovery observable trust anchor | **OWNER DESIGN DECISION REQUIRED (D02-02)** | Redis-only marker that disappears together with keys is **insufficient proof** of a past flush. Need independent loss/epoch detector plus verified recovery/quarantine and fault injection, or **stop and propose revised ADR**. Never silently fail open |
| Audit/error representation for infrastructure failure | **PROPOSED NOT NORMATIVE (D02-03)** | Public `401` invalid authentication, `403` valid principal but forbidden operation; **proposed `503` problem response** for Redis safety dependency unavailable, without granting access. Must verify exact existing OpenAPI/error contract before implementation; reason codes sanitized |
| Key custody, registry and OIDC integration | **OWNER DESIGN/OPERATOR DECISION REQUIRED (D02-04)** | Nonproduction ephemeral test-only keys isolated from production, separate key identity for caller/proof role, reviewable fingerprint and rotation; no real Keycloak client/token or production private key used for design tests |

**Important domain separation:** The current `trust-contract.json` encodes a `mode=dual_assertion` expectation and a combined required-claims inventory; `validate-trust-crypto.php` exercises **one** signed synthetic combined test object. The ADR explicitly requires independently validated logical controls. A versioned **wire-format/role separation design** and two-token negative tests are mandatory before code. A developer must not interpret existing one-token fixture PASS as two-token HTTP acceptance.

## 5. Detailed proposed runtime middleware placement and deterministic STOP behavior

The names below are **suggested implementation components**, not files that currently exist; a future coding PR needs its **own allowlist** and test approval.

| Order | Boundary / proposed component | Output on PASS | Fail-closed condition |
|---|---|---|---|
| P0 | Edge/Nginx only Gateway exposed | Only public Gateway receives browser traffic | Direct hit to service port/DNS denied by network layer, including IPv6 exposure |
| P1 | Gateway `RequestIdMiddleware` | Correlation ID; not principal identity | Do not promote `X-Request-ID` or any `X-User-Id` to trusted auth |
| P2 | Gateway `VerifyOidcAccessJwt` | Immutable verified JWT identity/context | No/malformed/ID token; wrong `iss`, `aud`, `azp`, expired, unpinned/unknown `alg/kid`; JWKS unavailable with no valid trusted key |
| P3 | Gateway `EnforceOperationPolicy` | Approved exact operation/client/capability/owner | Guest, wrong client, capability inflation or disabled operation denied; no fallback student |
| P4 | Gateway `CreateScopedInternalAssertions` | Fresh separately signed caller workload and bounded delegation proofs | Signing key absent/expired/unauthorized, clock/entropy errors, unapproved wire encoding, or unsupported user context -> no downstream call |
| P5 | Private provider `VerifyWorkloadAssertion` | Independently authenticated caller/service/recipient | Unknown caller/kid/fingerprint, altered alg/audience/recipient, missing signature -> deny |
| P6 | Private provider `VerifyDelegatedPrincipal` | Independently authenticated signed user delegation where required | Missing, unrelated, invalid/expired or principal/operation/capability mismatch -> deny; machine-only exception by explicit approved scope |
| P7 | Private provider `ReserveReplayProofs` | Atomic one-time jti reservations for relevant proofs | Duplicate, race lost, Redis timeout/loss, unknown replay epoch, partial uncertain result, quarantine active -> deny **before any controller side effect** |
| P8 | Private provider `EnforceProviderOwnership` | Bounded request context and owner-scoped query authority | Cross-sub/tenant/client/capability -> deny; provider never trusts user-supplied headers |
| P9 | Owner controller/domain write path | Only approved operation; domain-state authority remains owning PostgreSQL service | No direct cross-owner DB writes; idempotency and outbox separate from replay nonce |
| P10 | Response/error normalization and safe audit | Correlated, non-secret Problem Details and decision metadata | Do not leak JWS, access token, private key, Redis data, full PII or internal stack trace |

**Middleware ordering nuance:** Reserve replay **only after verifying signatures/claims/relationships**, but **before business side effects**. Two proof reservations must have well-defined atomic semantics; burning a nonce on a failed subsequent check is acceptable fail-closed behavior, but no handler must execute on partial reserve or uncertainty. The eventual request pipeline needs real tests that validate **execution ordering**. No current `api.php` business route exists to exercise these layers.

**Availability gate:** existing `/health/ready` currently returns static `ok`; it is not a real trust/Redis health check. A future private readiness policy should fail on unverifiable trust dependencies without disclosing detailed Redis internals to public callers. Do not change existing health behavior under this design-only phase.

## 6. Redis replay and failure-state machine (design candidate, STOP if unknown)

Redis 8 is **already used by production HRM/Keycloak workloads** on a shared 1-vCPU VPS. For this phase we do **NOT** access or mutate that Redis instance. Plan an isolated nonproduction Redis instance or deterministic fault-injection adapter with **no credentials or side effects on existing redis-server**.

| State | Trigger | Internal signed requests | Exit requirement |
|---|---|---|---|
| `COLD_UNVERIFIED` | Boot with unknown nonce state, missing independently trusted epoch or uncertain crash history | **DENY** | Observe independently trustworthy replay epoch and recovery proof |
| `HEALTHY_VERIFIED` | Epoch/source continuity established and atomic store healthy, no quarantine | May proceed **only after** all token, policy and atomic jti checks | Any timeout, unknown reply, reset/lost epoch -> `DENY_UNKNOWN` |
| `DENY_UNKNOWN` | Redis unreachable/auth failure/timeout, ambiguous SET reply, suspected keyspace loss, failover identity unknown | **DENY**; do not retry a possibly committed nonce as authorization | Wait for verified recovery and consistent epoch; don't assume Redis PING alone proves previous keys |
| `QUARANTINED` | Verified recovery after possible loss | **DENY** for >=65s monotonic elapsed after verified recovery; restart if evidence becomes uncertain | Revalidate epoch/health and elapsed quarantine, then reenable if no new anomaly |
| `REVOKED_OR_STOPPED` | Operator safety stop/compromised key/failed independent detector | **DENY** even if Redis responds PONG | New explicit security acceptance and owner-controlled recovery |

**Why 65s?** Maximum signed assertion lifetime 60s and allowed skew 5s; a replay keyspace loss may make old previously seen tokens appear unused, so merely reconnecting to Redis is unsafe. **Independent epoch detection is the unresolved hard problem.** A Redis-stored sentinel or memory-only timestamp by itself cannot prove no reset during process downtime, Redis failover or container replacement; if no dependable out-of-band detection and quarantine exists, `RUNTIME_ACCEPTANCE=BLOCKED` and no traffic routed to the new verifier. **This phase does not claim the solution is implemented.**

**Atomic logic (pseudocode, NOT an approved Redis command to run now):**

```text
deny unless: signatures, strict claims, caller/recipient/op/request_id,
             delegation, client/capability/owner binding all verified
deny unless: replay epoch independently verified and healthy
deny if quarantine active
for every independently verified proof requiring replay protection:
  atomic reserve opaque key(namespace + iss + caller + recipient + jti)
  with NX and PX >= remaining-expiry + skew
  if already exists, error, timed out, or reply indeterminate: DENY
deny unless: all required reservations returned authoritative success
only then: enter authorized controller/domain transaction
```

**Race/rollback consequences:** Two simultaneous uses of the *same* `jti`: only one can win. A failed request may still consume a nonce; clients must obtain a new signed assertion rather than reusing the old one. Redis replay guard is **not business idempotency**; booking retries require the separately governed durable idempotency record. No production Redis `FLUSH*`, `CONFIG SET`, `ACL`, `AUTH` bypass, restart or SSH operations permitted.

## 7. Nonproduction acceptance contract — deterministic gates

| ID | Expected evidence required to PASS | Current status |
|---|---|---|
| `B02-D01` | Verified BE/Docs SHA, frozen 20+24 invariant baseline, G03 E36 | **PASS SOURCE DISCOVERY** |
| `B02-D02` | Six bootstraps/middleware dirs/routes/health as observed, classified absent vs present | **PASS SOURCE DISCOVERY** |
| `B02-D03` | Exact 26 operation/19 capability projection, Gateway-only public and five private | **PASS CONTRACT READING** |
| `B02-D04` | OIDC issuer/aud/azp/alg/JWKS distinction; unknown effective OIDC algorithm explicitly BLOCKED | **PASS DESIGN CLASSIFICATION, OIDC ALGORITHM BLOCKED** |
| `B02-D05` | Owner approves exact two-assertion wire encoding, token type, separate key scopes and semantics | **PENDING OWNER D02-01** |
| `B02-D06` | Owner approves independently reliable Redis loss/epoch detection or revised ADR | **PENDING OWNER D02-02** |
| `B02-D07` | Nonproduction key custody/rotation/emergency revoke plan and safe test-only keys | **PENDING OWNER D02-04** |
| `B02-D08` | Source-aware middleware order + private ingress + no bypass in health/admin/guest paths | **DESIGN CANDIDATE** |
| `B02-D09` | Complete positive/negative real HTTP matrix with side-effect assertions and concurrency/outage | **TEST CONTRACT DRAFTED, NOT EXECUTED** |
| `B02-D10` | Every negative case has expected denial, reason category, response contract, no side effects, audit hygiene | **TEST CONTRACT DRAFTED, NOT EXECUTED** |
| `B02-D11` | Nonproduction isolated resources + budget + HRM/Keycloak no-mutation + rollback controls | **PENDING OWNER ENVIRONMENT PLAN** |
| `B02-D12` | Seven BE CI jobs, fixture + genuine HTTP tests, exact branch PR HEAD with production unchanged | **NOT EXECUTED FOR 4B-02** |
| `B02-D13` | Independent owner sign-off on this design and every unresolved proposed choice before coding | **PENDING OWNER FINAL** |
| `B02-D14` | Separate owner approval for any code change and later any runtime deployment | **NOT AUTHORIZED** |

**Never label `B02-D05/D06/D07/D09/D10/D11/D12/D13/D14` PASS from this documentation PR alone.** Current milestone can be `DESIGN_PACKAGE_PREPARED_FOR_OWNER_REVIEW`, **not** `DESIGN_RATIFIED`, `HTTP_VERIFIER_IMPLEMENTED`, `G03_RUNTIME_CLOSED` or `PRODUCTION_READY`.

### 7.1 Real HTTP/negative test matrix — portable separate source

See [Phase4B-02 negative/positive acceptance matrix](./phase4b-02-internal-trust-nonproduction-negative-test-matrix-20261011.md) for case IDs `T02-001...`, input perturbations, denial expectations and no-side-effect verification. Tests must be executable in future **isolated** Laravel HTTP integration and fault-injection environment. **No 404 from an absent route counts as verifying auth.** Each test must pin runtime environment + candidate SHA + fake key fingerprint + actual status/headers/body/audit outcome and unchanged domain persistence.

## 8. Strict future work decomposition — design first, coding only after gates

**Package P4B-02A (NOW):** documentation-only canonical design, exact inventory, cases, unresolved decision register and PR; no local script required to establish GitHub source inventory. Human owner reviews it.

**Package P4B-02B (FUTURE, permission required):** isolated source-only nonproduction unit and real Laravel HTTP integration harness for **workload assertion + delegation assertion** using temporary deterministic TEST keys (never commit a private production key) and in-memory replay fault adapter. Must not add routes to the frozen 26 public surface, relax OIDC policy or merge without CI/owner review.

**Package P4B-02C (FUTURE, independent approval):** isolated Redis 8 fault tests + independently trusted epoch detector / verified recovery quarantine, concurrency, key rotation/revoke and rollback; no existing VPS/HRM Redis mutations. **Cannot claim full nonproduction safety if loss detection has no credible implementation.**

**Package P4B-02D (FUTURE, distinct approval):** only after G09 Keycloak client/JWKS/OIDC algorithm design and nonproduction proof, integrate Gateway access JWT verifier and provider trust chain with exact API-02 proof, negative authn/authz and no-side-effects tests; retain separate production release gate.

**No automatic large-bang implementation:** Different service and layer PRs, no secret in Git, no guessing final Keycloak algorithm, no feature push to main, and no direct production code execution merely to make a checklist green. Maintain reversible feature PRs; production rollback procedures are not yet certified.

## 9. Owner decision register — resolve before implementation

| Decision | Required input | Conservative decision if not supplied |
|---|---|---|
| **D02-01 Two proof wire format** | Exact protected `typ` / proof headers, separate `iss/sub/kid/jti` namespaces, service-role keys, when user vs machine call applies, request binding; versioned compatibility strategy | **BLOCK CODING** of trust verifier to avoid inventing ambiguous credentials |
| **D02-02 Replay-loss/epoch trust anchor** | Independent restart/flush/failover evidence source, unambiguous verified recovery, monotonic >=65s quarantine; affordable isolated testing | **BLOCK any accept traffic**; design alternative/ADR review if no provable detector |
| **D02-03 Error response mapping** | Whether 503 for store unavailable and exact Problem Details `code` can be added without violating frozen OpenAPI/route requirements | Keep only category expectations, don't alter frozen contract unilaterally |
| **D02-04 Test key and environment boundary** | Nonproduction test key storage, fingerprint review, separate no-cost local Redis fault simulation, owner risk acceptance, 1-vCPU HRM protection | Prefer synthetic/in-memory nonproduction only; **NO live connection or new spend** |
| **D02-05 Effective OIDC algorithm/KC audience** | Fresh operator-approved read-only Keycloak JWKS/realm client/effective token verification and independent explicit alg allowlist decision | **BLOCK Gateway OIDC runtime** rather than copying internal EdDSA profile into JWT verifier |

**No fabricated owner ratification:** The new request authorizes **design and acceptance-contract drafting**, not acceptance of these new downstream implementation choices, nor any runtime deployment. Record owner decisions explicitly in a future dated append-only receipt.

## 10. Completion boundary, stop policy and handoff

**Design artifact delivery:** one canonical work order, one explicit 60+ case matrix (if actual file count verifies), README/ledger overlays via documentation-only PR; all anchored to G03 postmerge `617dadc...`, FROZEN contracts, ratified design ADR; factual/proposed/blocked fields never mixed. No PHP source code, CI, user laptop, credentials or VPS altered by this package.

**STOP if:** frozen owner/operation/capability semantics need changing; two assertions cannot be independently validated; no reliable Redis-loss detection; OIDC algorithm or Keycloak client existence presumed; other apps receive new public ingress; trust keys are placed in repo; desired test environment touches active HRM/Keycloak/Redis; a coder attempts to bypass tests or silently change 26 API operations. Any proposed deviation requires owner-reviewed new ADR/work order, not this document's implicit authority.

**Next user action:** Review the design candidate/decision register before authorizing a bounded Gemini IDE implementation; alternatively run a **read-only local PowerShell 5.1 inventory** that asserts the pinned BE main (not the older G03 worktree). Do not use the G03 worktree as if it were synchronized with current BE main: G03 squash merge created a different commit `617dadc...`, so any later code worktree must be based on that new exact SHA in a separate workspace.

**Current checkpoint:** `P4A_CLOSED -> P4B00_E32_PASS -> P4B01_G03_MERGED_CI_PASS -> P4B02_DESIGN_CANDIDATE -> WIRE_FORMAT_AND_REDIS_RECOVERY_DECISIONS_PENDING -> HTTP_CODE_NOT_AUTHORIZED -> PRODUCTION_NOT_AUTHORIZED`.
