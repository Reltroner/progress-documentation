# LMS Phase 4B-02 — E44B Python CLI unavailable, SQLite alternative capability discovery

> **Record:** `LMS-P4B02-E44B-20261011`  
> **State:** `E43S_SHA_AND_ARCHIVE_GATES_PASS; E41_WINDOWS_SQLITE_NOT_RUN_PYTHON_CLI_UNAVAILABLE; E44_READONLY_PENDING; E44B_PREPARED_NOT_EXECUTED_ON_OWNER_WINDOWS`.  
> **Authority:** Owner requested correction after actual Windows PowerShell 5.1 E43S console output. This is **not** permission to install Python, compile code, activate WSL/Docker, contact a Redis/PostgreSQL/Keycloak service, change repositories or deploy.  
> **Source GitHub pin:** `Reltroner/LMS-BE/main=617dadc0d0d627071d713ceb729df6658202b43e`, pending revalidation; docs PR #46 OPEN at start of E44B.

## 1. Evidence and exact classification

Owner Windows E43S output confirms SHA256 and source checks:

```text
E43S_GATE01_FIXED_ZIP=PASS_SHA256
E43S_GATE02_ZIP_MEMBER_ALLOWLIST=PASS_FIVE_ROOT_FILES
E43S_ZIP_LAYOUT=ORIGINAL_ARCHIVE_ROOT_DIRECT_EXTRACTION
E43S_GATE03_PHP_SOURCE=PASS_SHA256
E43S_GATE04_SQL_PYTHON_SOURCE=PASS_SHA256
E43S_GATE05_SQL_RUNNER=PASS_SHA256
STOP_REASON=STOP: Python 3.8+ CLI unavailable; E41 NOT_RUN; do not install automatically
E41_WINDOWS_SQLITE=NOT_RUN_PRECHECK_BLOCKED
E43S_FINAL_RESULT=STOP_REVIEW_REQUIRED
```

The **ZIP layout failure was repaired**; E43S extracted the original five SHA-pinned members directly, and the terminal stopped only at Python discovery. No individual `SQL-001..SQL-008` case was run on Windows. The outer batch then did **not start E44**. `Python 3.8+ CLI unavailable` does **not necessarily mean Python absent from the whole PC**: it could be off PATH, launcher/untrusted alias, unsupported version or a different execution configuration. Do **not** automatically install or modify PATH.

**Evidence taxonomy:** E40 Windows PHP 30/30 **OWNER_REPORTED_PASS** with actual Ed25519 signatures and replay *model*; E41 assistant SQLite8/8 Linux pass **separate evidence**; E41 Windows `NOT_RUN` due to Python CLI; E44 Windows `NOT_RUN`; Redis-only silent-loss counterexample **UNSAFE**; real PG18/Redis8 `NOT_TESTED`; canonical T02 real HTTP `0/86`.

## 2. Lower-risk dependency strategy before another implementation

Do not replace the original cryptographic proof or silently weaken checks to mark E41 green. Instead **discover existing local execution capabilities**, without installation:

- PHP 8.2+ CLI already worked for E40; `php -m` can disclose whether `sqlite3` or `pdo_sqlite` modules are already enabled; this does **not** execute any SQL or connect to production.
- Windows 11 generally ships `%SystemRoot%\System32\winsqlite3.dll`; check only file presence. **Presence does not prove the DLL is authorized/compatible with a future test harness**. Any alternate Windows-native SQLite tests need a separate reviewed, exact-SHA proof package and direct owner Windows output.
- `Get-Command python.exe,py.exe` checks PATH hints, not necessarily a working Python runtime. WindowsApps Store aliases can be misleading. No installation automatically.
- Run **E44 separately** even if Python isn't available. It only inventories local CLI names, Windows service state, memory and local disk, with no daemon/database/network access.

## 3. New SHA-pinned helper for Windows PowerShell 5.1

Created chat artifact `LMS-P4B02-E44B-OFFLINE-SQLITE-RUNTIME-DISCOVERY-PS51.ps1`, **SHA256 `15246790967ced14634c8e9b25a400f1921a0a7f87449b3b062482b352d9982b`**, 95 lines. No GitHub script binary is claimed. Validated statically in the assistant's Linux container; **Windows execution not observed**.

The script probes PHP `-m` and Windows native SQLite DLL without running SQLite, then verifies the **unchanged** owner-downloaded E44 script SHA256 `53734B5345D5C44E2B3B1803A4F5867BA58E70756E7D71CFB844A8B5A22559B2`, launches E44 separately without `2>&1`, and demands an E44 **fresh** TEMP report with `E44_DISCOVERY_RESULT=INVENTORY_COMPLETE_PENDING_OWNER_ENVIRONMENT_SELECTION` before printing `E44B_FINAL=OFFLINE_OPTIONS_AND_E44_DISCOVERY_COMPLETE`. Only TEMP report I/O from E44 is allowed.

**Neither PHP SQLite nor Windows-native SQLite nor Python availability has been independently established on the user's machine at time of writing.** No attempt to run 8/8 SQL tests without an actual available engine/interpreter was made.

## 4. Deterministic next gate based on actual E44B output

| Discovery outcome | Next conditional action, not automatic permission |
|---|---|
| `PHP_SQLITE3_EXTENSION=PRESENT` or `PHP_PDO_SQLITE_EXTENSION=PRESENT` | Prepare separately reviewed PHP-native SQLite SQL harness with real concurrency, dual-nonce atomic transactions, and input/source SHA guard; run locally only under owner approval |
| PHP SQLite absent, `WINDOWS_NATIVE_SQLITE_DLL=PRESENT_NOT_INVOKED` | Consider separately reviewed Windows built-in SQLite `winsqlite3.dll` test harness with process isolation and exact same SQL-001..008 conditions; **no assumption it works until executed** |
| No verified SQLite engine or Python available | Keep E41 Windows `BLOCKED_DEPENDENCY`; user may explicitly approve installing a no-cost offline runtime later, but **never install automatically** |
| E44 reports Docker/WSL/PG/Redis CLI installed | This is **not** proof of local isolated server readiness; do not contact daemon, run Docker or connect to any service without owner-approved localhost isolation and no-spend preflight |

**Phase4B-02 remains:** `D02-01_TWO_JWS=MODEL_PASS_OWNER_WIRE_RATIFICATION_PENDING`; `D02-02_REDIS_ONLY_SILENT_LOSS=UNSAFE`; `D02-02_OWNER_DB_DURABLE_PROPOSAL=REAL_PG18_REDIS8_TEST_BLOCKED`; `D02-05_KEYCLOAK_EFFECTIVE_OIDC_ALG=UNVERIFIED`; `DESIGN_RATIFICATION=HOLD`; `PRODUCTION=NOT_AUTHORIZED`.
