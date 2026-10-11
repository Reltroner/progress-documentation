# reltroner.com — Phase 1 Frontend Production Readiness

> Status: OWNER-RATIFIED REQUIREMENTS / W0 READ-ONLY DISCOVERY AUTHORIZED / IMPLEMENTATION NOT YET ACCEPTED.
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
5. [02 — W0 discovery work order](./02-w0-00-read-only-discovery-work-order-20261012.md): **FIRST executable engineering workstream**, read-only.
6. [03 — Traceability / acceptance](./03-phase1-acceptance-and-invariant-traceability.md): proposed measurable acceptance, gate-by-gate.
7. [04 — Cost, privacy and provider boundaries](./04-zero-incremental-spend-and-provider-boundaries.md).
8. [05 — Git workspace / release governance](./05-source-workspace-and-release-governance.md).
9. [06 — TS/TSX content and component design](./06-frontend-component-and-content-architecture.md).

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
| W0-00 read-only discovery | AUTHORIZED / EVIDENCE PENDING | First engineering action; no code, local checkout, provider or production changes |
| W1+ scoped implementation | NOT YET AUTHORIZED AS MUTATION | Requires W0 receipts, path allowlist, exact SHA/branch, acceptance plan |
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

The first workstream is W0 **OBSERVE → EVIDENCE → GAP → DECISION**, not W1 implementation. No new provider purchase, DNS change, paid plan, Vercel purge, live API activation, source merge, direct main edit in Studio, Keycloak/Redis/PostgreSQL mutation or VPS LLM inference. The owner-approved **documentation commit** is not an application release.

For any new AI: TUJUAN → FAKTA → GAP → RISIKO → SOLUSI → TOOLS/OWNER → OTORISASI → BUKTI. Every claimed PASS must name the test or exact observation. Use the next-step/stop conditions from [W0](./02-w0-00-read-only-discovery-work-order-20261012.md).
