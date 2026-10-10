# Reltroner LMS Phase 4B-02 — E46-F3A Verified Empty Public Lab Receipt and E46-F3B Review Work Order

> **Record:** LMS-P4B02-E46-F3A-LIVE-20261011
> **Evidence status:** F3-A PASS VERIFIED by connected GitHub read-only live API on 2026-10-11; F3-B DESIGN / SECURITY REVIEW PREPARED ONLY; F3-C RUNTIME NOT AUTHORIZED.
> **Hierarchy:** [LMS canonical README §7](./README.md), [E46-F2 security + billing](./phase4b-02-e46-f2-owner-github-actions-policy-billing-evidence-and-manual-pg18-redis8-sandbox-contract-20261011.md), [E46-F3 owner creation-only approval](./phase4b-02-e46-f3-owner-conditional-approval-zero-additional-cost-public-sandbox-provisioning-20261011.md), frozen placement and logical boundary contracts; this is an operational evidence receipt, NOT a frozen architecture amendment.
> **Production, LMS-BE, LMS-FE, Keycloak, DNS, and VPS:** NO MUTATION AUTHORIZED.

## 1. Live GitHub F3-A facts — not inferred from a URL

At the exact read-only connected GitHub inspection:
- URL: https://github.com/Reltroner/lms-trust-sandbox ; clone URL https://github.com/Reltroner/lms-trust-sandbox.git
- Full repo name **Reltroner/lms-trust-sandbox**; stable repository ID **1413681840**; owner **Reltroner** personal User.
- Visibility **public**; archived **false**; default branch *configured name* **main**, but **NO ACTUAL main ref yet**.
- Repository size **0**; `GET /repos/Reltroner/lms-trust-sandbox/branches` returned exactly `[]`.
- `GET /repos/Reltroner/lms-trust-sandbox/contents` returned GitHub 404 message **"This repository is empty."** Distinguish this expected empty-repository 404 from inaccessible repository.
- `GET /repos/Reltroner/lms-trust-sandbox/actions/runs?per_page=1` returned `total_count=0` and no run objects.
- GitHub REST creation timestamp `2026-10-10T21:28:06Z` = **2026-10-11 04:28:06 Asia/Jakarta**.
- Description exactly: `Nonproduction synthetic-only security and data-integrity lab for Reltroner LMS. No production data, secrets, or deployments.`
- GitHub connected application reports read/write access to the repository; branch, secrets, workflow, checkout, deploy, image pulls and runtime were **NOT CREATED/PERFORMED** in this inspection.
- Claims limited to endpoints inspected; no GitHub repo setting or payment/spending hard-stop is inferred from empty repo or zero workflow runs.

**F3-A decision:** `PASS_VERIFIED_EMPTY_PUBLIC_LAB`. The owner created it through GUI; assistant performed read-only confirmation, NOT repository creation.

## 2. Trust boundary, cost, scope

The lab is a **repository-level disposable test fixture**, not a seventh deployable Laravel microservice, not a fifth PostgreSQL owner DB, and not a source of production credentials. The existing frozen six-service/four-owner-DB architecture remains binding.

Current official GitHub docs: standard `ubuntu-24.04` runner in a **public** repository is free/unlimited for standard hosted-runner usage and has **4 vCPU, 16 GiB RAM, 14 GiB SSD**. This is a runner billability statement, not proof of zero overall bill under all GitHub services; `Billing > Budgets` hard-stop remains `UNVERIFIED`. Larger runners, private-repository minutes, artifacts, cache, Packages, premium add-ons, cross-repo credentials, and production connectivity are excluded.

Initial proposed experimental shape (NOT DEPLOYED): one `workflow_dispatch`-only job on standard `ubuntu-24.04`, `timeout-minutes: 10`, `permissions: {}` if no repo checkout is needed; zero marketplace `uses:`; no `push`/`pull_request`/`schedule`, matrices, retries, workflow artifacts/cache/Packages, production secrets, self-hosted runners, environments or public host-mapped PostgreSQL/Redis ports.

To avoid host-published service ports, use `jobs.<id>.container` PLUS `services.postgres` and `services.redis` on GitHub's per-job internal network; the job must have tested PostgreSQL18 and Redis8 client capabilities. **Client tooling for both services is a PENDING design preflight**, not something assumed from any image. Each of the **job container, postgres service and redis service** requires a real digest-pinned OCI reference verified from its registry and `linux/amd64` manifest; a string matching 64 hex alone is insufficient provenance. Runtime version checks and health checks must fail closed.

## 3. F3-B security acceptance before creating ANY first commit or workflow

The next GitHub GUI discovery is **READ-ONLY**, on the NEW lab repo, not `LMS-BE`:

1. Open https://github.com/Reltroner/lms-trust-sandbox/settings/actions . If the General settings page is available, inspect **Actions permissions**, third-party actions allowance, **Require actions to be pinned to full-length commit SHA**, workflow default `GITHUB_TOKEN` permissions, fork approval and retention. Do not press `Save` or change settings yet.
2. Open https://github.com/Reltroner/lms-trust-sandbox/actions . Expect empty workflow/run listing while first commit has not been authorized; do not use workflow templates or select `Configure`.
3. Open https://github.com/settings/billing and inspect **Actions** product and **Budgets** (read-only). Record whether a spending hard cap is actually present; never copy payment data, billing address, account IDs, card or token details.
4. Give result in concise text or cropped screenshots **without secrets**. GitHub App may not be permitted to access repository administration settings directly; this is why GUI evidence is separately required.

**Before a first default-branch commit, every box must be evidenced**: (a) exact reviewed source and hash for static harness/workflow, (b) registry-approved immutable digests for all containers with verified platform and engine major/minor version, (c) synthetic-only DB fixtures and runtime credentials, (d) no public port mappings or production contacts, (e) zero marketplace `uses:`, (f) manual trigger alone, (g) standard public runner and cost checks, (h) no load/failover topology in first batch, (i) owner-specific `ALLOW_F3B_DEFAULT_BRANCH_WORKFLOW_BOOTSTRAP` authorization. **Owner's earlier F3-A permission is not equivalent.**

A fresh empty repository has no base Git commit; it is valid to *plan* a single reviewed first commit after owner authorization, but impossible to create a conventional PR against non-existent `main` before bootstrapping it. The initial commit is its own change-control gate, and first run is a different gate. No need to generate an artificial orphan branch or create a CI workflow to show a PR prematurely.

## 4. Actual PostgreSQL18+Redis8 PG-R01..10 coverage, with non-overclaiming

| Test | Definition | First reviewed lab run |
|---|---|---|
| PG-R01 | Parallel claims for same durable SQL UNIQUE key; one winner, one rejected | CANDIDATE after multi-client proof |
| PG-R02 | Two separate nonce proofs reserved in ONE SQL transaction; duplicate second causes full rollback of first | CANDIDATE |
| PG-R03 | Actual disposable Redis8 key loss / FLUSHDB; pre-consumed nonce remains denied using independent durable SQL authority | CANDIDATE; Redis-only strategy still UNSAFE |
| PG-R04 | Client process death/restart after acknowledged durable COMMIT | DEFER |
| PG-R05 | SQL unavailable/error/unknown write ACK never grants authorization | DEFER |
| PG-R06 | Real PostgreSQL WAL + server restart durability | DEFER — separate restart-specific safety |
| PG-R07 | Standby lag / promotion missing-commit fencing safety | DEFER — replica topology |
| PG-R08 | Token expiry/quarantine/cleanup boundaries under concurrency | DEFER |
| PG-R09 | Load/resource contention validation | DEFER — separate controlled capacity scope |
| PG-R10 | Distinct owner DB grants and cross-service authority enforcement | DEFER — four owner-DB privileges |

**Initial engine run MUST NOT be described as 10/10**; partial tests become `PASS` only with exact on-run stdout/exit logs, version proof, reproducible snapshot SHA, expected-vs-actual assertions, independent authority and failure-mode evidence. The existing Windows E40 30/30 model and E45 8/8 SQLite proof remain **38/38 local exploratory**, separate from **PG-R01..10 0/10 real** and **canonical T02 HTTP 0/86**.

## 5. F3-B digest evidence process (READ-ONLY planning)

Official Docker Registry v2 manifest `HEAD /v2/{name}/manifests/{reference}` supplies `Docker-Content-Digest` when using an authenticated *public pull-scope* bearer request and appropriate OCI/Docker `Accept` types. The `GET` manifest index provides `manifests[].platform` to verify `linux/amd64`. Read-only public registry inspection does **not** pull image layers, require docker daemon, or create a GitHub Actions runner. Pin workflow images to actual `name@sha256:<verified-index-digest>`; never use mutable `:18` / `:8` alone or invented digests. Verify resolved database versions **inside the actual job** after owner authorizes F3-C. Re-run digest review if tag or source changes before bootstrap.

Docs:
- https://docs.docker.com/reference/api/registry/latest/operations/HeadImageManifest/
- https://docs.docker.com/reference/api/registry/latest/operations/GetImageManifest/
- https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax
- https://docs.github.com/en/actions/reference/runners/github-hosted-runners

At this F3-A receipt, no image SHA256 digest is ratified, no job image client-capability selection is ratified, no workflow SHA exists, and **no actual service is running**.

## 6. Absolute STOP / GO

`F3A=PASS`; `F3B_GUI_ACTIONS_REVIEW=PENDING`; `F3B_EXACT_WORKFLOW_AND_DIGEST_REVIEW=PENDING`; `F3B_INITIAL_DEFAULT_BRANCH_COMMIT=NOT_AUTHORIZED`; `F3C_FIRST_MANUAL_RUN=NOT_AUTHORIZED`; `GH_ACTIONS_RUNS=0`; `REAL_PG18_REDIS8=0/10`; `CANONICAL_HTTP_T02=0/86`; `D02_OWNER_RATIFICATION=HOLD`; `BE_FE_PROD_MUTATION=NOT_AUTHORIZED`.

**No one should interpret "maximize productivity" or "avoid rollback" as a security-proof or guarantee of zero risk:** instead use fail-closed, documented blast-radius controls and exact consent for irreversible/shared-state transitions.
