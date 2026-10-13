# LMS Phase 4B-02 — E43R Windows PowerShell ZIP Member Layout Remediation

> **Receipt:** `LMS-P4B02-E43R-20261011`  
> **Status:** `PRECHECK_DEFECT_DIAGNOSED_AND_SCRIPT_PATCHED / WINDOWS_RERUN_PENDING`.  
> **Scope:** Correct E43's ZIP layout validation only; retain SHA256 checks, all five exact file allowlists, SQLite test assertions and the production no-contact policy. No source LMS-BE/FE, production, Redis, PostgreSQL or Keycloak changes.

## 1. Exact operator evidence

The operator's E43 PowerShell 5.1 batch verified original **fixed** ZIP checksum, E43 and E44 launcher checksums (`E42_ZIP_SHA256=PASS`, `E43_SCRIPT_SHA256=PASS`, `E44_SCRIPT_SHA256=PASS`), then E43 reported:

```text
E43_GATE01_ARCHIVE=PASS_SHA256
STOP_REASON=STOP: Archive member allowlist mismatch. Files=f4/proof.php,f4/README.md,f4/run-proof-ps51.ps1,f4/run-sql-proof-ps51.ps1,f4/sql_ledger_proof.py
E41_WINDOWS_SQLITE=FAILED_OR_PRECHECK_BLOCKED
E43_FINAL_RESULT=STOP_REVIEW_REQUIRED
```

The batch STOPPED at archive path classification: **SQLite was never executed**, and **E44 read-only discovery was not executed**, because the enclosing batch fail-closed after E43. Do not call this `SQL 8 FAIL`; correctly classify `E41_WINDOWS=NOT_RUN_E43_PRECHECK_BLOCKED`, `E44_WINDOWS=NOT_RUN_BY_BATCH`.

The original E43 script assumed all members would be extracted immediately under `$Target`. The observed Windows extraction placed precisely the five allowlisted file basenames under a single `f4/` directory. The SHA-pinned archive was also independently inspected by the assistant in an isolated container: exact ZIP SHA256 `4D5EC802F7B0835F1E12D0B7909A01388E2343332BA2EC5C9E3575792A49042E`, and five root-level member filenames were seen with that ZIP parser; the discrepancy is about **the observed extraction layout**, not evidence of a changed or compromised ZIP.

## 2. Exact bounded fix — E43R

**New conversation artifact**: `LMS-P4B02-E43R-WINDOWS-E41-SQL-VERIFY-PS51.ps1` (PowerShell 5.1 UTF-8 BOM, CRLF), SHA256 **`F48B91A88F98FBF1438D52A5D3D1C2F0F1D6FB12EB6C6669E5161CFC047E9754`**. It retains all E43 test/result checks. After extracting the original SHA-pinned fixed ZIP to a new random TEMP folder, it accepts only these exact five file basenames under **one of two layouts**:

- `ROOT`: five exact files, no subdirectories.
- `EXACT_F4_WRAPPER`: the same five exact files under exactly one `f4` subdirectory; no other directory or file.

**It still denies** a sixth file, another directory name, mixed root/wrapped files, missing file, unexpected directory, extracted reparse point, SHA mismatch for the PHP/SQL files, absent Python, test exit failure, missing required result marker or wrong 8/0 PASS counts. It never strips an arbitrary path prefix or accepts arbitrary nested directories. Only `$PayloadRoot` is selected after exact layout verification.

**Integrity guard:** ZIP hash remains `4D5EC802...`, unchanged PHP proof `0DF6D1D5...`, unchanged SQL Python source `A6BEAA88...`, unchanged SQL runner `72B1BDE5...`. E44 separate script remains unchanged, SHA256 `53734B5345D5C44E2B3B1803A4F5867BA58E70756E7D71CFB844A8B5A22559B2`. **Original E43 script is retained unchanged as historical failed-precheck evidence**.

## 3. Validation accomplished vs still pending

The assistant independently re-extracted the ZIP, verified actual source checksum, reran the **existing SQLite Python harness in an isolated Linux container** (8 individual SQL test PASSES, `SQL_SUMMARY total=8 passed=8 failed=0`, `PRODUCTION_ACCESS=NO`), and checked both `ROOT` and `EXACT_F4_WRAPPER` file-layout constructions. E43R itself was statically inspected for PowerShell 5.1 syntax/UTF-8 BOM/CRLF/old-file hashes. **PowerShell 5.1 was NOT executed by the assistant's Linux container**; E43R Windows acceptance needs operator's actual rerun.

**Next operator gates:** Download E43R to Windows Downloads, compute exact SHA256 and compare to receipt, execute `powershell.exe -NoProfile -ExecutionPolicy Bypass -File` for this **new** E43R only. If it prints `E43_ARCHIVE_LAYOUT=EXACT_F4_WRAPPER`, `E43_GATE02_ARCHIVE_ALLOWLIST=PASS_FIVE_FILES`, `SQL_SUMMARY total=8 passed=8 failed=0`, `E43_GATE07_SQLITE_TESTS=PASS_8_OF_8_ZERO_FAIL` and `E43_FINAL_RESULT=PASS_NONPRODUCTION_SQLITE_ONLY`, count **E41_WINDOWS_SQLITE=PASS**. Then run unchanged E44 read-only environment inventory separately, subject to its own exact SHA guard. On any STOP, retain report and inspect; **do not override hash/allowlist**.

**No ratification shortcut:** E40 Windows 30/30 remains operator-confirmed, E41 Windows is **PENDING**, canonical 86 real HTTP tests **0 run**, D02-02 Redis-only unsafe counterexample still stands. Real PG18/Redis8 replay integrity and owner ADR revisions remain BLOCKED; no BE source coding or production authorization.
