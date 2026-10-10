# LMS Phase 4B-02 — E46-F3 Owner Conditional Approval: Zero-Additional-Cost Public Trust Lab Repository

> **Record:** `LMS-P4B02-E46-F3-20261011`.  
> **Authority:** Owner statement 2026-10-11: *"aku menyetujui keputusan selama produktifitas meningkat, arah engineering tetap on track comply ... dan hemat resource alocation dan usage. tetapi kalau ada yang lebih murah biaya, maka pilih yang lebih murah tetapi tidak mengorbankan produktifitas."* This authorizes a **single empty, PUBLIC, nonproduction lab repository** when it is the most efficient no-additional-cost isolation option. **It does NOT authorize workflows, GitHub Actions jobs/runner starts, OCI pulls, image scans, Postgres/Redis instances, broader secrets or production mutation.**
> **Status:** `E46_F3_ARCHITECTURE_DECISION=APPROVED_CONDITIONALLY_EMPTY_PUBLIC_LAB`; `GITHUB_REPO_CREATION_PENDING_HUMAN_GUI`; `WORKFLOW_DEPLOYMENT=NOT_AUTHORIZED`; `REAL_DB_RUN=NOT_AUTHORIZED`; `PG_R01..10=0/10`; `T02_HTTP=0/86`; `DESIGN_RATIFICATION=HOLD`.
> **Canonical:** Binding [README §7](./README.md), [E46-F2 GitHub billing/security evidence](./phase4b-02-e46-f2-owner-github-actions-policy-billing-evidence-and-manual-pg18-redis8-sandbox-contract-20261011.md), frozen Phase0C placement and Phase1 logical service/API contracts. Do not reinterpret a lab repo as a seventh LMS microservice or fifth owner database.

## 1. Explicit pricing and current usage evidence

Owner submitted GitHub **Billing & licensing → Overview → Actions** product screenshot at `github.com/settings/billing` showing:
- **Plan:** GitHub Free $0.00/month; Copilot Free $0.00/month.
- **Actions billable usage:** `$0` for screenshot-selected current month, with `$1.82 consumed usage - $1.82 discounts`.
- **Included Actions minutes:** `0 min used / 2,000 min included`.
- **Included Actions storage:** `0 GB used / 0.5 GB included`.
- **Top repository gross usage:** LMS-BE $1.22, LMS-FE $0.47, reltroner-hr-app $0.13. **Gross amounts are not actual out-of-pocket charges** when fully discounted.
- **Actions Budgets and alerts settings:** owner screenshot shows the navigation / `Manage budgets` affordance, **not a verified spending cap or hard stop**. Current $0 usage is not proof all future actions or services will have a $0 invoice.

Current official GitHub Docs, independently checked by assistant: **standard GitHub-hosted runners are free and unlimited on PUBLIC repositories**; standard `ubuntu-24.04` label in a public repo has **4 vCPU, 16 GiB RAM and 14 GiB SSD**. **Larger runners are always billed**; storage (artifacts/cache/Packages) and any other paid GitHub products must be separately excluded/reviewed. Therefore **new PUBLIC repo + standard `ubuntu-24.04` + no artifact/cache/package** is a strong design with **expected $0 incremental runner expense**. It is not a guarantee that any unrelated GitHub account use is free. References:
- https://docs.github.com/en/actions/how-tos/write-workflows/choose-where-workflows-run/choose-the-runner-for-a-job
- https://docs.github.com/en/billing/concepts/product-billing/github-actions
- https://docs.github.com/en/actions/tutorials/use-containerized-services/use-docker-service-containers
- https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository
- https://docs.github.com/en/actions/how-tos/manage-workflow-runs/manually-run-a-workflow

## 2. Comparative decision — both monetary cost and engineering productivity

| Option | Additional expected cost | Security / engineering reality | Decision |
|---|---|---|---|
| **Separate PUBLIC blank GitHub lab repo + future standard hosted runner** | **$0 repo / $0 runner** under documented public+standard usage | New scope and synthetic-only; no production secrets; 16GiB ephemeral runner when future authorized | **APPROVED CONDITIONAL: CREATE EMPTY REPO ONLY** |
| Add test workflow to `LMS-BE` repo | $0 standard runner, fewer repos | Existing Phase3B `push` and `pull_request` CI, security/current sources are a bigger blast radius; may accidentally run unrelated CI | Rejected for this security-fault lab |
| Reuse `Reltroner/reltroner-proof` | $0 standard runner, no extra repo | Actually contains Reltroner Studio authorship/ownership evidence; mixing database fault testing would contaminate unrelated intellectual-property proof boundary | Rejected |
| Local Windows Docker Desktop | $0 purchase | Owner OS free RAM **2.73GiB** under project 4GiB review screen; Docker stopped, daemon unverified; would consume workstation resources | **NO-GO** |
| Shared already-bought Hostinger VPS | No added subscription if capacity permits | Existing production-facing services/Keycloak/DB, single vCPU; fault injection risk unacceptable | **NO-GO** |
| Larger hosted runner or new VPS | Paid (unknown rate) | No technical need for initial PostgreSQL18/Redis8 boundary proof | Rejected |

Connected GitHub inventory showed owner account **47 existing repos**, including public `Reltroner/reltroner-proof` (actual README: *Reltroner Studio — Proof of Authorship*, NOT an LMS test repo); no existing `Reltroner/lms-trust-sandbox` repo was returned (404 at check; NOT a reservation/guarantee name is unclaimed in the entire GitHub registry). The connected GitHub action catalogue **does not expose a create-repository action**; it can inspect repositories, but cannot create a new repo. Accordingly there is **NO CLAIM** that the assistant created it. **One user GUI action** is required for this authorized resource creation, not installing GH CLI or handling a personal access token.

## 3. Deterministic E46-F3-A operator GUI creation — exact authorization boundary

**Start:** https://github.com/new

Set these exact fields:
- **Owner:** `Reltroner` personal account, not another organization.
- **Repository name:** `lms-trust-sandbox` (lowercase). If GitHub says unavailable, stop and return exact name availability status; do not choose a different owner or silently suffix.
- **Description (optional):** `Nonproduction synthetic-only security and data-integrity lab for Reltroner LMS. No production data, secrets, or deployments.`
- **Visibility:** `Public`. NEVER `Private` for free-standard public-runner budget assumptions.
- **Template:** None.
- **Add a README file:** OFF / unchecked. Deliberate **empty repository**.
- **Add .gitignore:** None.
- **Choose a license:** None.
- Do not copy a GitHub repository, fork, set credentials/secrets, use Codespaces, or select paid features.
- **Click Create repository once** and wait; return the resulting browser URL and whether GitHub displays the empty-repo Quick setup page.
- **STOP there**. No `README.md`, workflow, branch, first commit, action, runner, image download, database start, billing change or settings edit from this approval.

**Audit evidence after creation:** assistant uses connected GitHub `get_repo` to verify `owner=Reltroner`, `name=lms-trust-sandbox`, `visibility=public`, repository creation and empty/no default-branch-commit state; should not claim absent commits without a successful read or GUI screenshot. A bare empty GitHub repository may not yet have an initial `main` commit; adding a workflow later will require a **separate** approved bootstrap commit.

If connected GitHub App has no access to the newly-created repo (installation restrictions), obtain explicit user-driven GitHub App repo selection/installation update or GUI evidence. Do not inject OAuth tokens or request PAT in chat.

## 4. F3-B and F3-C gates deliberately held

**F3-B:** Review and explicitly authorize creating first non-executable `README` and the exact SHA-reviewed manual workflow on the dedicated lab **default branch**. GitHub `workflow_dispatch` requires the workflow file on default branch. No `push`, `pull_request`, `schedule`, third-party `uses:`, broad token permissions, prod credentials/environments, uploads/cache, public host-mapped DB ports, self-hosted/larger runners, or unverified mutable container tags. Initial engine `postgres:18` / `redis:8` references are *not* immutable until actual digest-verification. Never invent exact hashes. New repo workflow security policy must be separately inspected.

**F3-C:** After F3-B code review and exact image digest + budget verification, owner must separately authorize **first manual `workflow_dispatch`** for a standard `ubuntu-24.04` job; service containers on an internal network use no host port mapping when the job itself runs inside a container. Image pulls use external registries and thus are network traffic; explicitly prohibit **production endpoints, credentials, public test DB ports**, not all outbound networking. Bound 10 minutes, one job, synthetic data, `PG-R01..03` subset first; advanced Postgres WAL restart, replica-promotion/failover, multi-DB grant and load tests need separately reviewed topology and resource limits. Neither F3-B nor F3-C was authorized by the user yet.

## 5. Safe continuation and checkpoint

Do not create a testing repository within `LMS-BE` or `progress-documentation` and do not change inherited Actions policy just to meet this F3 gate. Follow [README §7](./README.md), keep PR #46 open until separate docs archival permission; do not merge source branches or production. Already existing Ed25519 replay **30/30** model and PDO_SQLite real local **8/8** tests remain scoped, with Redis-only **silent selective nonce-loss UNSAFE**. Real PostgreSQL18+Redis8 `PG-R01..10=0/10`; canonical T02-001..086 actual HTTP acceptance `0/86`; D02 owner design, effective Keycloak signed OIDC alg/JWKS, backend/FE code, production **HOLD**.

**Checkpoint:** `E40_WIN30/30_OWNER_PASS -> E45_WIN8/8_OWNER_PASS -> E46_F0S_RAM2.73GIB_LOCAL_DOCKER_NO_GO -> E46_F2_OWNER_ACTIONS_BILLING_$0_SNAPSHOT -> E46_F3_OWNER_APPROVED_CREATE_EMPTY_PUBLIC_REPO_ONLY -> WAIT_HUMAN_GUI_AND_GITHUB_VERIFICATION -> NO_WORKFLOW_NO_RUNNER_NO_CONTAINER -> REAL_PG18_REDIS8_0/10 -> T02_HTTP_0/86 -> DESIGN_RATIFICATION_HOLD -> PRODUCTION_NOT_AUTHORIZED`.
