# RC-WEB-ARCH-001 — Reltroner.com Phase 1 Frontend Architecture & Production-Readiness Contract

> Version: 1.0.0; decision: OWNER RATIFIED 2026-10-12 Asia/Jakarta.
> Normative status: RATIFIED WEBSITE SCOPE; detailed vendor/provider placement remains conditional until discovery/acceptance.
> Implementation status: NOT IMPLEMENTED / NOT PRODUCTION CERTIFIED by this contract.
> Parents: [strategy 05](../all-in-reltroner-master-source-of-truth/05-phase1-phase2-exit-entry-and-reentry.md), [website 11](../all-in-reltroner-master-source-of-truth/11-reltroner-com-landing-and-ux-journeys.md), [Studio Master](https://github.com/Reltroner/reltroner-studio/blob/main/content/principles/reltroner-studio-master-source-of-truth.md).
> Related operational standards: [LMS frozen physical](../lms/master-infrastructure-placement-contract.md), [LMS frozen logical](../lms/logical-service-boundary-api-contract.md). Those contracts **retain authority over LMS** and are not amended here.

## 1. Objective and system boundary

Reltroner.com remains a **frontend-first identity, discovery, knowledge and relationship gateway**, not a new authenticated LMS, payroll/ERP, paid marketplace, multitenant business app or canonical novel-writing database. Required frontend journeys can use narrowly scoped external backend endpoints (AI inference proxy, subscription) because exposing API secrets in a browser is prohibited. These integrations must not alter LMS business state.

Primary value: Creative Compound Machine and Asthortera / The Abyss of Comfort, expressed without requiring first-time visitors to know internal jargon. Skill-Wanderer is a **reference for audience-first information architecture and contact lifecycle**, not a UI copy, service promise, recruitment guild, free prototype offer or business model. Production-ready means tested and operator maintainable; it does not mean every future feature.

## 2. Nonnegotiable website invariants (WEB-I01..WEB-I18)

| ID | Binding rule |
|---|---|
| WEB-I01 | Phase 1 website acceptance is separate from LMS final DoD and Phase 2 activation. No implicit phase switch. |
| WEB-I02 | Frontend-first Next.js, TypeScript/TSX for new UI/logic. Avoid rewrite-for-appearance, broad any types and new business-state servers. |
| WEB-I03 | Two first-contact primary paths: for creators and for readers. Portfolio/collaborators remain explicit secondary access. |
| WEB-I04 | Label epistemic scope of published information: FICTION_CANON, FICTION_SPECULATIVE, REAL_WORLD_ANALYSIS, CREATIVE_FRAMEWORK, ENGINEERING_CASE_STUDY, CROSS_DOMAIN_ANALOGY. Analogy is not empirical evidence; worldbuilding is not Earth fact. |
| WEB-I05 | Markdown/Git remains Studio content authority. Indexes, chat answers, excerpt summaries, search and sitemap are derived and published-only, not authorities replacing Git. |
| WEB-I06 | Shared search contract for Ctrl+K and archive sidebar; contextual filters must not silently hide all other valid public content. |
| WEB-I07 | Wide desktop may have left Reading Path / center bounded prose / right Archive Explorer; responsive adaptive/mobile nav with no lost keyboard path. Avoid rail overlays or unreadably wide text. |
| WEB-I08 | No broken or silently stale critical images; source filename can stay unchanged while resource commit ID changes. Immutable URL release, automation, content reference validation and render checks. |
| WEB-I09 | A branded Reltroner Navigator launcher is accessible across public pages; welcome prompts, reset, intentional context and citations. Do not copy Admiral Orion identity/artwork or military promises. |
| WEB-I10 | Chat AI accesses only approved public evidence and bounded inference; no privileged LMS, HRM, SQL, shell, Keycloak, canon writes, customer data or arbitrary agent tools. When inference is unavailable, deterministic navigation remains usable and clearly labeled non-AI. |
| WEB-I11 | Contact via Web3Forms, independent from newsletter. Explicit inquiry intent, accurate acceptance state, spam defenses, alternate contact path; no invented SLA/calls. |
| WEB-I12 | Subscribe via Resend with server-only credential, explicit opt-in, no silent enrollment from contact inquiry, duplicate/idempotency and unsubscribe lifecycle, clear status/error. |
| WEB-I13 | Privacy/cookies claims must match actual GA, third-party embeds, chatbot and forms. Remove/consent-gate nonessential tracking before advertising 'no tracking'. |
| WEB-I14 | Hard budget: **Rp0 additional cash**; no upgrade, automatic paid overage, purchase, paid APIs or extra VPS without a new explicit owner decision. Enforce failure/fallback before charge risk. |
| WEB-I15 | Protect the owner's 14 reported untracked Studio content files. Source work on separate worktree/branch and explicit staged paths; never clean/reset the primary working tree. |
| WEB-I16 | No cross-write/redefine of six-service LMS, its frozen trust/identity, private database or runtime placement; no local LLM inference on current KVM1 as a workaround. |
| WEB-I17 | Security, accessibility, performance, SEO, link integrity and operational handoff need evidence, not assertions based on UI screenshots, preview URLs or green build alone. |
| WEB-I18 | Separate documentation ratification, nonproduction source implementation, preview acceptance, main integration, production deployment and Phase 1 exit approvals. No step grants the next implicitly. |

All 18 invariants must be traced in the acceptance matrix; any change requires a versioned ADR/amendment with explicit owner approval and impact analysis.

## 3. Feature architecture by user need

1. Landing: plain-language hero, two prominent Creator/Reader routes, visible creator framework proof, spoiler-safe Asthortera entry, secondary engineering/collaboration evidence, available-vs-upcoming labels, LMS guest CTA and contact/subscription.
2. Knowledge: three navigation lenses — **Creative Universe**, **Real-world Knowledge**, **Builder/Ecosystem** — while retaining the two strategic homepage entry routes. These are IA labels, **not** separate websites, paid offerings or LMS services.
3. Library: each collection and entry provides provenance, classification, search/filter, related links and accessible route/heading navigation. Preserve existing slugs and redirects unless evidenced migration is approved.
4. Reltroner Navigator: fixed bottom-right nonblocking launcher; keyboard/ARIA/modal focus behavior; context-relevant quick actions that operate deterministically; approved-public content grounding and source links; bounded AI explanations, quota/error fallback. Vendor provider selection remains gated.
5. Contact: collaboration, creative/worldbuilding and learning inquiry are intent routing options. Web3Forms receives contact messages, **not** mailing list subscriptions. Provide privacy notice, manual email-first expectation and valid alternate contact.
6. Newsletter: Resend Contacts + optional welcome/verification flow with accurate active-vs-unverified semantics, unsubscribe preferences and zero-cost limits. No mass marketing before Phase 2 activation.
7. Content images: GitHub resource repository as authoring source, jsDelivr immutable commit-addressed assets or demonstrably equivalent existing no-cost delivery; automatic new version on source push and acceptance smoke tests.

## 4. Deployment, cost and optional vendor topology

- Existing www.reltroner.com on Vercel Hobby is an **observed baseline, not a mandate to buy Pro**; verify terms of service for current/future commercial use and measured free quotas.
- Existing Cloudflare infrastructure is a candidate for **small, bounded edge API** for protected Resend key and optional Workers AI; AI availability, model, cost/no-overage guarantees and implementation compatibility MUST be verified before selection.
- Web3Forms Free client-side flow is a candidate provider implementation (public access key expected), subject to active account entitlement, spam configuration and data-handling acceptance.
- Existing Hostinger/VPS/Redis/PostgreSQL/Keycloak capacity is **not freely allocable** merely because already paid. Shared resources require independent capacity and blast-radius approval; do not move an LLM onto the 1-vCPU VPS.
- If free AI inference cannot meet an owner-approved production-quality gate without spending, record a **BLOCKED cost/quality conflict** and ask the owner to amend feature scope. Do not claim an always-static FAQ fulfills a ratified *generative AI* requirement.
- No new vendor can begin a paid billing lifecycle by accident: hard stops, dashboard evidence and operator-owned alert/usage review are required.

## 5. Engineering sequencing and exits

W0 Discovery (authorized read-only) → W1 Information architecture/taxonomy → W2 library navigation/search/sidebars → W3 asset freshness & rendering → W4 privacy/security → W5 Navigator UI and AI runtime → W6 newsletter/contact → W7 integration, SEO/performance/E2E, zero-spend review, release handoff. Workstreams may be rearranged after dependencies/evidence, but no production or vendor mutation without separate change authorization. No 'one huge PR'.

Detailed [W0 work order](./02-w0-00-read-only-discovery-work-order-20261012.md), [acceptance](./03-phase1-acceptance-and-invariant-traceability.md), [cost controls](./04-zero-incremental-spend-and-provider-boundaries.md) and [worktree rules](./05-source-workspace-and-release-governance.md) are subordinated implementation contracts.

## 6. Modification, precedence and rollback

Normative order by subject: Studio apex/ratified strategy → website parent ratification 05/11 → this ratified website architecture for its domain → accepted website ADR → W0/other bounded work orders → immutable source/test/production evidence → living ledger → brainstorm candidates. Conflicts with LMS frozen architecture are blocked pending LMS ADR; this document alone never modifies LMS. If application/infra changes unexpectedly occur, STOP, preserve audit data and restore only by separately approved rollback with known-good SHA. There is **no application release implied by this documentation ratification**.
