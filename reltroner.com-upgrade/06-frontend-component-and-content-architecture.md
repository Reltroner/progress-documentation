# RC-WEB-DESIGN-001 — Frontend Component, Public Index, AI and Media Design

> **LATEST 2026-10-13 UI OWNER REFINEMENT — [RC-UX-05R2](./12-owner-navigator-reading-path-fullwidth-article-and-media-debugging-20261013.md):** The screenshot at `/philosophies` crosses out **desktop-left “Reltroner Studio” header brand label** and points the currently left-aligned breadcrumb to **horizontal center above category name**. Remove only that desktop header text/control through the shared header and reclaim its grid space; retain remaining desktop main menu, Apps and search and keep Reltroner identity in page content, SEO and Compass. Center collection breadcrumbs across Knowledge Base collection templates, responsive with semantic nav/ol and links. Do not change article-detail breadcrumbs gratuitously, or regress mobile header-to-Compass consolidation. No local source patch has been run by this documentation write.


> **2026-10-13 OWNER MOBILE NAV OVERRIDE — [RC-WEB-ADR-012 mobile addendum](./12-owner-navigator-reading-path-fullwidth-article-and-media-debugging-20261013.md):** On 320px/375px and actual existing mobile breakpoint, REMOVE the entire existing mobile header strip containing Reltroner branding + global search icon + hamburger **only after migrating those controls' real functions** to the already-existing floating **Compass Navigator**. The Compass panel is the single functional entry for global nav, shared public-index search, article-specific Reading Path, and existing Navigator features; it is NOT dependent on successful AI inference. Keep brand identity visibly/semantically present in the open panel and accessible launcher, but no duplicate mobile header or placeholder height. Desktop header unchanged. Mobile screenshot also shows Navigator near bottom content; enforce nonobstructive safe-area positioning, 44px touch targets, accessible focus and no overflow. **This overrides ADR-012's legacy instruction to keep mobile hamburger ordinary site nav**; all other media/fullwidth details of ADR-012 remain binding. No local source edits claimed.


> **NEWEST OWNER UX OVERRIDE 2026-10-13 — [RC-WEB-ADR-012](./12-owner-navigator-reading-path-fullwidth-article-and-media-debugging-20261013.md):** The left desktop/article **Reading Path sidebar must be removed from all article UIs**, and its *actual* functionality is transferred to the global **compass-branded Reltroner Navigator** (existing context-scoped heading outline; section/hash click; keyboard/focus; clearing stale state). Hamburger reverts to normal global navigation; no duplicate article outline/pill. Remove obsolete article left rail grid track and let the centered main content use substantially more available width, with readable text measure and full responsive media width. Target highlighted native HTML5 video 0:00/fallback and YouTube embed Error 153 separately through source/network/codecs/HTTP Referer diagnostics. This is the owner's **latest design requirement and supersedes both ADR-011's desktop left rail and its mobile hamburger TOC**; older wording below is historical. Preserve 18 invariants, 27 acceptance, no-cost and protected drafts. No local source modification or runtime QA was performed by ChatGPT in creating this addendum.


> **LATEST OWNER UX AMENDMENT 2026-10-13 — [RC-WEB-ADR-011](./11-mobile-reading-path-in-hamburger-and-editorial-shell-refinement-20261013.md):** Existing **mobile global hamburger** must contain active article `Reading Path` outline; **remove** separate mobile `Reading path` and `Explore archive` pills. Keep global search/Ctrl+K and public collection discovery usable. On desktop adopt Skill-Wanderer-inspired **single contextual left Reading Path rail + dominant editorial body**, rather than competing persistent right Archive Explorer rail. Preserve sticky rail's article-body boundary and correct focus, route state and no stale article TOC. This supersedes conflicting dual-rail/dual-drawer *presentation* language below, **not** the W2 index/search and WCAG/security invariants. Agent's prior 72/72 reported browser QA did not establish owner visual acceptance; code must be corrected locally and visually revalidated.


> **2026-10-13 OWNER SCREENSHOT UX FIX — [RC-WEB-ADR-010](./10-owner-screenshot-led-ui-ux-debugging-layout-rails-and-section-order-20261013.md):** Skill-Wanderer screenshot is the owner's **UI/UX pattern reference**, not a request to copy branding or claims. **DOM order** on Reltroner homepage must be Newsletter (`Notes from the Studio`) **before** the existing final `Ready to explore?` CTA and then footer. Article Reading Path/Archive Explorer desktop sticky rails must be **bounded by the editorial article region**, stop before related-content/newsletter/footer, avoid two cramped independent scroll traps and preserve 65–76ch center prose. Mid-screen collapse Explorer to accessible drawer; mobile drawers and keyboard/focus handling. Navigator must not cover rails, footer or newsletter. Local `localhost:3000` screenshot prototype not present on GitHub `main`; agent must inspect actual isolated worktree before editing. No local code fix has been executed by ChatGPT.


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

