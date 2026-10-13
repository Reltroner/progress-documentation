# LMS Phase 4B-02 — E46-F0S Owner Windows Capacity Evidence and E46-F1 GitHub Actions Sandbox Feasibility

> **Record:** `LMS-P4B02-E46-F1-20261011`  
> **Engineering status:** `E46_F0S_WINDOWS=OWNER_OUTPUT_PASS_READONLY_CAPACITY_FACTS_ONLY`; `LOCAL_DOCKER_RUNTIME=NO_GO`; `E46_F1_GITHUB_ACTIONS=READ_ONLY_FEASIBILITY_PARTIAL_BILLING_ACTIONS_SETTINGS_UNVERIFIED`; `REAL_POSTGRESQL18_REDIS8_TESTS=0`; `DESIGN_RATIFICATION=HOLD`; `SOURCE_AND_PRODUCTION_DEPLOY_NOT_AUTHORIZED`.  
> **Observed operator local timestamp:** 2026-10-11 03:48:49 +07.  
> **Reference:** README §7 clarity-first binding policy, frozen Phase0C/1, ADR-LMS-TRUST-001 nonproduction design only, E46 owner evidence, existing Phase3B contracts and test taxonomy.

## 1. E46-F0S owner Windows facts (not independent remote host telemetry)

Owner pasted `E46_F0S_MEMORY_SAMPLES=3`, `HOST_RAM_FREE_SAMPLE_1_GIB=2.73`, `...2_GIB=2.74`, `...3_GIB=2.74`, `HOST_RAM_MIN_FREE_GIB=2.73`, `HOST_RAM_TOTAL_GIB=15.33`, `SYSTEM_DRIVE_FREE_GIB=45.84`, `DOCKER_DESKTOP_SERVICE=Stopped_READONLY`. Process category working sets (GiB) as **approximate, shared-page-overlapping, not reclaimed RAM**: `BROWSER=6.15`; `IDE=1.37`; `VIRTUALIZATION=0.01`; `DATABASE=0.14`; `OTHER=8.15`. Three samples pass **fact collection only**: `E46_F0S_FINAL=PASS_READONLY_CAPACITY_FACTS_ONLY`; screening classification `E46_F0S_CAPACITY_SCREEN=UNDER_4GIB_REVIEW`; `E46_F0S_RUNTIME_AUTHORIZATION=NO_GO_OWNER_APPROVAL_REQUIRED`; explicit `NO_PROCESS_TERMINATION_OR_SERVICE_START=YES`, `REAL_PG18_REDIS8_TESTS=NOT_PERFORMED`, `PRODUCTION_MUTATION=NO`.

**Interpretation:** 2.73 GiB was the observed **minimum** of three samples, not continuously monitored physical capacity. The project’s 4 GiB marker is a conservative human-review trigger, **not a vendor runtime minimum or guarantee of sufficient headroom**. Summing per-process working-set buckets can double-count shared pages, and browser working set 6.15 GiB is **not** 6.15 GiB of immediately reclaimable RAM. Neither killing Chrome/IDE nor starting Docker/WSL is authorized. The current Docker context was classified in the preceding E46-F0R purely as `LOCAL_WINDOWS_NPIPE_CANDIDATE_UNVERIFIED` with one matching metadata entry; no authenticated daemon call. **Local Docker remains NO_GO.**

## 2. E46-F1 remote public CI feasibility — actual read-only observations

The assistant used the **connected GitHub read-only API** to inspect actual repository metadata and current workflow sources, without creating a new workflow/job, changing permissions, touching source or contacting a GitHub runner.

- `Reltroner/LMS-BE` **public**, owner account type `User`, default branch `main`, connector `admin/push` permission available but **NOT exercised** for workflow changes. Source `LMS-BE/main=617dadc0d0d627071d713ceb729df6658202b43e` at discovery. Current workflow `.github/workflows/phase3b-contract-ci.yml` blob SHA `78c507dc57910eadc9de31819dac7fb6a3d845f1`. It already uses **`runs-on: ubuntu-24.04`**, explicit `permissions: contents: read`, and `timeout-minutes` 10/20; but triggers **push and pull_request** on `main` and `phase3b/**`. Reusing main or broad branch trigger would start unrelated CI and break bounded scope.
- Read-only workflow runs listing showed **30** historical workflow runs; most recent completed success (push `2026-10-10T18:03:19Z`, head `617dadc...`), recent pull_request success and previous push success. This proves **historical GitHub-hosted runner use occurred**, **not** that the account’s billing is capped or that isolated container services can currently start.
- `Reltroner/LMS-FE` is also public and has separate Next.js build CI (should remain untouched). `Reltroner/progress-documentation` is public with **no `.github/workflows` directory found on main**; the existing documentation PR #46 therefore has no identified repository-owned workflow to execute these new doc commits. No new workflow has been committed to either repo.
- **Official GitHub documentation checked 2026-10-11:** standard GitHub-hosted runners in **public repositories** are free, whereas **larger runners are billed** and artifact/cache storage has quotas/possible billing; and Linux Ubuntu GitHub Actions **service containers** support ephemeral PostgreSQL and Redis per-job network. References:
  - https://docs.github.com/en/billing/concepts/product-billing/github-actions
  - https://docs.github.com/en/actions/tutorials/use-containerized-services/create-postgresql-service-containers
  - https://docs.github.com/en/actions/tutorials/use-containerized-services/use-docker-service-containers
  - https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax

**Remaining account-specific evidence:** Workflow policy/status on `LMS-BE`, present billing/spending limit, whether secret-free repository is appropriate, owner approval for a new dedicated security lab, exact image digests and runner release capacities **NOT VERIFIED**. GitHub’s public standard runner pricing statement is **not blanket assurance that this exact future workflow cannot incur a charge or storage cost**.

## 3. Architecture recommendation (PROPOSAL ONLY, not a green gate)

Prefer **a separate public, disposable, secret-free GitHub Actions test repository** controlled by owner, rather than putting database-fault injection into the live LMS-BE CI, starting local Docker Desktop with 2.73 GiB free, or using the VPS production PostgreSQL/Redis. This separation limits blast radius and prevents pushing a new workflow from unintentionally starting existing main/PR CI. No new repository is requested/created automatically; name `LMS-Trust-Sandbox` is only an optional placeholder, not an existing confirmed repo.

**Initial controlled CI job template constraints (future owner approval before any execution):**
1. New lab repo must be public (or have separately owner-verified private repo budget); GitHub-hosted **standard `ubuntu-24.04` runner only**, not larger/self-hosted; `permissions: contents: read`; `timeout-minutes: 10`; `cancel-in-progress: true`; `on: workflow_dispatch` only (**no push/PR/schedule triggers**). Note: manual dispatch typically requires the workflow to be present on the default branch; a review/merge to the new *isolated lab* default branch must be approved **before** manual launch. Do not expect a branch-only workflow to be dispatchable automatically.
2. No repository or environment production secrets, no `secrets:` environment mappings, no production domains, SSH keys or production checkout. Use randomly created test-only PostgreSQL/Redis credentials scoped to the single job (carefully avoid printing raw values), and **never configure CI to connect to actual deployed Reltroner infrastructure**. A public repo exposes workflow source and logs; use only synthetic test data.
3. Pin exact OCI `@sha256` digests for PostgreSQL **18.x** and Redis **8.x** plus any job image, verify real server versions at job runtime, archive digest/version evidence without exposing credentials. A tag `postgres:18` or `redis:8` alone is **insufficient** for an immutable, deterministic experiment. Image digest provenance and architecture must be independently verified before insertion; do not invent a digest.
4. Job as an Ubuntu **job container** with PostgreSQL and Redis service containers on a private per-job network, **no published host ports**, no volume mounts of anything from production, no `docker.sock` mount, no privileged mode. GitHub Actions runner still has external network for fetching images; the initial Docker image pull and dependency retrieval are real **external traffic** (to registries), so do NOT label entire CI run `NO_NETWORK`—the security boundary is **no contact with production and no public exposed test DB port**.
5. First approve only bounded **PG-R01/R02/R03/R05/R08/R10 subset** that can be safely covered without forcibly killing service containers. PG-R04 (worker process restart) can be scoped separately. PG-R06 (Postgres server restart/WAL), PG-R07 (standby failover with acknowledged commit gap) need an independently reviewed isolated topology with fault-injection permissions and must **not** be marked passed by a one-Postgres service setup. PG-R09 load testing requires separately approved resource budget and bounded workload—not uncontrolled traffic. Record per-case `PASS`/`FAIL`/`NOT_RUN` without elevating partial subset to ten-of-ten.
6. No `upload-artifact`, `actions/cache`, GitHub Packages publication, deployment, release, or network-reachable externally mapped database listener in the first bounded lab run. Limit log verbosity and sanitize SQL identities/usernames. Separate workflow review and manual owner dispatch.
7. For any failed test, `fail-closed` verdict; no rerun loop on same uncontrolled runner, no retries to production, no automatic merge/deploy. The output is exploratory evidence, not ratification of a new replay-authority ADR.

## 4. Strict next required operator read-only GUI gates (nothing to click to change yet)

**GitHub Settings and billing visibility are account-specific; no connector admin endpoint was used or verified.** Owner should **inspect only**, without saving/toggling settings:

- Open https://github.com/Reltroner/LMS-BE/settings/actions and read **Actions → General** policy. Capture **only** whether Actions is enabled/allowed, workflow permissions, and third-party action restrictions. Do not include tokens or private authorization data. Existing `permissions: contents: read` in YAML is a useful defense but does not replace current account/repository policy review.
- For owner account `Reltroner` (verified GitHub `User` type), open GitHub avatar → **Settings → Billing and licensing → Actions usage/spending** (section labels can change); check current free/paid runner storage/limit relevant to repository. Record **only** `STANDARD_PUBLIC_RUNNERS_FREE_PER_GITHUB_DOCS`, `BILLING_SPEND_LIMIT_VERIFIED=YES/NO`, and `ARTIFACT_STORAGE_LIMIT_REVIEWED=YES/NO`. Do NOT provide payment methods, addresses, billing invoices or account IDs. An account may have nonzero spending enabled for unrelated repos; do not assume no spend based only on public repo status.
- GitHub `LMS-BE` → **Actions** tab: observe recent runs and GitHub-hosted runner labels, **do not rerun**. We have already verified latest successful `phase3b-contract-ci.yml` via API; no need to launch a new test to prove Actions works generally.
- Do **not** create a repository/workflow, change permissions, use a larger runner, upload secrets, trigger `workflow_dispatch`, or merge current docs PR until owner explicitly approves the bounded lab policy and budget.

## 5. Evidence taxonomy and exit

| Gate | Exact status |
|---|---|
| E40 30 local real Ed25519 and replay **model** cases on Windows | `OWNER_OUTPUT_PASS_30/30`; **Redis-only silent nonce deletion UNSAFE counterexample** |
| E45 8 real local PDO_SQLite transactional cases on Windows | `OWNER_OUTPUT_PASS_8/8` |
| E46-F0S local capacity fact collection | `OWNER_OUTPUT_PASS_READONLY`; `HOST_RAM_MIN_FREE_GIB=2.73`; `LOCAL_DOCKER_NO_GO` |
| E46-F1 repository/CI technical feasibility | `PARTIAL_READONLY` — public BE + existing Ubuntu workflow + successful historical runs |
| E46-F1 account billing, runner/sandbox credentials and workflow policy | `UNKNOWN_OWNER_GUI_REVIEW_PENDING` |
| Real isolated PostgreSQL18+Redis8 PG-R01..PG-R10 | `0/10 ACTUAL_ENGINE_CASES_RUN` |
| Canonical 86 HTTP T02 acceptance | `0/86 EXECUTED` |
| D02-01..05 design ratification and production | `HOLD` / `NOT_AUTHORIZED` |

**Checkpoint:** `E40_OWNER_WINDOWS30/30 -> E45_OWNER_WINDOWS8/8 -> E46_F0R_LOCAL_NPIPE_METADATA_CANDIDATE -> E46_F0S_RAM_2.73GiB_READONLY_PASS_LOCAL_DOCKER_NO_GO -> E46_F1_GITHUB_PUBLIC_STANDARD_RUNNER_CONCEPT_VALIDATED_ACCOUNT_POLICY_BILLING_PENDING -> OWNER_ISOLATED_LAB_APPROVAL_PENDING -> PG18_REDIS8_REAL_0/10 -> 86_CANONICAL_HTTP_0/86 -> DESIGN_RATIFICATION_HOLD -> PRODUCTION_NOT_AUTHORIZED`.

**Ultimate target remains** secure end-to-end Reltroner LMS public gateway + five private microservices, Keycloak OIDC, independently owned four PostgreSQL domain DBs, Redis with bounded operational use (never unconditional redis-only authoritative replay after silent loss), real HTTP acceptance, deterministic security and no unsanctioned production risk/cost.
