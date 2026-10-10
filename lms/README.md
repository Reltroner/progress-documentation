# Reltroner LMS — Canonical AI Entry & Engineering State

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

Before writing code or issuing commands: state **phase, work-order ID, authorized scope, immutable base and expected head SHA, file allowlist, negative tests, CI, Cloudflare deployment policy, owner approvals, stop/rollback condition**. IDE agent writes code only on isolated branch/worktree; ChatGPT governs source evidence. **Never clean folders or rewrite Git history merely because names appear duplicated.**

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

For Windows `C:\Projects` test worktrees: verify `git worktree list --porcelain`, `git status --porcelain -uall`, current HEAD and untracked/ignored artifacts **before** removal. Primary clones and unmerged/dirty trees are retained. Only explicitly identified, clean, owner-run disposable verification worktrees may be removed with `git worktree remove` **without `--force`**, and never as a side effect of an AI reasoning step. The screenshot alone cannot prove any folder is disposable.

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
- **No destructive shortcuts:** No `git reset --hard`, `git clean -fd`, forced pushes, database writes, Redis authentication bypass or production changes merely to produce a green checklist. Preserve the known three dirty FE entries until separately reviewed.

### 7.3 Canonical example of the required distinction

**G01 — API belum diimplementasikan:** Six Laravel `services/*/routes/api.php` files contain only a PHP opening tag at accepted BE `main` SHA `a2672d...`; Gateway does have separate health endpoints. The **API contract is written**, but **business routes are not implemented in these files**. Phase4A read-only discovery can classify this precisely and create an owner-review implementation package, but cannot silently deploy handlers. Runtime acceptance later requires positive and negative authenticated HTTP tests against the correct service boundaries.

**G04/G05 — DB/cache inspection denied:** PostgreSQL's HBA and Redis's NOAUTH rejected unauthorized catalog/INFO reads. This means **the specific unauthenticated attempts were denied**, not that the database/cache are down, not that access controls are fully secure, and not that four LMS databases exist. Document `ACCESS_BLOCKED_BY_SECURITY` rather than `FAILED_OBSERVED`.

**G13 — admin UI versus independent admin application:** FE `src/app/admin/page.tsx` exists and explicitly warns it is only a frontend UX role gate; operator did not find an independently deployed `lms-admin.reltroner.com` Pages application and DNS cannot resolve it. A source UI route **does not satisfy** separate-admin-host/identity/API capability boundaries. No Keycloak/admin deployment changes under Phase 4A.

## 8. Current gap-discovery navigation / decision status (E30, 2026-10-10)

The full **G01–G13 evidence-to-future-work mapping** is [Work Order §25 E30](./phase4a-00-read-only-runtime-infrastructure-discovery-work-order-20261010.md), with portable dated summary at [Ledger §42](./engineering-end-to-end-progress-ledger.md). It was produced using actual GitHub read-only evidence and owner-provided E01–E28 operator receipts, **without claiming 13 engineering gaps were fixed**.

**Precise checkpoint:** `PHASE0C+1_FROZEN -> PHASE3B_NONPROD_ACCEPTED -> PHASE4A_E29_AUDITED -> E30_ALL_13_GAPS_DISCOVERY_CLASSIFIED -> AC18_OWNER_FINAL_PENDING -> PHASE4B_IMPLEMENTATION_NOT_AUTHORIZED -> PRODUCTION_NOT_AUTHORIZED`.

**Read-only discovery exit decision is separate:** Owner may explicitly accept Phase4A closeout **with open implementation/verification gaps** (that does **not** make AC05/07–10/12–16 PASS), or authorize a narrow further discovery. Owner must separately authorize any Phase4B source implementation, Keycloak clients, PostgreSQL/Redis permissions or data inspection, Cloudflare/DNS/hosting changes, new cost or production operation. The documentation-only GitHub PR must be reviewed/merged under manual governance before its new instructions appear on default-branch README.
