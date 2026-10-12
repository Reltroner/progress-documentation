# RC-WEB-ADR-010 — Owner Screenshot-Driven UI/UX Debugging: Editorial Rails and End-of-Page Conversion Order

> **Owner directive:** 2026-10-13 Asia/Jakarta, nine screenshots supplied in conversation: Skill-Wanderer site footer/navigation/Dojo lesson at multiple reading positions, plus Reltroner `localhost:3000` homepage and TDA article at multiple scroll positions. The screenshots are the **owner's UX reference** for interaction/structural principles, **not** permission to reuse Skill-Wanderer trademarks, styles, business assertions or protected assets.
> **Status:** owner-requested UI/UX correction architecture/acceptance recorded; **Windows local source patch and browser QA are NOT executed by ChatGPT**. Existing Studio GitHub `main` checked at `18b295f96ccb521b228a1855e79448158c09db15`, and does **not** contain the screenshots' locally running multi-rail/newsletter prototype. **Do not edit the remote main to “fix” an invisible local version.** Operate in `C:\Projects\reltroner-studio-w1-ia` after fresh read-only inspection of the exact dirty files.
> **Normative hierarchy:** [WEB architecture](./00-ratified-frontend-architecture-contract-20261012.md), [WEB design](./06-frontend-component-and-content-architecture.md), [27 acceptance](./03-phase1-acceptance-and-invariant-traceability.md), [zero spend](./04-zero-incremental-spend-and-provider-boundaries.md), [owner process override](./08-owner-execution-authority-and-dedicated-creator-reader-tsx-adr-20261013.md), [owner portfolio amendment](./09-owner-approved-pathway-and-portfolio-landing-refinement-20261013.md). Screenshot reference governs these specific design conflicts; WEB-I01–18 and WEB-AC01–27 remain unchanged.

## A. Confirmed observable issues and owner-intended UI behavior

| ID | Visual observation from owner screenshot | Required correction |
|---|---|---|
| UX-01 — P1 | Reltroner homepage `Ready to explore?` section (orange rectangle) appears **BEFORE** `Notes from the Studio` newsletter (brown rectangle). | **Actual JSX/DOM order**: other home content → newsletter → **Ready to explore? final CTA** → footer. No duplicate newsletter or final CTA. Do NOT only visually reorder with CSS order. |
| UX-02 — P1 | TDA article has two side rails with constrained embedded scrollbars, each competing for attention. Skill-Wanderer Dojo reference emphasizes **one clear contextual lesson navigation** and a readable editorial column. | Maintain Reltroner contract's possible dual rails only where width and accessibility actually support them; left Reading Path, bounded prose, optional right Archive Explorer on wide desktop; below breakpoint prefer one rail + drawer, mobile drawers. Avoid 2 unnecessary scroll traps. |
| UX-03 — P1 | Reading Path and Archive Explorer still float/stick while scroll reaches related content and lower newsletter/footer, causing distracting rails that appear to outlive the article body. | Sticky rails must remain **within article-content grid's containing block** only. Related content, newsletter and footer occur **AFTER** article grid; sticky ends with article body. No rail overlay/footer collision or empty sticky space. |
| UX-04 — P2 | On TDA, huge article title wraps into several tall lines; two sidebars steal space from text. | Editorial center width targeted ~65–76ch, responsive heading scaling/line-height, narrowest plausible side rail widths, no content cropped or 320px overflow. Never truncate the article title. |
| UX-05 — P2 | Floating Reltroner Navigator at bottom right sometimes competes with archive rail/lower footer; sticky bottom controls may overlap. | Safe-area offsets, responsive dock placement/z-index; footer links, newsletter fields, rail drawer and content remain reachable without obstruction; no fake modal access or background scroll trapping. |
| UX-06 — P2 | Reltroner footer is sparse versus Skill-Wanderer footer's clear multi-group information architecture and newsletter-before-footer ending. | Improve footer with **actual verified** destinations grouped by purpose (Explore/Creative Practice/Ecosystem/Contact/Privacy etc) preserving unique Reltroner visual identity. Do not invent legal pages, promises, client proofs, subscriptions or destination URLs. |
| UX-07 — follow-up separate from layout | TDA article shown under `ENGINEERING`, `SYSTEMS ARCHIVE`, and `SCOPE AWAITING EDITORIAL REVIEW`; within headings, entity text displayed literally as `&#x26;` in the left outline. | Audit classification mapping and heading text extraction. Keep ambiguous scope explicitly pending rather than silently reclassifying fiction as Earth engineering; safely render/decode entities **as text, not unsafe HTML injection**. Coordinate W2 epistemic review, do not rewrite protected content or assert real-world claims. |

**UX adaptation goal:** Skill-Wanderer's visible pattern of (1) readable, task-focused lesson navigation, (2) bounded editorial content, (3) contextual navigation stopping before lower content, (4) separate newsletter below content, (5) meaningful final action and structured footer. **Do not replicate** its orange palette, lesson auth/quiz/completion state, open-source license labels, legal/monetization claims, or logo.

## B. DOM structure contract

**Homepage exact logical order** (selected segments may exist earlier): existing Hero/Use-Case/Knowledge/Portfolio/Roadmap and other core sections → **`NewsletterSection`** → **existing `Ready to explore?` final CTA** → footer. If newsletter is globally injected from `app/layout.tsx`, move it to the intended correct *home-specific* placement without duplicating across routes. Verify the actual current worktree, not stale GitHub `main`. DOM element order must match keyboard/screen-reader order and visual order.

**Article recommended structure:**

```tsx
<main>
  <ArticleHeaderAndBreadcrumb />
  <section aria-label="Article content and navigation" className="... article-boundary ...">
    <ReadingPathRail />   {/* sticky bounded only by article body */}
    <ArticleBody />       {/* editorial width ~65-76ch, unobscured */}
    <ArchiveExplorerRail /> {/* wide desktop only or accessible drawer */}
  </section>
  <RelatedPublicContent />   {/* outside sticky boundary */}
  <NewsletterSection />      {/* if article-specific, no duplication */}
</main>
<SiteFooter />
<Navigator />                {/* global overlay cannot obscure above */}
```

Do not blindly use this JSX as exact local source: adapt to existing components/layout and preserve working route/SEO. Note sticky positioning depends on **containing block**; changing CSS `position:sticky` alone while leaving rails within a page-height parent may not fix the late-page float. Ensure parent does not unintentionally `overflow:hidden/auto` and create the wrong scroll container.

**Breakpoints:** desktop ≥1440px may show both rails if center width remains readable; mid-size ~1024–1439px should prefer only left rail and an explicit Archive Explorer drawer/button; tablet and mobile should have accessible rail drawers/inline disclosure and **one primary document scroll**, no dual desktop sticky rails. Breakpoints can adapt to real source/test if readable behavior is preserved. Avoid fixed height rail `max-height` so small that most heading text is truncated. If nested rail scrolling is genuinely needed for a long table-of-contents, clearly label and keyboard-enable it, cap it to viewport safely and terminate at article body. Every article section anchor must be navigable via keyboard.

## C. Implementation constraints

- Operate on owner local isolated `C:\Projects\reltroner-studio-w1-ia`, **never `C:\Projects\reltroner-studio` primary with 14 author drafts**.
- Check current status and source paths first, because screenshots at `localhost:3000` reflect uncommitted prototype changes absent from GitHub main. Do not apply older W1 five/six-file script with stale exact status assumptions.
- Change **existing components** and imports in place, not a parallel second page/route. CSS tokens and hierarchy should be aligned with existing Reltroner navy/blue and Tailwind 4. No new packages, no build loops, no provider activation.
- Preserve Hero Creator/Reader TSX paths, Use-Case pathways, the two certificates with truthful labels, markdown/publication logic, existing site routes, and contact/network isolation. Do not send newsletters or production form submissions.
- W4 Google Analytics pre-consent issue is historically open. Use browser network blocking before first navigation unless its new implementation has actual clean-browser verified privacy behavior; do not call local blocked-network QA a production consent fix.

## D. Required QA/DoD evidence

1. Homepage DOM + screenshots show **newsletter BEFORE final `Ready to explore?`** at 320×480, 375×812, 768×1024, 1440×900. Tab order follows DOM; footer is last. No duplicate.
2. TDA representative `/technologies/tda-twin-digital-atom` browser at initial H1, mid-article, after last paragraph/related content and at footer; **both desktop rails cease sticky before article-related/footer region**, no multi-scroll trap, no overlap with floating Navigator.
3. At a wide viewport central prose reads ~65–76ch while side rails remain usable; at 1024 and below no unreadable three-column squeeze; 200% zoom and 320px text reflow without horizontal scrolling.
4. Heading navigation reaches the right targets, correct focus behavior (Tab/Shift+Tab, Escape and focus return for drawers) and safe text headings (no literal `&#x26;` in navigation unless source intentionally says that). No unsafe `dangerouslySetInnerHTML` for heading labels.
5. Newsletter state remains truthful: if Resend is not connected, prototype-only message/no subscriber created; no real form submit. Footer only working public links; no mislabeled legal route.
6. Run existing `npm run typecheck`, `npm run content:validate`, `npm run build` **once after integration settles**, plus targeted browser checks; preserve initial and final local Git exact paths and return exit codes. Local `next dev` visual preview is not proof of production `next start` build.
7. No source push/PR/preview/merge/prod deploy, DNS, pricing/provider, LMS/HRM private services, or destructive cleanup.

**Engineering disposition at documentation creation:** `RC_UX_01=OWNER_REQUESTED`, `LOCAL_CODE_FIX=NOT_EXECUTED_BY_ASSISTANT`, `ARTICLE_STICKY_ROOT_CAUSE=TO_VERIFY_IN_LOCAL_CSS/DOM`, `HOMEPAGE_ORDER_REQUIREMENT=CONFIRMED`, `STUDIO_MAIN=UNCHANGED_AS_CHECKED`, `G3_G8=NOT_RUN`, `PHASE1_DOD=NOT_ACCEPTED`.
