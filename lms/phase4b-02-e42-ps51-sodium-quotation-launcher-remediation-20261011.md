# Reltroner LMS — Phase 4B-02 E42 Windows PowerShell 5.1 PHP Sodium preflight remediation

> **Receipt:** `LMS-P4B02-E42-PS51-PREFLIGHT-20261011`  
> **Evidence:** Operator pasted original E40 Windows PowerShell 5.1 error while running unmodified archive `LMS-P4B02-D02-D01-ISOLATED-PROOF-20261011.zip` (original SHA256 `7C06EBE907102C6B01CD939FEE3124363620581444CB24D3D9C5601BE5DFABE3`).  
> **Result:** `LAUNCHER_QUOTING_DEFECT_CONFIRMED_IN_SOURCE`, `PACKAGE_PATCHED_AND_LINUX_REVALIDATED`, `WINDOWS_E40=AWAIT_OPERATOR_RERUN`. Not a Redis/PostgreSQL or production fault.

## 1. Exact observed failure, distinct from application security result

The old `run-proof-ps51.ps1` called `php.exe -r` with PHP source held in single-quoted **PowerShell** text containing nested **double-quoted PHP strings**:

```powershell
$Ext = & $Php.Source -r 'echo (extension_loaded("sodium") && function_exists("proc_open")) ? "READY" : "BLOCKED";'
```

The operator observed `PHP Fatal error: Uncaught Error: Undefined constant "sodium" in Command line code:1`, then `STOP: sodium/proc_open missing` and `STOP: Pengujian PHP belum PASS` in a timestamped TEMP extraction folder. Under Windows PowerShell 5.1, nested double quotes can be lost across native argument marshalling. PHP then evaluates `extension_loaded(sodium)` (unquoted identifier) rather than `extension_loaded('sodium')` (string). **The old launcher was broken; the error alone does NOT establish whether the user's Sodium module is present.** Proof test cases were not reached on this Windows attempt: `WINDOWS_E40=NOT_RUN_PRECHECK_BLOCKED`, **not** `30_FAIL`. E41 SQL test was not reached by the enclosing batch.

## 2. Corrected package and integrity boundaries

**New user-facing ZIP:** `LMS-P4B02-D02-D01-ISOLATED-PROOF-20261011-PS51-FIXED.zip`. **New SHA256:** `4D5EC802F7B0835F1E12D0B7909A01388E2343332BA2EC5C9E3575792A49042E`. The original ZIP SHA is invalid for this new archive by design.

- Changed only `run-proof-ps51.ps1` (new SHA256 `9E04DEE943C69941157DA94E33F08E0442E310A987A99D5C95469015A415FEB1`) and human README compatibility notes; all unchanged binaries/source have their prior hashes.
- **Unchanged** `proof.php` SHA256: `0DF6D1D50BCB99D0EEE2D7F7422ECADB7DE21C1DE96BF191B4DC2045F499867E`.
- **Unchanged** `sql_ledger_proof.py` SHA256: `A6BEAA88238F7C31D49268FA049BAD6928162444B31AC51A667440241F872859`.
- The corrected launcher avoids the brittle inline PHP `extension_loaded()` command: it obtains module inventory using argument-free `php.exe -m` and requires exactly one `sodium` module entry; **`proof.php` already performs both `extension_loaded('sodium')` and `function_exists('proc_open')` checks internally before running any scenario, exiting nonzero if missing**.
- The Windows launcher validates the *unchanged* PHP proof SHA, PHP >=8.2, the Sodium module inventory, the summary `SUMMARY total=30 passed=30 failed=0`, the 3 no-production scope lines and the program exit code before reporting `E40_PROOF=PASS_LOCAL_MODEL_ONLY`. The same archive retains the optional 8-test Python SQLite launcher with its own source SHA guard.
- ZIP CRC/extraction test completed successfully. Re-running the PHP proof in the isolated assistant Linux container gave **30/30 PASS**, and the SQLite Python supplement **8/8 PASS**. **Windows PowerShell 5.1 is unavailable in the assistant environment**, so no Windows runtime PASS is claimed before operator output.

## 3. Owner execution and stop conditions

Download the **new fixed ZIP**, compare its SHA256 to the NEW value above using Windows `Get-FileHash`, extract into a **new unique TEMP directory**, verify that `proof.php` has its pinned SHA and run the fixed `run-proof-ps51.ps1` in Windows PowerShell 5.1. **Do not reuse the old extracted launcher** or edit the cryptographic proof to bypass checks.

Expected report-only success markers: `SOURCE_SHA256=PASS`, `PHP_SODIUM_MODULE=PASS`, `SODIUM_PROC_OPEN=PASS_VERIFIED_BY_PROOF_PHP`, `SUMMARY total=30 passed=30 failed=0`, `E40_PROOF=PASS_LOCAL_MODEL_ONLY`. The optional SQLite report must say `SQL_SUMMARY total=8 passed=8 failed=0` and `SQL_E41_PROOF=PASS_ACTUAL_SQLITE_ONLY_NOT_POSTGRES18` when Python 3 is available. If either binary is missing or a test fails, **STOP**, capture non-secret error/output and classify as `BLOCKED/FAIL`; do not install tools or modify `php.ini`/production software automatically.

**Authority:** This is test-runner correction, **not** ADR/D02-01..05 ratification, real Redis8/PG18 acceptance, Laravel HTTP proof, source merge or deployment. All canonical T02-001..086 cases remain drafted/0 executed. Protected LMS-BE/FE source/dirty worktrees, HRM VPS, Keycloak, Redis, PostgreSQL, DNS and production remain out of scope.
