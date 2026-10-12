# reltroner.com — Phase 1 Frontend Production Readiness

> **CURRENT OWNER REFINEMENT — 2026-10-13:** [RC-WEB-ADR-009](./09-owner-approved-pathway-and-portfolio-landing-refinement-20261013.md) requires Use-Case Pathways Creator → `/start/creators`, Reader → `/start/readers`, plus **Selected Work & Practice** inserted between Roadmap Preview and the final CTA with verified Git-resource `direktori-listing.webp` and `rei-kelas-digi.webp`. Style reference Skill-Wanderer image-first portfolio; maintain Reltroner navy/blue and avoid unverified paid-client claims. Local exact scoped RC-W1-21 patch and updated RC-W1-22 **six-path validator are prepared but NOT yet owner-executed**; remote Studio main unchanged in last check. Older W1-19 PASS still applies only to its earlier five-file source snapshot; do not execute stale RC-W1-20 after RC-W1-21. Core 18 invariants, 27 WEB-AC, Rp0 and protected drafts remain binding.


> **NEW OWNER RATIFICATION — 2026-10-13:** [RC-WEB-ADR-008: owner-directed W0–W9 execution authority and dedicated TSX Creator/Reader onboarding](./08-owner-execution-authority-and-dedicated-creator-reader-tsx-adr-20261013.md). The homepage blue CTAs must go to **`/start/creators`** and **`/start/readers`** (`app/start/*/page.tsx`), not directly to existing `/blog/*.md`-derived article routes. A self-contained guarded implementation script has been prepared for the isolated Windows W1 worktree, but its execution/build/QA is **PENDING**. Prior 3-file G3 packet requires 5-file scope refresh. Original 18 invariants, 27 WEB-AC and zero-additional-cost remain unchanged. RC-W1-18 operator report provides correlated Chrome CDP viewport measurements `PASS_SCOPED`, but no new ZIP was attached for independent screenshot-byte review. Older lines below are historical, not an instruction to hold clearly owner-ordered local work.


> **CURRENT EXECUTION BULLETIN — 2026-10-12 (supersedes the historical status header below):** G1 W0 owner-approved CLOSED_WITH_RESIDUALS; G2 W1 source/local build PASS_SCOPED (three isolated TSX patches; `next-env.d.ts` restored); browser QA agent PASS_SCOPED **but direct PNG review RC-W1-17 found 320/375/768 screenshot-viewport evidence conflicts and invalid WebP recording**. W1-IA07 PARTIAL pending [RC-W1-18 targeted one-shot recapture](./progress-engineering-canonical/RC-W1-18-targeted-viewport-correlation-and-evidence-closure-work-order-20261012.md). [RC-G3-00 separate PR decision packet](./progress-engineering-canonical/RC-G3-00-separate-w1-source-pr-decision-packet-pending-owner-20261012.md) is prepared, **NOT OWNER-APPROVED**. W2 index/search, W3 CDN, W4 privacy, W5 AI, W6 email/contact, W7 integration have detailed proposed contracts/research but **NOT source-implemented**. W3 broken image, W4 GA preconsent, W5 Workers AI entitlement, W6 Resend DNS remain unresolved. **G3–G8 HOLD; 27 WEB-AC mandatory; website/global Phase 1 NOT ACCEPTED; Phase 2 NOT ACTIVE.** Read the [current operational status index](./07-current-execution-status-and-next-gates-20261012.md) rather than treating earlier prose or historic receipts as live permission.


> Status: OWNER-RATIFIED REQUIREMENTS / G1 W0 DISCOVERY CLOSED WITH RESIDUALS / G2 W1 OWNER APPROVED / PROVISIONING PENDING.
> Ratification date: 2026-10-12 Asia/Jakarta (owner in conversation).
> Product: https://www.reltroner.com/ ; code: https://github.com/Reltroner/reltroner-studio
> Documentation repository: https://github.com/Reltroner/progress-documentation
> Current operating mode: PHASE_1_NOT_YET_ACCEPTED; Phase 2 NOT ACTIVE.
> Cash boundary: Rp0 INCREMENTAL SPENDING; NO upgrade/subscription/automatic overage.
> Always recheck live HEADs and provider entitlements before operating. This README is the *living entry register*, not a production acceptance certificate.

## 1. Read this first — authority and order

1. [Ratified strategy 05](../all-in-reltroner-master-source-of-truth/05-phase1-phase2-exit-entry-and-reentry.md): global Phase 1 exit / Phase 2 entry.
2. [Ratified website intention 11](../all-in-reltroner-master-source-of-truth/11-reltroner-com-landing-and-ux-journeys.md): outcome and audience journey.
3. [00 — Frontend architecture contract](./00-ratified-frontend-architecture-contract-20261012.md): binding website scope/invariants, not LMS authority.
4. [01 — Live engineering ledger](./01-engineering-progress-ledger.md): evidence, known gaps, current gate.
5. [02 — W0 discovery work order](./02-w0-00-read-only-discovery-work-order-20261012.md): historical authorized read-only evidence protocol; **G1 formally closed** in [RC-W0-10](./progress-engineering-canonical/RC-W0-10-owner-g1-ratification-and-discovery-closure-20261012.md).
6. [03 — Traceability / acceptance](./03-phase1-acceptance-and-invariant-traceability.md): proposed measurable acceptance, gate-by-gate.
7. [04 — Cost, privacy and provider boundaries](./04-zero-incremental-spend-and-provider-boundaries.md).
8. [05 — Git workspace / release governance](./05-source-workspace-and-release-governance.md).
9. [06 — TS/TSX content and component design](./06-frontend-component-and-content-architecture.md).
10. [Canonical engineering progress archive](./progress-engineering-canonical/README.md): W0 dated evidence and future workstream receipts (documentation-only).

External authoritative sources: [Studio Master](https://github.com/Reltroner/reltroner-studio/blob/main/content/principles/reltroner-studio-master-source-of-truth.md), [LMS README](../lms/README.md), [LMS frozen placement](../lms/master-infrastructure-placement-contract.md) and [LMS frozen API](../lms/logical-service-boundary-api-contract.md). LMS governance methodology is reused; **its service topology is not transplanted into the website**.

## 2. Current snapshot (2026-10-12, GitHub checked at documentation entry)

| Source | Snapshot | Evidence class |
|---|---|---|
| progress-documentation main before ratification write | 73c24bcf0210b533020823c2d32680a2fea7eecb | GIT-VERIFIED |
| reltroner-studio main | 18b295f96ccb521b228a1855e79448158c09db15 | GIT-VERIFIED |
| reltroner-studio-resource main | 6c6fb38f8ff3376c0789c15bcfe4d0cafc4d057e | GIT-VERIFIED |
| Local reltroner-studio Windows main | user reported up to date, 14 untracked Markdown documents | OWNER-REPORTED, NOT independently inspected |
| Existing Vercel Hobby domains/UI | screenshots show www production and root redirect | OWNER-SUPPLIED UI SNAPSHOT, not live billing/capacity proof |

Re-read refs before writing; frozen snapshot strings must never be mistaken for perpetually current branch tips.

## 3. Project phase state

| Gate | Status | What it means |
|---|---|---|
| Owner scope ratification | RATIFIED | Design outcomes and no-spend boundary approved; this documentation records that decision |
| W0-00 discovery (G1) | **CLOSED_WITH_ACCEPTED_RESIDUALS / OWNER_APPROVED** | W0-AC12 owner signoff recorded in RC-W0-10; other ACs retain original PARTIAL/BLOCKED statuses |
| W1 G2 work order | **OWNER APPROVED / NOT YET EXECUTION-VERIFIED** | [RC-W1-01](./progress-engineering-canonical/RC-W1-01-proposed-g2-first-contact-creator-reader-ia-work-order-20261012.md): three TSX files and safe read-only preflight, separately approved G2 required |
| Integrated preview | NOT EXECUTED | Cannot report PASS |
| Production readiness | NOT CERTIFIED | User has not accepted final release |
| Global Phase 1 exit | NOT ACCEPTED | Requires independent LMS final DoD and operations gates |
| Phase 2 community activation | NOT ACTIVE | Requires final founder approval |

## 4. Required Phase 1 website outcomes

- Identity and first-contact discovery: two prominent *creator* and *reader* entrances; collaborator/real-world engineering is a distinct secondary experience; no false service or canon claims.
- Epistemic classification: fiction canon, speculative fiction, real-world analysis, creative framework, engineering proof and explicit cross-domain analogies.
- Context-sensitive left reading-path and right archive-explorer rails on wide viewports, responsive drawers on small viewports; unified Ctrl+K/search behavior.
- CDN image delivery: detect failures, immutable resource commit addressing, automatically surface modified bytes *without filename changes* after resource pushes, verify rendered update.
- Global Reltroner Navigator: original brand, accessible launcher, real contextual AI explanation on approved public knowledge **within verified zero-cost envelope**, deterministic navigation fallback, citations, no privileged tools.
- Essential-cookie/privacy transparency aligned with actual analytics and third-party behavior; no inaccurate 'no tracking' claim.
- Resend newsletter: permission-based subscription, server-side API key, subscriber status/duplicate handling, unsubscribe and honest acceptance feedback.
- Web3Forms contact: intent-based pathways (collaboration, creative, learning), manual asynchronous follow-up, spam mitigation, privacy disclosure and alternative contact.
- TypeScript/TSX-first and frontend-first. Bounded serverless/edge integrations are permitted where required to protect vendor credentials; not a new LMS/ERP/backend monolith.
- Zero incremental spending, measurable nonfunctional and operational acceptance, source isolation and known-good rollback.

## 5. Scope guardrail

W0 was executed as **OBSERVE → EVIDENCE → GAP → DECISION** and G1 is now owner-approved, with residuals deferred as mandatory later work. The next activity is **W1 G2 decision preparation**, not implementation until separate owner authorization. No new provider purchase, DNS change, paid plan, Vercel purge, live API activation, source merge, direct main edit in Studio, Keycloak/Redis/PostgreSQL mutation or VPS LLM inference. The owner-approved **documentation commit** is not an application release.

For any new AI: TUJUAN → FAKTA → GAP → RISIKO → SOLUSI → TOOLS/OWNER → OTORISASI → BUKTI. Every claimed PASS must name the test or exact observation. Use the next-step/stop conditions from [W0](./02-w0-00-read-only-discovery-work-order-20261012.md).

## 5.1 Owner G1 closure (2026-10-12)

Owner explicitly approved RC-W0-09 closure with every residual blocker and **all 27 WEB-AC still mandatory**. See [RC-W0-10 G1 signed decision](./progress-engineering-canonical/RC-W0-10-owner-g1-ratification-and-discovery-closure-20261012.md). This is **not** G2 implementation approval and does not permit source edits, creating worktree, DNS/provider activation, preview, push/merge or production release.

Current planned G2 candidate: [RC-W1-01 first-contact Creator/Reader IA slice](./progress-engineering-canonical/RC-W1-01-proposed-g2-first-contact-creator-reader-ia-work-order-20261012.md), proposed three files `app/page.tsx`, `components/ecosystem/EcosystemHero.tsx`, `components/ecosystem/UseCasePathways.tsx`, exact Studio main SHA only after independent read-only source preflight. Previously reported primary checkout is locally behind GitHub main with 14 protected untracked Markdown; no primary `git pull/reset/clean`. Existing W3 image 404, W4 GA consent gap, W5 Workers AI entitlement and W6 Resend failed DNS remain mandatory before website Phase 1 DoD.

## 6. Canonical progress publication

Read [`progress-engineering-canonical/`](./progress-engineering-canonical/README.md) for dated, sanitized engineering progress receipts (W0, subsequent tests/CI and handoff evidence), while [`01-engineering-progress-ledger.md`](./01-engineering-progress-ledger.md) remains the phase-wide summary. When explicitly authorized, merge evidence documentation directly into this canonical GitHub path with exact SHA checks; **documentation publication never authorizes source changes, provider activation, deployments, or Phase 1/2 transitions**.

## 5.2 Explicit G2 owner approval (2026-10-12)

The owner approved **combined RC-W1-01 + RC-W1-02** under the previously published exact scope: one narrow Git object fetch if necessary; one isolated worktree and branch; three allowlisted TSX files for Creator/Reader IA; and bounded tests without dependency installation. This ratification is archived in [RC-W1-03](./progress-engineering-canonical/RC-W1-03-owner-g2-ratification-and-isolated-execution-20261012.md); the implementation/QA agent prompt is [RC-W1-04](./progress-engineering-canonical/RC-W1-04-gemini-ide-authorized-bounded-implementation-and-qa-prompt-20261012.md). Primary `main` and 14 untracked owner Markdown remain protected. **No worktree/fetch/coding execution is verified until owner Windows output is supplied.** No push/PR/Preview/main merge/production or DNS/provider authorization is granted.
