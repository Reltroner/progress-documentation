# LMS Phase 4B-02 — E44C E44B Checksum Mismatch Remediation and Offline Discovery

> **Record:** `LMS-P4B02-E44C-20261011`  
> **Status:** `E44B_INTEGRITY_GUARD_CORRECTLY_STOPPED / WINDOWS_ACTUAL_HASH_UNKNOWN / DIRECT_INLINE_DISCOVERY_AND_BOM_CRLF_OPTION_PREPARED / E44C_WINDOWS_NOT_RUN`.  
> **Boundary:** documentation and local read-only capability discovery only. No LMS-BE/FE source, production, Redis, PostgreSQL, Keycloak, VPS, Docker, WSL, install or network mutation. Phase4B-02 ratification remains HOLD.

## 1. Actual owner observation and why no bypass is acceptable

The operator's Windows PowerShell 5.1 wrapper found the E44B downloaded script but reported `STOP: E44B SHA256 mismatch` **before executing E44B**. The owner did **not** provide the Windows-side actual SHA256 nor file length. Therefore no one can conclusively attribute the mismatch to the browser, text normalization, download naming or code tampering. Do **not** change the expected hash to an invented value or disable the SHA gate.

The assistant inspected the exact E44B file from its own conversation artifact container `/mnt/data/LMS-P4B02-E44B-OFFLINE-SQLITE-RUNTIME-DISCOVERY-PS51.ps1`: **4,766 bytes**, **95 LF-only lines**, UTF-8 **without BOM**, SHA256 `15246790967CED14634C8E9B25A400F1921A0A7F87449B3B062482B352D9982B`. Prior E44B archive receipt claimed UTF-8 BOM/CRLF; that formatting claim was **factually wrong** for the supplied container file. Text transformations between downloads or editor saves are a possible explanation of Windows mismatch, **not verified as the actual root cause** without a Windows-side hash. The code integrity stop was the correct outcome.

## 2. Deterministic resolution without E44B

**Primary recommended action:** Use a directly copy-pasted, self-contained Windows PowerShell 5.1 script/one-block command that:
1. Queries `php.exe -m` for **existing** `sqlite3` and `pdo_sqlite` modules (no inline `php -r` quoting; no SQL writes).
2. Checks the existence, **without loading**, of `%SystemRoot%\System32\winsqlite3.dll` and the presence of Python/py command names (not a Python version test).
3. Verifies SHA256 of the original E44 read-only script already downloaded to Windows `Downloads`: `53734B5345D5C44E2B3B1803A4F5867BA58E70756E7D71CFB844A8B5A22559B2`.
4. Executes that E44 script alone via a local PowerShell subprocess with stdout/stderr captured separately and requires a **fresh** E44 report with exact `E44_DISCOVERY_RESULT=INVENTORY_COMPLETE_PENDING_OWNER_ENVIRONMENT_SELECTION`.
5. Writes a new isolated TEMP report; never installs packages, contacts Docker daemon, Redis, PostgreSQL, Keycloak or production.

The direct inline command **does not need to download or trust E44B** at all. It still cryptographically pins the actual E44 script that performs the environment inventory. If E44 itself fails its hash, **STOP** and do not execute. No automatic approval for PostgreSQL18/Redis8 test containers follows from command presence.

**Optional convenience artifact:** `LMS-P4B02-E44C-OFFLINE-SQLITE-DISCOVERY-PS51.ps1` created with explicit **UTF-8 BOM + CRLF** and SHA256 **`4290E24E2CF626F61DC73369B421928DC40B86D613C28877D8FB2E7A350081E5`**, length **6,222 bytes**, 121 CRLF-terminated lines. The E44C download is a separate conversation artifact, **NOT part of this GitHub docs PR as executable**. Static review of PowerShell control flow and syntax was performed in Linux, but **native Windows PowerShell 5.1 cannot be executed from the assistant's Linux container**. Therefore `E44C_WINDOWS=NOT_RUN`.

## 3. Current engineering status and exit

- E40 Windows real Sodium dual-assertion + replay **model**: operator previously reported **30/30 PASS**.
- E43S protected E41 Windows SQLite: ZIP and three source hashes PASS; **Python 3.8+ CLI unavailable**, **E41_WINDOWS_SQLITE=NOT_RUN**.
- E44B discovery: **NOT_RUN_SHA256_MISMATCH** (not security proof failure, no E44 script run).
- E44C direct discovery: **PREPARED, WINDOWS NOT RUN**; only existing local module and OS file checks plus SHA-pinned E44 inventory, no install or network.
- Original E41 assistant SQLite actual SQL engine 8/8 PASS in **isolated Linux**; not proof of SQL executed on owner Windows.
- **Real PostgreSQL18 + Redis8 runtime, Keycloak effective access-token algorithm, and canonical T02 HTTP acceptance remain NOT RUN**; `D02-02=REDIS_ONLY_SILENT_NONCE_LOSS_UNSAFE`, owner ADR/ratification HOLD.

**Next:** operator runs the **inline** E44C discovery or the independently SHA-verified BOM/CRLF artifact, provides `PHP_SQLITE3_EXTENSION`, `PHP_PDO_SQLITE_EXTENSION`, `WINDOWS_NATIVE_SQLITE_DLL`, fresh E44 report, and optional actual E44B SHA as factual diagnostic. Only after knowing the existing engine should a separately versioned and reviewed SQLite alternative harness be proposed.

**Checkpoint:** `E40_WINDOWS_30/30_PASS -> E43S_SQLITE_NOT_RUN_PYTHON_UNAVAILABLE -> E44B_HASH_MISMATCH_FAIL_CLOSED -> E44C_INLINE_READONLY_DISCOVERY_PREPARED -> E44_WINDOWS_PENDING -> ACTUAL_PG18_REDIS8_NOT_RUN -> DESIGN_RATIFICATION_HOLD -> PRODUCTION_NOT_AUTHORIZED`.
