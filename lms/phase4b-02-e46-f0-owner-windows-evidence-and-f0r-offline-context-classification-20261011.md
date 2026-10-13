# LMS Phase 4B-02 — E46-F0 owner Windows PASS (fact collection) / isolation BLOCKED; E46-F0R safe offline context classification

> **Evidence record:** `LMS-P4B02-E46-F0R-20261011`.  
> **Source:** operator-pasted Windows PowerShell5.1 E46-F0 command and full resulting TEMP report, local timestamp `2026-10-11T03:31:23+07:00`. Do not treat owner-pasted output as independently accessed Windows host telemetry.  
> **Stage:** `E46_F0_FACT_COLLECTION=PASS`, `E46_ISOLATION_ELIGIBILITY=BLOCKED_PENDING_OWNER_ENVIRONMENT_REVIEW`, `E46_F0R_OFFLINE_CONTEXT_CLASSIFIER=PREPARED_NOT_RUN_ON_WINDOWS`, `PG18_REDIS8_REAL_ENGINE=NOT_RUN`, `DESIGN_RATIFICATION=HOLD`, `PRODUCTION=NOT_AUTHORIZED`.  
> **Source pins from prior verification:** `LMS-BE/main=617dadc0d0d627071d713ceb729df6658202b43e`; `progress-documentation/main=183372371b3a40a0349ac390848911273ccd2361`; docs PR #46 still OPEN.

## 1. Directly observed owner output — evidence and interpretation

The operator's SHA-verified E46-F0 script completed `E46_F0_FINAL=PASS_READONLY_FACT_COLLECTION_ONLY`. All seven reported environment overrides were `UNSET`: `DOCKER_HOST`, `DOCKER_CONTEXT`, `DOCKER_TLS_VERIFY`, `DOCKER_CERT_PATH`, `DOCKER_CONFIG`, `CONTAINER_HOST` and `KUBECONFIG`. The Docker local config file exists; its `currentContext` is defined **but deliberately not displayed**, and **one** saved context metadata file was counted. Docker Desktop service was `Stopped_OBSERVED_ONLY`. Host RAM total 15.33GiB, free **2.78GiB**; system drive free **45.85GiB**. Docker, WSL, Redis server/CLI command **names** were found but none invoked. PostgreSQL server and psql were not on PATH (not proof that no PG installation exists elsewhere). `DOCKER_DAEMON_CONTACTED=NO`, `IMAGE_DOWNLOADED=NO`, `LOCAL_CONTAINER_STARTED=NO`, `DOCKER_CONTEXT_CHANGED=NO`, `PRODUCTION_MUTATION=NO`.

The operator's **four reported risk flags**, none resolved by the PASS status, were:
- `DOCKER_DESKTOP_NOT_RUNNING_NO_AUTOSTART`
- `CURRENT_DOCKER_CONTEXT_REQUIRES_HUMAN_REVIEW`
- `SAVED_DOCKER_CONTEXTS_REQUIRE_OFFLINE_REVIEW`
- `FREE_RAM_UNDER_4GIB_REVIEW_CAPACITY_NO_START`

**Correct conclusion:** `E46_F0_READONLY_DISCOVERY=PASS` indicates the factual inventory ran; it is **not** `PG18_REDIS8_RUNTIME_READY`, and **NOT** owner authorization to start Docker Desktop or local/remote workloads. `E46_ISOLATION_ELIGIBILITY=BLOCKED_PENDING_OWNER_ENVIRONMENT_REVIEW` remains binding. An unrecognized/default remote Docker context could target infrastructure outside the disposable sandbox. Local RAM headroom is limited and not automatically safe for Docker Desktop+PG18+Redis8. No progress is advanced to real engine acceptance on this receipt alone.

## 2. E46-F0R — deterministic read-only review before spending or contacting any daemon

To avoid copying/hardcoding Docker context names, endpoint URLs, certificates or credentials into ChatGPT/CI/reports, the next **one scoped operator action** is a new **OFFLINE** Windows PowerShell5.1 context classifier. It reads local `%USERPROFILE%\.docker\config.json` for `currentContext` and the local `%USERPROFILE%\.docker\contexts\meta\*\meta.json` entries for matching `Name` and `Endpoints.docker.Host`, **without printing the values**. It classifies only:

- `LOCAL_WINDOWS_NPIPE_CANDIDATE_UNVERIFIED` for **explicit allowlisted** Windows Docker named pipe `npipe:////./pipe/dockerDesktopLinuxEngine` or `npipe:////./pipe/docker_engine`. This means only a *candidate local endpoint string*, **not** trusted daemon verification or permission to connect.
- `REMOTE_OR_TCP_BLOCKED` for `tcp://`, `ssh://`, `http://` or `https://` endpoint types.
- `OTHER_OR_UNRECOGNIZED_BLOCKED`, `UNKNOWN_NO_DOCKER_HOST` or `UNRESOLVED` for all other cases. Never guess default Docker context network endpoint from a missing metadata file.

The classifier checks only environment variable **presence** (no values), a bounded JSON size, no symlinks/reparse meta files, at most 32 directly nested metadata directories, exact unique context match and local RAM. It reads Docker Desktop Windows service state; **never invokes `docker.exe`, WSL, PostgreSQL, Redis, Keycloak, SSH, any remote API or network command**, never starts a service or edits settings. It outputs **category only** and a uniquely named TEMP receipt, keeping `E46_F0R_RUNTIME_AUTHORIZATION=NO_GO_OWNER_APPROVAL_AND_REAL_ENV_REQUIRED` on *all* paths.

**Optional operator script file actually created:** `LMS-P4B02-E46-F0R-OFFLINE-CONTEXT-REVIEW-PS51.ps1` in the conversation artifacts, UTF-8 BOM, CRLF, 159 lines, **SHA256 `A94D79BA341452B3715CA99013221CB62BE0CC4E4838C8CDD874F53AFBCB0131`**. It was statically reviewed against known daemon/network/installation commands but **not executed on owner Windows**, so `E46_F0R_WINDOWS=NOT_RUN`. The exact script is a **chat download**, **not** a GitHub executable committed in this docs PR; scripts should be SHA-checked before execution. An in-chat **direct copy/paste** block can be used instead, avoiding a downloaded file transformation; it implements the same logic without needing another SHA-based download.

**Report fields requested:** `ENV_DO{CKER_HOST,CKER_CONTEXT,...}` only set/unset (do not send raw env values), `CURRENT_CONTEXT`, `SAVED_CONTEXT_METADATA_FILES`, `CURRENT_CONTEXT_EXACT_MATCH_COUNT`, `CURRENT_ENDPOINT_CLASS`, `DOCKER_DESKTOP_SERVICE`, `HOST_RAM_FREE_GIB`, `ISOLATION_FLAG`, `E46_F0R_RUNTIME_AUTHORIZATION`, `E46_F0R_FINAL`. No names/URLs/hostnames/credentials should be supplied.

## 3. Explicit gate for real PostgreSQL18/Redis8 and alternatives

Even if E46-F0R finds an allowlisted local named pipe, **real PG18+Redis8 testing stays BLOCKED**. Require separate explicit owner approval of a disposable sandbox (on-machine-only context and authenticated daemon, hard CPU/RAM/disk caps, no production mounts/tokens, fixed non-public network, content-digest pinned database binaries or OCI images, no extra spending/pulls without approval, safe fault injection and teardown). The current observed **2.78GiB free** is a resource-review flag; there is no universal proof that all services can run safely inside that headroom. Until then prefer documentation and isolated model tests, not starting Docker.

An option exists to run a completely isolated *nonproduction* engine sandbox on an independently provisioned test machine, but **do not reuse the existing production VPS or any shared Redis/PostgreSQL instance** without its own approval, configuration and isolated accounts. The assistant is not authorized to activate a sandbox, incur charges or implement material replay-auth change merely from F0R output. Actual tests `PG-R01..PG-R10`, failover/WAL/cross-owner/latency acceptance remain pending; candidate `ADR-LMS-TRUST-002` requires human ratification separate from current owner-ratified *nonproduction design* ADR-LMS-TRUST-001.

## 4. Preserved security acceptance and end state

- `E40_WINDOWS_REAL_ED25519_PLUS_REPLAY_MODEL=30/30_OWNER_REPORTED_PASS`. Two Redis-only silent nonce deletion/flush cases PASS by **demonstrating an UNSAFE replay counterexample**, not safe Redis.
- `E45_WINDOWS_ACTUAL_PDO_SQLITE=8/8_OWNER_REPORTED_PASS`, tests involve a **simulated Redis flush**, not actual Redis8 or Postgres18.
- `E46_F0_WINDOWS_OFFLINE=PASS_FACT_COLLECTION_ONLY`, `E46_ISOLATION_ELIGIBILITY=BLOCKED`, `E46_F0R_WINDOWS=NOT_RUN`.
- `T02_001..086_REAL_HTTP=0/86_EXECUTED`. `D02-01` two-JWS on-wire ratification/normalization/key custody PENDING; `D02-02` Redis-only unsafe with durable owner-DB ADR change and PG18/Redis8 proof BLOCKED; `D02-05` Keycloak signed effective access token alg/JWKS/grants UNKNOWN.
- No GitHub source, FE dirty worktree, HRM, VPS, PostgreSQL, Redis, Keycloak, Cloudflare, DNS or production mutation. No production authorization or zero-risk claims.

**Checkpoint:** `E40_WIN30/30 -> E45_WIN8/8 -> E46_F0_OFFLINE_PASS_WITH_4_FLAGS -> E46_F0R_METADATA_CLASSIFIER_PREPARED_NOT_RUN -> DOCKER_REAL_SANDBOX_NO_GO -> PG18_REDIS8_REAL_NOT_RUN -> D02_OWNER_DESIGN_RATIFICATION_HOLD -> PRODUCTION_NOT_AUTHORIZED`.
