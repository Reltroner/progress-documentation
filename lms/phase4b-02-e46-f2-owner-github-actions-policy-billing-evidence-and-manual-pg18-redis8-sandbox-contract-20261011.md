# LMS Phase 4B-02 — E46-F2 Owner GitHub Actions Policy & Billing Evidence; Manual-only PG18/Redis8 Lab Contract

> **Record:** `LMS-P4B02-E46-F2-20261011`.  
> **Current status:** `OWNER_GUI_ACTIONS_SETTINGS_REVIEW=PARTIAL_PASS_WITH_SUPPLY_CHAIN_GAPS`; `OWNER_GUI_BILLING_OVERVIEW=PASS_SNAPSHOT_NET_METERED_ZERO`; `GH_ACTIONS_PER_PRODUCT_SPENDING_CAP=NOT_VERIFIED`; `E46_F2_POLICY_DESIGN=PREPARED_NOT_RATIFIED`; `NEW_LAB_REPO/WORKFLOW/RUN=NOT_CREATED`; `PG18_REDIS8_REAL=0/10`; `T02_REAL_HTTP=0/86`; `D02_OWNER_RATIFICATION=HOLD`; `PRODUCTION=NOT_AUTHORIZED`.  
> **Evidence:** Owner-submitted screenshots of `github.com/Reltroner/LMS-BE/settings/actions` (top and lower portions), `github.com/Reltroner/LMS-BE/actions`, and text copied from `github.com/settings/billing` on 2026-10-11, plus **read-only** linked GitHub repository/workflow verification. The browser UI screenshots are **not evidence the owner clicked Save**; no settings changes requested or performed.  
> **Governance:** Existing [README §7 clarity-first workflow](./README.md), [master infrastructure placement frozen contract](./master-infrastructure-placement-contract.md), [logical service boundary frozen contract](./logical-service-boundary-api-contract.md), [E46-F1 repo/billing feasibility](./phase4b-02-e46-f0s-windows-capacity-acceptance-and-f1-github-actions-isolation-feasibility-20261011.md).  
> **Source pins last reviewed before writing:** `Reltroner/LMS-BE/main=617dadc0d0d627071d713ceb729df6658202b43e`; `Reltroner/progress-documentation/main=183372371b3a40a0349ac390848911273ccd2361`; existing BE workflow blob `78c507dc57910eadc9de31819dac7fb6a3d845f1`; docs PR #46 remains OPEN; pin must be refreshed before future writes.

## 1. Owner-screen evidence — exact policy facts, not inferred settings

| Control shown on existing `LMS-BE` Actions → General page | Owner screenshot state | Engineering classification |
|---|---|---|
| Actions policy | **Allow all actions and reusable workflows** selected | `ENABLED_BROAD_THIRD_PARTY_ALLOWED`; supply-chain policy broad; independent narrowing desirable after compatibility review |
| Require actions pinned to full-length commit SHA | **Unchecked** | `NOT_ENFORCED`; treat as gap, **do not toggle immediately** |
| Check, workflow run, status, artifact and log retention | **90 days**, maximum shown 90 | existing repo retention fact; new lab should avoid artifact upload/cache |
| Fork workflow approval | **Require approval for first-time contributors** selected | narrower than "all external contributors"; do not change without contribution/CI trigger risk assessment |
| Default `GITHUB_TOKEN` workflow permissions | **Read repository contents and packages** selected | `DEFAULT_READ_ONLY`, safer than write; still require minimal permissions in every workflow |
| Allow GitHub Actions to create and approve pull requests | **Unchecked** | `DISABLED`; keep |
| Existing Actions history | **30 workflow runs**, recent green successes and some historical failures | `HISTORICAL_CI_EXISTS` — NOT proof new isolated PG18/Redis8 image runtime works |

Linked GitHub read-only inspection of actual `LMS-BE/main/.github/workflows/phase3b-contract-ci.yml` at blob `78c507dc57910eadc9de31819dac7fb6a3d845f1` confirmed: `actions/checkout@v4` and `shivammathur/setup-php@v2`, `ubuntu-24.04`, `permissions: contents: read`, and `push`/`pull_request` triggers for existing scope. These are **tag references**, not full 40-character pinned commit hashes. GitHub states that enabling repository `Require actions to be pinned to full-length commit SHA` enforces it for **all** referenced actions, including GitHub-owned actions; toggling now would predictably **block these existing tagged actions**. Do not impair Phase3B main CI without a separate owner-approved, separately tested **dependency source SHA migration**. Likewise, selecting only owner-defined actions could block `actions/checkout` unless GitHub-owned actions are explicitly permitted. Do not click `Save` today.

Existing read-only `GITHUB_TOKEN` default plus job-level `permissions: contents: read` is a positive control; it does not prevent an allowed malicious action from reading data it has access to, and does not prove repo secrets/runner network isolation.

## 2. Billing screenshot — exact interpretation, no false zero-risk claim

The owner copied personal settings billing overview:
- `GitHub Free` plan at **$0.00/month** and `Copilot Free` at **$0.00/month**.
- `Current metered usage` for displayed Oct 1–30 2026 period: **$1.82 gross**.
- `Current included usage` / included discounts for displayed period: **$1.82**.
- **Difference displayed from those two aggregates: $0.00**. This is a snapshot/net arithmetic deduction, **not** a verified account spending-cap setting, account payment method state, no future bills guarantee, or proof that the entire $1.82 originated from GitHub Actions.
- Top-three gross usage by repository: `LMS-BE=$1.22`, `LMS-FE=$0.47`, `reltroner-hr-app=$0.13`. This widget's product allocation and complete future billing behavior **cannot** be inferred from a copied overview. Owner did not provide Actions-only metering breakdown or a `Budget`/spending-limit setting.

As of 2026-10-11 official GitHub documentation states **standard GitHub-hosted runners in public repositories are free**, and `ubuntu-24.04` on public repositories is a **standard** runner label (4 vCPU, 16GiB according to the current official spec). Larger runners **always billed**, and artifact/cache/Packages storage limits or billing remain distinct. A public GitHub Free account is a **credible no-additional-runner-cost candidate**, not automatic authority to run anything or consume storage quota. Official sources:
- https://docs.github.com/en/billing/concepts/product-billing/github-actions
- https://docs.github.com/en/actions/how-tos/write-workflows/choose-where-workflows-run/choose-the-runner-for-a-job
- https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository
- https://docs.github.com/en/actions/reference/security/secure-use

**Unclosed billing subgate:** inspect **Actions** product-specific current usage and any budgets/limits in Billing and licensing. Record only `ACTIONS_PRODUCT_METERING_REVIEWED=YES/NO`, `ADDITIONAL_SPENDING_BUDGET_LIMIT_CONFIRMED=YES/NO`, `NO_EXTRA_EXPENSE_POLICY_ACCEPTED=YES/NO` and high-level status, **never payment details/account IDs/invoices**. Avoid larger runners, artifact uploads/caching and recurring workflow triggers.

## 3. E46-F2 strategic choice and operational separation

**Chosen design candidate (requires owner ratification):** A dedicated **PUBLIC**, **synthetic-data-only**, manually dispatched, temporary `Reltroner` GitHub repository for real PostgreSQL18+Redis8 **failure-model lab**. Reason: current local Windows Docker has a metadata-only local-npipe candidate but Docker Desktop stopped and RAM minimum **2.73GiB**, with owner-local Docker **NO_GO**; using existing production VPS or existing `LMS-BE/main` would increase blast radius and/or cause existing triggered CI to run.

**Strict three-stage change-control proposal:**

- **F2-A review only (CURRENT):** Produce documentation ratification and standalone lab workflow/harness source in docs/non-executable paths. No repository creation, image downloads, workflow trigger, secrets or costs. Consider repository Actions policies and billing separately from production-facing BE.
- **F2-B explicit OWNER approval for creating a public, empty lab repo only:** Separately grant `CREATE_PUBLIC_SYNTHETIC_ONLY_REPO=YES`; evaluate that public repository visibility and name are acceptable; **creation itself** may create a public resource and must not be inferred from approval of a design write. No `.github/workflows/` executable workflow yet until owner's second approval.
- **F2-C explicit OWNER approval for a specific SHA-reviewed manual workflow and its first `workflow_dispatch` run:** Require reviewed exact OCI digests, no secrets, fixed 10-minute standard runner, bounded job limits/CPU/memory, per-job identity, no production network endpoints, explicit synthetic test usernames/passwords and a separate `ALLOW_FIRST_REAL_PG18_REDIS8_CI_RUN=YES` approval. A workflow with `workflow_dispatch` **must be present on the repo's default branch** before it is manually dispatchable. Thus the owner must approve the initial lab default-branch workflow placement separately from the manual run. No auto-triggered push/PR/schedule, and do not add workflow YAML to active `LMS-BE` or docs repo.

**Lab workflow mandatory controls** (do not imply they are already implemented):
- `on: workflow_dispatch` **only**; `runs-on: ubuntu-24.04` standard only, `permissions: {}` if no checkout needed, or `contents: read` at most, and `timeout-minutes: 10` with one-job concurrency; no matrix or scheduled retries.
- Prefer **zero external `uses:` steps** in the first lab to remove tagged action/SHA policy hazards. If later adding `uses:`, each external action must be pinned to a **verified full commit SHA from its upstream repository**, never invented/guessed/tag-only. A fresh separate lab may set strict SHA policy *before* approving its first workflow; **do not turn it on in existing LMS-BE** while its workflow is tag-referenced.
- A Linux job container plus PostgreSQL and Redis **service containers** share ephemeral per-job bridge networking; service container names `postgres`, `redis` can be used internally with **no host-published service ports**. Jobs running directly on VM need host port mapping and are **not** accepted as equivalent for this no-host-port lab. OCI images for **PostgreSQL18.x**, **Redis8.x** and the **job container** must be digest-pinned `@sha256:REAL_VERIFIED_DIGEST`; this contract does **not** claim any digest has yet been verified. Real database versions are checked at runtime, and health checks must fail closed.
- Third-party package installation/registry pulls imply external traffic to image registries; **do not claim NO_NETWORK overall**. In scope is `NO_PRODUCTION_ENDPOINT`, no production credentials, no public inbound test database port, minimal egress/identity and no environment-scoped deployment.
- The first run is **bounded functional subset**, not full fault testing or all ten PG-R cases: atomic two-proof SQL reservation, uniqueness and rollback, controlled Redis8 replay-key removal/FLUSH of **disposable isolated service**, fail-closed authority errors and retention clocks. `PG-R06` PostgreSQL WAL/server restart and `PG-R07` standby failover need separate hardware/container topology and explicit permission; `PG-R09` load/performance and `PG-R10` owner DB grant parity also require separate mapping, not asserted complete by one ephemeral PostgreSQL and Redis service.
- Zero production .env, no GitHub production secrets/environments/deploy tokens/SSH, no PR-derived untrusted code, no public DB service ports, no cache/upload-artifact/Packages writes, no logs of credentials or connection strings. Synthetic passwords/role IDs scoped to disposable lab only; cleanup is performed by GitHub after run, not by scripts targeting user resources. Every step's exit code, engine version and isolated test sample hash must be logged, without credentials.

## 4. Exact PostgreSQL18/Redis8 acceptance classifications

| Gate | Meaning | Current |
|---|---|---|
| `PG-R01` | concurrent SQL UNIQUE claim, one accept/one duplicate denied | `NOT_RUN` |
| `PG-R02` | two-proofs atomic transaction, duplicate delegation triggers full ROLLBACK | `NOT_RUN` |
| `PG-R03` | real isolated Redis8 `FLUSHDB`/loss, previously consumed nonce remains denied by *durable SQL authority* | `NOT_RUN` |
| `PG-R04` | process crash/restart after acknowledged COMMIT, nonce remains denied | `NOT_RUN` |
| `PG-R05` | SQL unavailable/errors/ambiguous acknowledgment fail closed | `NOT_RUN` |
| `PG-R06` | PostgreSQL18 WAL/server restart durability, true restart proof | `NOT_RUN` |
| `PG-R07` | missing-commit after standby promotion, fence/quarantine failure safety | `NOT_RUN` |
| `PG-R08` | expiry/cleanup clocks and concurrent clients cannot free still-valid nonce | `NOT_RUN` |
| `PG-R09` | bounded load under documented resource limit and WAL/latency observations | `NOT_RUN` |
| `PG-R10` | grant/ownership parity with **existing four owner DBs**, Assistant still no DB | `NOT_RUN` |

**Do not silently close D02-02:** local E40 30/30 signed Ed25519/replay-model PASS with Redis-only silent-loss **UNSAFE counterexample** + E45 8/8 real local PDO_SQLite PASS are valuable **38/38 exploratory local tests**, but **not** PostgreSQL18 replica failover or actual Redis8 evidence. Source implementation can proceed only after a separately owner-ratified changed replay-authority ADR and applicable acceptance gates; the exact six microservice architecture (only Gateway public, five private, four owner DBs) and Keycloak OIDC remain governed by the frozen contracts. **Canonical T02 HTTP=0/86 executed**.

## 5. Owner-required actions and final checkpoint

**No action altering production settings should be performed now.** Next safe GUI action: in `https://github.com/settings/billing`, select **Actions** product-specific metered-usage and *Budgets* if present, **read only**. Provide high-level state of spending control, *not* amount on card/payment details. Existing `LMS-BE/settings/actions` GUI has been inspected sufficiently; **do not click any Save, toggle full-SHA requirement or change first-time contributor approval**.

**After review**, seek **one explicit owner decision**: approval of separately creating a public, synthetic-only trust sandbox repo with NO workflows yet. If not approved, continue local deterministic evidence/ADR design and keep `PG18_REDIS8_REAL=BLOCKED`. If approved, create exactly that isolated repo with no production secrets, inspect new repo Actions policy and then seek **second** approval before adding/running any real-engine workflow. This prevents a vague "go ahead" from being interpreted as unlimited authority to start services or incur charges.

**Final state:** `E46_F2_OWNER_GUI_SECURITY_POLICY=OBSERVED_GAPS_IDENTIFIED`; `BILLING_SNAPSHOT_GROSS_1_82_INCLUDED_1_82_NET_0_00` but `ACTIONS_SPECIFIC_BUDGET=UNVERIFIED`; `PUBLIC_STANDARD_RUNNER=DOCUMENTED_FREE`; `BE_CI_SHA_PINNING_REQUIREMENT=OFF_WITH_EXISTING_TAGGED_ACTIONS`; `LOCAL_DOCKER=NO_GO`; `NEW_CI_LAB=DESIGN_ONLY_NO_REPO_OR_WORKFLOW`; `PG18_REDIS8=0/10`; `T02_HTTP=0/86`; `DESIGN_RATIFICATION=HOLD`; `PRODUCTION=NOT_AUTHORIZED`.
