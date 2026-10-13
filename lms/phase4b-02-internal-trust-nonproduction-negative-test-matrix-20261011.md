# Reltroner LMS Phase 4B-02 — Real HTTP / Redis Fault Injection Acceptance Matrix

> **Machine-readable handoff by stable test IDs:** `LMS-P4B-02-T02-MATRIX-20261011`.  
> **Status:** **DESIGN-ONLY TEST CONTRACT DRAFT; ZERO TESTS EXECUTED**. Required before actual trust middleware coding or any nonproduction runtime acceptance.  
> **Sources:** [Phase 4B-02 design/work order](./phase4b-02-internal-trust-runtime-design-and-nonproduction-acceptance-contract-20261011.md), [FROZEN Phase 1](./logical-service-boundary-api-contract.md), [ADR-LMS-TRUST-001](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md).  
> **Source pin:** BE `main=617dadc0d0d627071d713ceb729df6658202b43e`, docs `main=183372371b3a40a0349ac390848911273ccd2361` at drafting; implementation PR SHAs must be refreshed.  
> **Evidence type:** proposed acceptance scenarios, **not** existing fixtures, verified HTTP handlers or runtime PASS.

## 1. Why this matrix and how a novice should read it

Each **T02 test ID** represents a behavior the future system must prove after coding in an **isolated nonproduction** runtime. `ALLOW` means the exact valid cryptographic, identity, resource and replay preconditions must be satisfied **before** handler dispatch; `DENY_*` means security must prevent any unauthorized side effects; `FAIL_*` indicates a system safety assertion that must never be observed; `INVALID_TEST_PROOF` indicates a misleading test such as receiving `404` because the route doesn't exist.

**DO NOT equate** existing six Laravel routes/api.php skeletons, a simulated `signature_verified=true` fixture, a static `/health/ready=ok` response or synthetic Ed25519 one-token test with genuine dual-assertion HTTP verification.

**Proposed HTTP response grouping, not a frozen status contract:** malformed/invalid authentication `401`; cryptographically authenticated but forbidden capability/owner `403`; unavailable/unknown Redis safety state `503` *candidate* with sanitized Problem Details and no processing. Network isolation denial may occur below HTTP. Exact `503`/new reason codes require D02-03 owner approval and compatibility review. Labels like `DENY_AUTHN` classify *security semantics*, not a commitment to emit that particular code in every internal transport.

## 2. Matrix totals by threat boundary

| Area | Test cases |
|---|---:|
| OIDC Gateway: token validation and client boundary | 16 |
| Workload assertion: caller proof independently verified | 14 |
| Delegated principal: independent user-bound proof and policy | 14 |
| Redis replay, concurrency and recovery fail-closed | 22 |
| Private routing, error hygiene, and server invariants | 10 |
| Rotation, operational continuity and anti-regression | 10 |
| **TOTAL planned** | **86** |

All cases below are **PENDING EXECUTION**. Reuse these identifiers in future unit, Laravel HTTP, Redis fault injection, and CI reports. A case is PASS only with precise test runner output, runtime SHA, fixture/key fingerprint, expected/actual statuses, and instrumentation that proves authorization middleware executed before any side effect.

## 3. Exhaustive scenario register

| ID | Manipulation / expected stimulus | Expected security disposition | Evidence that must be asserted |
|---|---|---|---|
| `T02-001` | valid signed learner access JWT for approved API-02 | `ALLOW` | Verified OIDC alg/JWKS/aud/azp/sub + exact cap, no mere fixture booleans |
| `T02-002` | valid signed admin access JWT for approved admin context | `ALLOW` | Correct admin-client and operation policy only; no learner fallback |
| `T02-003` | missing Authorization bearer | `DENY_AUTHN` | 401 with valid implemented route and middleware invocation |
| `T02-004` | ID token used instead of access token | `DENY_AUTHN` | Incorrect token type, never used as API credential |
| `T02-005` | alg none unsigned JWT | `DENY_AUTHN` | No signature bypass |
| `T02-006` | alg EdDSA incorrectly substituted from internal workload ADR | `DENY_AUTHN` | OIDC algorithm must follow independently approved Keycloak policy |
| `T02-007` | kid unknown or header-controlled jku/x5u | `DENY_AUTHN` | No untrusted token-supplied key fetching |
| `T02-008` | wrong issuer | `DENY_AUTHN` | Reject foreign realm |
| `T02-009` | wrong aud (not lms-api) | `DENY_AUTHN` | No cross-audience token |
| `T02-010` | wrong azp client for learner API-02 | `DENY_AUTHZ` | No role-based fallback |
| `T02-011` | expired access token | `DENY_AUTHN` | Clock/time boundary proof |
| `T02-012` | nbf beyond allowed time window | `DENY_AUTHN` | Not before enforcement |
| `T02-013` | missing required sub | `DENY_AUTHN` | No fabricated principal |
| `T02-014` | valid identity missing learning.enrollment.read.self capability | `DENY_AUTHZ` | Signed token alone insufficient |
| `T02-015` | unrecognized client and forged student fallback | `DENY_AUTHN` | No inferred client context |
| `T02-016` | JWKS network unavailable and no trusted usable cached key | `DENY_SAFETY` | No skip of signature verification |
| `T02-017` | valid signed Gateway workload proof to Learning API-02 | `ALLOW` | Signed caller/kid/recipient/operation, independent of delegated user |
| `T02-018` | missing workload proof with valid delegation | `DENY_AUTHN` | Delegation cannot substitute caller authentication |
| `T02-019` | unsigned X-Service-Id or X-User-Id header | `DENY_AUTHN` | Header has no security authority |
| `T02-020` | tampered workload signature | `DENY_AUTHN` | Real detached signature verification |
| `T02-021` | wrong alg HS256 / none | `DENY_AUTHN` | Algorithm confusion denied |
| `T02-022` | token header jku/x5u attempts remote key discovery | `DENY_AUTHN` | Pinned registry only |
| `T02-023` | unknown kid or wrong caller-kid binding | `DENY_AUTHN` | Caller identity scoped key |
| `T02-024` | payload kid differs protected header kid | `DENY_AUTHN` | Exact equality |
| `T02-025` | wrong audience or issuer | `DENY_AUTHN` | Exact internal trust domain |
| `T02-026` | wrong recipient service | `DENY_AUTHZ` | Cannot replay Learning proof to Audit |
| `T02-027` | wrong operation ID | `DENY_AUTHZ` | API-02 cannot authorize API-14 |
| `T02-028` | future iat beyond 5s skew | `DENY_AUTHN` | Clock bound |
| `T02-029` | exp-iat exceeds 60s | `DENY_AUTHN` | Maximum assertion lifetime |
| `T02-030` | emergency-revoked caller key | `DENY_AUTHN` | No overlap after compromise |
| `T02-031` | valid signed delegation for same user/caller/recipient/API-02 | `ALLOW` | Separate signed proof + same request ID + capability intersection |
| `T02-032` | missing delegation on user-bound request | `DENY_AUTHN` | Workload proof alone insufficient |
| `T02-033` | delegation with invalid independent signature | `DENY_AUTHN` | Two independent logical checks |
| `T02-034` | delegation token accepted as workload token | `DENY_AUTHN` | Independent type/domain/role separation |
| `T02-035` | workload token accepted as delegation token | `DENY_AUTHN` | Reverse substitution denied |
| `T02-036` | delegation issued for other caller | `DENY_AUTHZ` | Caller binding |
| `T02-037` | delegation issued for other recipient | `DENY_AUTHZ` | Recipient binding |
| `T02-038` | delegation operation != actual API-02 | `DENY_AUTHZ` | Operation binding |
| `T02-039` | delegation request ID differs workload/request | `DENY_AUTHZ` | End-to-end request binding |
| `T02-040` | principal sub altered or unrelated to authenticated Gateway JWT | `DENY_AUTHZ` | No header impersonation |
| `T02-041` | delegation capability exceeds verified OIDC grants | `DENY_AUTHZ` | Intersection; never elevation |
| `T02-042` | wrong resource owner of enrollment | `DENY_AUTHZ` | Owner-scoped business query |
| `T02-043` | learner delegation used for admin principal role operation | `DENY_AUTHZ` | Admin client/capability segregation |
| `T02-044` | machine-only call given invented principal_sub | `DENY_AUTHZ` | Explicit machine-only policy needed |
| `T02-045` | new signed unique jti with healthy verified epoch | `ALLOW` | Atomic SET NX PX equivalent before side effects |
| `T02-046` | same jti duplicate sequentially | `DENY_AUTHN` | Second request no side effects |
| `T02-047` | same jti concurrent pair, 2 workers | `DENY_AUTHN` | Exactly one authorized winner, other denied |
| `T02-048` | same jti reused with changed principal and same namespace | `DENY_AUTHN` | Key includes issuer/caller/recipient/jti; no bypass by principal change |
| `T02-049` | same delegation jti with newly signed workload proof | `DENY_AUTHN` | Delegation nonce independently consumed |
| `T02-050` | same workload jti with new delegation jti | `DENY_AUTHN` | Workload nonce independently consumed |
| `T02-051` | nonce missing or malformed | `DENY_AUTHN` | No default nonce |
| `T02-052` | jti generator entropy below 128-bit policy | `DENY_SAFETY` | CSPRNG must be verified at signing |
| `T02-053` | Redis connection refused | `DENY_SAFETY` | No controller invocation |
| `T02-054` | Redis authentication rejection NOAUTH | `DENY_SAFETY` | Never bypass ACL |
| `T02-055` | Redis SET NX PX command timeout unknown result | `DENY_SAFETY` | Never assume reservation failed or retry authorization |
| `T02-056` | Redis reply ambiguous/non-boolean | `DENY_SAFETY` | No fail-open interpretation |
| `T02-057` | Redis restart with lost keys | `DENY_SAFETY` | Epoch continuity unknown |
| `T02-058` | Redis FLUSH/eviction of replay namespace detected | `DENY_SAFETY` | Fail closed and enter recovery |
| `T02-059` | Redis failover to replica without proven nonce state | `DENY_SAFETY` | Unknown epoch -> deny |
| `T02-060` | Redis-only sentinel lost together with keys | `DENY_SAFETY` | Not independent loss detection |
| `T02-061` | recovery PING succeeds but no independent epoch proof | `DENY_SAFETY` | PING is not replay state integrity |
| `T02-062` | verified recovery quarantine at 64 seconds | `DENY_SAFETY` | At least 65s required |
| `T02-063` | verified recovery quarantine at >=65 seconds plus intact epoch | `ALLOW` | Only if independent health, continuity and all auth checks PASS |
| `T02-064` | quarantine interrupted by second uncertain restart | `DENY_SAFETY` | Restart recovery evaluation; no stale timer acceptance |
| `T02-065` | replay reservation TTL shorter than exp+skew | `DENY_SAFETY` | Do not allow early replay window |
| `T02-066` | partial two-assertion nonce reservation | `DENY_SAFETY` | No business effects; first consumed nonce may stay burned |
| `T02-067` | direct Internet connection to Learning port or public hostname | `DENY_NETWORK` | Loopback/private service only; IPv4+IPv6 check |
| `T02-068` | browser bearer forwarded to Learning as workload proof | `DENY_AUTHN` | Audience/role separation |
| `T02-069` | any unsigned principal request header | `DENY_AUTHN` | Never trust client-origin X-User-Id |
| `T02-070` | unimplemented business route yields default 404 | `INVALID_TEST_PROOF` | 404 alone is not evidence of auth middleware enforcement |
| `T02-071` | health live succeeds while replay dependency unavailable | `OBSERVE_ONLY` | Must not be mistaken for trust readiness |
| `T02-072` | readiness claims ready while trust replay unverified | `DENY_SAFETY` | Future readiness contract should gate protected work; existing ready is static |
| `T02-073` | invalid internal token error response leaks signed token/private key | `FAIL_SECURITY` | Sensitive output leak is hard failure |
| `T02-074` | Redis outage returns safe problem response with no business write | `DENY_SAFETY` | 503 proposed only; final exact HTTP code needs owner contract approval |
| `T02-075` | failed auth logs full user PII/private-key material | `FAIL_SECURITY` | Only safe kid/service/op/request/decision fields allowed |
| `T02-076` | mutating owner request uses wrong DB role or cross-domain write | `DENY_AUTHZ` | Ownership and PostgreSQL grants required separately |
| `T02-077` | old current key during approved 180s rotation overlap | `ALLOW` | Only valid current+previous and no compromise |
| `T02-078` | previous key beyond approved overlap | `DENY_AUTHN` | No stale key acceptance |
| `T02-079` | emergency revoked key during nominal overlap | `DENY_AUTHN` | Revoke immediately |
| `T02-080` | key registry fingerprint changes without reviewed release | `DENY_SAFETY` | No silent key trust substitution |
| `T02-081` | no private signing key in CI logs/repo or artifacts | `PASS_SECURITY_HYGIENE` | Test-only fixtures; secret scan as separate CI |
| `T02-082` | new internal tests accidentally alter 26 public routes | `FAIL_COMPATIBILITY` | Frozen OpenAPI unchanged |
| `T02-083` | new internal tests weaken 19 capabilities or owner contract | `FAIL_COMPATIBILITY` | Immutable authz inventory |
| `T02-084` | new middleware modifies HRM/Keycloak production clients or mappers | `FAIL_BOUNDARY` | Strict NO mutation |
| `T02-085` | both assertions valid but controller side effect executed before replay reservation | `FAIL_SECURITY` | Instrument execution order |
| `T02-086` | feature PR tests all green at different SHAs | `INVALID_TEST_PROOF` | Same exact candidate SHA required for CI acceptance |

## 4. Cross-cutting mandatory test rules

1. **Independent controls:** Verify workload proof and scoped delegated principal proof as separately constructed and independently verified signed objects. `T02-017` and `T02-031` are not the same signature. Run substitution and cross-assertion mismatch tests. The exact two-token wire format/roles remain **D02-01 pending owner ratification**; adapt harness after ratification without changing the frozen 26 public operations.
2. **Real HTTP path exists:** For each authorization-denial test, create an explicitly approved isolated protected route and assert the verifier/authz middleware actually executed. A default `404` or `405` from an empty API skeleton **does not count**.
3. **No side effects on denial:** instrument controller invocation counts, PostgreSQL owning-domain test transaction counts, outbox/event emission counts, external HTTP/key-store call counts, safe audit metadata and response secret scrubbing. `DENY_*` PASS requires all inappropriate side-effect counters remain zero. Existing production Redis/PG MUST NOT be used.
4. **No privileged production resources:** provision only locally isolated ephemeral test-only keys, self-contained fake clock, in-memory fault adapter then separately authorized isolated Redis test instance; no real Keycloak tokens, no existing Redis ACL checks, no sudo/VPS scripts, no HRM/Cloudflare/DNS/FE writes.
5. **Deterministic concurrency:** `T02-047` must run truly concurrent workers against the **same atomic nonce store**, not a sequential fake; assert exactly one reservation succeeds. Same with partially reserved two-token cases; controller must not execute on partial denial.
6. **Independent replay-loss detector:** `T02-057` to `T02-065` require a credible out-of-band integrity/epoch source. `PING`, a Redis-only sentinel or process-local timer **cannot** alone justify `HEALTHY_VERIFIED` after lost state. If impossible, stop and return D02-02 revised owner ADR before any runtime acceptance.
7. **Time and rotation proofs:** use a controlled test clock plus real-time controlled tests with max `exp-iat<=60s`, skew <=5s, >=65s quarantine after verified recovery, 180s maximum key overlap and immediate compromised-key revoke. Tests must cover nonmonotonic host time and clock reset before production design signoff.
8. **Test verdict taxonomy:** each case has one of `NOT_IMPLEMENTED`, `NOT_RUN`, `PASS_NONPROD_HTTP`, `FAIL_OBSERVED`, `BLOCKED_POLICY`, `BLOCKED_INFRA`, `NOT_APPLICABLE_WITH_REASON`. Never mark an entire category PASS from one synthetic unit test.
9. **Owner scope:** This test matrix is a candidate and may not silently expand public API, Keycloak client roles, capability strings, service owners, PostgreSQL DB count, source-content authority, hosting or production exposure. Design divergence needs explicit versioned owner decision.
10. **Minimum exit:** All applicable **86** cases individually resolved and reviewed, B02-D05–D13 design/implementation preconditions actually satisfied and CI green on exact source SHA. This is a **future implementation exit**; merely merging this documentation matrix never marks the future gates complete.

## 5. Design-only checkpoint

`TEST_MATRIX_CREATED=86`, `TEST_MATRIX_EXECUTED=0`, `HTTP_DUAL_ASSERTION_VERIFIED=NO`, `REDIS_LOSS_DETECTION_VERIFIED=NO`, `OIDC_REAL_ALG_VERIFIED=NO`, `PRODUCTION_AUTHORIZED=NO`.

**Next:** owner design review of D02-01/D02-02/D02-03/D02-04/D02-05, then a new separately scoped implementation work order; do not ask Gemini to implement all 86 scenarios and six microservices in one unreviewed commit.

## 6. E38 — mandatory test-interpretation errata after Gemini independent review (2026-10-11)

**The original T02-001..T02-086 test rows remain unchanged as historical proposed acceptance.** The owner-supplied Gemini review independently counted 86 table rows; this review reverified exactly 86 unique sequential IDs. **0 actual nonproduction HTTP, Redis fault-injection or Keycloak runtime tests executed.** Detailed source errors in [E38 review](./phase4b-02-gemini-independent-design-review-e38-20261011.md).

- **T02-006:** `alg EdDSA incorrectly substituted from internal workload ADR` means reject **algorithm trust inferred from the unrelated internal service Ed25519 ADR**. Do **NOT** claim all EdDSA OIDC tokens are categorically forbidden regardless of effective Keycloak/JWKS and an independently ratified strict OIDC algorithm policy. `D02-05` remains `BLOCKED`.
- **T02-047:** the replay race uses two genuinely concurrent workers. Exactly one eligible authorized request may win and the other must be denied; do not fake the test with a sequential in-memory array.
- **T02-062/T02-063:** 65 seconds is a **minimum quarantine after independently verified Redis recovery**, not sufficient without loss detection, safe monotonic timer/clock controls, intact trusted state, and all signature/policy checks. `D02-02` remains blocked.
- **No-unauthorized-effects rule:** before authorization, zero controller invocation, business writes, outbox messages and unauthorized data access. In a late ownership-denial, a **bounded permitted database read may occur to evaluate ownership**, so assert no unauthorized cross-owner information exposure/reads and no forbidden side effects rather than universally demanding zero DB reads on every denial.
- **Gemini-only candidate additions `T02-087..T02-090` are NOT accepted into the matrix** until an explicit versioned owner decision; core 86 count stays constant.

**Test execution checkpoint:** `T02_86_ROWS_UNIQUE_VERIFIED`, `T02_0_RUNTIME_EXECUTED`, `T02_RATIFICATION_PENDING`, `PRODUCTION_NOT_AUTHORIZED`.

## 7. E39 — test-verdict disambiguation and conditional PASS semantics before design ratification (2026-10-11)

**This versioned interpretation takes precedence over ambiguous `ALLOW` labels in historical table rows without deleting, renumbering, or implying execution of a single T02 test.** The **canonical original matrix remains 86 cases (T02-001–T02-086), 0 executed**. E39 risk analysis and 18 **proposed-only** new cases T02-087–T02-104 are at [E39 assurance register](./phase4b-02-e39-pre-ratification-assurance-risk-register-20261011.md); they are **not** adopted, not included in the manifest's canonical test total, not PASS.

| Existing ID | Original shorthand | Binding clarified acceptance before runtime coding | Classification today |
|---|---|---|---|
| Applies to `T02-001/T02-002` | `ALLOW` Gateway signed access token | **Gateway OIDC component-only PASS**, not an API success without actual route, backend operation/capability/owner and downstream controls; effective Keycloak alg remains unratified | `DRAFT_NOT_RUN` |
| Applies to `T02-006` | `DENY_AUTHN` EdDSA "substituted" | Deny EdDSA accepted **solely** by assuming internal Ed25519 profile; a future separately observed and approved Keycloak OIDC EdDSA profile must not be universally prohibited | `DRAFT_NOT_RUN` |
| Applies to `T02-017` | `ALLOW` signed workload assertion | Means **component VALID**, not a user-bound HTTP request allowed without independently valid delegation, replay reservations and owner checks | `DRAFT_NOT_RUN` |
| Applies to `T02-031` | `ALLOW` delegation assertion | Means **component VALID**, not permission to omit independent workload proof or cross-token request binding | `DRAFT_NOT_RUN` |
| Applies to `T02-045` | `ALLOW` unique jti reservation | Means **atomic replay reservation VALID if entire independently verified epoch/clock gate is healthy**; does not authorize handler execution by itself | `DRAFT_NOT_RUN` |
| Applies to `T02-047` | `DENY_AUTHN` same-jti concurrent pair | **Exactly ONE valid request may pass the complete gate, other(s) DENY**, with two truly concurrent workers and zero unauthorized/double side effects. A result in which both DENY is a security-safe outage but does **not** prove expected healthy-path atomic success; both ALLOW is an immediate security FAIL | `DRAFT_NOT_RUN` |
| Applies to `T02-063` | `ALLOW` after 65s quarantine | Only **component RESUMED** if verified recovery, independent loss detection, monotonic safe elapsed time across all workers, intact epoch and all authentication/authorization checks. 65s timer alone insufficient | `BLOCKED_D02-02` |
| Applies to `T02-077` | `ALLOW` previous key within overlap | Means **key status ELIGIBLE**, only if actual assertion and all remaining checks PASS; emergency revocation overrides overlap | `DRAFT_NOT_RUN` |
| Applies to `T02-038..044` | `DENY_AUTHZ` owner/delegation failures | No unauthorized data reads/disclosure and no domain writes/outbox; owner resolution at later authz stage may include **approved bounded DB reads**. Early signature failure must not touch business DB | `DRAFT_NOT_RUN` |
| Applies to `T02-070` | `INVALID_TEST_PROOF` default 404 | A nonexistent `api.php` route is NOT evidence of middleware trust enforcement; instrument an actual protected route | `DRAFT_NOT_RUN` |
| Applies to `T02-085` | `FAIL_SECURITY` handler invoked too early | Verify method/route/query/body and two-token context are bound before replay/handler, and side-effect counters are instrumented; fail on premature handler execution | `DRAFT_NOT_RUN` |

**Additional cross-cutting STOP rules:** A protected write request must prove an owner-approved signed binding to the **actual** HTTP method, canonical path+parameters, query, relevant body bytes/hash and recipient before execution. This is **proposed D02-01**, not yet ratified. Neither client-chosen `X-Request-ID` nor an untrusted `Host`/forwarded header can grant identity or substitute unique signed request binding. Harden duplicate headers, unsupported critical JWS fields, `jwk/x5c`, type/key role confusion and resource bounds if owner adopts additions T02-087–104.

**PASS remains impossible on paper:** this E39 clarification is **documentation semantics**, not a real HTTP/Redis test. Future CI must pin and execute each applicable case on the same source/runtime SHA and capture exact allow/deny, no forbidden effects and recovery/clock evidence. Existing E37 86-case manifest remains `executed_cases=0`; do not inflate count or assert full coverage.
