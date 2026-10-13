# Reltroner LMS Phase 4B-02 — E46-F3C-R5B PostgreSQL-Only Final Static Review and Secure Redis Local UDS/ACL Design

> Evidence date: 2026-10-11. **Scope:** review, audit, static tests, inert review artifacts only. No R5B runner, SQL write, Redis ACL change, FLUSHDB, first R5B workflow commit, or production mutation.
> Source-of-truth parents: [canonical README](./README.md), [end-to-end ledger](./engineering-end-to-end-progress-ledger.md), [frozen logical boundary](./logical-service-boundary-api-contract.md), [frozen infrastructure placement](./master-infrastructure-placement-contract.md), [actual R5A runtime PASS](./phase4b-02-e46-f3c-r5a-actual-github-actions-pg18-redis8-runtime-acceptance-20261011.md).
> Status: SQL-only STATIC REVIEW COMPLETE / ACTUAL PG-R01,R02 NOT RUN; Redis UDS+ACL SECURITY DESIGN PREPARED / ACTUAL REDIS AUTH NOT RUN; PG-R01..10=0/10; T02 HTTP=0/86; D02 HOLD.

## 1. Verified baseline and limits

Sandbox `Reltroner/lms-trust-sandbox` remains public, `main@3f8f923bf444f18b7ed5eed8ab738345f9b1a728`, one R5A read-only workflow, **exactly one** historical Actions run `38092783946`, attempt 1 success; previous one-time owner permission consumed. Actual PostgreSQL18.6 / Redis8.10.2 R5A diagnostic passed. R5A Redis service logs warned unauthenticated access; PostgreSQL initdb had local trust warning. These are not production-ready security settings. The last owner-supplied Actions billing evidence was $0 budget / Stop usage Yes before the run; post-run charge was not independently rechecked.

## 2. R5B-SQL-ONLY audit (new independent candidate, no Redis dependency)

Reviewed original SHA256-verified ZIP `LMS-E46-F3B-R5-split-candidates-REVIEW-ONLY.zip`. In original inert R5B combined source: PG-R01 used independent client subprocesses and `ON CONFLICT DO NOTHING RETURNING` (a scoped one-winner proof; NOT proof of deterministic scheduler overlap). PG-R02 used `BEGIN; INSERT workload; INSERT duplicate delegation; COMMIT;`, SQLSTATE 23505 and checks that first nonce rolled back, existing nonce survived, valid pair persisted. PG-R03 was mixed in with Redis and real `FLUSHDB`, outside SQL-only authority.

**Remediation:** a new **PostgreSQL-only candidate** has exactly one job+one synthetic PostgreSQL18 service, **zero Redis services/clients/ports**, one manual-only GitHub Actions trigger, explicit zero token permissions and 10-min standard public runner, pinned PostgreSQL job+service image. Bash source has unconditional `fail R5B_SQL_ONLY_SOURCE_LOCKED_NOT_AUTHORIZED` **before any DB/network I/O**; ZIP workflow source is `.yml.txt`, not an active workflow.

Scoped tests after separate future owner commit/run gates:
- PG-R01: two real PG client processes launch independently, exactly one successful durable `r5b-r01` claim and DB count one; cannot claim a deterministic interleaving barrier. SQL grammar includes `WHERE true` before `ON CONFLICT` to avoid INSERT SELECT parser ambiguity.
- PG-R02: preseed delegation collision, run an explicit two-reservation SQL transaction, require nonzero status AND SQLSTATE **23505 on stderr**, ensure first claim absent and pre-existing claim still exactly one; valid two-nonce pair then commits. Exactly four expected final table rows; fail closed on unexpected fixtures.
- Fresh table `public.r5b_sql_nonce_claims` created only inside `lms_synthetic`, principal `lab_client`, PG18.x, active transaction read-write checked explicitly; fixture-exists check prevents silent reuse.
- This tests *synthetic PostgreSQL semantics only*. Neither Keycloak, JWS, LMS middleware, nor PG-R03 and canonical T02 are exercised.

**Static proof actually performed:** `bash -n` PASS; YAML PyYAML BaseLoader PASS; trigger only `workflow_dispatch`; only PostgreSQL service, no host port map, no external `uses:`; standalone Bash equals workflow-inline Bash. Running the Bash source in the isolated assistant shell caused deliberate exit code **1** and `R5B_SQL_STOP=R5B_SQL_ONLY_SOURCE_LOCKED_NOT_AUTHORIZED` before any external command. No PostgreSQL engine or SQL statements executed; `PG-R01=0/10` and `PG-R02=NOT RUN`.

**Review-only ZIP:** `LMS-E46-F3C-R5B-SQL-only-Redis-security-review-20261011.zip`, SHA256 **f87f189a00dea4ec46cdf7b1166a44ca0e87fce5236de816c12a2796ca979f94**, 9317 bytes.
- `R5B-SQL-ONLY-WITHHELD.sh.txt` SHA256 `a6a61eae93c9efd718ccbc34ff1b07433834cc71f410ff62a7a66a2e42284396`.
- `R5B-SQL-ONLY-WORKFLOW-SPECIMEN.yml.txt` SHA256 `5e5b9c17c949b1510139f19681e61b7ebd9a48f92fe45347a08cfbc50574df4b`.
- `R5B-REDIS-SECURITY-NO-FLUSH-THREAT-MODEL.md` SHA256 `bb7f73c3f043787dfc8cf51f524aa973748990802783170e7e6fe7f8747a3257`.
- README plus SHA256SUMS included. User-visible review artifact, NOT a GitHub executable or accepted PG test.

## 3. Redis security: move authorization proof to LOCAL Unix socket job container, not open default service

**Security issue**: R5A's Docker bridge and no host-published Redis port reduce blast radius, but the Redis service was started without ACL/authentication. An arbitrary client on that bridge could attempt commands; GitHub job metadata does not cryptographically authenticate remote hostnames. Redis ACLs can restrict named user commands and keys; **FLUSHDB is database-wide** and cannot be restricted to one key prefix.

**Preferred new design (source prepared, NOT runtime tested):**
1. Separate Redis8 Official Image **job container**, no GitHub Redis service and no PostgreSQL. On startup GitHub runner executes the job container with a non-server process; the **job script** would create a fresh 0700 private local directory, two separate 256-bit run-scoped passwords from `/dev/urandom`, and a Redis ACL file in mode 0600 **before launching Redis**.
2. Start Redis as a child with `--port 0` (no TCP listener) plus `--unixsocket`, `--unixsocketperm 700`, `--aclfile` and no AOF/snapshot persistence, all scoped to a disposable local filesystem. **Default user OFF before listener startup**. The only transport is local Unix socket within the same ephemeral job container, so no Redis DNS target can be confused with a production Redis endpoint.
3. Named `lab_observer` has only `+ping +info +dbsize`; named `lab_auditor` has only those commands and `+acl|dryrun`; both are authenticated. No `+@all`, keyspace mutations, data sets, `+flushdb`, `+config` or general ACL admin powers.
4. Validate fresh unauthenticated/wrong-password denials, authenticated PING/DBSIZE/INFO and version 8.x, empty DB, then **Redis ACL DRYRUN** for `lab_observer FLUSHDB` and unauthorized SET, with explicit refusal, plus DRYRUN positive for PING. `ACL DRYRUN` simulates authorization without executing the command. Actual `FLUSHDB` is NEVER issued.
5. Cleanup terminates the local Redis process and removes socket/ACL file even on failure; no secrets/credentials in GitHub YAML, CLI password command-line arguments, public logs, artifacts, cache or production systems.
6. Runtime prerequisites like Redis-job-image `bash`, `redis-cli -e`, `redis-server`, coreutils, ACL-file parsing, socket startup and exact Redis8 DRYRUN outputs remain **NOT YET VERIFIED**; static review and source interlock alone are insufficient.

**Review-only Redis ZIP:** `LMS-E46-F3C-R5B-Redis-UDS-ACL-security-review-20261011.zip`, SHA256 **0d73b7f27fe45b05c040f2c21db91ade8173a3559ab550897db0f9e0e10a5cf8**, 5115 bytes:
- `R5B-REDIS-UDS-ACL-WITHHELD.sh.txt` SHA256 `6c1bd7b58fa2ad974f9366f7a83196c98bd692c968eae81bc77c31b35d88b48d`.
- `R5B-REDIS-UDS-ACL-SECURITY-WORKORDER.md` SHA256 `54135383e1d6bbc698246a9a103c528bfc3cd07a72f0e3615b5a9383b0a23b44`.
- README and checksum manifest also included.

**Static proof:** `bash -n` PASS; direct Bash execution exited **1** with `R5B_REDIS_SECURITY_STOP=R5B_REDIS_LOCAL_AUTH_SOURCE_LOCKED_NOT_AUTHORIZED` before starting Redis or issuing any command. Redis real ACL authentication tests **0**; keyspace deletion **0**.

## 4. Explicit residual blockers and architecture boundary

This new standalone local-UDS Redis security approach substantially reduces initial exposure and DNS target ambiguity **at design level**, but its startup/ACL behavior requires a future **separately owner-approved security-only first workflow commit** and later **separately owner-approved one-time run**. Do not assert Redis target authentication is already proven. This standalone UDS diagnostic is **not** yet the combined PG+Redis topology PG-R03 needs; the future integration of SQL durable authority with secure Redis loss needs another frozen source/permission design. Never silently use auth-disabled bridge Redis, share credentials, publish Redis ports, rerun R5A, or promote SQL-only/ACL static evidence to the PG-R counters.

**Acceptance gate sequence:** R5B-SQL-DESIGN=PASS_STATIC_LOCKED, R5B-SQL-ACTUAL=NOT_RUN; R5B-REDIS-ACL-DESIGN=PASS_STATIC_LOCKED, R5B-REDIS-ACL-ACTUAL=NOT_RUN, R5B-REDIS-TARGET-SECURITY=HOLD_RUNTIME, PG-R03-FLUSHDB=NOT_AUTHORIZED, PG-R01..10=0/10, T02=0/86, D02 design ratification HOLD, production untouched.

## 5. Decision and next actor

No current owner permission grants a new executable workflow file or run. Safest next bounded decision is **owner approval for the SQL-only R5B first-commit candidate** (source frozen after independent code review; no run), OR to prioritize an independent Redis security-only diagnostic first. The previous R5A authorization cannot be reused. For Redis target assurance, recommend approving a separate **non-destructive security-only UDS/ACL diagnostic run after the exact-source audit**, before any consideration of keyspace-loss injection.

Official technical references: [Redis ACL](https://redis.io/docs/latest/operate/oss_and_stack/management/security/acl/), [ACL DRYRUN](https://redis.io/docs/latest/commands/acl-dryrun/), [Redis security](https://redis.io/docs/latest/operate/oss_and_stack/management/security/), [GitHub service networks](https://docs.github.com/en/actions/tutorials/use-containerized-services/use-docker-service-containers).
