# 11 — reltroner.com Front-End Landing Experience & Product Journeys

> Status: **OWNER-RATIFIED EXPANDED PHASE 1 WEBSITE REQUIREMENTS** (2026-10-12); **NOT IMPLEMENTED / NOT PRODUCTION CERTIFIED**. Detailed gates in [website engineering contract](../reltroner.com-upgrade/00-ratified-frontend-architecture-contract-20261012.md).

## Architectural role
`reltroner.com` is the **identity and discovery gateway** for the intellectual studio, not a new monolithic LMS/ERP or the master source of business truth. The existing website remains primarily front-end. Skill-Wanderer was mentioned as a **minimum professional UX reference**; the studio should not copy its design, commercial claims or platform architecture without independent need.

## Proposed first-contact sequence
~~~text
LANDING
→ recognizable human/creator question
→ two distinct paths
    → FOR CREATORS: learn system thinking / Creative Compound Machine
    → FOR READERS: Asthortera / The Abyss of Comfort
→ concise mechanism / concrete evidence
→ honest links to existing experiences
→ optional follow/return path
~~~

## Original information architecture (historical Phase 1 baseline; extended by §8 below)
1. **Hero** — concise “creativity that compounds” identity without jargon wall.
2. **Creator path** — anti-stagnation mechanism and accessible introduction.
3. **Reader path** — advanced civilization as speculative laboratory for 2026+ anxiety, with no premature canon claim.
4. **How it works** — seed, constraints, interactions, consequence and future input.
5. **Evidence/proof** — inspectable work, engineering-reasoning examples, non-spoiler Asthortera analysis; proper development status.
6. **Start learning** — link to guest-readable LMS.
7. **Explore series** — route to canonical/forward architecture with clear maturity labels.
8. **Follow/contact** — accessible, minimal, privacy-conscious.

The eight-section presentation above is the **original experience outline**. Audience-first goals remain ratified; exact section count stays a design choice. §8 and the versioned website contract add the owner's later ratified functional requirements.

## UX acceptance dimensions
- Mobile and desktop layout, keyboard navigation, clear hierarchy and comfortable typography.
- Primary purpose and two entry pathways intelligible to a first-time visitor.
- All displayed destinations work; no false “subscribe now” for unavailable paid service.
- Stable metadata/SEO, performance budget derived from measurement, meaningful accessible labels.
- Privacy/cookie handling must reflect actual active third-party scripts; no needless guest gate or artificial account requirement.
- User can reach LMS, case studies and studio narrative without understanding framework jargon first.

## Distinct product surfaces
- `reltroner.com`: concise outward-facing discovery/identity.
- `lms.reltroner.com`: guest-first learning experience.
- `lms-admin.reltroner.com`: separately governed privileged frontend.
- `lms-api.reltroner.com`: accepted API boundary, not website marketing runtime.
- Reltroner Studio content: deeper framework, canon and speculative narrative.
- External socials, Patreon, Kickstarter: optional channels/offer mechanisms, not core brand identity.

## Validation method
Use a small first-time visitor comprehension test: after viewing the landing page, can they explain who it is for, why it matters, what the two entry paths are, and what is currently available versus upcoming? Record defects and refine; do not claim design success without feedback.

## Scope control
Do not introduce backend account CRUD, marketplace, new social networking, payment gateway or unrestricted AI agents merely because it fits a startup landing page pattern. **The bounded Studio contextual AI chatbot, Resend newsletter and Web3Forms contact are now owner-ratified Phase 1 website requirements**, governed by the zero-incremental-spend and trust-boundary gates below. Any further addition remains value- and acceptance-driven.

## Authority
[Studio Master §55.2](https://github.com/Reltroner/reltroner-studio/blob/main/content/principles/reltroner-studio-master-source-of-truth.md), [Phase transition 05](./05-phase1-phase2-exit-entry-and-reentry.md), and [ratified website engineering contract](../reltroner.com-upgrade/00-ratified-frontend-architecture-contract-20261012.md). This file records ratified product outcomes; implementation proof and gate status are kept separately.

---

## 8. Ratified expanded website experience — 2026-10-12 owner amendment

The owner explicitly approved the cumulative frontend upgrade discussed on 2026-10-12. This section **supersedes older candidate-only or 'AI optional merely by curiosity' language for the enumerated website features**, without retroactively rewriting the original design history. Ratification means **required delivery outcome**, NOT successful integration/deployment. New mandatory outcomes can be deferred only through a later explicit owner-approved scope amendment, not silently because providers charge fees.

### 8.1 Identity, audience and epistemic IA

- Primary entry pathways remain **For Creators** (Creative Compound Machine/systemic generation) and **For Readers** (Asthortera / The Abyss of Comfort).
- Provide a distinct secondary **Builder / Real-World / Collaborators** route to credible engineering case studies and contact; do not confuse it with the two primary identity routes.
- Support **Creative Universe, Real-World Knowledge and Builder/Ecosystem** discovery lenses across heterogeneous collection routes without splitting the website into three businesses.
- Each released item identifies FICTION_CANON, FICTION_SPECULATIVE, REAL_WORLD_ANALYSIS, CREATIVE_FRAMEWORK, ENGINEERING_CASE_STUDY or CROSS_DOMAIN_ANALOGY; do not represent a fictional national metric as empirical Earth evidence, nor an analogy as a canon fact.
- Skill-Wanderer is a model of **intent-based IA, contact clarity and follow-up transparency**, not a copied UI/brand or implied free-prototype/agency promise.

### 8.2 Navigation, reading and media reliability

- Use existing horizontal desktop space for left **Reading Path** and right **Archive Explorer** with collection selector, Ctrl+K-compatible search, related content and adaptive responsive behavior; do not widen editorial paragraphs excessively or hide navigation on mobile.
- Shared published-only search/index contract must serve command palette and archive rail.
- Harden jsDelivr/GitHub images against broken loading and cache staleness. **When source image bytes change at reltroner-studio-resource with the original filename unchanged, the live site must automatically use the new version after the approved release pipeline.** Prefer immutable asset commit URLs and validate actual image bytes/rendered content; Vercel CDN cache purge alone cannot be presumed to clear jsDelivr.
- Keep Git + Markdown as canonical public Studio content with publication/canon provenance. Do not stage or rewrite the 14 owner-reported untracked music/places Markdown files in the existing Windows checkout.

### 8.3 Branded contextual Reltroner Navigator (AI chatbot)

- Fixed accessible launcher at the bottom right on all public pages; original Reltroner character/visual identity, not Admiral Orion's military persona/artwork.
- Welcome choices, deterministic quick navigation, contextual public-content retrieval, explanatory **real generative AI** within an accepted no-spend provider envelope, citations, restart and safe offline/quota fallback.
- AI may not access privileged LMS/Keycloak/HRM/private data or mutate canon/business truth. Distinguish fiction, real-world and creative analogy, and disclose AI limitations/provider data processing.
- Cloudflare Workers AI Free is a preferred **conditional candidate**, not a preapproved deployment: verified provider entitlements, model, quality, limits, protective rate controls, legal/privacy posture and no-charge behavior are required. A deterministic-only FAQ is not equivalent to passing the AI feature gate; report BLOCKED if no qualifying free inference provider exists.

### 8.4 Privacy, newsletter and contact

- Visible factual essential-cookie/privacy disclosure. Audit and resolve existing production Google Analytics and third-party embeds before any "no tracking" claim; keep cookie policy and consent behavior truthful.
- **Resend** for opt-in subscription: contacts, separate contact-accepted/welcome-sent/verification states, duplicate handling, unsubscribe/suppression, source/consent provenance and secured server-only API key. Newsletter is not an authorization to commence Phase 2 marketing prematurely.
- **Web3Forms** for contact replacing existing Formspree/reCAPTCHA flow after controlled migration. Provide intent-specific collaboration, creative/worldbuilding and learning inquiry, clear status, manual written follow-up expectations, privacy/terms and a genuine alternate email contact. Do not auto-enroll contact inquiries in Resend.
- Both providers are gated by actually available **Free** account quotas and anti-abuse behavior; no upgrade, auto top-up or hidden spend.

### 8.5 Implementation, production and nonfunctional gates

- **Frontend-first Next.js + TypeScript/TSX** is mandatory for new features; use narrowly bounded API/Worker functions only for secrets and inference. No new application database or VPS service by default; do not rewrite frozen LMS boundaries.
- Responsive accessibility, source-validated security (including Markdown embeds/HTML), performance Core Web Vitals, SEO, links, privacy, monitoring, provider failures, finite quotas, and operator rollback all require independent production/preview evidence.
- **Rp0 incremental spending hard constraint**: no new subscription, paid plan, charged inference, VPS purchase or auto-usage-billing exposure without a separate explicit owner decision. Financial conflict is a BLOCKED requirement needing a change decision, never automatic feature downgrade or payment.
- Engineering runs as discovery W0 → bounded isolated TS/TSX PR workstreams → preview/cost/negative tests → separate production authorization → final owner website acceptance. Avoid touching the primary checkout's untracked files.
- This is a **Phase 1 website readiness contract**, not a green light to merge into Reltroner Studio main, change Vercel/Cloudflare provider settings or activate Phase 2.

**Operational navigation:** [Website upgrade README](../reltroner.com-upgrade/README.md) · [Architecture contract](../reltroner.com-upgrade/00-ratified-frontend-architecture-contract-20261012.md) · [Initial read-only W0](../reltroner.com-upgrade/02-w0-00-read-only-discovery-work-order-20261012.md) · [27 acceptance criteria](../reltroner.com-upgrade/03-phase1-acceptance-and-invariant-traceability.md).
