# LMS Phase 4B-02 — E40 Owner Decisions D02-01..05 and Ratification Reassessment

> **ID:** `LMS-P4B02-E40-DECISION-PROPOSAL`  
> **Status:** `TECHNICALLY_REASONED_CANDIDATE / NOT OWNER-RATIFIED / IMPLEMENTATION HOLD`. This is NOT an amendment to a frozen contract or to owner-ratified ADR-LMS-TRUST-001.  
> **Evidence:** [E40 reproducible local model proof](./phase4b-02-e40-d02-01-dual-assertion-and-d02-02-replay-integrity-feasibility-proof-20261011.md) (30/30 model PASS, including deliberate Redis-only **unsafe** counterexample); [E39 assurance register](./phase4b-02-e39-pre-ratification-assurance-risk-register-20261011.md); [E38 errata](./phase4b-02-gemini-independent-design-review-e38-20261011.md).  
> **Safety:** No Redis8, PostgreSQL18, Keycloak/VPS/Cloudflare production calls performed. No BE/FE changes. The 86 canonical HTTP acceptance scenarios still have **0 executed**.

## 1. Key owner question: which replay authority has a verifiable safety story?

**Option A: keep Redis-only authoritative replay as currently ratified (ADR-LMS-TRUST-001).** E40 gives a falsifiable counterexample when a consumed nonce is silently removed while `PING` succeeds: a replica/app with only Redis state **cannot distinguish a fresh nonce from a replay**. Without a proven policy that excludes or independently detects such loss, this option is **NOT RECOMMENDED** and **BLOCKED_FOR_RUNTIME**. `noeviction`, ACL and separate instance can reduce risk; E40 did not establish their sufficiency against every failure in the present threat model.

**Option B: propose a material ADR revision — owner-scoped PostgreSQL durable replay authority + Redis ephemeral optional.** A **transactionally unique** replay ledger in each applicable *existing* domain owner's PostgreSQL 18 DB has a clearer integrity invariant: a second reservation for an already committed `jti` must fail, even after Redis loses state. Two independent JWS nonce claims must be reserved together atomically in one owner-DB transaction. A local locked-file substitute passed 13 replay-model cases; **real PostgreSQL 18, replica failover, WAL loss/restore and performance have NOT been proven**. This design adds DB writes, availability coupling and operational cleanup. No new fifth database and no Assistant DB should be created. **RECOMMEND AS A STUDY/ADR-002 CANDIDATE**, not a current ratified change. Exact owner SQL permissions, table schema, retention, index pressure, replication and recovery must be reviewed.

**Option C: decline current replay runtime feature pending another owner-reviewed architecture.** Maintain `DENY` for unprovable nonce state. No fake 65-second pass, no trust traffic accepted, no service deployed. This is the immediate safe default while Option B is unverified.

**Owner selection recommended:** Review a future `ADR-LMS-TRUST-002` proposal allowing **Option B only in isolated nonproduction tests**; retain `D02-02=BLOCKED` until real PG18/Redis8 failure-injection and cross-worker tests prove the claimed properties. Avoid a production commitment or capacity promises.

## 2. D02-01 — complete proposed two-proof wire contract, not yet ratified

| Area | Candidate contract for owner review | Rejection behavior |
|---|---|---|
| Token transport | Internal-only two separate HTTP headers (proposed `X-LMS-Workload-JWS`, `X-LMS-Delegation-JWS`), one compact JWS per header, bounded size, duplicate headers denied | Reject missing/duplicate/oversize and browser-origin trusted headers |
| Protected header | `alg=EdDSA`, distinct proposed `typ` per workload/delegation, pinned key `kid`, service+role scoped Ed25519 registry; no `jku/x5u/jwk/x5c`, unknown/unsupported `crit` | Reject key role substitution, unapproved algorithm, remote key injection |
| Caller proof | `iss=lms-internal-trust`, `aud=lms-internal-services`, caller service ID, recipient ID, exact API operation ID, fresh `jti`, `iat/nbf/exp`, Gateway-generated `exchange_id`, binding to actual private request | Reject wrong caller/recipient/operation, stale proof, role mismatch |
| Delegation proof | Independent Ed25519 signature/nonce/key scope, approved end-user `principal_sub` and intersection capabilities, same caller/recipient/operation/request target/`exchange_id`, `workload_token_sha256` of exact signed caller token | Reject combined/mix-and-match valid proofs, missing user delegation on user-bound API |
| HTTP message binding | Versioned canonical private request representation: uppercase method, validated normalized target path+route params, exact ordered/sorted query contract, content type, digest of body raw bytes, explicit recipient/operation; hash signed into both proofs | Reject path/query/body modification, duplicate query/headers, URL ambiguity, proxy canonicalization mismatch |
| Nonce enforcement | Both roles have distinct fresh >=128bit `jti`; after both signatures and signed request bindings verify, reserve **both** replay keys atomically against chosen trusted ledger before handler; reject uncertain result | Deny duplicate/concurrent/partial reserve/timeout; never silently retry possibly committed proof |
| Machine-only exception | Only if operation explicitly classified machine-only in frozen authorization contract: signed caller proof required, no fabricated end-user; separate future test contract | Reject replacing required user delegation with "no user" |
| Signing trust limits | Distinct keys and independent logical validation **do not** provide two independent organizational trust roots if Gateway possesses both signing roles; explicit Gateway compromise remains in scope | No invented claim of protection from total signing authority compromise |

**Unresolved precise points before D02-01 approval:** canonicalization compatibility with Laravel/Next/NGINX (duplicate query, encoded paths, UTF-8, MIME, forwarded host), prevention of raw-body mutation by proxies, `kid` and `typ` approved literals, route operation mapping, user-only vs machine-only calls, approved actor `sub` mapping, and key provisioning/rotation custody. E40 demonstrates a *restricted model*, not those real behaviors.

## 3. D02-02 — minimum real PostgreSQL + Redis feasibility suite (future)

A separate owner-authorized isolated no-cost test environment with actual PostgreSQL **18** and Redis **8** must prove these cases, or classify them blocked rather than pass:

| Gate | Experiment | Acceptance condition |
|---|---|---|
| `PG-R01` | Attempt two identical nonce claims concurrently on same owner DB unique key | Exactly 1 durable success, others conflict; no double business effects |
| `PG-R02` | Atomically reserve two JWS jtis; second conflicts after first would otherwise succeed | Entire transaction rolls back, no orphan nonce reservation or handler action |
| `PG-R03` | Redis cache FLUSH/evict silently (ONLY isolated disposable test Redis) after acknowledged SQL reservation | Second replay denied by authoritative SQL, irrespective of Redis state |
| `PG-R04` | Kill backend worker after transaction commit, then retry old proof | Replay denied when recovered from same durable authority |
| `PG-R05` | SQL unavailable / ACL deny / lock timeout / serialization retry / commit response ambiguous | DENY, no silent Redis fallback; any retry must follow explicit safe idempotency policy |
| `PG-R06` | PostgreSQL restart with retained WAL and recovery | No accepted nonce lost; if uncertain, fail closed and quarantine |
| `PG-R07` | Force standby promotion with unreplicated acknowledged commit in isolated replica topology | If ledger loses commit, **block promotion for trust acceptance** or fail closed until all old proofs expired; no false availability PASS |
| `PG-R08` | Cleanup expired nonce rows with clock skew and running transactions | Never deletes still-valid jti; bounded reclaim cost and availability |
| `PG-R09` | Record 100/1000 concurrent requests in isolated benchmark under one-CPU target budget | Measure latency, WAL bytes, disk, locks, backlog; human capacity signoff; do NOT infer from old 2% CPU production idle |
| `PG-R10` | Apply owner-specific DB role grants across Learning/Mentorship/Knowledge/Audit only | No fifth DB, no cross-owner writes, no real HRM/PostgreSQL production modifications |

**Hard limit:** This design inherently cannot guarantee safety against **arbitrary privileged deletion of both authoritative ledgers or loss of acknowledged durable commits** without separately defined trusted recovery/quarantine/fencing. Any such event must cause protected traffic to fail closed. Merely migrating from Redis to PostgreSQL does not yield mathematically zero risk.

## 4. D02-03 — proposed failure HTTP policy

Recommend `401` for missing/invalid identity or proof, `403` for authenticated but forbidden operation/capability/owner, and **`503 Service Unavailable`** for safety dependency (replay authority unknown/unavailable) with sanitized RFC 9457 Problem Details and consistent `request_id`; no JWT/JWS/PII in error. Deny BEFORE any unauthorized effect; use deliberate HTTP retry policy so an indeterminate durable write isn't repeated blindly. **Not approved until frozen OpenAPI/error contract compatibility confirmed.**

## 5. D02-04 — isolation and key custody decision

**Locally demonstrated:** Synthetic test-only keys generated and zeroed in memory; standalone file-lock concurrency model; no network and no production access; no new spending. **Not demonstrated:** service key custody, Keycloak real client, Redis 8/PG 18 runtime under isolation, VPS 1-vCPU capacity, secret rotation/revocation and secure artifact signing. A future Docker/localhost sandbox must use **new test-only ports** and process identities, explicit environment naming and stop-on-any-production-host string; no production `.env`, dump or token printed. Human approval needed before provisioning even a test instance if it would touch existing VPS or billing.

## 6. D02-05 — Keycloak OIDC status and next read-only evidence

The frozen realm issuer is `https://auth.reltroner.com/realms/reltroner`, expected API access audience `lms-api`, browser clients `lms-user` and `lms-admin`. **Do not infer effective access JWT `alg` from the Ed25519 internal ADR or from JWKS keys alone.** Public OIDC discovery/JWKS were not independently retrievable through the current test environment; no Keycloak admin console or authenticated client scope was accessed. **Require owner-approved read-only collection** of exact effective signed access-token protected header `alg/kid` **without copying the token itself**, issuer/audience/azp and capability mapper configuration, authorized client and JWKS rotation profile, followed by separate owner-signed strict JWT allowlist decision. `D02-05=BLOCKED_EVIDENCE`.

## 7. Owner design ratification — exact status, not blanket yes/no

| Decision | Evidence achieved | Ratification status |
|---|---|---|
| `D02-01` | Real Ed25519 model proof 17/17, tamper/cross-token denial | **CANDIDATE, PENDING OWNER WIRE/POLICY SIGNOFF** |
| `D02-02` | Redis-only unsafe scenario **demonstrated**; independently durable local ledger 13/13 model proof | **BLOCKED REAL PG18/REDIS8 & REVISED ADR** |
| `D02-03` | 401/403/503 proposed | **PENDING OWNER COMPATIBILITY** |
| `D02-04` | Synthetic ephemeral keys used without production | **MODEL SCOPE PASS / REAL SERVER & CUSTODY PENDING** |
| `D02-05` | No verified effective Keycloak alg/client/mappers | **BLOCKED EVIDENCE** |
| **Phase4B-02 design ratification** | Model results archived and options fully mapped | **HOLD — technical/owner gates unresolved** |
| **Nonproduction runtime / 86 test cases** | `0/86` executed against real Laravel HTTP/Redis | **NOT IMPLEMENTED/NOT TESTED** |
| **Production deployment** | Not requested/authorized | **NOT AUTHORIZED** |

**Next valid owner decision:** whether to **authorize investigation and drafting of an ADR-LMS-TRUST-002 candidate for owner-scoped PostgreSQL anti-replay authority in a new isolated disposable environment**, and separately review the D02-01 two-JWS protocol for final literals, route canonicalization and key roles. Merely approving this E40 research archive is **not** approval of ADR changes, BE coding, DB migration, Keycloak or production use.
