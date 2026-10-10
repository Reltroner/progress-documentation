# Reltroner LMS — E46-F3C R5-A First Real PG18/Redis8 Diagnostic Acceptance (GitHub Actions)

> **Record:** `LMS-P4B02-E46-F3C-R5A-REAL-DIAGNOSTIC-20261011`  
> **Evidence status:** `PASS_ACTUAL_GITHUB_HOSTED_RUN_READONLY_SCOPE`; **one owner-approved dispatch CONSUMED**; no reruns; no R5-B authorization.
> **Sources:** [canonical README](./README.md); [R5A immutable bootstrap receipt](./phase4b-02-e46-f3b-r5a-first-diagnostic-bootstrap-commit-and-first-run-decision-20261011.md); [owner-approved dispatch work order](./phase4b-02-e46-f3c-r5a-owner-first-run-approval-and-dispatch-operator-handoff-20261011.md); [actual run #38092783946](https://github.com/Reltroner/lms-trust-sandbox/actions/runs/38092783946).
> **Authority:** This is **operational read-only runtime evidence**, not approval to amend frozen physical/logical contracts, grant trust D02 ratification, merge BE/FE, or deploy production.

## 1. What ran; immutable identity and execution

| Item | GitHub live evidence |
|---|---|
| Repository | `Reltroner/lms-trust-sandbox` public |
| Run URL | https://github.com/Reltroner/lms-trust-sandbox/actions/runs/38092783946 |
| Workflow name | `E46-F3B-R5A Diagnostic Read Only` |
| Event | `workflow_dispatch` |
| Branch | `main` |
| Commit SHA | `3f8f923bf444f18b7ed5eed8ab738345f9b1a728` |
| Workflow source path | `.github/workflows/e46-f3b-r5a-diagnostic.yml` |
| Workflow source SHA256 (prior audited and postcommit readback) | `1e318115f31d15fc5feb7d0af0cb18c704a62c1e8d94f030809dbb1b2e4e10a4` |
| GitHub workflow ID | `380865984` |
| GitHub run ID | `38092783946` |
| GitHub job ID | `114332472709` |
| Attempt/number | `1/1`, `run_number=1` |
| Actor/triggering actor | `Reltroner` |
| API run created/started UTC | `2026-10-10T22:48:26Z` |
| API last updated UTC | `2026-10-10T22:48:48Z` |
| Approx API start-to-updated wall duration | **22 seconds**, NOT billable runner minutes metric |
| Run status and conclusion | `completed/success` |
| Job status and conclusion | `completed/success` |
| Entire repo run count at audit | **1** (no duplicate/retry) |
| Uploaded artifacts | **0** |
| Changes to sandbox after authorized root commit | **none observed** |

**All five job steps completed successfully:** Set up job; Initialize containers; Read-only PG18 Redis8 diagnostics; Stop containers; Complete job. Logs show standard `ubuntu-24.04` image and PostgreSQL/Redis OCI image pulls by exact previously verified index digest references. Both services became healthy, and all three job/service containers were stopped/removed by post-job cleanup. No host port mapping is present in the committed workflow; Docker `port` inspections alone do not constitute network segregation proof.

## 2. Exact runtime stdout assertions (short sanitized whitelist, no credentials)

```text
R5A_GITHUB_JOB_NETWORK_METADATA=PASS_SCOPED
R5A_POSTGRES_SERVER_VERSION_NUM=180006
R5A_POSTGRES_READONLY=PASS
R5A_REDIS_VERSION=8.10.2
R5A_REDIS_EMPTY_DB=PASS
R5A_DIAGNOSTIC=PASS_READ_ONLY_CANDIDATE_SCOPE
PG_R_REAL=0_OF_10_UNCHANGED_BY_THIS_DIAGNOSTIC
T02_HTTP_REAL=0_OF_86_UNCHANGED_BY_THIS_DIAGNOSTIC
```

- **PostgreSQL**: server `18.6`, numeric `180006`; synthetic `lms_synthetic` database / `lab_client` principal; real `psql` SELECT verifies both `default_transaction_read_only=on` and active `transaction_read_only=on`. Image service logs identify Postgres 18.6 x86_64; `pg_isready` PASS.
- **Redis**: real 8.10.2 (reported both INFO server response and Redis service startup logs); Bash RESP `PING`, `INFO server`, `DBSIZE` returned correct responses, key count 0; `timeout` binary, Bash TCP, connection and read flows worked in actual job.
- **GitHub topology**: job container and named `postgres`/`redis` service container IDs and GitHub-assigned Docker network metadata nonempty, same network, IDs distinct. This is scoped runner metadata assurance, **not a cryptographic Redis server identity proof**.
- **Functional limit**: No user-level SQL INSERT/UPDATE/DELETE/CREATE, Redis SET/DEL/FLUSHDB or signed HTTP request in R5A. The disposable PG service itself initialized a cluster, which is an internal startup write and is not the same as a user-level mutating acceptance test.

This is the **first actual real PG18 and Redis8 engine proof**, but it is a **READ-ONLY DIAGNOSTIC**, not the PG-R01..10 trust/replay/failover test matrix. Maintain `PG-R_REAL=0/10`, `CANONICAL_HTTP_T02=0/86`, `D02_RATIFICATION=HOLD`.

## 3. Warnings and risk classification before future R5-B

Actual service logs contain two security-relevant startup warnings:
1. PostgreSQL `initdb: warning: enabling "trust" authentication for local connections`. This is image/bootstrap-local auth behavior inside the ephemeral PG service. **Do not extrapolate that this would be acceptable for production PostgreSQL**; actual remote service auth and four owner-DB isolation permissions must be separately proven.
2. Redis **`WARNING: Redis does not require authentication and is not protected by network restrictions. Redis will accept connections from any IP address on any network interface.`** The Docker job had an ephemeral per-run network with no host-published Redis port, limiting exposure, but this is **NOT equivalent to Redis authentication/TLS or verified destructive-operation target identity**. Treat as **P1 gating issue before any `FLUSHDB` fault injection**. An R5B network+authentication/isolated target verification design is required; cannot infer permission from R5A success.

Further safety notes:
- GitHub container job runtime may mount Docker socket by default, which is a privilege exposure within the short-lived hosted runner; no workflow step used it intentionally. Pinning digests reduces mutable-tag drift, not all OCI image/supply-chain risk.
- Synthetic PostgreSQL password is deliberately nonproduction and appears in GitHub Actions setup log configuration; NEVER use the lab's known fixture password for real services, and do not copy raw log dumps into public progress documentation.
- Public hosted-runner pricing is generally $0 for standard runs on PUBLIC repos and budget Actions `$0 / Stop usage Yes` was re-observed in the owner's immediate GUI billing report; **actual post-run billable usage/cost was NOT re-read**. State `NO_PAID_RESOURCE_AUTHORIZED`, not `PROVEN_POST_RUN_SPEND=0`. The 22-second API wall duration is not an invoice.
- R5-A run approval was **one-time only and has been CONSUMED**. No reruns, new `workflow_dispatch`, source mutation or budget change without a new owner gate.
- The workflow and SSH/VPS/Cloudflare/Keycloak/prod source unchanged; `R5B` remains withheld and not executable.

## 4. Deterministic next work and GO/NO-GO

**Gate R5-A environment readiness:** `PASS_ACTUAL_GITHUB_HOSTED_DIAGNOSTIC`. This removes prior uncertainty about the pinned job image's Bash/psql/timeout availability and the real GitHub job/service container runtime.

**Gate R5-B future SQL-only nonproduction fault-injection:** `DESIGN_READY_FOR_INDEPENDENT_REVIEW`, **NOT AUTHORIZED**. Require exact-source review, verified isolated synthetic DB target, direct SQLSTATE+row-count proof, and separate first code commit and first dispatch. Do not use the R5-A run grant again.

**Gate R5-B future Redis8 FLUSHDB:** `HOLD_SECURITY_REDESIGN_AND_OWNER_CONSENT`. The no-auth Redis startup warning and lack of cryptographic endpoint proof make target scoping inadequate for a destructive command without stronger runtime restrictions. Prefer non-destructive `DEL` rehearsal (which is not PG-R03 FLUSH evidence), or add credential-validated isolated fixture and runtime allowlist before attempting actual loss injection. Must not point to production Redis.

**Absolute STOP:** No auto-rerun, no R5-B workflow commit, no SQL/Redis write, no modifications to LMS-BE/LMS-FE/VPS/production, no spending-cap change, no contract ratification, and no increment to replay/HTTP counters until their own exact evidence and explicit owner decisions exist.

**Current:** `R5A_1_OF_1=SUCCESS_PASS` | `ACTIONS_RUN_COUNT=1` | `OWNER_R5A_DISPATCH_PERMISSION=CONSUMED` | `R5B=HOLD` | `PG_R=0/10` | `T02=0/86` | `D02=HOLD` | `PRODUCTION=UNTOUCHED`.
