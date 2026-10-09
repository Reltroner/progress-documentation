# Reltroner LMS — Canonical AI Entry & Engineering State

> **READ THIS FILE FIRST in every new AI/agent conversation about Reltroner LMS.**  
> **Document role:** authoritative *navigation/current-state overlay*, **NOT a replacement or modification of FROZEN architecture**.  
> **Project owner:** decisions and release authority remain with the human owner.  
> **Reporting date:** 2026-10-10 Asia/Jakarta; source authority comes from actual immutable GitHub commits/checks, not assumed calendar freshness.  
> **Next phase:** **Phase 4 NOT AUTHORIZED**. Do not run live probing/mutations or introduce infrastructure until an independently approved scoped work order.

## 1. Operational snapshot — exact verified GitHub states

| Item | Live checkpoint / boundary |
|---|---|
| Phase 0C physical / Phase 1 logical contracts | **FROZEN** — 20 physical and 24 logical normative invariant IDs |
| Phase 2D six Laravel-service foundation | **ACCEPTED / FROZEN** within its stated source/local scope |
| Phase 3A | **DESIGN FROZEN** — FZ-11 owner accepted and merged |
| Phase 3B | **CLOSED / OWNER-ACCEPTED** within NONPRODUCTION design/contract/source/CI scope, B3-AC01..28 = **28/28 accepted** (27 scoped including owner waiver; one trace-only) |
| Invariants | **44/44 traceable**, **0 newly live/runtime-certified** by Phase 3 |
| LMS-BE `main` | `a2672d0085fe84b55520f8f52f41a8c7fc8568a0` — accepted Phase 3 backend; [postmerge CI 7/7](https://github.com/Reltroner/LMS-BE/actions/runs/37970800113) |
| LMS-FE `main` | `eb01a4d2c924299b929aebf0f4826b94cf341fc6` — accepted Phase3 source + [PR #4](https://github.com/Reltroner/LMS-FE/pull/4) Windows LF staging + [PR #5](https://github.com/Reltroner/LMS-FE/pull/5) CLI exit-status fix |
| Latest FE postmerge CI | [push-main run 37987959614](https://github.com/Reltroner/LMS-FE/actions/runs/37987959614): **2/2 SUCCESS**, 19/19 catalog/regression tests, 3 published Contentlayer docs, 25/25 static pages, publication privacy PASS, **no ERR_INVALID_ARG_TYPE** in build logs |
| PR #5 operator Windows evidence | Owner-supplied PowerShell 5.1 isolated worktree at PR `5f2ac1f4383dfd2fe8a09ce4a33294d73cd71083`: 19/19 PASS, build 25/25, clean CLI, negative missing-staging test exit **1**. Windows main merge SHA itself has not been independently run on the user's laptop |
| Cloudflare | Merge `eb01a4d2...` title **starts `[CF-Pages-Skip]`**. **Production-main deployment exclusion at this new SHA NOT YET independently verified in Cloudflare account**; prior owner UI evidenced a `skipped` **Preview** entry, not a production-main receipt. **No release or DNS/Cloudflare mutation is authorized** |
| Governance | Both app `main` branch APIs report `protected:false`. [GOV-WVR-001](./gov-wvr-001-phase3b-branch-protection-owner-exception-20261010.md) is a Phase-3 technical-branch-rule waiver, **not** proof of enforcement; [BRANCH-GOV-001](./branch-gov-001-main-branch-contractual-protection-20261010.md) manual discipline still binds every later source change |
| Next | **Source maintenance complete; Phase 3 frozen.** Phase 4 read-only planning/approval must be distinct; runtime integration, Keycloak secrets, database roles, Redis replay fault tests, VPN/SSH, deployment and final-product DoD have **NOT** been accepted by Phase 3 |

If these pins become stale, **STOP, re-read GitHub live** `main` HEADs/CI and append a dated update. Do not silently change frozen contracts or overwrite historical acceptance counts.

## 2. Source-of-truth precedence — conflict resolution

1. **Immutable normative architecture:** [Phase 0C Master Infrastructure Placement](./master-infrastructure-placement-contract.md) 20 `I-01..I-20` + [Phase 1 Logical/API Boundary](./logical-service-boundary-api-contract.md) 24 `P1-I01..P1-I24`. These define hostnames, six service owners, DB separation, identity/privacy and placement. They are not superseded by this README, ledger, source implementation or a newer discussion.
2. **Ratified bounded design:** [FZ-11 final freeze](./reltroner-lms-phase3a-fz11-final-design-freeze-acceptance-20261009.md), [FZ-10 28-gate scope](./reltroner-lms-phase3a-04-fz10-phase3b-entry-exit-authorization-20261009.md), and [ADR-LMS-TRUST-001](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md). Ed25519/JWS signing/replay is approved **as nonproduction design**, **not live credentials or a successful runtime test**.
3. **Governance exceptions/owner acceptance:** [BRANCH-GOV-001](./branch-gov-001-main-branch-contractual-protection-20261010.md), [GOV-WVR-001](./gov-wvr-001-phase3b-branch-protection-owner-exception-20261010.md), and [Phase 3B-11 final owner acceptance](./reltroner-lms-phase3b-11-final-owner-exit-acceptance-20261010.md). Later owner-approved **scoped** decisions supersede only the named older gate dispositions; no blanket rewrite.
4. **Living execution truth:** [Append-only End-to-End Ledger](./engineering-end-to-end-progress-ledger.md) **read newest numbered section first**, then earlier sections only as dated history. Source repos, actual commit trees, GitHub Actions raw logs, and owner-supplied Cloudflare UI carry their *stated observation scope*; never substitute a PR green check for production certification.
5. **Historical evidence:** all `*.candidate*`, `*.partial*`, dated Phase 3A/3B markdown and JSON audit snapshots below are **retained for traceability**, not automatically current permissions, architecture or approval. A historical `BLOCKED` table does not override a later owner acceptance; a later status overlay cannot override the frozen contract without versioned ADR and owner decision.

**Conflict algorithm for any AI:** identify the precise claim and phase timestamp → locate normative contract/owner-approved ADR → read latest dated acceptance **and its limitations** → verify actual repo SHA/CI → classify `PROVEN / PROPOSED / HISTORICAL / DEFERRED / UNVERIFIED` → STOP/ask owner for any new authority. **Never promise 100% factual correctness without source verification.**

## 3. Frozen compact topology (navigation, not new contract)

- Six separate Laravel 13 services in one BE source repo: **Gateway (only public API ingress), Learning, Mentorship, Knowledge, Assistant, Audit**. Five non-Gateway business services remain private; this is microservice architecture, **not a modular monolith**.
- Canonical authentication: Keycloak issuer `auth.reltroner.com/realms/reltroner`, separate learner/admin clients, API audience `lms-api`, server-side capabilities and principal ownership. Avoid forwarding unverifiable principal headers.
- **26** frozen public API method+path operations; **19** frozen capabilities; **9** named events; **4** owned PostgreSQL domain DBs. PostgreSQL is durable business truth; Redis replaceable operational state, never canonical business truth.
- Published LMS course content stays **Git-owned** under its catalog allowlist; draft/archived MDX must not enter public bundles. Cloudflare Pages delivers static FE; Premium Hosting is versioned public asset origin; VPS is not a local LLM inference target without new accepted placement.
- Critical Phase 4 runtime deferred gates: OIDC audience/JWKS/client/HRM nonregression; Ed25519 workload + delegation real keys, request/recipient/capability proof, TTL/skew/replay/Redis-loss fail closed; private service exposure; PG ownership/GRANT; event durability; Cloudflare / TLS + VPS capacity evidence. **Read-only inventory first; no mutations until separate authorization.**

## 4. Minimal AI handoff protocol — do not confuse status and scope

**Read in this order (context-efficient):** this README → both frozen parent contracts, focusing on the section relevant to the proposed operation → owner ADR/waiver if relevant → Phase 3B-11 exit → **latest two ledger sections** → exact BE/FE `main` GitHub SHA and check-runs → only then a scoped phase work order. For a new AI, copy the checkpoint and links, not every historical 57-document body.

Before writing code or issuing commands: state **phase, work-order ID, authorized scope, immutable base and expected head SHA, file allowlist, negative tests, CI, Cloudflare deployment policy, owner approvals, stop/rollback condition**. IDE agent writes code only on isolated branch/worktree; ChatGPT governs source evidence. **Never clean folders or rewrite Git history merely because names appear duplicated.**

**Present checkpoint:** `PHASE0C/1_FROZEN → PHASE2D_ACCEPTED → PHASE3A_FROZEN → PHASE3B_28_OF_28_OWNER_ACCEPTED → BE_MAIN=a2672d... → FE_MAIN=eb01a4d... → FE_PR4_PR5_MERGED + PUSH_MAIN_CI_GREEN → CLOUDFLARE_PRODUCTION_NEW_SHA_UNVERIFIED → PHASE4_NOT_AUTHORIZED`.

## 5. Complete document inventory: canonical authority vs dated history

**Exactly 57 preexisting lms/ root records indexed here as of docs main `8e2bc1819a5e063dae742940249ebd55312a8510`: 30 Markdown + 27 JSON.** For link stability and preserved Git blobs, none are deleted or moved by this consolidation. Older files are **archival evidence**, not competing current master documents.

### Canonical binding and gate sources (read selectively)

- [`master-infrastructure-placement-contract.md`](./master-infrastructure-placement-contract.md)
- [`logical-service-boundary-api-contract.md`](./logical-service-boundary-api-contract.md)
- [`reltroner-lms-phase3a-fz11-final-design-freeze-acceptance-20261009.md`](./reltroner-lms-phase3a-fz11-final-design-freeze-acceptance-20261009.md)
- [`reltroner-lms-phase3a-04-fz10-phase3b-entry-exit-authorization-20261009.md`](./reltroner-lms-phase3a-04-fz10-phase3b-entry-exit-authorization-20261009.md)
- [`reltroner-lms-phase3a-04-fz02-cross-contract-invariant-traceability-20261009.md`](./reltroner-lms-phase3a-04-fz02-cross-contract-invariant-traceability-20261009.md)
- [`reltroner-lms-phase3b-11-final-owner-exit-acceptance-20261010.md`](./reltroner-lms-phase3b-11-final-owner-exit-acceptance-20261010.md)
- [`adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md`](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md)
- [`branch-gov-001-main-branch-contractual-protection-20261010.md`](./branch-gov-001-main-branch-contractual-protection-20261010.md)
- [`gov-wvr-001-phase3b-branch-protection-owner-exception-20261010.md`](./gov-wvr-001-phase3b-branch-protection-owner-exception-20261010.md)
- [`engineering-end-to-end-progress-ledger.md`](./engineering-end-to-end-progress-ledger.md)
- [`reltroner-lms-phase3b-11-final-28-gate-exit-acceptance-20261010.json`](./reltroner-lms-phase3b-11-final-28-gate-exit-acceptance-20261010.json)
- [`reltroner-lms-phase3b-07r-invariant-44-crosswalk-20261009.json`](./reltroner-lms-phase3b-07r-invariant-44-crosswalk-20261009.json)

### Historical dated evidence (collapse when browsing)

<details>
<summary><strong>Early architecture / ADR exploration</strong> — 8 preserved records</summary>

- [`adr-lms-kc-001-identity-provisioning-review-candidate.md`](./adr-lms-kc-001-identity-provisioning-review-candidate.md)
- [`reltroner-lms-catalog-manifest-v1.candidate.schema.json`](./reltroner-lms-catalog-manifest-v1.candidate.schema.json)
- [`reltroner-lms-catalog-manifest-v1.partial-example.json`](./reltroner-lms-catalog-manifest-v1.partial-example.json)
- [`reltroner-lms-phase3a-03c-2d-provisioning-adr-review-20261009.md`](./reltroner-lms-phase3a-03c-2d-provisioning-adr-review-20261009.md)
- [`reltroner-lms-phase3a-03d-persistence-event-model-20261009.md`](./reltroner-lms-phase3a-03d-persistence-event-model-20261009.md)
- [`reltroner-lms-phase3a-03e-catalog-manifest-versioning-20261009.md`](./reltroner-lms-phase3a-03e-catalog-manifest-versioning-20261009.md)
- [`reltroner-lms-phase3a-03f-cross-contract-business-reconciliation-20261009.md`](./reltroner-lms-phase3a-03f-cross-contract-business-reconciliation-20261009.md)
- [`reltroner-lms-phase3a-03f-decision-register-20261009.json`](./reltroner-lms-phase3a-03f-decision-register-20261009.json)

</details>

<details>
<summary><strong>Phase 3A freeze and design evidence</strong> — 8 preserved records</summary>

- [`reltroner-lms-phase3a-04-fz02-invariant-traceability-20261009.json`](./reltroner-lms-phase3a-04-fz02-invariant-traceability-20261009.json)
- [`reltroner-lms-phase3a-04-fz04-subordinate-adr-closure-20261009.md`](./reltroner-lms-phase3a-04-fz04-subordinate-adr-closure-20261009.md)
- [`reltroner-lms-phase3a-04-fz04-subordinate-adr-dispositions-20261009.json`](./reltroner-lms-phase3a-04-fz04-subordinate-adr-dispositions-20261009.json)
- [`reltroner-lms-phase3a-04-ratification-freeze-readiness-20261009.md`](./reltroner-lms-phase3a-04-ratification-freeze-readiness-20261009.md)
- [`reltroner-lms-phase3a-04-ratification-register-20261009.json`](./reltroner-lms-phase3a-04-ratification-register-20261009.json)
- [`reltroner-lms-phase3a-fz11-final-freeze-manifest-20261009.json`](./reltroner-lms-phase3a-fz11-final-freeze-manifest-20261009.json)
- [`reltroner-lms-phase3a-fz11-postmerge-activation-20261009.json`](./reltroner-lms-phase3a-fz11-postmerge-activation-20261009.json)
- [`reltroner-lms-phase3a-fz11-postmerge-activation-20261009.md`](./reltroner-lms-phase3a-fz11-postmerge-activation-20261009.md)

</details>

<details>
<summary><strong>Phase 3B candidate engineering and CI</strong> — 12 preserved records</summary>

- [`reltroner-lms-phase3a-04-fz10-phase3b-work-order-20261009.json`](./reltroner-lms-phase3a-04-fz10-phase3b-work-order-20261009.json)
- [`reltroner-lms-phase3b-00-local-git-ci-preflight-acceptance-20261009.md`](./reltroner-lms-phase3b-00-local-git-ci-preflight-acceptance-20261009.md)
- [`reltroner-lms-phase3b-00-preflight-acceptance-20261009.json`](./reltroner-lms-phase3b-00-preflight-acceptance-20261009.json)
- [`reltroner-lms-phase3b-01-local-php-validation-evidence-20261009.json`](./reltroner-lms-phase3b-01-local-php-validation-evidence-20261009.json)
- [`reltroner-lms-phase3b-01-local-php-validation-evidence-20261009.md`](./reltroner-lms-phase3b-01-local-php-validation-evidence-20261009.md)
- [`reltroner-lms-phase3b-01-openapi-contract-candidate-20261009.json`](./reltroner-lms-phase3b-01-openapi-contract-candidate-20261009.json)
- [`reltroner-lms-phase3b-01-openapi-contract-candidate-20261009.md`](./reltroner-lms-phase3b-01-openapi-contract-candidate-20261009.md)
- [`reltroner-lms-phase3b-02-to-06-staged-engineering-20261009.json`](./reltroner-lms-phase3b-02-to-06-staged-engineering-20261009.json)
- [`reltroner-lms-phase3b-02-to-06-staged-engineering-20261009.md`](./reltroner-lms-phase3b-02-to-06-staged-engineering-20261009.md)
- [`reltroner-lms-phase3b-central-candidate-owner-approval-20261009.json`](./reltroner-lms-phase3b-central-candidate-owner-approval-20261009.json)
- [`reltroner-lms-phase3b-central-dev-topology-20261009.json`](./reltroner-lms-phase3b-central-dev-topology-20261009.json)
- [`reltroner-lms-phase3b-central-dev-topology-20261009.md`](./reltroner-lms-phase3b-central-dev-topology-20261009.md)

</details>

<details>
<summary><strong>Phase 3B revalidation / owner decisions</strong> — 11 preserved records</summary>

- [`reltroner-lms-phase3b-07-44-invariant-evidence-crosswalk-20261009.json`](./reltroner-lms-phase3b-07-44-invariant-evidence-crosswalk-20261009.json)
- [`reltroner-lms-phase3b-07-acceptance-28-gate-audit-20261009.json`](./reltroner-lms-phase3b-07-acceptance-28-gate-audit-20261009.json)
- [`reltroner-lms-phase3b-07-holistic-end-to-end-audit-20261009.md`](./reltroner-lms-phase3b-07-holistic-end-to-end-audit-20261009.md)
- [`reltroner-lms-phase3b-07-risk-remediation-register-20261009.json`](./reltroner-lms-phase3b-07-risk-remediation-register-20261009.json)
- [`reltroner-lms-phase3b-07r-acceptance-revalidation-20261009.json`](./reltroner-lms-phase3b-07r-acceptance-revalidation-20261009.json)
- [`reltroner-lms-phase3b-07r-remediation-and-revalidation-20261009.md`](./reltroner-lms-phase3b-07r-remediation-and-revalidation-20261009.md)
- [`reltroner-lms-phase3b-07r-risk-revalidation-20261009.json`](./reltroner-lms-phase3b-07r-risk-revalidation-20261009.json)
- [`reltroner-lms-phase3b-08-governance-decision-register-20261010.json`](./reltroner-lms-phase3b-08-governance-decision-register-20261010.json)
- [`reltroner-lms-phase3b-08-security-and-final-merge-governance-20261010.md`](./reltroner-lms-phase3b-08-security-and-final-merge-governance-20261010.md)
- [`reltroner-lms-phase3b-10-ac07-ac25-formal-revalidation-20261010.md`](./reltroner-lms-phase3b-10-ac07-ac25-formal-revalidation-20261010.md)
- [`reltroner-lms-phase3b-10-acceptance-28-governance-revalidation-20261010.json`](./reltroner-lms-phase3b-10-acceptance-28-governance-revalidation-20261010.json)

</details>

<details>
<summary><strong>Post-source integration / operator receipts</strong> — 6 preserved records</summary>

- [`reltroner-lms-phase3-holistic-source-merge-hold-20261009.json`](./reltroner-lms-phase3-holistic-source-merge-hold-20261009.json)
- [`reltroner-lms-phase3-holistic-source-merge-hold-20261009.md`](./reltroner-lms-phase3-holistic-source-merge-hold-20261009.md)
- [`reltroner-lms-phase3-local-windows-isolation-evidence-20261010.json`](./reltroner-lms-phase3-local-windows-isolation-evidence-20261010.json)
- [`reltroner-lms-phase3-local-windows-powershell-isolation-receipt-20261010.md`](./reltroner-lms-phase3-local-windows-powershell-isolation-receipt-20261010.md)
- [`reltroner-lms-phase3-main-integration-postmerge-ci-20261010.json`](./reltroner-lms-phase3-main-integration-postmerge-ci-20261010.json)
- [`reltroner-lms-phase3b-main-merge-and-postmerge-ci-20261010.md`](./reltroner-lms-phase3b-main-merge-and-postmerge-ci-20261010.md)

</details>

## 6. Repository/folder hygiene policy

For Windows `C:\Projects` test worktrees: verify `git worktree list --porcelain`, `git status --porcelain -uall`, current HEAD and untracked/ignored artifacts **before** removal. Primary clones and unmerged/dirty trees are retained. Only explicitly identified, clean, owner-run disposable verification worktrees may be removed with `git worktree remove` **without `--force`**, and never as a side effect of an AI reasoning step. The screenshot alone cannot prove any folder is disposable.

**Documentation cleanup policy:** prefer one concise living README + append-only ledger + frozen canonical contracts; do not create one status file per thought. Old dated docs/JSON are immutable audit lineage. Reorganization/moving historical files requires a separate complete incoming-link audit because changing paths can break old Markdown, JSON and externally pinned GitHub URLs; do not delete history to make the directory look smaller.
