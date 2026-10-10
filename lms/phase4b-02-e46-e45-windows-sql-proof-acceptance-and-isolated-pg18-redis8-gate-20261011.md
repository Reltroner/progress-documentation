# LMS Phase 4B-02 — E46: E45 Windows PDO_SQLite acceptance and next real PostgreSQL 18 / Redis 8 isolation gate

> **Record:** `LMS-P4B02-E46-20261011`  
> **Evidence status:** `E45_WINDOWS_SQLITE_8_OF_8_OWNER_OUTPUT_PASS / E40_WINDOWS_CRYPTO_MODEL_30_OF_30_OWNER_OUTPUT_PASS / E46_REAL_PG18_REDIS8_NOT_RUN / OWNER_DESIGN_RATIFICATION_HOLD`.  
> **Authorized scope:** document receipt and **read-only Windows environment/safety discovery**. Not authorization to install Python, start Docker/WSL, pull container images, run Redis/PostgreSQL, connect to production, change source/frozen contracts, perform migration, merge PR or deploy.  
> **Source pins observed before documentation:** `Reltroner/LMS-BE/main=617dadc0d0d627071d713ceb729df6658202b43e`; `Reltroner/progress-documentation/main=183372371b3a40a0349ac390848911273ccd2361`; PR #46 draft design branch OPEN. Reverify immediately before any later source/code action.  
> **Frozen authority:** [Phase 0C placement](./master-infrastructure-placement-contract.md), [Phase 1 logical/API](./logical-service-boundary-api-contract.md), [ADR-LMS-TRUST-001 nonproduction design only](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md), [E40 D02-01..05 decision proposal](./phase4b-02-e40-owner-design-decision-d02-01-to-d02-05-and-ratification-reassessment-20261011.md), [README §7](./README.md).

## 1. Operator evidence — exact E45 Windows acceptance

The owner pasted the entire Windows PowerShell 5.1 E45 session, including:
- `E45_PHP_PROOF_SHA256=PASS`; `E45_PS51_RUNNER_SHA256=PASS`; PHP runner `E45_GATE01_PHP_SOURCE_SHA256=PASS`, `E45_GATE02_LOCAL_PDO_SQLITE=PASS`, `E45_GATE03_PHP_SYNTAX=PASS`.
- All exact case IDs **SQL-001 through SQL-008 PASS**, mapping to: atomic two-nonce commit, unique replay denial, rollback on delegation duplicate, persisted nonce after **simulated** Redis cache flush, persistence after reopening SQLite connection, actual concurrent two PHP child processes exactly one succeeds/one denied, rollback when child exits before COMMIT, and fail-closed missing SQL authority.
- `SQL_SUMMARY total=8 passed=8 failed=0`, `SQL_ENGINE=PDO_SQLITE_ACTUAL_SQL_TRANSACTIONS_NOT_POSTGRESQL18`, `E45_GATE04_PHP_PROCESS_EXIT=PASS_0`, `E45_GATE05_SQLITE_SCENARIOS=PASS_8_OF_8`, `E45_FINAL_RESULT=PASS_LOCAL_PDO_SQLITE_8_OF_8`.
- `LIVE_REDIS_SERVER_ACCESSED=NO`, `LIVE_POSTGRES_SERVER_ACCESSED=NO`, `LIVE_KEYCLOAK_ACCESSED=NO`, `PRODUCTION_ACCESS=NO`, `PG18_REPLICA_FAILOVER_AND_WAL_PROOF=NOT_PERFORMED`. The owner also reported `SOURCE_MAIN_MERGE=NOT_PERFORMED` and `PRODUCTION_MUTATION=NOT_PERFORMED`.

**Evidence provenance:** These are **operator-submitted actual Windows process output lines**, not an independent agent-controlled Windows session. The provided output and the source SHA checks support `E45_WINDOWS_PDO_SQLITE=PROVEN_SCOPED_8/8`, **not** PostgreSQL18/Redis8 availability or security. Independent earlier PHP harness SHA256 observed in the assistant session: `4DBBD24D495587788FACF9D4B60D73625B5A1B8C04E5325CAA14DAA922928A35`; runner `7EE19ED7FF1083572F9B53F7A09655B4411F6F1C5555744A9954DDABB40A89DE`. The existing original Python-backed E41 SQL tests were **not** run on owner Windows; E45 is an independently implemented equivalent test family.

The owner has now reported **30/30 E40 local crypto/replay-model tests + 8/8 E45 real PDO_SQLite tests = 38/38 LOCAL EXPLORATORY PASS**. These are **not** 38 of the canonical 86 HTTP T02 tests: `T02-001..086=86_DRAFTED/0_REAL_HTTP_EXECUTED`.

## 2. What E45 resolves, and what it cannot resolve

**Resolved under actual local Windows SQLite engine:** ordinary SQL unique nonce constraints, two-role atomic transaction, persistence across connection close/reopen, race safety across two PHP processes, rollback before commit and conservative authority failure, using disposable TEMP SQLite and no application or production database.

**Not resolved:** acknowledged PostgreSQL18 COMMIT durability during crash/standby failover/restore; actual Redis8 eviction/flush/ACL/unreachable/unknown reply; loss of authoritative SQL history; cross-service owner-DB grants; transaction integration with Laravel HTTP/authz/outbox; resource consumption and latency on ~2.84GiB free RAM; Keycloak effective signed access-JWT algorithm; on-wire two-JWS verification; multiworker Keycloak/replay; post-deploy rollback; the 86 canonical HTTP scenarios.

**Critical security finding retained:** E40 Redis-only silent selective loss and full flush intentionally accepted a consumed nonce again in the vulnerable model; those two PASS markers are **counterexample PASS**, proving that a Redis-only integrity guarantee fails under unobservable nonce deletion. E45 SQL alternative reduces *this* failure mode if a genuinely durable, correctly fenced SQL authority is adopted, but **does not mean Redis is fixed or D02-02 closed**.

## 3. E46 constrained engineering decision: no runtime before a safe physical isolation boundary

E44C owner inventory observed Docker and WSL CLIs present (not executed/validated), Docker Desktop service `Stopped_READ_ONLY_OBSERVATION`, PostgreSQL18 binaries/psql not on PATH, Redis server+CLI executable names present (not runtime-verified), ~15.33GiB total RAM/2.84GiB free/45.86GiB local C: free. **No actual isolated containers or databases exist as verified evidence**. Because Docker CLI could point to a remote/prod daemon and Docker Desktop may require extra memory, **do NOT call `docker info`, `docker run`, `docker compose up`, `docker context use`, `wsl --install`, Redis/Pg commands or any remote SSH by inference from CLI presence.**

The next safe action is **E46-F0 offline isolation eligibility**, designed to record only environment risks (never dump secrets):
- Read only Windows environment variable *presence*, not their contents: `DOCKER_HOST`, `DOCKER_CONTEXT`, `DOCKER_TLS_VERIFY`, `DOCKER_CERT_PATH`, `CONTAINER_HOST`, `KUBECONFIG`.
- Read only Docker config/context **metadata**, without printing endpoint URL, auth values, certificates or accessing daemon; if configuration is ambiguous/remote, `ISOLATION_ELIGIBILITY=BLOCKED_REVIEW`.
- Confirm physical local memory and disk headroom and owner-approved no-spend budget. Existing 2.84GiB available RAM may be insufficient for safe test Docker Desktop+PG18+Redis8 operation while other workloads are active.
- Read only whether local Docker Desktop service is running; **do not start it**. No extension installations or image pulls.
- Record machine and tool availability without assuming version. A CLI present is never a real PG18 or Redis8 PASS.

**Next E46-F1 conditional owner-approved local sandbox:** Before creating even a disposable local container, require explicit documented human signoff for (a) on-machine-only local Docker context isolation and no production endpoint, (b) resource caps and no extra spending/network pulls unless separately approved, (c) images pinned to trusted exact OCI digests, (d) no host bind of production volumes or socket, no production .env/SSH keys, no external DB endpoints, (e) immutable container ownership/lifetime/delete policy, (f) no localhost port published unless separately needed, and (g) fault injection restricted to disposable, uniquely named test resources. Direct SQL/Redis networking may be needed **inside isolated network only**, not the Internet. If these are not independently satisfied, **HARD STOP without attempting real tests**.

**No choice of replay-authority ADR is implied:** Existing ADR-LMS-TRUST-001 ratified Redis as an ephemeral replay store **for nonproduction design**, subject to independent lost-state safety proof. A PostgreSQL18 owner-domain transactional ledger would materially revise that authority and requires new explicit human approval (e.g. owner-reviewed `ADR-LMS-TRUST-002`), no fifth DB, capacity and permission review. Redis-only options need an independently falsifiable prevention/detection model for selective silent loss; simply PING/noeviction/local elapsed timer does not provide universal assurance.

## 4. Planned real-engine negative/failure tests, once separately authorized

Keep `PG-R01..PG-R10` as **proposed test plan, zero actual real-engine executions**:

| ID | Isolated PostgreSQL18 / Redis8 experiment | Required evidence / STOP |
|---|---|---|
| PG-R01 | SQL unique nonce claims from competing database sessions | Exactly one committed reservation and all duplicates denied |
| PG-R02 | Atomic two-proof insert where second nonce conflicts | Full SQL rollback, no partial phantom insert |
| PG-R03 | Real disposable Redis8 `FLUSHDB` or controlled eviction **after** SQL durable commit | Reused nonce denied by PG authority, even if Redis key absent; never run against shared Redis |
| PG-R04 | Kill isolated worker after commit, restart against same preserved owner DB | Previously consumed nonce remains blocked |
| PG-R05 | PG unavailable, permission rejected, transaction deadlock/timeouts, ambiguous commit acknowledgment | Deny unknown state, no Redis fail-open or automated unsafe retry |
| PG-R06 | Restart test-only PostgreSQL18 instance with persisted WAL | Previously acknowledged nonce survives, otherwise hard stop for runtime |
| PG-R07 | Standby promotion when previous acknowledged commit is missing | Fail closed and quarantine/fence before accepting fresh workload; requires a separate replica test topology, do not assert success merely because single-primary test passes |
| PG-R08 | Expired nonce cleanup during concurrent transactions and clock skew | No deletion of still-valid nonce; retention and WAL pressure measured |
| PG-R09 | Bounded 100/1000 request benchmark at hard CPU/RAM/disk limits | Capture latency, locks, WAL, memory, disk; no performance promise without results |
| PG-R10 | Four existing owner DB grants and service access boundaries | No unauthorized cross-owner DB reads/writes or fifth DB; assistant service remains without owned PostgreSQL domain DB |

**Proof of safety must include real fault-injection on actual versioned engines, independent verification of no side effects, postcrash durable state, image/content digests and exact test provenance.** Early subset success cannot be called all-ten PASS.

## 5. Nonproduction ratification gate — STOP unchanged

`D02-01=CRYPTO_MODEL_PROOF_PASS_BUT_ON_WIRE_OWNER_APPROVAL_PENDING`; `D02-02=SQLITE_LOCAL_8_OF_8_PASS_BUT_REDIS_ONLY_UNSAFE_AND_REAL_PG18_REDIS8_UNTESTED`; `D02-03=HTTP_ERROR_POLICY_OWNER_APPROVAL_PENDING`; `D02-04=TEST_KEYS_MODEL_SCOPE_ONLY_REAL_SANDBOX_NOT_AUTHORIZED`; `D02-05=EFFECTIVE_KEYCLOAK_OIDC_ALG_AND_CLIENT_GRANTS_UNVERIFIED`; `CANONICAL_T02_HTTP_0/86`; `BE_SOURCE_CODING_NOT_AUTHORIZED`; `PRODUCTION_NOT_AUTHORIZED`.

Engineering end goal remains a secure integrated Reltroner LMS with sole public `https://lms-api.reltroner.com` Gateway, five private providers, exact 26 public operations and 19 capability contracts, four existing owner PostgreSQL domain DBs (`lms_learning_db`, `lms_mentorship_db`, `lms_knowledge_db`, `lms_audit_db`), Keycloak OIDC, reliable internal dual-proof trust/replay, and actual end-to-end frontend/backend/observability/AI integration. An AI cannot certify “zero risk/no technical debt”; it can eliminate **known** contract gaps through falsifiable gates and halt at unknowns.

**Checkpoint:** `E40_WINDOWS_30/30_OWNER_PASS -> E44C_OFFLINE_PASS -> E45_WINDOWS_8/8_OWNER_PASS -> E46_F0_OFFLINE_ISOLATION_READINESS_NEXT -> PG18_REDIS8_REAL_TESTS_NOT_RUN -> ADR_D02_01..05_PENDING -> PHASE4B02_DESIGN_RATIFICATION_HOLD -> PRODUCTION_NOT_AUTHORIZED`.

## 6. E46-F0 deterministic offline Windows isolation preflight artifact — prepared, not yet run (2026-10-11)

A **standalone Windows PowerShell 5.1** `LMS-P4B02-E46-F0-OFFLINE-ISOLATION-PREFLIGHT-PS51.ps1` was generated in the conversation artifacts with SHA256 **`560038D47ADB98FCA547C74D9CF089A527EC798707461D68731BB236920C389B`**. It contains **144 CRLF lines** and UTF-8 BOM; static checks found **no** `docker info`, `docker run`, `docker compose`, `wsl --`, Redis/PG connection CLI calls, SSH, remote HTTP, package install, service start, source edit or destructive delete. The exact file is **not committed to GitHub** and has **not** run in the owner's Windows session. Download/check SHA before execution, and preserve original output/report.

The script outputs only whether sensitive Docker-related environment variables are **SET/UNSET**, never their values. It locally reads Docker `config.json` solely for whether `currentContext` is defined and counts `meta.json` metadata files without printing endpoint URLs or credentials. It obtains read-only Docker Desktop service status and host free RAM/system drive disk via CIM. It never calls `docker.exe` or any daemon; it never starts Docker Desktop. It records a report in TEMP with `E46_F0_FINAL=PASS_READONLY_FACT_COLLECTION_ONLY` when read-only inventory completes. **That PASS explicitly does NOT authorize or imply safe environment ready to start containers**, and risk flags can still be `BLOCKED_PENDING_OWNER_ENVIRONMENT_REVIEW`. Failures write `STOP_REASON` and exit nonzero.

**Owner exit needed:** Return `E46_F0_FINAL`, `E46_ISOLATION_ELIGIBILITY`, `ISOLATION_FLAG` (if any), `DOCKER_DESKTOP_SERVICE`, `HOST_RAM_FREE_GIB`, `SYSTEM_DRIVE_FREE_GIB`, `E46_F0_REPORT_PATH`. These metadata contain no connection strings, credentials or raw token. Next engineering must decide whether the workstation can safely run **genuinely local, disposable, digest-pinned PostgreSQL18+Redis8 instances**, or whether to choose another zero-extra-spend isolated machine/test profile. Do not start anything until owner explicitly signs off the physical boundary and resource limits.
