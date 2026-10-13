# LMS Phase 4B-02 — E43S PowerShell NativeCommandError and ZIP extraction hardening

> **Receipt:** `LMS-P4B02-E43S-20261011`.  
> **Status:** `OUTER_NATIVE_ERROR_MASKING_VERIFIED_FROM_OWNER_LOG; E43R_INTERNAL_STOP_REASON_NOT_YET_OBSERVED; E43S_SAFE_SCRIPT_PREPARED_STATICALLY; WINDOWS_EXECUTION_PENDING`.  
> **Nonproduction-only:** No LMS-BE/LMS-FE source mutation, Git worktree change, VPS, Keycloak, Redis, PostgreSQL, Docker, WSL or production action authorized.

## 1. Operator evidence and exact diagnosis

The Windows PowerShell5.1 user-provided batch verified all three downloaded artifact SHA256 digests. The parent block then used `$ErrorActionPreference='Stop'` and invoked another `powershell.exe` using `2>&1 | ForEach-Object { "$_" }`. The child E43R emitted `E43 stopped; see report and STOP_REASON` on stderr, which the parent turned into a **`NativeCommandError` terminating exception**. Consequently, the parent stopped before printing the captured child report and before E44, so the **actual E43R internal `STOP_REASON` has not been shared**. It is not justified to attribute that hidden cause to Python, SQLite, ZIP or another specific internal gate.

The last reliable status is `E40_WINDOWS_PHP=OWNER_REPORTED_30/30_PASS`, `E41_WINDOWS_SQLITE=NOT_VERIFIED`, `E44_WINDOWS_CAPABILITY=NOT_RUN`, `REAL_PG18_REDIS8=NOT_RUN`, `CANONICAL_HTTP_T02=0/86_RUN`. No statement of SQLite eight failing test assertions can be made from this log.

## 2. Corrected bounded execution method

**New chat artifact:** `LMS-P4B02-E43S-WINDOWS-E41-SQL-VERIFY-PS51.ps1`, SHA256 `232FBCC99257921176C4DC46B77068ADEA0529B2A572D2930C8A91C7E3A71416`, UTF-8 BOM/CRLF, 183 lines. **Not a GitHub committed executable.** It is a fresh runner rather than an edit to the prior E43/E43R record.

- Reads the original fixed ZIP SHA256 `4D5EC802F7B0835F1E12D0B7909A01388E2343332BA2EC5C9E3575792A49042E` using `System.IO.Compression.ZipFile::OpenRead`, verifies **exactly five root members** and bounded entry sizes, then copies only those bytes to a **new random TEMP folder**, avoiding `Expand-Archive` layout differences entirely.
- Verifies byte SHA256 of `proof.php` (`0DF6D1D50BCB99D0EEE2D7F7422ECADB7DE21C1DE96BF191B4DC2045F499867E`), `sql_ledger_proof.py` (`A6BEAA88238F7C31D49268FA049BAD6928162444B31AC51A667440241F872859`) and `run-sql-proof-ps51.ps1` (`72B1BDE5C15000C7F6857ED639BBDBD9E38CFD34E1C120E731C0F2F249701F28`); proof sources and ZIP **remain unchanged**.
- Calls a Python **3.8+** CLI by `System.Diagnostics.ProcessStartInfo` with stdout/stderr captured separately and exit code checked, avoiding native stderr promotion to `NativeCommandError` in PowerShell5.1. The original Python harness runs under TEMP SQLite and its two worker processes; no server or network is contacted.
- Requires each `PASS SQL-001` to `SQL-008` exactly once, the full `SQL_SUMMARY total=8 passed=8 failed=0`, matching scope and NO production markers. Reports `E43S_FINAL_RESULT=PASS_NONPRODUCTION_SQLITE_ONLY` only when these exact gates pass. Error results include a concrete `STOP_REASON` and are saved to `E43S_REPORT_PATH`; the runner exits **nonzero** without a new uncaught PowerShell terminating exception, so parent should inspect its exit status without `2>&1`.
- **Static and isolated testing only**: The assistant validated ZIP membership and SHA256, reran the unchanged SQLite harness in Linux (**8/8 PASS**). The new **PowerShell 5.1 runtime has NOT been tested on operator Windows**, so `E41_WINDOWS=AWAIT_NEW_RUN` even though original Python code passes on Linux.
- If Python3.8+ is missing, print STOP and `E41_WINDOWS_SQLITE=NOT_RUN_PRECHECK_BLOCKED`, not PASS. No automatic Python install, `php.ini` edit, dangerous path modification or test bypass.

## 3. Operator diagnostics and next safe action

**Immediate read-only investigation of the previous failure**, without running a test again:

```powershell
$Latest = Get-ChildItem -LiteralPath $env:TEMP -Filter 'LMS-P4B02-E43-REPORT-*.txt' -File |
    Sort-Object LastWriteTime -Descending | Select-Object -First 1
if ($Latest) {
    Write-Host ('PREVIOUS_REPORT=' + $Latest.FullName)
    Get-Content -LiteralPath $Latest.FullName |
        Select-String 'STOP_REASON=|E43_FINAL_RESULT=|E43_ARCHIVE_LAYOUT=|E43_GATE|PYTHON_VERSION=|E41_WINDOWS_SQLITE='
}
```

Then download the SHA-verified E43S artifact and run it as a new `powershell.exe -File` process **without `2>&1`**, check `$LASTEXITCODE`, read the `E43S_REPORT_PATH` on STOP. Only after E43S yields eight actual SQLite passes and `E43S_FINAL_RESULT=PASS_NONPRODUCTION_SQLITE_ONLY` may the unchanged E44 **read-only** inventory be invoked. This still does **not** authorize PostgreSQL18/Redis8 real tests, source implementation, architecture ratification or production.

**Checkpoint:** `E40_WINDOWS_30/30_OWNER_PASS -> E43R_NATIVE_STDERR_MASKED_INTERNAL_REASON_UNAVAILABLE -> E43S_DIRECT_ZIP_EXTRACTION_SCRIPT_PREPARED -> SQLITE_WINDOWS_RERUN_PENDING -> E44_READONLY_PENDING -> D02_02_REAL_PG18_REDIS8_AND_OWNER_ADR_BLOCKED -> PRODUCTION_NOT_AUTHORIZED`.
