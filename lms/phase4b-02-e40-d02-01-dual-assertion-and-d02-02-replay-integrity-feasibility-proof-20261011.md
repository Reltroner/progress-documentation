# LMS Phase 4B-02 — E40 D02-01 & D02-02 Isolated Cryptographic / Replay-Loss Feasibility Proof

> **Record:** `LMS-P4B02-E40-20261011`.  
> **Scope:** OWNER-REQUESTED **isolated nonproduction D02-02 failure-model proof**, then D02-01 two-proof binding proof, followed by reassessment of D02-03/04/05. **Not a production-ready implementation or owner ratification.**  
> **Evidence baseline:** `LMS-BE/main=617dadc0d0d627071d713ceb729df6658202b43e`; docs `main=183372371b3a40a0349ac390848911273ccd2361` before PR #46. Reference [FROZEN Phase0C physical](./master-infrastructure-placement-contract.md), [FROZEN Phase1 logical](./logical-service-boundary-api-contract.md), [ADR-LMS-TRUST-001 (nonproduction design-only)](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md), [E39 16-finding register](./phase4b-02-e39-pre-ratification-assurance-risk-register-20261011.md).  
> **Status:** `CRYPTOGRAPHIC_MODEL_PROOF=PASS_17/17`; `REPLAY_FAILURE_MODEL_PROOF=PASS_13/13`; `REDIS_ONLY_REPLAY_INTEGRITY=COUNTEREXAMPLE_FOUND_UNSAFE`; `DURABLE_LEDGER_ALTERNATIVE=LOCAL_MODEL_PASS_ONLY`; `ACTUAL_REDIS8_AND_PG18_RUNTIME=NOT_TESTED`; `OWNER_DESIGN_RATIFICATION=HOLD`.

## 1. Purpose, basic terms and strict test boundary

**Replay:** an attacker (or faulty caller) sends a previously accepted valid signed assertion again. **Nonce/jti:** a fresh unpredictable per-proof identifier that must be accepted only once. **Independently signed assertions:** two role-specific JWS Compact signed using distinct Ed25519 test keypairs, one for the caller workload, another for scoped user delegation. **Durable replay ledger:** a crash-survivable transactional record of consumed jti values. **Counterexample:** an executable test demonstrating that an allegedly safe design permits a replay under some supported failure.

This proof was **run** inside the assistant's isolated Linux execution container on **2026-10-11**, using **PHP 8.4.24, sodium, and proc_open**. Distinct ephemeral Ed25519 signing keys were created in memory and zeroed afterward; no private key/actual token written to Git or output. One temporary file-backed ledger under system TEMP was used and deleted; **no network endpoints were contacted**, no Redis daemon was installed or invoked, no PostgreSQL server, Keycloak, Laravel HTTP handler, Cloudflare, VPS or production accessed. **30/30 test scenarios passed in this exact local proof.**

A reproducible **three-file proof package** was produced for the operator (ZIP named `LMS-P4B02-D02-D01-ISOLATED-PROOF-20261011.zip` in the original project conversation), containing `proof.php`, `run-proof-ps51.ps1` and `README.md`. `proof.php` SHA256 **`0DF6D1D50BCB99D0EEE2D7F7422ECADB7DE21C1DE96BF191B4DC2045F499867E`**. The PS5.1 runner validates that SHA, runs PHP 8.2+ and writes one TEMP report. **The package is a conversation artifact, NOT already committed to GitHub source**; an engineer/AI requiring the executable must obtain the exact original artifact and verify SHA rather than assume this Markdown contains all executable code.

## 2. Evidence — real signatures, model transport and 30 test verdicts

**Actual observed stdout tail:**

```text
SUMMARY total=30 passed=30 failed=0
PROOF_SCOPE=REAL_SODIUM_CRYPTO_PLUS_PHP_LOCAL_FILE_LEDGER_AND_REDIS_FAULT_MODEL
REDIS_SERVER_USED=NO
POSTGRESQL_SERVER_USED=NO
KEYCLOAK_USED=NO
PRODUCTION_ACCESS=NO
ACTUAL_REDIS_LOSS_INTEGRITY_PROVEN=NO
ACTUAL_POSTGRES_ATOMICITY_PROVEN=NO
D02_01_DESIGN_CANDIDATE_PROOF=MODEL_GREEN_OWNER_RATIFICATION_PENDING
D02_02_REDIS_ONLY_SAFETY=DISPROVEN_BY_COUNTEREXAMPLE
D02_02_ALTERNATIVE_DURABLE_ATOMIC_LEDGER=MODEL_GREEN_ADR_CHANGE_AND_REAL_DB_TEST_PENDING
```

**`D01-001..017` (17 PASS) — cryptographic D02-01 model:** real separate signed Ed25519 JWS verifying a workload token + signed delegated principal; rejects altered HTTP method, path, query, body, content type, mixed independent valid pairs, missing/swapped proof roles, tampered detached signature, inappropriate capability, future iat, >60s ttl, unsafe path; confirms simple canonical query ordering. The delegation includes a **signed SHA256 of the actual workload JWS**, and both proofs include a signed digest of a deliberately restricted canonical target (method + path + single-valued sorted query + media type + raw body hash), a fresh server-generated `exchange_id` and `request_id`. Each proof uses distinct test `kid`, role-specific `typ`, signature key, and `jti`. **These literal `typ` and transport choices are proposals, not ratified wire protocol.**

**`D02-001..013` (13 PASS) — Redis failure and independent-authority model:** Redis-only nonce reservation rejects a sequential replay when keys remain; intentionally vulnerable Redis-only model **ACCEPTS replay after the relevant nonce is silently selectively removed, or after FLUSH** (tests PASS by demonstrating the failure, NOT by showing Redis is safe). A separate finite-state quarantine model denies cold/unknown/outage and at 64s, allows conditionally after 65s of *externally declared verified* recovery, and restarts denial after another loss. A transient **file-backed** ledger using exclusive OS locks (NOT real PostgreSQL) rejects the replay despite simulated Redis loss, atomically reserves two nonce identifiers, denies when ledger file unavailable, and on **two genuinely concurrent child processes** produces exactly one success and one denied reservation.

**Honest scope:** No real Redis 8 `SET NX PX` or eviction/failover, no PostgreSQL 18 `UNIQUE` transactions/replication crash testing, no network HTTP or Laravel authorization middleware, no live Keycloak access token and no applied production signing keys. Model green cannot be translated into `T02-001..086 HTTP PASS` (the original 86-case matrix remains 86 drafted, 0 executed). A PHP file lock is not a Postgres durability guarantee. A test-provided `verifiedRecovered()` boolean does not prove that a real independent recovery detector exists.

## 3. Impossibility of replay safety with Redis-only invisible key deletion — scoped proof

Consider two histories with identical observable Redis state **at verification time**:

- **World A (fresh):** signed unexpired proof `jti=X` has not been accepted; Redis key `X` does not exist.
- **World B (replay):** exactly the same proof `jti=X` was accepted and its Redis nonce key was then silently evicted/deleted. Redis key `X` does not exist; `PING` and unrelated health checks can still succeed.

If the verifier observes **only** Redis key existence and the unchanged signed proof, its inputs are identical in both worlds. **It must make the same decision**: if A is accepted for valid new traffic, B is accepted despite replay. A Redis-only `PING` or a marker stored solely in the same keyspace does not distinguish these histories. This is a bounded *indistinguishability argument* against the stated failure model; it does not mean Redis is intrinsically defective or that every locked-down Redis deployment experiences unobservable key deletion. It demonstrates why the E39 D02-02 claim **cannot be closed from Redis-only logic while silent selective loss remains in scope**.

**What would be required to claim Redis-only safe?** Restrict threat assumptions (no silent selective loss possible) and enforce them with verified `noeviction`, narrow ACL, isolated instance, durability/failover behavior, independent monitoring/epoch, cold-start deny and measured >=65s quarantine. **No such isolation or loss detector was tested in E40**, so this is at most an unproven alternative with explicit residual failure modes.

## 4. Conditional safer fallback — existing owner-scoped PostgreSQL durable nonce authority

**PROPOSED NEW ADR AMENDMENT — NOT AUTOMATICALLY APPROVED:** Preserve Redis as a disposable cache/optimization, but require a **durable atomic anti-replay authority** in the owner service's *existing* PostgreSQL 18 domain DB; avoid a fifth DB or cross-owner write. Under `learning`, the prototype owner would be **`lms_learning_db`**; other service owners would need reviewed analogous security tables in **`lms_mentorship_db`, `lms_knowledge_db`, `lms_audit_db`** only where their contract permits such writes. Assistant retains **no new owned fifth DB** without an explicit frozen-contract change.

**Future DB acceptance candidate:**
1. Scoped unguessable replay ledger entry covers `proof_role, issuer, caller_service, recipient_service, jti`, with unique constraint and expiry `exp + permitted skew`. Never expose full principal/PII/token in the ledger.
2. **Both** independently verified proof nonce reservations insert atomically inside **one** owner-DB transaction, via unique constraints; duplicate/partial conflict → entire transaction rolls back and request DENIED (no domain handler side effects). Reserve only after cryptographic and operation checks; for mutation, coordinate replay acceptance and domain write semantics under an explicitly reviewed DB transaction/idempotency policy.
3. On SQL unavailable, uncertain commit response, lost connection, uncertain standby failover, stale replica, key/ownership mismatch or storage retention gap → **DENY**; never replace authoritative SQL unique decision with Redis fallback.
4. A `UNIQUE` index proves one reservation **on the chosen authoritative database timeline**; it **does not** by itself prove no nonce can reappear after loss of committed WAL/async failover/restore. Specify primary failover fencing, durability settings, accepted commit acknowledgments, retention, backups and post-restore quarantine; test failures directly before claiming runtime PASS.
5. Redis `SET NX PX` may act as an additional early performance/safety check but is **not** the only record of accepted proof. An out-of-band durable journal adds write amplification, contention and failure coupling. On the existing 1-vCPU shared VPS, require isolated cost/capacity benchmarks before deciding feasibility; do not add Redis/PG deployments under this document.

**Compatibility blocker:** ADR-LMS-TRUST-001 currently calls for Redis as ephemeral anti-replay store. Shifting authoritative single-use enforcement to PostgreSQL is a **material architectural design change** to that earlier owner-ratified *nonproduction* profile. It requires a new owner-reviewed `ADR-LMS-TRUST-002` or an explicit versioned amendment, a frozen Phase0C/1 compatibility review, and end-to-end PG18 tests. **E40 does not ratify that change**, despite its favorable model proof.

## 5. Proposed D02-01 wire format — verified locally but owner approval pending

Candidate two independent proof headers (**header names provisional**): `X-LMS-Workload-JWS` and `X-LMS-Delegation-JWS`. Each contains a separate JWS Compact with protected `alg=EdDSA`, `kid` from exact pinned per-role/per-service Ed25519 registry and explicit distinct protected `typ`. Reject `none`, unrelated algorithms, duplicate headers, untrusted `jku/x5u/jwk/x5c`, unsupported critical headers and key-role confusion.

**Workload token (caller service identity):** exact `iss/aud/caller_service/recipient_service/operation_id`, bounded `iat/nbf/exp <=60s`, >=128-bit unpredictable `jti`, Gateway-controlled **`exchange_id`**, and **`http_binding_sha256`** of the *actual* private request's canonical method+path+query+media type+body. **Delegation token (end user):** independent signed principal `principal_sub`, approved capability intersection, separate nonce/key/role, all matching caller/recipient/operation/exchange/digest claims, **`workload_token_sha256`** binding to exact signed workload JWS, no unsigned user headers. Both independently verified, then cross-related, then both nonce reservations authorized before any business side effect.

**Trust nuance:** Independent JWS cryptographic verification does not imply separately governed signer trust roots if Gateway holds both signing roles. Scope this as **two independent logical controls** (per ratified ADR), define per-role key custody and blast radius, and do not pretend it survives total Gateway compromise. Request ID is tracing only unless replaced by Gateway-generated binding. Signed digest is necessary to prevent token use on a modified request, but the **true proxy/HTTP canonicalization** rules (duplicate query/header keys, percent encoding, Unicode normalization, body transformations, trusted forwarded Host, content type and path routing) require owner protocol decision and real Laravel HTTP tests. The executable model accepts only an intentionally limited ASCII path and single-string-value query subset; do **not** deploy its canonicalizer unchanged for real traffic.

**Next D02-01 tests:** Prove real Gateway-generated JWS, provider signature verification, role-specific key resolution, exact external-to-private method/route mapping, body tamper and two-JWS mixing, no handler execution before authoritative nonce reservation, and no cross-capability/owner effect. The 17 simulated tests prove a bounded cryptographic design construct, not deployed HTTP integration.

## 6. Remaining decisions and acceptance — no fabricated closure

| Decision/gate | E40 result | Exact remaining proof/owner authority |
|---|---|---|
| **D02-01** two JWS format and request binding | **`CRYPTO_MODEL_PASS_17/17`**, format **CANDIDATE** | Owner ratifies on-wire transport, canonical URI/body, proof role/custody, signer scope; real HTTP/provider tests pending |
| **D02-02** replay integrity | **`REDIS_ONLY_SILENT_LOSS_UNSAFE_COUNTEREXAMPLE`**, safer ledger **`MODEL_PASS_13/13`** | Owner approves/rejects ADR revision for owner-scoped durable replay authority; run actual PG18 unique/failover, Redis8 negative cases, capacity; until then **BLOCKED** |
| **D02-03** error mapping | **NOT TESTED** | Candidate `401` invalid proof, `403` forbidden context, `503` unknown replay dependency; confirm frozen OpenAPI/Problem Details; no automatic retries of ambiguous mutating requests |
| **D02-04** isolated key/test environment | **`TEST_ONLY_EPHEMERAL_KEYS=USED`**, no cost or production access | Local Linux proof meets narrow isolated model task; separate owner permission needed for real Redis8/PG18 nonprod sandbox/key custody/performance test |
| **D02-05** effective Keycloak OIDC alg/JWKS | **BLOCKED** | Public OIDC discovery/JWKS could not be independently verified via this execution environment; must inspect actual signed access-token `alg/kid` and issuer/aud/azp/client mapper safely with owner-approved read-only scope; no token dump |
| **B02-D09/10/12** real HTTP and CI | **0/86 executed** | Approved protected route, actual clock/headers/crypto/DB/Redis failure injection, exact CI SHA and negative side-effect evidence |
| **Design ratification** | **HOLD** | Explicit owner decisions plus credible runtime feasibility/architecture proof; source-only green never converts to production-ready |

**Risk/classification correction:** E39 16 issues still have explicit dispositions; E40 gives bounded **proof for D02-01** and a **counterexample for Redis-only D02-02**, not 16/16 remediation. No claim of “zero risk, zero technical debt, no missing” or that Redis and PostgreSQL were physically tested.

## 7. Next safe work order — owner-driven choices in an auditable sequence

1. **Owner design choice:** either approve a bounded draft `ADR-LMS-TRUST-002` **for proposed Postgres replay authority** *without yet activating it*, or request a separate independently evidenced restricted-Redis profile that can detect/exclude selective nonce deletion. A Redis-only design cannot be marked safe for the original silent-loss threat model by adding a timeout alone. Design documents may be merged as **research/decision evidence**, not as ratification.
2. **Owner D02-01 choice:** accept or amend the candidate two-JWS typed protocol and request binding, with canonical HTTP representation and private key role custody defined in a versioned contract. Only then give a new BE worktree-based coding prompt **with exact allowlist and nonproduction test scope**. No reuse of prior G03 worktree `598440f...`.
3. **Isolated real services test gate:** under a later separately approved no-cost environment, use **real PostgreSQL 18 and Redis 8 binaries** separate from existing HRM/VPS to reproduce silent eviction, failure, concurrent inserts, uncertain commit and restart/failover. The current environment lacked those binaries. If capacity/replication uncertainties cannot be resolved, acceptance must remain fail-closed.
4. **D02-03/04/05:** ratify error contract, test-only keys/environment, then obtain masked evidence of Keycloak effective signed access JWT and policy—without leaking raw tokens or changing clients.
5. **Independent CI and ratification:** exact source SHA, positive/negative real HTTP tests, owner approval of ADR/protocol separately from eventual PR merge, and separate later production release authority. Keep historical 86-case T02 matrix untouched until owner explicitly accepts suggested additions.

**Checkpoint:** `4B02_E39_HOLD -> E40_D02-01_CRYPTOGRAPHIC_MODEL_PASS -> E40_D02-02_REDIS_ONLY_UNSAFE_PROVEN -> DURABLE_ALT_MODEL_PASS_BUT_ADR_PENDING -> D02-03/04/05_PARTIAL_OR_BLOCKED -> ZERO_PRODUCTION_ACCESS -> OWNER_RATIFICATION_HOLD`.
