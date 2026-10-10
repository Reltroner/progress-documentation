# Reltroner LMS Phase 4B-02 — E46-F3B-R5 Read-Only Diagnostic and Withheld Fault Injection

**Record:** LMS-P4B02-E46-F3B-R5-20261011. **Authority:** [Canonical README](./README.md), [frozen physical placement](./master-infrastructure-placement-contract.md), [frozen logical service contract](./logical-service-boundary-api-contract.md), [R4 risk audit](./phase4b-02-e46-f3b-r4-owner-zip-integrity-and-static-client-network-risk-review-20261011.md). R5 is a nonproduction source-design work order, not an architecture contract amendment.

**Authorization:** Owner requested creation and audit of separate R5-A (read-only) and R5-B (destructive, withheld) candidates. This does NOT authorize the first sandbox default-branch workflow commit, starting Actions, pulling image layers, creating database services, destroying a Redis keyspace, production access, or changing the $0 spending budget.

## 1. Current acceptance

| Gate | Status |
|---|---|
| Public sandbox provisioning | PASS owner GUI + connected GitHub |
| Actions origin Reltroner-only and full-length action SHA | PASS owner post-refresh screenshot |
| Account Actions $0 / Stop usage Yes | PASS owner GUI snapshot; enforcement not live-tested |
| OCI index and linux/amd64 SHA256 digests | OWNER-OPERATOR PASS 3/3 manifest metadata |
| R5-A source/YAML/Bash syntax | PASS offline scoped |
| R5-A Redis RESP parser with local fake socket | PASS mock 3/3; NOT Redis8 |
| R5-A actual PostgreSQL18 and Redis8 runtime | NOT RUN |
| R5-B source | WITHHELD, unconditional early STOP |
| R5-B real SQL/Redis fault injection | NOT AUTHORIZED / NOT RUN |
| First sandbox main workflow commit | HOLD, separate owner permission |
| First manual standard runner start | HOLD, separate owner permission |
| PG-R01..10 real / canonical T02 HTTP | 0/10 / 0/86 |
| D02 owner trust design ratification / production | HOLD / NOT AUTHORIZED |

## 2. R5-A diagnostic-only candidate — inspect without changing business state

The candidate file R5A-DIAGNOSTIC-CANDIDATE.yml is a **workflow specimen** outside any active .github/workflows directory. The source includes a single workflow_dispatch job with ubuntu-24.04 standard public runner, 10-minute timeout, permissions empty, zero external uses, zero host-published ports, no artifacts/cache, no additional packages, and immutable-index pinned job PostgreSQL image plus PostgreSQL and Redis service images.

Runtime command checks, only once separately authorized:
1. Require Github Actions event workflow_dispatch, exact Reltroner/lms-trust-sandbox repository, main ref, exact workflow path; validate job container plus postgres/redis service ID and common network from GitHub job contexts. This is **metadata evidence, not cryptographic peer attestation**.
2. Verify Bash, psql, pg_isready and GNU timeout availability in the pinned PostgreSQL job container. The job image has NOT been started or independently inspected for executable availability.
3. PostgreSQL pg_isready plus one SELECT query under PGOPTIONS default_transaction_read_only=on. Require server_version_num 18.x, database lms_synthetic, role lab_client and default read-only session mode on. No CREATE, UPDATE, INSERT or DELETE issued by the diagnostic.
4. Redis PING, INFO server and DBSIZE only, using a custom, time-bounded Bash RESP reader. Require Redis 8.x and an initially empty disposable Redis DB. No SET, DEL, FLUSHDB, EVAL or key mutation.
5. Fail closed on mismatch, missing context, unavailable service, incorrect version, unsafe read-only configuration, protocol timeout or malformed response. Do not output secrets or production data.

**Clarification:** Even R5-A starts disposable PostgreSQL and Redis service containers when later approved; PostgreSQL itself initializes files/cluster state. Read-only means **the diagnostic scripts issue no SQL business writes or Redis mutations**, not literally zero internal system disk writes.

## 3. Exact conversation artifact and provenance

The separate review-only ZIP has size **10864 bytes** and SHA256 **91b8cd9bd7750a81ab1489362741c3e27ec6aca0ee0fb5e37e0d303909818125**. It was generated in the assistant scratch environment and is not in GitHub sandbox or docs source control. Preserve/upload the exact ZIP for an independent AI code audit; merely quoting hashes does not recreate its contents.

| Member name | SHA256 (UTF-8 bytes) | Lines |
|---|---|---:|
| R5A-DIAGNOSTIC-CANDIDATE.yml | 3d61fb43f5b9f4c3f6c1b759ccdbb682b731459568b711c653e4327adcd7a25e | 131 |
| R5A-diagnostic.sh | 450a8837db293cae4d3a94a81027eda1a21325bee648a486d7f8c4c6d9564605 | 78 |
| R5B-WITHHELD-fault-harness.sh.txt | 256789de8a399d7d70cd871f0bb3309abc5c09df486c7c914551d2b174648b5c | 112 |
| R5B-DESTRUCTIVE-GATE-CONTRACT.md | 5f96f64825896d55f3c32d6c7b77edf0ce1d281c65cb7e8a658b62eda69d7414 | 45 |
| README-REVIEW-ONLY.md | 607573038c68d0ebcc3052745f3df3963a14120bb5e7c81d33cc013be5a3b87c | 41 |

Archive includes SHA256SUMS.txt (SHA256 9ab45154aaf1019acca813eb155c946dc08366cfa495ef3d44b2601963caac0c). All member hashes verified after final packaging.

**Offline checks:** Bash -n R5-A and R5-B PASS. PyYAML BaseLoader parse PASS, one manual event/job, zero marketplace uses, zero host ports, 10-minute standard Ubuntu runner, empty permissions, digest-pinned job/services; YAML inline Bash matches standalone exact content. R5-A has zero user SQL mutating statements and zero Redis mutation commands. ShellCheck and actionlint NOT INSTALLED/NOT RUN. There is no live GitHub runner, PostgreSQL18 or Redis8 test.

**Bug remediation before runtime:** R4 INFO RESP had unescaped $4 and $6 literals in a nested double-quoted printf, potentially corrupting the request. R5 candidate escapes literal dollar bytes. An initial R5-A local fake-server run FAILED because INFO bulk trailing CRLF was not consumed before DBSIZE; this was repaired. After fix, a localhost Python RESP simulator accepted Redis 8.4.1 with empty DB, rejected Redis 7.4.2, and rejected Redis 8.4.1 with nonempty DB: **three mock cases PASS**, not a claim of real Redis functionality.

## 4. R5-B destructive source expressly LOCKED

There is **NO R5-B runnable workflow YAML**. The R5B-WITHHELD-fault-harness.sh.txt is an inert review reference derived from R4 and corrected for dollar literal formatting; it contains **an unconditional fail R5B_LOCKED_NOT_AUTHORIZED_IN_REVIEW_SOURCE** before any network/database operation. Do not remove this interlock without a new exact-source review and explicit user approval after actual R5-A diagnostic PASS.

Intended, not executed: PG-R01 two SQL clients contest unique nonce (one persistent acceptance), PG-R02 two-assertion reservation atomicity with SQLSTATE 23505 duplicate and rollback, PG-R03 Redis8 real disposable FLUSHDB with independent PostgreSQL replay denial. R5-B is **not a security proof** of LMS middleware or real signed HTTP, nor of PG-R04..10. A fresh keyspace and shared GitHub network labels are necessary precautions but are **not authentication** of Redis target; destructive execution requires a risk-assessed disposable-service guard and separately approved run, potentially splitting SQL-only and Redis-FLUSH into separate sub-gates.

## 5. Deterministic owner change-control for continuation

**Next F3-B decision:** After source review, obtain express authorization solely for bootstrapping exact R5-A diagnostic workflow onto previously empty sandbox main (named authorization ALLOW_F3B_R5A_FIRST_DEFAULT_BRANCH_COMMIT). Do NOT imply that review/source generation already authorized first commit.

**Next F3-C decision:** After default-branch workflow source hash verified, obtain separate ALLOW_F3C_R5A_FIRST_MANUAL_DIAGNOSTIC_RUN. Only then launch one standard public hosted runner and disposable PG18+Redis8 services, collect engine versions, metadata/diagnostic markers, run ID, evidence SHA, timing and spending. If Actions $0 Stop-usage budget blocks runner, STOP, do not raise spending cap.

**Only after R5-A real PASS** begin R5-B final risk/source review. Require explicit new owner commit and execution approvals before any CREATE/INSERT/ROLLBACK/FLUSHDB commands. Do not let approval of R5-A imply approval of R5-B.

No LMS-BE/LMS-FE, Keycloak, VPS, public production databases, Cloudflare, HRM or production settings were changed by R5.


## 6. R5-A first default-branch bootstrap actually executed and verified (2026-10-11)

**Superseding current state:** user requested first commit limited to exact reviewed R5-A diagnostic only, WITHOUT job run. The assistant performed final static source review, improved PostgreSQL SELECT to verify active `transaction_read_only=on` as well as default, anchored Redis8 version regex, then committed **one** `.github/workflows/e46-f3b-r5a-diagnostic.yml` to previously empty `Reltroner/lms-trust-sandbox/main`. Actual root commit `3f8f923bf444f18b7ed5eed8ab738345f9b1a728` parent count 0; GitHub returned YAML blob `d2f616c72e7c225431b54b2fa51d0e5b7b4139b8`. **Post-commit GitHub content SHA256 equals locally audited final YAML `1e318115f31d15fc5feb7d0af0cb18c704a62c1e8d94f030809dbb1b2e4e10a4`**. One tree leaf file, branch main only and Actions runs **0**. R5-B still absent/uncommitted/locked. Initial commit approval consumed; NO approval to dispatch. [Exact source, immutable SHA, and separate F3-C first-run GO/NO-GO matrix](./phase4b-02-e46-f3b-r5a-first-diagnostic-bootstrap-commit-and-first-run-decision-20261011.md). 4/4 fake RESP tests incl malformed version, no real PG/Redis runtime; first-run proposal CONDITIONAL_GO_ONLY_IF_OWNER_SEPARATELY_APPROVES. PG-R 0/10, T02 0/86; D02/production HOLD.
