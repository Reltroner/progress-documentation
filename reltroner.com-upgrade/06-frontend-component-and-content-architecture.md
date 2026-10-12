# RC-WEB-DESIGN-001 — Frontend Component, Public Index, AI and Media Design

> **2026-10-13 W1 owner correction — [RC-WEB-ADR-008](./08-owner-execution-authority-and-dedicated-creator-reader-tsx-adr-20261013.md):** The landing design's two strategic Creator/Reader CTA actions now link directly to first-class TSX routes `app/start/creators/page.tsx` and `app/start/readers/page.tsx`; Markdown articles remain deeper source material, not the direct primary CTA destination. Do not mistake this small user-journey implementation for completed W2 archive/index/AI architecture; no new content source is established. Owner can directly order scoped work across workstreams without sequence theater while all functional/security/cost DoD remains binding.


> Status: TARGET COMPONENT DESIGN RATIFIED AT OUTCOME LEVEL / IMPLEMENTATION NOT STARTED.
> Target stack: current Next.js 16 / React 19, TypeScript-first .ts/.tsx, static and frontend-first. Actual source versions must be reverified before PR.
> This design is subordinate to [WEB architecture](./00-ratified-frontend-architecture-contract-20261012.md) and [financial/privacy contract](./04-zero-incremental-spend-and-provider-boundaries.md).

## 1. Baseline analysis / candidates, not an implementation receipt

At checked Studio SHA 18b295f96ccb521b228a1855e79448158c09db15:
- app/layout.tsx already mounts CommandPalette, ShellBackdrop, GoogleAnalytics and RouteAnalytics; app/page.tsx is an ecosystem-oriented gateway.
- ContentEntryPage.tsx defines ReadingPath but currently keeps it inside the 48rem editorial-shell; CollectionPageClient.tsx filters locally; CommandPaletteDialog.tsx has separate scoring. Reuse and compose instead of cloning search logic.
- lib/utils/content.js is the canonical parsed Markdown path for this app; types/content.ts already exists. getCollectionEntries filters published; separate getCollectionEntry rendering/HTML needs negative tests and metadata review.
- CDN resolution in lib/assets/cdn.js uses mutable @main; next.config.mjs remotePatterns matches @main; ArchiveCardMedia.jsx is unoptimized for jsDelivr. Treat CDN origin/cache behavior as unverified beyond source.
- Contact is app/contact/page.jsx and components/sections/ContactForm.jsx (Formspree, Google reCAPTCHA). No Resend newsletter or Studio Navigator integration proven.
- Some existing .js/.jsx are legitimate migration candidates, not a mandate to rename the whole project before adding functionality.

## 2. Publication and epistemic taxonomy

Each public archive entry derives stable ID, collection, slug, canonical route, title, description, version/revision and publication flag from accepted Git content. Add an explicit validated epistemic classification:
FICTION_CANON / FICTION_SPECULATIVE / REAL_WORLD_ANALYSIS / CREATIVE_FRAMEWORK / ENGINEERING_CASE_STUDY / CROSS_DOMAIN_ANALOGY.

Do not infer fiction vs Earth solely from a route or nation name. For transitional content, map existing metadata with explicit documented defaults and **manual review of ambiguous entries**, not a blanket fiction label. Distinguish public canon and author working drafts, and preserve legacy URLs. Public search index is generated at build time, filters publication in one place and supports both global Ctrl+K and scoped archive rails; HTML/sitemap/chat retrieval must use equivalent publication predicate or negative tests.

## 3. Component and route plan (new files .ts/.tsx)

~~~text
app/
  page.tsx
  layout.tsx
  contact/page.tsx          (replace old page.jsx in same reviewed change)
components/
  navigation/               (audience-first creator/reader routes)
  archive/
    ReadingPathRail.tsx
    ArchiveExplorerRail.tsx
    AdaptiveArchiveShell.tsx
  assistant/
    AssistantRoot.tsx
    AssistantLauncher.tsx
    AssistantPanel.tsx
    AssistantWelcome.tsx
    AssistantQuickActions.tsx
    AssistantConversation.tsx
    AssistantMessage.tsx
    AssistantInput.tsx
  newsletter/
    NewsletterSection.tsx
    SubscribeForm.tsx
    SubscriptionFeedback.tsx
  contact/
    ContactExperience.tsx
    ContactIntentTabs.tsx
    ContactInquiryForm.tsx
    ContactNextSteps.tsx
    ContactFAQ.tsx
lib/
  content/
    taxonomy.ts
    public-index.ts
    search.ts
  assistant/
    types.ts
    context.ts
    retrieval.ts
    guardrails.ts
  newsletter/
    types.ts
    schema.ts
  contact/
    types.ts
    schema.ts
  assets/
    resource-manifest.ts
~~~

Names are proposed target boundaries, not permission to add every file at once. No duplicate competing route under app/contact. Server secrets should live only in a separately approved protected edge endpoint; do not put Resend key into NEXT_PUBLIC variables.

## 4. Chatbot context and truth

Public assistant input: current pathname, public document ID, explicit requested intent and bounded conversation; all inputs untrusted. Static quick actions perform navigation **without inference**. Retrieval returns public passages with revision IDs and source URLs; LLM must clearly distinguish fiction, analogy and real-world claims. Answer renderer shows citations and 'insufficient evidence' state. AI error/quota state degrades to labeled deterministic search/navigation, not fake generative answer.

Original Reltroner branding replaces Admiral Orion motif. Global bottom-right launcher remains present without blocking cookies/footer/reading rails, and is keyboard/screen-reader/mobile accessible. History may be session-only by default; disclosure for AI external processing required.

## 5. Adaptive layout

Wide viewports: bounded center editorial prose (roughly 65–76 characters per line) flanked by sticky (within-safe viewport) left heading/path rail and right collection/search/explorer rail. Home need not use both rails; collection index uses collection nav/search rather than empty article TOC. Medium: show one rail or collapse. Mobile: both rails become distinct labeled accessible drawers without covering assistant or main content. Test scroll, focus return, hit targets, accessibility and reduced-motion.

## 6. CDN image update and cache

Source Markdown may keep /images/original-filename.webp. A controlled version manifest resolves:
asset path + reltroner-studio-resource commit SHA → immutable jsDelivr URL.
Never rely on stale @main URL or assume Vercel purge invalidates third-party jsDelivr. When resource repository changes, an authorized no-cost trigger updates manifest/deployment (within provider quota); postdeploy test confirms both URL revision and displayed image bytes. Verify response codes, content-type, dimensions, alt/fallback, lazy-load vs LCP priority, sizes and mobile. If automated trigger is unavailable free, mark BLOCKED and propose evidence-based alternatives, not manual purge masquerading as an automatic solution.

## 7. Form ownership

Contact intent form: Web3Forms client-only if verified free and safe with anti-spam, success/error differentiation and manual email fallback. Newsletter: client sends opt-in only to protected TypeScript handler; handler holds Resend secret, validates rate and provider state, implements unsubscribe, and refuses paid overages. Neither form silently enrolls users in the other.

## 8. Verification and sequencing

Begin with [W0 discovery](./02-w0-00-read-only-discovery-work-order-20261012.md), inventory actual CSS/JS, and derive a minimal W1 PR. Test representative routes from /, /contact, /blog/for-recruiters, /music, /music/[slug], and /places/[slug] and other collections to avoid regressions. Do not modify content/music or content/places owner drafts. Proposed crosscutting checks: npm run typecheck, npm run build, npm run content:validate, route/index/link tests, CSS responsive and keyboard tests; verify scripts first and **never state tests passed unless executed**.

