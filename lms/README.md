# Reltroner LMS — Canonical AI Entry & Engineering State

> **NEW BINDING OWNER WORKSPACE / AI-AGENT RULE — 2026-10-14:** For LMS local work, the **sole approved existing Windows working directory** is `C:\Projects\lms-reltroner-studio`. **Do not create another local Git clone, worktree, parallel checkout, project copy, or checkout folder without new explicit owner approval.** Prefer the already connected **GitHub integration** for remote branch/file/commit/PR/CI work; use PowerShell or an IDE agent only in the designated root, after scope and safety checks. Preserve the owner's `content/` files, external recovery backup and Git stash during all synchronization. **The newer workspace rule in [§16](#16-binding-local-workspace-and-agent-execution-rules-owner-instruction-2026-10-14) supersedes older local-isolation/worktree suggestions in this README for future local operations; it does not cancel frozen technical security contracts or authorize production changes.**

> **LATEST LMS-FE UX D4 STATUS — 2026-10-14 (NEWER THAN OLDER FE SNAPSHOTS BELOW):** [D4 Prototype-to-Canonical UX Integration / AI-to-AI Handoff & Release Evidence](./fe-ux-prototype-d4-handoff-and-release-evidence-20261014.md). LMS-FE [PR #6](https://github.com/Reltroner/LMS-FE/pull/6) is **MERGED**; FE `main=cfc0393740efbb7164f27a31b83c492c8a36fe8d`; [postmerge main CI run 38459777864](https://github.com/Reltroner/LMS-FE/actions/runs/38459777864) **2/2 SUCCESS**. Prototype D4 discovery, source migration, accessibility fixes, preview HTTP tests and security audit already documented: **do not re-run completed discovery without evidence of drift**. Cloudflare production deployment status at this new SHA remains **UNKNOWN / NOT CERTIFIED**; merged commit lacks `[CF-Pages-Skip]` while automatic production deployments were previously enabled, so verify Cloudflare immediately. **This FE UX status overlay does NOT supersede frozen Phase 0C/1 contracts, Phase 4B BE gates or the owner's production authorization.**

> **CURRENT SOURCE STATUS — E36 (2026-10-11):** **LMS-BE PR #12 owner-authorized MERGED**, BE `main=617dadc0d0d627071d713ceb729df6658202b43e`, candidate `598440f50114ce851521e664c62239cbf0658234` reviewed (4/4 files identical after squash); PR and postmerge `main` CI **7/7 successful**. G03 ADR metadata/source-only alignment is **CLOSED**, but live dual assertion, Redis replay/key custody/production remain **NOT CERTIFIED / NOT AUTHORIZED**. Latest detailed [§15](#15-e36--phase-4b-01-g03-source-merge-complete-with-postmerge-ci-2026-10-11), [work order §9](./phase4b-01-g03-adr-status-source-alignment-work-order-20261011.md), [ledger §50](./engineering-end-to-end-progress-ledger.md). Earlier "PR #12 OPEN" text is dated history.

> **LATEST P4B-00 STATUS — 2026-10-11 (E32):** **Phase 4B-00 Windows local preflight PRE01–PRE07 passed within read-only operator scope; next 4B-01 worktree inventory, NOT code/deploy authorization.**
> **LATEST P4B-00 STATUS — 2026-10-11:** **Phase 4A-00 remains CLOSED; Phase 4B-00 local READ-ONLY ENTRY PREFLIGHT is now OWNER-REQUESTED/ACTIVE, with results PENDING operator batch.** [Current Phase 4B-00 work order](./phase4b-00-entry-preflight-isolation-work-order-20261011.md) and [Ledger §44](./engineering-end-to-end-progress-ledger.md) supersede older blanket ‘Phase 4B unauthorized’ text **only for this non-mutating preflight**. Gemini coding, DB/Keycloak/Redis, Cloudflare/DNS, VPS deployment, source merge and production are NOT authorized by this entry instruction. See [§10](#10-phase-4b-00-entry-activation-and-human-operator-handoff-2026-10-11).

> **LATEST CANONICAL STATUS — E31 owner-conditional decision (2026-10-10):** **Phase 4A-00 READ-ONLY DISCOVERY CLOSED WITH ACCEPTED RESIDUAL GAPS; AC18=PASS_OWNER_DISCOVERY_CLOSEOUT_WITH_EXPLICIT_RESIDUALS.** This supersedes only older in-progress/AC18-pending *status* text below. Phase 4A has **8 scoped PASS / 10 unresolved partial, blocked or gap gates**, not 18/18 PASS; all **13 known G01–G13 gaps are discovery-triaged, not fixed**. [Owner acceptance §26](./phase4a-00-read-only-runtime-infrastructure-discovery-work-order-20261010.md#26-e31--phase-4a-00-owner-conditional-final-discovery-acceptance--closed-with-residuals-2026-10-10) · [Ledger §43](./engineering-end-to-end-progress-ledger.md#43-e31--phase-4a-00-final-owner-conditional-discovery-closeout-receipt-2026-10-10). **Phase 4B implementation and production remain NOT AUTHORIZED.**

> **BINDING COMMUNICATION POLICY FOR EVERY RELTRONER LMS AI/ENGINEER CHAT:** Explain all engineering topics with deterministic clarity, accessible to a complete beginner while retaining professional software-engineering accuracy. Always use the mandatory explanatory order in [§7](#7-binding-ai-communication-and-execution-clarity-policy-owner-instruction-2026-10-10). This policy applies to every current and future LMS AI handoff that reads this README, until the owner explicitly changes it. It is a presentation/execution protocol, **not** permission to change frozen architecture, security or production.
> **Latest discovery overlay (2026-10-10, docs PR pending):** [Phase 4A-00 Work Order §§21–25](./phase4a-00-read-only-runtime-infrastructure-discovery-work-order-20261010.md) + [Engineering Ledger §§41–42](./engineering-end-to-end-progress-ledger.md) include E27/E27R/E28/E29 and E30 gap discovery G01–G13. **All 13 gap dispositions are documented; implementation gaps stay OPEN**. AC18 remains **PENDING_OWNER_FINAL**; documentation PR merge and 4B permission are separate owner decisions. Earlier dated 'pending E26' sentences below remain historical and must not override this newer scoped overlay.

> **READ THIS FILE FIRST in every new AI/agent conversation about Reltroner LMS.**  
> **Document role:** authoritative *navigation/current-state overlay*, **NOT a replacement or modification of FROZEN architecture**.  
> **Project owner:** decisions and release authority remain with the human owner.  
> **Reporting date:** 2026-10-10 Asia/Jakarta; source authority comes from actual immutable GitHub commits/checks, not assumed calendar freshness.  
> **Next phase:** **Phase 4A-00 READ-ONLY DISCOVERY OWNER-AUTHORIZED (2026-10-10)**; [read the exact scoped work order](./phase4a-00-read-only-runtime-infrastructure-discovery-work-order-20261010.md). **Phase 4 implementation / provisioning / production NOT AUTHORIZED**. Do not infer runtime certification from Phase 3.

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
| Next | **Phase 4A-00 read-only discovery AUTHORIZED / IN PROGRESS**, with GitHub source preflight PASS; live VPS/Keycloak/PostgreSQL/Redis/Cloudflare evidence pending. Phase 4 implementation, release and final-product DoD remain **NOT AUTHORIZED** |

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

Before writing code or issuing commands: state **phase, work-order ID, authorized scope, immutable base and expected head SHA, file allowlist, negative tests, CI, Cloudflare deployment policy, owner approvals, stop/rollback condition**. IDE agents write only within the existing owner-designated workspace and approved Git branch; ChatGPT may handle bounded GitHub operations via the connected GitHub integration. **Do not create a new local branch worktree/clone/checkout directory without explicit fresh owner approval**; if an older work order requires one, stop for owner reconciliation instead of silently doing it. See [§16](#16-binding-local-workspace-and-agent-execution-rules-owner-instruction-2026-10-14). **Never clean folders or rewrite Git history merely because names appear duplicated.**

**Current work order:** [Phase 4A-00 Read-Only Runtime & Infrastructure Discovery](./phase4a-00-read-only-runtime-infrastructure-discovery-work-order-20261010.md). Owner permission applies only to observation, evidence, and scoped planning; no Phase 4B/production action.

**Historical Phase 3 handoff checkpoint (superseded for CURRENT phase status only):** `PHASE0C/1_FROZEN → PHASE2D_ACCEPTED → PHASE3A_FROZEN → PHASE3B_28_OF_28_OWNER_ACCEPTED → BE_MAIN=a2672d... → FE_MAIN=eb01a4d... → FE_PR4_PR5_MERGED + PUSH_MAIN_CI_GREEN → CLOUDFLARE_PRODUCTION_NEW_SHA_UNVERIFIED → PHASE4_NOT_AUTHORIZED`.

## 5. Complete document inventory: canonical authority vs dated history

**Exactly 57 preexisting lms/ root records indexed here as of docs main `8e2bc1819a5e063dae742940249ebd55312a8510`: 30 Markdown + 27 JSON.** For link stability and preserved Git blobs, none are deleted or moved by this consolidation. Older files are **archival evidence**, not competing current master documents.

### Canonical binding and gate sources (read selectively)

- [**ACTIVE Phase 4A-00 discovery work order**](./phase4a-00-read-only-runtime-infrastructure-discovery-work-order-20261010.md) - source-pinned read-only evidence, gaps, acceptance matrix and operator handoff

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

**Historical cleanup guidance only (not permission to create new trees):** For pre-existing Windows `C:\Projects` test worktrees, verify `git worktree list --porcelain`, `git status --porcelain -uall`, current HEAD and untracked/ignored artifacts **before** any removal. A clone may be a standalone repository rather than a linked worktree: verify which it is. Never infer disposability from screenshots alone. The owner already explicitly approved removal of three old LMS prototype/integration folders; do not generalize that approval. **The binding forward-looking rule is [§16](#16-binding-local-workspace-and-agent-execution-rules-owner-instruction-2026-10-14): one existing local workspace and no new worktrees/clones without fresh approval.**

**Documentation cleanup policy:** prefer one concise living README + append-only ledger + frozen canonical contracts; do not create one status file per thought. Old dated docs/JSON are immutable audit lineage. Reorganization/moving historical files requires a separate complete incoming-link audit because changing paths can break old Markdown, JSON and externally pinned GitHub URLs; do not delete history to make the directory look smaller.

## 7. Binding AI communication and execution clarity policy (owner instruction, 2026-10-10)

> **PERSISTENT MANDATE — for every Reltroner LMS ChatGPT/AI/agent response, handoff, work order, PR review, and technical explanation.** The project owner explicitly requires `clarity-first`, determinism, and explanations understandable by **an absolute beginner while maintaining professional software-engineering precision**. A new AI must read and apply this section on every related conversation. Do not silently drop it after chat migration. This is a documentation-based handoff rule, not a guarantee of another AI's compliance outside the project context.

### 7.1 Mandatory eight-part reasoning/explanation structure

For each meaningful engineering topic, explain in **plain Indonesian first**, with English software terminology defined on first occurrence. Preserve technical identifiers, actual command flags, contracts and SHA exactly. Always identify:

1. **Tujuan / why:** What user/business result we are trying to achieve; give a one-sentence beginner analogy when useful.
2. **Kondisi faktual / evidence:** Exactly what source/file/GUI/CLI shows, including the environment, date, SHA, evidence ID and confidence. Distinguish GitHub source, local laptop, preview, active production and design documents.
3. **Gap / problem:** Precisely what is missing and classify as `NOT_IMPLEMENTED`, `NOT_PROVISIONED`, `NOT_TESTED`, `ACCESS_BLOCKED_BY_SECURITY`, `FAILED_OBSERVED`, `HISTORICAL_DRIFT`, `OWNER_DECISION_PENDING`, or `PROVEN_SCOPED`. These categories are **not interchangeable**.
4. **Alasan penting / consequence:** What could go wrong, affected boundary and blast radius, and why the observation matters. Avoid hypotheticals presented as incidents.
5. **Cara menyelesaikan / solution:** Smallest contract-compliant, deterministic action or bounded decision, prerequisites, dependencies and cheaper/no-cost alternative.
6. **Siapa & tools / ownership:** Human owner approval vs ChatGPT reasoning/GitHub documentation vs Windows PowerShell vs SSH terminal vs Hostinger/Cloudflare/Keycloak GUI vs IDE coding agent. Do not ask beginners to run a code-editing agent for security decisions.
7. **Kapan boleh / authorization:** Phase/subphase, exact work-order ID, what is allowed NOW and NOT AUTHORIZED, frozen boundaries, expected SHA, safety/stop/rollback constraints, and whether the step is read-only, nonproduction or production.
8. **Bukti selesai / verification:** Exact acceptance gate, command or GUI evidence expected, how PASS/PARTIAL/BLOCKED/FAIL should be interpreted, negative tests in safe environments and the **next decision required**. Never call a test PASS from a command that errored part-way through.

For tiny straightforward questions, these eight concepts may be compressed into cohesive paragraphs, but do not omit evidence-vs-inference, authorization or result status when they matter. For complicated workflows, provide an explicit numbered execution plan **before** asking for commands.

### 7.2 Deterministic operator interaction

- **No guessing:** Never invent test results, source SHA, service deployment, identity scope, API availability, budget, DNS/TLS state, RTO/RPO, access, or the owner's decision. If tooling cannot inspect something, label `UNVERIFIED` or `ACCESS_BLOCKED` and state the smallest safe observation that could change it.
- **Beginner-friendly and professionally correct:** Explain `API` (communication interface), `OIDC` (login protocol), `RBAC/capability` (permission boundary), `RPO` (maximum tolerable lost time of data), `RTO` (restoration time objective), `PR` (reviewable code proposal), `CI` (automated checks) and `SHA` (immutable Git object ID) when first used; avoid unexplained acronyms and intimidating walls of commands.
- **One batch when useful:** When the owner requests copy/paste-ready discovery, provide a single safe, idempotent, bounded command block per environment, with exact location of execution, prerequisites, expected summary, redaction rules and failure path. Never say `SSH_EXIT=0` proves all subcommands passed if a pipeline failed. Avoid unnecessary re-probes already denied by HBA/Redis auth.
- **Clear approval boundaries:** Distinguish `DISCOVERY_COMPLETE` from `IMPLEMENTATION_COMPLETE` and `PRODUCTION_CERTIFIED`. A documented risk does not mean it has been remediated. PR creation does not mean merge. Green CI does not mean production release. Never treat the owner's documentation request as automatic approval to provision, purchase, deploy, relax authentication, restore backups or alter frozen contracts.
- **Human-driven GUI:** Specify the exact navigation path and visual fields to capture for Hostinger, Cloudflare and Keycloak; redact account identifiers, URLs containing tokens, credentials and private evidence. Do not require repeated screenshots of previously accepted frozen HRM evidence.
- **Always report progress:** Current phase/subphase, gate outcomes, exact evidence scope and next actionable blocker in each substantial LMS engineering response. Use concise structured tables only when they materially improve clarity.
- **No destructive shortcuts:** No `git reset --hard`, `git clean -fd`, forced pushes, database writes, Redis authentication bypass or production changes merely to produce a green checklist. **The formerly documented three dirty FE entries are a historical snapshot:** by 2026-10-14 the owner had stashed them before synchronizing the designated local workspace; see [§16](#16-binding-local-workspace-and-agent-execution-rules-owner-instruction-2026-10-14) for the preserved stash and content-backup receipt. Never apply, pop, drop or clear that stash automatically.

### 7.3 Canonical example of the required distinction

**G01 — API belum diimplementasikan:** Six Laravel `services/*/routes/api.php` files contain only a PHP opening tag at accepted BE `main` SHA `a2672d...`; Gateway does have separate health endpoints. The **API contract is written**, but **business routes are not implemented in these files**. Phase4A read-only discovery can classify this precisely and create an owner-review implementation package, but cannot silently deploy handlers. Runtime acceptance later requires positive and negative authenticated HTTP tests against the correct service boundaries.

**G04/G05 — DB/cache inspection denied:** PostgreSQL's HBA and Redis's NOAUTH rejected unauthorized catalog/INFO reads. This means **the specific unauthenticated attempts were denied**, not that the database/cache are down, not that access controls are fully secure, and not that four LMS databases exist. Document `ACCESS_BLOCKED_BY_SECURITY` rather than `FAILED_OBSERVED`.

**G13 — admin UI versus independent admin application:** FE `src/app/admin/page.tsx` exists and explicitly warns it is only a frontend UX role gate; operator did not find an independently deployed `lms-admin.reltroner.com` Pages application and DNS cannot resolve it. A source UI route **does not satisfy** separate-admin-host/identity/API capability boundaries. No Keycloak/admin deployment changes under Phase 4A.

## 8. Current gap-discovery navigation / decision status (E30, 2026-10-10)

The full **G01–G13 evidence-to-future-work mapping** is [Work Order §25 E30](./phase4a-00-read-only-runtime-infrastructure-discovery-work-order-20261010.md), with portable dated summary at [Ledger §42](./engineering-end-to-end-progress-ledger.md). It was produced using actual GitHub read-only evidence and owner-provided E01–E28 operator receipts, **without claiming 13 engineering gaps were fixed**.

**Precise checkpoint:** `PHASE0C+1_FROZEN -> PHASE3B_NONPROD_ACCEPTED -> PHASE4A_E29_AUDITED -> E30_ALL_13_GAPS_DISCOVERY_CLASSIFIED -> AC18_OWNER_FINAL_PENDING -> PHASE4B_IMPLEMENTATION_NOT_AUTHORIZED -> PRODUCTION_NOT_AUTHORIZED`.

**Read-only discovery exit decision is separate:** Owner may explicitly accept Phase4A closeout **with open implementation/verification gaps** (that does **not** make AC05/07–10/12–16 PASS), or authorize a narrow further discovery. Owner must separately authorize any Phase4B source implementation, Keycloak clients, PostgreSQL/Redis permissions or data inspection, Cloudflare/DNS/hosting changes, new cost or production operation. The documentation-only GitHub PR must be reviewed/merged under manual governance before its new instructions appear on default-branch README.

## 9. Current Phase 4A-00 owner-conditional closure overlay (E31, 2026-10-10)

**Binding current handoff: `PHASE 4A-00 CLOSED_WITH_ACCEPTED_DISCOVERY_RESIDUALS`, not product readiness.** The owner issued a conditional instruction to merge documentation PR #39 and close Phase4A if reviewing AI could defend that all **known G01–G13** were sufficiently identified; an evidence-scope review determined 13/13 gap IDs individually triaged, with no claim of exhaustive prediction of all possible future issues. [PR #39 merged](https://github.com/Reltroner/progress-documentation/pull/39) into `main` at **`9689575a2f2edc6a24e0dd45dffe75265a1ccf3e`**, containing E27–E30 and README's permanent §7 clarity policy.

**Exact formal closeout classification:** **7 prior scoped PASS (AC01–04, AC06, AC11, AC17) + AC18 owner DISCOVERY closeout PASS = 8 scoped PASS; 10 still NOT PASS (AC05, AC07–10, AC12–16)**. Formal closure means read-only evidence collection and risk classification achieved their bounded purpose; **it does NOT promote source-only CI or design into six running microservices, approve sensitive data access, establish the missing domain hostnames, certify Disaster Recovery, or waive future security acceptance.**

**Carry forward all thirteen residual engineering gaps**, with exact evidence/status/action and assigned decision owners in [Work Order §25 E30](./phase4a-00-read-only-runtime-infrastructure-discovery-work-order-20261010.md#25-e30--complete-g01g13-read-only-source--operator-evidence-reconciliation-2026-10-10), final signed-condition interpretation in [Work Order §26 E31](./phase4a-00-read-only-runtime-infrastructure-discovery-work-order-20261010.md#26-e31--phase-4a-00-owner-conditional-final-discovery-acceptance--closed-with-residuals-2026-10-10), and portable [Ledger §43](./engineering-end-to-end-progress-ledger.md#43-e31--phase-4a-00-final-owner-conditional-discovery-closeout-receipt-2026-10-10). G04/G05 remain `ACCESS_BLOCKED`; G01/G08/G09/G13 contain not-yet-provisioned implementation; G06/G10 are capacity/recovery proof pending; G11 preserves three dirty local FE entries. **No G01–G13 implementation closure was executed in E31.**

**Next:** `LMS-P4B-00-ENTRY-CANDIDATE` **NOT AUTHORIZED**. The next AI must first apply [§7 clarity-first communication contract](#7-binding-ai-communication-and-execution-clarity-policy-owner-instruction-2026-10-10), verify fresh immutable BE/FE/docs pins and current infrastructure facts, and request **separate owner work-order authorization** before source PR implementation, identity/DB/Redis provisioning, DNS/hosting change, backup restore or production release. Do not interpret closing 4A as approval to deploy or spend.

## 10. Phase 4B-00 entry activation and human operator handoff (2026-10-11)

**Owner now explicitly requests to BEGIN PHASE 4B-00**, prioritizing maximal deterministic execution with Windows PowerShell 5.1, Gemini IDE coding prompts, or scoped GUI instructions. The FIRST ACTIVE step is an **unprivileged local Windows read-only preflight and branch-isolation evidence gate**, defined in [LMS-P4B-00-ENTRY-20261011](./phase4b-00-entry-preflight-isolation-work-order-20261011.md). The new Phase 4B starts as **ENTRY_PREFLIGHT_ACTIVE**, not deployed/implementation-complete. This later dated overlay supersedes older 'Phase 4B not authorized' statements **only as to the explicitly authorized 4B-00 preflight**; it does not authorize app code changes, DNS/identity/DB/Redis writes, production operations, purchases, or 4B-01 implementation.

**GitHub baseline read on entry:** `LMS-BE/main=a2672d0085fe84b55520f8f52f41a8c7fc8568a0`, `LMS-FE/main=eb01a4d2c924299b929aebf0f4826b94cf341fc6`, `progress-documentation/main=c9f3498965cd46c452006cc2d02ac0831db4ea26`. Owner-reported earlier local FE main had three dirty entries; preserve unchanged. Required operator handoff report: `P4B00-PRE01..PRE07` source remote pin, local repo identity, BE clean, FE preservation, tool availability, API placeholder inventory, no-mutation report. Never claim PASS before the Windows batch actually runs.

**Next:** after the report, prepare a separately authorized **4B-01** isolated code work order and Gemini IDE implementation prompt constrained to exact file allowlist, contract, negative tests, CI and owner review. **4B-01 CODE/PRODUCTION NOT AUTHORIZED BY THIS ENTRY**. Read §7 deterministic communication instructions on every future chat.

## 11. E32 — Phase 4B-00 read-only operator preflight received and accepted (2026-10-11)

**Current snapshot:** Owner's corrected Windows PowerShell 5.1 entry batch **successfully reported P4B00-PRE01..PRE07 scoped PASS**. Remote pins BE=`a2672d0085fe84b55520f8f52f41a8c7fc8568a0`, FE=`eb01a4d2c924299b929aebf0f4826b94cf341fc6`, docs=`c9f3498965cd46c452006cc2d02ac0831db4ea26` at **2026-10-11T00:14:32+07:00**; this docs pin is historical once current 4B-00 docs PR merges. BE local main clean, two BE worktrees; FE local main older `f2d40417...` with three dirty entries and two FE worktrees — **protect all four existing worktrees and especially FE dirty state**. PHP 8.4.4 / Node 22.23.1 / npm / Composer detected. All six `routes/api.php` files still source skeletons. Earlier Windows PowerShell 5.1 `Tee-Object -Encoding` script defect fixed; report created nonempty, **5,318 bytes**.

**What PASS means:** READY TO **REVIEW 4B-01 ISOLATION**, not direct Gemini code editing, API completion, CI verification, production deployment, DB/Redis/Keycloak login or unverified rollback. The next read-only operator batch should classify preexisting BE/FE worktree paths/branches/status without modifying them. See [4B-00 Work Order §6 E32](./phase4b-00-entry-preflight-isolation-work-order-20261011.md) and [Ledger §45](./engineering-end-to-end-progress-ledger.md). Separate bounded authorization required to create/edit an isolated BE worktree for 4B-01.

**Current state:** `PHASE4A_CLOSED -> PHASE4B00_ENTRY_PRE01-07_PASS_OPERATOR_SCOPED -> 4B01_EXISTING_WORKTREE_INVENTORY_PENDING -> 4B01_IMPLEMENTATION_NOT_YET_AUTHORIZED -> PRODUCTION_NOT_AUTHORIZED`.

## 12. Phase 4B-01 isolated backend workspace & G03 test-aware source remediation proposal (2026-10-11)

**Latest execution handoff:** Phase 4B-00 **PRE01–PRE07 PASS_OPERATOR_SCOPED**; next **`LMS-P4B-01-G03-20261011`** has a bounded work order for (1) a guarded PowerShell 5.1 inventory of **two existing BE and two existing FE worktrees** and creation of **one new isolated BE worktree only after hard checks**, then (2) conditional Gemini IDE source/test-only G03 ADR status reconciliation. No automatic source commit/PR merge, no direct `main` edits, no production operation.

The first G03 source coding issue is **not merely two stale JSON statuses**: Phase3B `validate-identity.php` and `validate-trust-crypto.php` contain tests specifically asserting the old pending statuses. See [4B-01 work order](./phase4b-01-g03-adr-status-source-alignment-work-order-20261011.md) for exact **four-file allowlist**, dual control under frozen ADR, initial local worktree location, test + CI gates, and STOP rules. Never authorize changes outside the four files silently. FE main remains older/dirty with three entries; do not touch it.

**Checkpoint:** `PHASE4A_CLOSED -> 4B00_E32_ENTRY_PASS -> PHASE4B01_LOCAL_ISOLATION_NEXT -> G03_CODING_CONDITIONAL -> SOURCE_MAIN_MERGE_NOT_AUTHORIZED -> PRODUCTION_NOT_AUTHORIZED`.

## 13. Phase 4B-01 E33 — isolated local G03 candidate GREEN; remote patch and CI still pending (2026-10-11)

**Latest owner evidence:** Windows ISO01–ISO04 all PASS at 2026-10-11 00:32 WIB. New isolated BE worktree on `phase4b/01-g03-adr-status-20261011`, original BE base SHA `a2672d0085fe84b55520f8f52f41a8c7fc8568a0`; original FE main still 3 dirty changes **preserved**. Gemini IDE reports exactly four unstaged G03 allowlist files changed; PHP lint and six synthetic contract harnesses **287 PASS / 0 FAIL**, but **no commit/push/PR, no independent diff review and no GitHub Actions run**. Its design-only ADR metadata does not prove real HTTP verifier, Redis replay, production key custody or Keycloak token enforcement.

**Next operator action:** [4B-01 Work Order §6 E33](./phase4b-01-g03-adr-status-source-alignment-work-order-20261011.md): guard-driven local audit, commit only approved four paths to the isolated branch, push non-force and read back exact remote commit SHA, then independent GitHub patch review, PR to `main` and **seven exact-SHA CI jobs**. Existing workflow triggers on PR to `main`; **feature-branch push alone is not a CI PASS**. **No BE source-main merge, FE mutation, VPS/Cloudflare/Keycloak/PG/Redis change or production authorization.**

**Checkpoint:** `4B00_E32_PASS -> 4B01_ISO_PASS -> G03_LOCAL_GREEN_OWNER_REPORTED -> AUDIT_COMMIT_PUSH_NEXT -> PR_CI_PENDING -> MERGE_AND_PRODUCTION_HOLD`.

## 14. E34–E35 — G03 PR #12 exact-head source audit and GitHub CI 7/7 PASS (2026-10-11)

**Current latest source-gate status:** G03 feature commit `598440f50114ce851521e664c62239cbf0658234` (direct BE main child `a2672d0085fe84b55520f8f52f41a8c7fc8568a0`) has **exactly four allowlist changes**, independently compared from GitHub. [LMS-BE PR #12](https://github.com/Reltroner/LMS-BE/pull/12) is OPEN, **not merged**. GitHub Actions [run 38073894387](https://github.com/Reltroner/LMS-BE/actions/runs/38073894387) concluded **success** for all **seven** required jobs (one pure PHP contracts + six independent Laravel services), **all on the same exact head SHA**; GitGuardian separately SUCCESS. Full evidence/negative boundaries at [4B-01 Work Order §§7–8](./phase4b-01-g03-adr-status-source-alignment-work-order-20261011.md) and [Engineering Ledger §§48–49](./engineering-end-to-end-progress-ledger.md).

**What this DOES NOT mean:** G03 has not been merged into BE `main`; the ADR alignment remains source-only design/fixture metadata (runtime `false`), not a real deployed dual-assertion verifier, Keycloak OIDC policy, Redis jti-replay outage handling, signing-key custody or production certificate. **Exact owner authorization to merge LMS-BE PR #12 at SHA `598440f...` remains mandatory**; even a green CI cannot waive the scope, freeze, HRM separation, or production gates.

**Next:** request owner exact-SHA BE PR merge decision. If approved, recheck head, base, 7/7 CI and allowlist before merging and append receipt; all live infrastructure/FE main dirty checkout remain unchanged.

## 15. E36 — Phase 4B-01 G03 source merge complete with postmerge CI (2026-10-11)

**Source-only milestone COMPLETED:** Per owner's explicit approval, [LMS-BE PR #12](https://github.com/Reltroner/LMS-BE/pull/12), candidate `598440f50114ce851521e664c62239cbf0658234`, was merged with exact-head SHA guard using squash. BE `main` now **`617dadc0d0d627071d713ceb729df6658202b43e`**. Four Git blobs on `main` **exactly match** the approved candidate. Premerge [PR CI 38073894387](https://github.com/Reltroner/LMS-BE/actions/runs/38073894387) **7/7 PASS** + GitGuardian PASS; postmerge [main push CI 38074231181](https://github.com/Reltroner/LMS-BE/actions/runs/38074231181) **7/7 PASS** at new SHA. Exact authorization, base, checks, comparison and closure receipt: [Phase4B-01 work order §9 E36](./phase4b-01-g03-adr-status-source-alignment-work-order-20261011.md) and [progress ledger §50](./engineering-end-to-end-progress-ledger.md).

**Distinguish statuses:** `G03_SOURCE_NONPRODUCTION_ADR_STATUS_ALIGNMENT=CLOSED_MERGED_CI_VERIFIED`. This only synchronizes Ed25519/JWS design metadata and test fixtures. `G03_RUNTIME_SIGNATURE_REPLAY_KEY_MANAGEMENT=OPEN_NOT_IMPLEMENTED/NOT_CERTIFIED`; the design retains `runtime_authorized=false`, separate OIDC algorithm decision and owner permission gate. No Keycloak client change, signing keys, Redis/Postgres mutation, VPS deployment, DNS, Cloudflare, HRM, frontend checkout change or production authorization. The local FE `main` still has three known dirty entries as last observed; no newer owner-local audit claimed.

**Next work:** draft a separate precise source/runtime trust work order with secure test environment, owner decision, immutable BE `main` SHA `617dadc...`, gate owners, isolated service boundaries, Keycloak/Redis negative cases, rollback and budget before authorizing implementation. Neither this source merge nor documentation receipt is a license to start live provisioning.

**Checkpoint:** `P4A_CLOSED -> P4B00_E32_PASS -> P4B01_G03_MERGED_AND_MAIN_CI_PASS -> REMAINING_RUNTIME_AND_G01-G13_REVIEW -> PHASE4B_RUNTIME_DEPLOY_NOT_AUTHORIZED`.

## 16. Binding local workspace and agent execution rules (owner instruction, 2026-10-14)

> **PERSISTENT OWNER DIRECTIVE, scoped to all future LMS local work.** This is an operational/agent execution rule and supersedes *older local workspace creation guidance* wherever they conflict. It does **not** amend the six-service boundaries, frozen Phase 0C/1 architecture, Contentlayer/publication policy, Keycloak, API contracts, security/CI gates, or independent production approval.

### 16.1 Exactly one approved local project workspace

- **Sole designated local directory:** `C:\Projects\lms-reltroner-studio`. Use this already-existing repository for any owner-run PowerShell, IDE agent coding or local Git/build operations. Do not assume other paths are interchangeable.
- **Explicit prohibition:** Without a **new, explicit, path-specific owner instruction**, an AI/agent must **NOT** run `git clone`, `git worktree add`, create another local checkout/integration/prototype project directory, copy the repository into a staging folder, or propose parallel Windows working trees as the default solution. A new *remote GitHub branch* is not a new local working tree; still obey exact-SHA review and scope approval.
- **Existing folder cleanup is separate:** Do not auto-delete, move, reset, reinitialize or overwrite *any* local project directory. Past owner authorization to delete named disposable folders does not cover anything else. Never claim an external GitHub connector can inspect or mutate `C:\Projects` directly.
- **When an older engineering work order says to use an isolated worktree:** Report the conflict and request a revised owner-approved approach. Prefer an isolated **remote GitHub branch**, scoped changes through the connector, or a bounded branch workflow **inside the designated project root**, without sacrificing local files. No silent override of mandatory security isolation.
- **Agent responsibility:** IDE coding agents work only on the active workspace and explicit file allowlist; ChatGPT owns reasoning, read-only source/CI/PR evidence, governance and user-facing status. Avoid assigning extra local folders to separate AI agents or inventing permission to edit another repo.

### 16.2 GitHub connector first, local PowerShell only as required

- If the connected GitHub integration can perform an action, use it to inspect source files, SHA/diff, Actions logs, branches, create small commits, update documentation, create PRs and review CI. Verify the remote object after writing. **Do not ask the owner to copy/paste commands that simply duplicate an available, authorized GitHub connector action.**
- If a task depends on local-only files, `localhost`, a Windows program or a Git-ignored asset, state the limitation: GitHub does not grant filesystem access to `C:\Projects`. Provide one minimal, deterministic, guarded, **PowerShell copy-paste-ready** command batch or a narrowly scoped IDE-agent prompt; never claim a local mutation succeeded without owner-provided evidence.
- For each command/edit, declare exact root, current branch/HEAD, target repository, changed-file allowlist, non-goals, validation gate, and whether commit/push/merge/deploy is or is not authorized. No automatic force-push, reset/clean, whole-repository format sweep, lockfile migration, PR merge or Cloudflare deployment to compensate for an unrelated failure.
- **Do not fabricate green checks:** Source compiles ≠ contract tests pass; prototype-only CI ≠ original Phase 3B publication-negative certification; a preview ≠ the live production deployment; a visual login toggle ≠ Keycloak OIDC authentication.

### 16.3 Preserve recovered LMS course content, stash and recovery assets

**Owner-reported completed preservation on 2026-10-14 (local evidence, not a current remote certification):**

- The designated `main` checkout was rebased/fast-forward-synchronized from local `f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7` to observed `origin/main@31aeab6722ce797acd46daa65b57eaa2b155f5d5` (53 commits behind at the time); **rebase succeeded**. Recheck SHA before later Git actions.
- The entire **65-file `content/` tree** was copied to `C:\Users\Reltropolis\AppData\Local\ReltronerBackups\LMS-FE-content-pre-rebase-20261014-064655-d17b07e1\content`, SHA-256 verified against source, then **65/65 files restored and verified** to `C:\Projects\lms-reltroner-studio\content`.
- Preserved stash: `523041d46c986140158c81978cf4a083ae918951` (`stash@{0}` **as observed at that instant**, not a stable index). It includes modified `content/courses/worldbuilding-operating-system/lessons/00-course-orientation.mdx`, the two deleted `docs/auth/*` files and untracked `structure.txt`. Never run `git stash pop`, `stash drop`, `stash clear` or a blanket `stash apply` automatically. Prefer immutable stash SHA over the moving `stash@{0}` index.
- Other local artifacts observed after rebase: untracked `.contentlayer/`, `content/` and local `next-dev-*.log` files. **Untracked does not mean disposable.** Never run `git clean -fd`, `git clean -fdx`, wipe `content/`, or silently add `content/` to a commit. A local content restore is **not** an approved production catalog migration.
- Dependency sync after rebase: source `package.json` / lockfile require Next.js `16.4.0`, React `19.3.0`, React Compiler `1.0.0` and `@tailwindcss/turbopack` `4.3.3`; the earlier `npm run dev` failure ran older Next.js `16.2.6` and missed two packages. A narrowly scoped `npm ci` was proposed, **but its execution result was not provided in the preserved transcript**. Do not claim it passed or repeat it if the owner already shows a working dev server.
- Recovery snapshot and stash are intentionally **retained**. Verify backup existence/hash and real Git status before changes that might impact content, including a new pull/rebase, dependency tooling or applying a stash. Never edit, delete, upload or publish old draft MDX unless a dedicated content-publication work order authorizes it.

### 16.4 Minimal-diff UI/asset tasks and AI-agent prompts

- For narrowly scoped UI requests (e.g. replacing the navbar brand icon), find the **existing** component and target asset first; modify **only** the smallest allowlisted file set. Retain layout/alignment/responsive behavior, auth/router contracts, data/publication semantics, and user-owned `content/`. Do not replace entire app layouts, add demo routes, duplicate components, run `prettier --write .`, or generate placeholders unless specifically requested.
- **Current illustrative logo target (not a global instruction to redesign):** when the owner requests the navbar logo swap, use the existing `public/reltroner-smoth.webp` as web URL `/reltroner-smoth.webp`, keep “Reltroner Learning Academy” text, preserve aspect ratio/accessible alt text and verify desktop/mobile sizing. Do not rename or move the asset.
- Validation for an allowed UI edit: compare before/after paths; check exact file diff; run only needed lint/typecheck/build/smoke checks; report which ran and which were not run. Include changed filenames, summary, styling changes and final diff excerpt. **No commit/push or PR is inferred from a request for a prompt.**

### 16.5 Handoff and acceptance — efficiency without skipping evidence

- First consult this README, [D4 FE UX handoff](./fe-ux-prototype-d4-handoff-and-release-evidence-20261014.md), relevant frozen parent contracts and **latest** dated ledger sections. Older D4 evidence is not a substitute for checking mutable current SHA, but **do not repeat completed discovery or duplicate 42+ commit inventories and prior passing tests absent drift**.
- Operator instructions must be beginner-readable in Indonesian and deterministic: **TUJUAN → FAKTA → GAP → RISIKO → SOLUSI → TOOLS/OWNER → OTORISASI → BUKTI**. Provide exact Windows GUI/PowerShell/IDE agent/GitHub action ownership. If a batch fails, isolate the root cause and continue from the last verified checkpoint instead of rerunning a non-idempotent earlier patch.
- Status categories remain distinct: `BACKED_UP`, `STASHED`, `REBASED`, `RESTORED`, `LOCAL_BUILD_VERIFIED`, `REMOTE_CI_VERIFIED`, `MERGED`, `PRODUCTION_DEPLOYED`, `AUTHENTICATED_E2E_CERTIFIED`. **Never elevate a status without its matching evidence.**
- **No silent project scope conflation:** FE prototype, canonical LMS-FE production source, LMS-BE six-service runtime, independent LMS admin, and Reltroner documentation have distinct boundaries. The owner may explicitly accept a prototyping-only merge, but it does not waive production auth/security, published-only, Cloudflare deploy or rollback verification.

**Effective rule:** One local LMS workspace, no newly created local worktree/clone by AI, use the GitHub connector where possible, protect all 65 locally restored `content/` files plus their backup/stash, execute minimal changes with exact evidence, and do not make a green CI or prototype screenshot stand in for production truth.
