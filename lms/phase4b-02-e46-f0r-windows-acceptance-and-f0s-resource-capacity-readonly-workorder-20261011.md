# LMS Phase 4B-02 — E46-F0R Windows context classification PASS; E46-F0S offline capacity-only gate

> **Evidence ID:** `LMS-P4B02-E46-F0R-OWNER-20261011`  
> **Owner observation timestamp:** `2026-10-11T03:41:23+07:00`, Windows PowerShell 5.1.  
> **Current exact status:** `E46_F0R_METADATA_CLASSIFICATION=PASS_READONLY`; `CURRENT_ENDPOINT_CLASS=LOCAL_WINDOWS_NPIPE_CANDIDATE_UNVERIFIED`; `CURRENT_CONTEXT_EXACT_MATCH_COUNT=1`; `DOCKER_DESKTOP_SERVICE=Stopped_OBSERVED_NOT_CHANGED`; `HOST_RAM_FREE_GIB=3.56`; `ISOLATION_FLAG_COUNT=1` with `HOST_RAM_UNDER_4GIB_NO_START`; `E46_F0R_RUNTIME_AUTHORIZATION=NO_GO_OWNER_APPROVAL_AND_REAL_ENV_REQUIRED`; `REAL_PG18_REDIS8_TESTS=NOT_RUN`.  
> **Source pins last checked:** `Reltroner/LMS-BE/main=617dadc0d0d627071d713ceb729df6658202b43e`; `Reltroner/progress-documentation/main=183372371b3a40a0349ac390848911273ccd2361`, PR #46 OPEN. No main merge authorized.

## 1. Exact evidence scope and interpretation

The operator's SHA-pinned downloaded E46-F0R script passed SHA256; all seven Docker/TLS/Kube env override variables were `UNSET`. Reading **only local configuration files** showed exactly **one** saved Docker context metadata file and exactly **one** matching current context. The endpoint *type* matched the restricted Windows local Docker named pipe allowlist: `LOCAL_WINDOWS_NPIPE_CANDIDATE_UNVERIFIED`. The script did **not** contact the daemon, show an endpoint/context name, activate a service, run Docker/WSL/PostgreSQL/Redis, download an image, modify git source, or access production. It reported `E46_F0R_FINAL=PASS_READONLY_CLASSIFICATION_ONLY`.

**What was resolved:** ambiguity about the *on-disk protocol class* and whether the saved context metadata could be associated with the active context. This improves confidence, but is **not cryptographic proof that the actual daemon would be local or appropriately isolated**, especially if configuration or context changes after sampling.

**What remains:** Docker Desktop was `Stopped_OBSERVED_NOT_CHANGED`. Owner Windows RAM free rose from **2.78GiB** (F0) to **3.56GiB** (F0R) without any authorized service start. 3.56GiB remains **below the conservative, project-defined 4GiB review threshold**. The 4GiB limit is a project safety *screen*, **not a vendor-certified minimum or proof that 4GiB is sufficient**; passing it would not authorize container starts. One remaining `ISOLATION_FLAG=HOST_RAM_UNDER_4GIB_NO_START`, `ISOLATION_FLAG_COUNT=1`; owner/runtime authorization remains NO-GO.

**Security/fail-close:** Even successful classification of a local named pipe must not trigger `docker info`, `docker run`, `docker context use`, `docker compose`, `wsl`, a Redis/Postgres command, SSH, network/API calls, image download or any production operation. Do not alter Docker Desktop memory/WSL settings, kill processes, reboot, or configure autostart. `CLI_FOUND` never implies running services or real Postgres18/Redis8 proof.

## 2. E46-F0S offline read-only capacity audit — next deterministic operator work

**Scope:** user copies one inline Windows PowerShell 5.1 block directly (no script download, no new SHA-dependent launcher), which records three *read-only* `Win32_OperatingSystem` memory samples, the system-drive free disk, Docker Desktop Windows service **status only**, and aggregated **anonymized process working-set categories** (Browser/IDE/Docker-WSL/Database/Other) without exposing process IDs, process paths, windows, user names or command-line arguments. It sleeps 0.7 seconds between samples; reads only local CIM/Get-Process information and writes a single UTF-8 report in random `TEMP`. It **does not** attempt to reclaim RAM or terminate/restart anything. No Docker/WSL/PostgreSQL/Redis/Keycloak/SSH/service daemon is invoked. A `Get-Process` working set is an **approximate** memory-pressure indicator; summing categories may double count shared pages, so it must not be treated as actual reclaimable RAM.

**Acceptance from owner run (NOT YET EXECUTED):**
- `E46_F0S_MEMORY_SAMPLES=3`; `E46_F0S_CAPACITY_SCREEN=UNDER_4GIB_REVIEW` if the minimum of three samples is below 4GiB, or `AT_LEAST_4GIB_REVIEW_ONLY` otherwise.
- `E46_F0S_RUNTIME_AUTHORIZATION=NO_GO_OWNER_APPROVAL_REQUIRED`, always.
- `E46_F0S_FINAL=PASS_READONLY_CAPACITY_FACTS_ONLY` means information collection succeeded, **not PostgreSQL/Redis sandbox safety**; `E46_F0S_REPORT_PATH` must be a *new* TEMP report. Any CIM/perms error -> `STOP_REASON` and `E46_F0S_FINAL=STOP_REVIEW_REQUIRED`, no invented PASS.

**One small decision after F0S:** If sufficient memory cannot safely be made available by the owner *manually* in normal application workflow, **prefer designing a separate isolated, no-secrets, no-production PostgreSQL18+Redis8 CI sandbox** (e.g. a narrowly scoped temporary GitHub Actions workflow in a disposable public repo/branch) rather than forcing local Docker startup. A CI-based alternative is **proposal only**: no GitHub runner started, no CI workflow added, no secrets exposed, no purchased resources, no assumption free quotas/runner sizes. Must obtain explicit owner permission, pin exact engine image digests and runner permissions, prove that it cannot access owner production accounts, and get a closed-budget/cost decision before actual usage. Exact PG-R01..PG-R10 real-engine acceptance still 0 executed.

## 3. Preserve independent proof and ratification state

- E40 Windows owner-output real Ed25519/anti-replay *model* **30/30 PASS**. Redis-only silent nonce loss + total FLUSH **UNSAFE demonstrated by counterexample**; this is not a Redis8 runtime test.
- E45 Windows owner-output actual PHP PDO_SQLite transaction suite **8/8 PASS**, including real two-process competition, uniqueness, rollback, connection reopen and fail-closed authority; **simulated Redis cache loss only**.
- E46-F0 Windows read-only fact collection PASS but had four flags; E46-F0R Windows **context-type classification PASS**, now **one remaining RAM review flag**. No production or Docker daemon contact.
- No actual isolated PostgreSQL18, Redis8, Keycloak JWKS/OIDC effective algorithm nor 86 canonical Laravel HTTP acceptance cases executed. `D02-01` on-wire/key custody still owner pending, `D02-02` real PG durability/Redis failure/ADR change still BLOCKED, `D02-03/04/05` remain unratified/unverified.
- Production, BE/FE source changes, GitHub PR merge, service startup and real-engine tests **NOT AUTHORIZED**. Do not promise zero risk or zero technical debt; preserve immutable evidence and provenance for each phase.

**Checkpoint:** `E40_OWNER_WIN30/30_PASS -> E45_OWNER_WIN8/8_PASS -> E46_F0R_OWNER_WIN_METADATA_PASS_LOCAL_NPIPE_CANDIDATE -> RAM_3_56_GIB_UNDER_PROJECT_SCREEN -> E46_F0S_CAPACITY_READONLY_NOT_RUN -> REAL_PG18_REDIS8_NOT_RUN -> DESIGN_RATIFICATION_HOLD -> PRODUCTION_NOT_AUTHORIZED`.
