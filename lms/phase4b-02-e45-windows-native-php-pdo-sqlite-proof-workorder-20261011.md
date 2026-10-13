# LMS Phase 4B-02 — E45 Native Windows PHP PDO_SQLite Replay Ledger Proof Work Order

> **Evidence ID:** `LMS-P4B02-E45-20261011`  
> **Stage:** `WINDOWS_PDO_SQLITE_TEST_HARNESS_PREPARED / STATIC_QA_PASS / WINDOWS_RUNTIME_NOT_RUN`.  
> **Owner data from E44C (2026-10-11 03:09 +07):** `PHP_CLI=FOUND`, `PHP_SQLITE3_EXTENSION=PRESENT`, `PHP_PDO_SQLITE_EXTENSION=PRESENT`, `WINDOWS_NATIVE_SQLITE_DLL=PRESENT_NOT_INVOKED`, `E44_READONLY_INVENTORY=PASS`, `E44C_FINAL=OFFLINE_DISCOVERY_PASS`. Docker CLI and WSL CLI were found but not contacted; Docker Desktop service observed **Stopped**. Local machine approximately **15.33GiB total RAM, 2.84GiB available, 45.86GiB C-drive free** at discovery. PostgreSQL server/psql binaries not on PATH; redis-server/redis-cli command names present but not runtime verified. No Redis/PostgreSQL production access.  
> **Authority:** [README §7 clarity-first](./README.md), [frozen Phase0C](./master-infrastructure-placement-contract.md), [frozen Phase1 logical](./logical-service-boundary-api-contract.md), [ADR-LMS-TRUST-001 (NONPRODUCTION DESIGN ONLY)](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md), [E40 owner decisions](./phase4b-02-e40-owner-design-decision-d02-01-to-d02-05-and-ratification-reassessment-20261011.md), [E44C operator recovery](./phase4b-02-e44c-file-format-checksum-remediation-and-inline-discovery-20261011.md).  
> **Main source pins observed:** `LMS-BE/main=617dadc0d0d627071d713ceb729df6658202b43e`; `progress-documentation/main=183372371b3a40a0349ac390848911273ccd2361`; documentation PR #46 still OPEN. Revalidate before future source work.

## 1. What is proved vs what is not yet proved

E44C on the owner's Windows host establishes that a PHP CLI already has **two usable candidate extensions** listed: `sqlite3` and `pdo_sqlite`. This is an extension discovery, **not actual SQL transaction evidence**. The original E41 Python-backed SQLite proof was run 8/8 successfully in the assistant isolated Linux environment; Python 3.8+ executable was not discoverable by E43S on owner Windows and E41 **has never been run there**. E40 Windows PHP/Sodium 30/30 was owner-reported PASS but those were independent cryptographic/replay **model** cases.

E45 supplies an **independent PHP-only real SQLite engine runner** with the **same eight scenario families** but a new implementation. The goal is to verify owner-local SQL rollback and multi-process nonce uniqueness **without Python, Docker, Redis or PostgreSQL 18**. It is a *separate E45 test suite*, not a claim that the original Python E41 harness magically ran on Windows, and is not equivalent to full 86 real HTTP/Laravel acceptance. Redis-only `jti` replay acceptance after silent loss remains an **UNSAFE design counterexample**, even if E45 SQLite passes.

## 2. Exact proposed operator artifacts — both standalone files, no ZIP

The assistant generated **two directly downloadable conversation artifacts**, with **no ZIP and no `Expand-Archive`**, placed by the operator into `Downloads`:

| File | SHA256 (uppercase) | Scope |
|---|---|---|
| `LMS-P4B02-E45-PDO-SQLITE-PROOF.php` | `4DBBD24D495587788FACF9D4B60D73625B5A1B8C04E5325CAA14DAA922928A35` | PHP 8.2+ `PDO_SQLite` SQL transaction/nonce fixture with workers |
| `LMS-P4B02-E45-RUN-WINDOWS-PS51.ps1` | `7EE19ED7FF1083572F9B53F7A09655B4411F6F1C5555744A9954DDABB40A89DE` | PowerShell5.1 UTF-8 BOM/CRLF runner, PHP source SHA/lint guard, fresh TEMP report, 8-case strict verdict |

A SHA verification **must** occur before executing the downloaded `.ps1`. The PowerShell script itself validates the `.php` SHA, installed active CLI `pdo_sqlite` module, lint output, process exit, exact eight `PASS SQL-00x` lines, `SQL_SUMMARY total=8 passed=8 failed=0` and exact environment isolation markers. It uses `ProcessStartInfo` rather than error-prone native pipeline `2>&1` and never invokes `php -r` with nested quotes or a Python executable. The test script itself uses **PDO_SQLite transactions and proc_open subprocess workers** in a uniquely randomized disposable directory under system TEMP; no service is contacted or database credentials required.

**Source static QA completed:** PHP 8.4.24 `php -l` on the exact proof source said `No syntax errors detected`; eight named tests were counted; all known network/DB-client access primitives were absent; PowerShell has UTF-8 BOM and exactly CRLF line endings; both source SHA checks were computed from the final bytes. **Assistant container has PHP/Sodium but NO `pdo_sqlite` extension**, so E45 runtime cases were **NOT executed by the assistant**. It would be false to report E45 8/8 PASS before Windows actually runs the files. These files are **conversation artifacts**, not committed to LMS-BE, FE or docs PR as executable source.

## 3. Exact eight nonproduction acceptance cases

| Case | Actual SQL experiment | Expected evidence |
|---|---|---|
| `SQL-001` | Begin immediate SQLite transaction and insert two role-specific nonce records with unique composite primary keys | One authorized atomic commit; both rows visible |
| `SQL-002` | Repeat same workload/delegation nonce pair | `DENY_DUPLICATE` from SQL uniqueness, not generic dependency failure |
| `SQL-003` | First new workload nonce + previously used delegation nonce | Full ROLLBACK; new workload nonce not prematurely burned; subsequent valid new pair succeeds |
| `SQL-004` | Clear **simulated** volatile Redis map after accepted SQL reservation | Persistent SQLite authority still denies consumed nonce; **no actual Redis server touched** |
| `SQL-005` | Close/reopen separate SQLite database connection | Previously committed unique nonce survives connection reopen |
| `SQL-006` | Two **real PHP child processes**, released with a common start barrier, concurrently reserve identical two-role nonce pair | Exactly **one** allowed and **one** duplicate denied; exactly one stored pair |
| `SQL-007` | PHP worker exits before COMMIT while transaction open | SQLite rolls back uncommitted row when connection closes; **not** a power-loss or hard OS process kill test |
| `SQL-008` | SQL database located within deliberately absent TEMP subdirectory | Must return fail-closed `DENY_SQL_ERROR`, not allow |

Strict output required: `E45_GATE01_PHP_SOURCE_SHA256=PASS`, `E45_GATE02_LOCAL_PDO_SQLITE=PASS`, `E45_GATE03_PHP_SYNTAX=PASS`, `SQL_SUMMARY total=8 passed=8 failed=0`, `E45_GATE04_PHP_PROCESS_EXIT=PASS_0`, `E45_GATE05_SQLITE_SCENARIOS=PASS_8_OF_8`, `E45_FINAL_RESULT=PASS_LOCAL_PDO_SQLITE_8_OF_8`, with `LIVE_REDIS_SERVER_ACCESSED=NO`, `LIVE_POSTGRES_SERVER_ACCESSED=NO`, `LIVE_KEYCLOAK_ACCESSED=NO`, `PRODUCTION_ACCESS=NO`.

If any test, dependency, process, source hash or exact result marker fails: stop, save `E45_REPORT_PATH`, submit `STOP_REASON` without bypass, do not mark E45 PASS and do not install anything automatically. The runner should not falsely turn a no-interpreter STOP into a SQL failure. **A file may be written only to a newly generated TEMP directory for this proof and one TEMP report.**

## 4. Real PG18/Redis8 next-stage decision and failure model

E45 proves only **actual local SQLite transaction behavior** if its eight tests run. The next meaningful `D02-02` evidence requires **real PostgreSQL18 and Redis8**, independently isolated, plus owner-reviewed `ADR-LMS-TRUST-002` proposal before adopting a PostgreSQL authority. A PostgreSQL unique constraint on the chosen authoritative timeline still cannot guarantee safety after acknowledged commit loss during async replica promotion, database restore or privileged deletion. Must deny unknown state or gate recovery against max JWS validity and bounded clock uncertainty. `PG-R01..PG-R10` live-server tests from [E40 owner decision register](./phase4b-02-e40-owner-design-decision-d02-01-to-d02-05-and-ratification-reassessment-20261011.md) remain required.

**No Docker context/network call is authorized by E44C discovery**, despite Docker CLI being found and service stopped, especially with ~2.84GiB available RAM. Real Redis command availability does not prove Redis8 or isolated daemon safety. Do not install/start server or connect to any unknown local/prod instance without a new bound environment allowlist/explicit owner decision. Similarly, D02-01 two-JWS proof still requires wire/type/request canonicalization owner signoff, and D02-05 effective Keycloak OIDC alg remains independently unverified.

## 5. Engineering end goal and checkpoint

The final target is a **secure six-service Reltroner LMS microservice platform**: a sole public LMS API Gateway and five private Learning, Mentorship, Knowledge, Assistant, Audit services; independently verified Keycloak user OIDC, authenticated scoped internal workload + delegated principal, owner-isolated domain data, replay-safe request boundaries, operational observability and full backend/frontend integration. The E45 effort is limited **security feasibility**, not source implementation, a frozen contract edit, production activation or zero-risk proof.

**Checkpoint:** `P4B01_G03_SOURCE_MAIN_MERGED -> P4B02_E40_WINDOWS_PHP30/30_OWNER_PASS -> E44C_WINDOWS_READONLY_PASS -> E45_NATIVE_PHP_SQLITE_CODE_READY_LINT_PASS_BUT_WINDOWS_NOT_RUN -> REDIS_ONLY_SILENT_LOSS_UNSAFE -> PG18_REDIS8_REAL_FAULT_TEST_NOT_RUN -> D02_01..05_RATIFICATION_PENDING -> T02_HTTP_0/86 -> SOURCE_AND_PRODUCTION_NOT_AUTHORIZED`.
