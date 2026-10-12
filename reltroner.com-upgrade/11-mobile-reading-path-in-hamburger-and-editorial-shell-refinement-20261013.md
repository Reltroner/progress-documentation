# RC-WEB-ADR-011 — Owner UX Correction: Mobile Reading Path in Hamburger, No Redundant Pills, Editorial-First Desktop

> **Status:** OWNER REQUEST 2026-10-13, **LOCAL SOURCE FIX NOT YET EXECUTED BY CHATGPT**, pending actual isolated worktree Antigravity implementation and fresh visual verification. This owner-specific design requirement **supersedes** conflicting desktop 3-column and mobile dual-drawer assumptions in [ADR-010](./10-owner-screenshot-led-ui-ux-debugging-layout-rails-and-section-order-20261013.md) and [WEB-DESIGN-001](./06-frontend-component-and-content-architecture.md) **for article UX only**. The 18 WEB-I invariants, 27 WEB-AC, publication/epistemic boundaries, no-cost and protected draft constraints remain binding.
> **Evidence:** owner provided 4 Reltroner desktop and 1 mobile annotated article screenshots, and Skill-Wanderer lesson/footer references; owner also supplied pasted Antigravity RC-UX-01 report dated 2026-10-13: local typecheck/validator/build and CDP suite reported PASS, but current screenshot-based owner acceptance **FAIL/PARTIAL** for navigational UX. Do not reuse previous automated PASS to close this new design requirement. GitHub Studio main `18b295f96ccb521b228a1855e79448158c09db15` was a stale remote relative to the user's uncommitted `localhost:3000` prototype. Do not commit source remotely or overwrite local state from GitHub main.

## A. Exact owner instruction

On the mobile article screenshot, the yellow arrow identifies the **existing top-right hamburger icon** in Reltroner Knowledge Ecosystem header. The yellow circle identifies the separate inline **Reading path** pill; the red cross identifies **Explore archive** pill. Owner requires:

1. **Move the ACTUAL Reading Path functionality into the existing hamburger menu**. Opening the menu on a published article must expose the current article heading outline (preserving section order, anchors, active section, scrolling and keyboard access). This must not merely move the text label or add a nonfunctional link.
2. **Remove both inline pills** `Reading path` and `Explore archive` from **mobile/tablet article UI**. No empty spacer or visually hidden duplicate interactive element remains. The existing hamburger's global navigation remains intact; outline is article-contextual and conditional, not shown as a fake empty menu on home/collection pages.
3. **Preserve archive discovery** using existing search icon, Ctrl+K and public collection navigation. If a route lacks an equivalent browsing entry, add a normal **Browse knowledge/Archives** link in the existing global menu—not another prominent pill. Do not delete W2 public index or search logic.
4. Use a mobile UI with **single article reading column, one primary document scroll, accessible menu drawer**, no nested reading-path or archive scroll traps and no Navigator/menu overlap. Keep top controls operable at 320px.

## B. Desktop screenshot critique relative to Skill-Wanderer Dojo

The source reference demonstrates **one useful left contextual navigation rail and a dominant editorial article column**. The user's Reltroner desktop screenshots show **two large competing nested-scroll rails** (Reading Path and Archive Explorer) at left/right, visually crowding the reading content. Owner instruction references this as a persistent UX bug after the RC-UX-01 technical suite passed. Target desktop article UX:

- **One persistent contextual left Reading Path** at appropriate wide viewport when headings warrant it; central content remains the dominant reading surface with comfortable text width (~65–76ch at normal zoom).
- **Do not keep Archive Explorer as a second persistent sticky rail** for this article layout. Preserve browsing/search through existing global header search/Ctrl+K and accessible archive/collection links (or low-emphasis discovery area outside body). W2 index remains intact.
- Constrain sticky Reading Path **within article-body containing block only**. It ends before `Associated records`, newsletter and footer. For unusually long TOCs, scrolling inside the TOC may be necessary but must be intentional, usable by keyboard and not create repeated competing bars.
- At medium/tablet widths, prioritise article readability; collapse Reading Path into existing navigation menu rather than adding toolbar pills. Desktop breakpoint may be chosen by measured available width, not the prior fixed `lg`/ `2xl` contract.
- Improve full article heading wrap and spacing without truncation. Skill-Wanderer's screenshot is a *principle reference*, not a pixel-perfect cloning or CSS source. Keep Reltroner navy/blue brand.

## C. Implementation boundaries

- Read current `C:\Projects\reltroner-studio-w1-ia` first: branch/HEAD and ALL modified/untracked paths, existing site header/mobile hamburger, `components/archive/AdaptiveArchiveShell.tsx`, `ReadingPathRail.tsx`, `ArchiveExplorerRail.tsx`, `ContentEntryPage.tsx`, header/global search, Navigator and styling.
- **Reuse the existing mobile hamburger state and interaction**; avoid introducing a second independent mobile menu or new package. Article outline data should be shared from the current article renderer with the header menu by a robust route-scoped mechanism (context/provider or equivalent), cleaned up on route transition; no stale headings on other pages. Ensure no hooks-rule violations or hydration mismatch.
- Close menu on section selection after navigation, scroll target below sticky header (e.g. `scroll-mt`), update hash, return logical focus to heading/content, Escape closes menu and restores trigger focus. Prevent background scroll when modal drawer open, accessible role/labels/expanded state/keyboard focus trap where appropriate.
- Remove the old inline dual triggers and orphaned drawer state/DOM branches carefully; **do not** delete the Reading Path component, public index, global search/Archive Explorer implementation if used in other routes; remove only redundant article-surface presentation. No dead imports, orphaned tests or fake fallbacks.
- Nav menu should provide coherent access to both ordinary site links and a clearly separated `On this page` article outline. If article has no meaningful headings, omit the section; never display stale previous-article headings.
- Preserve 14 protected untracked `content/music` and `content/places` original author drafts under primary worktree `C:\Projects\reltroner-studio`. Do not write primary, Git clean/reset, reinstall dependencies, provider calls, send email, source push/PR/preview/deploy.

## D. Mandatory browser acceptance (visually informed, not only a 72-check aggregate)

| Environment | Required observed result |
|---|---|
| Mobile 320×480 / 375×812 | Header burger is the **only article outline trigger**; no inline Reading path / Explore archive buttons under header, including keyboard accessibility tree; click burger reveals populated, correct TDA headings; click a deep heading updates hash, scrolls to content and dismisses menu; Escape/focus return works; no horizontal clipping |
| Tablet 768×1024 / 1024×768 | Article content remains primary; no duplicated drawer triggers or sticky overlay; mobile navigation breakpoint matches actual layout |
| Desktop 1440×900 and wide | One intentional Reading Path rail at left and dominant reading column; no right Archive Explorer sticky panel occupying equal importance; Archive/search functions remain reachable; rail sticky bounded to article |
| Article at top/mid/end/associated/footer | No sticky rail over related content, footer or Navigator; long left outline navigable; article reading remains legible |
| Other article, collection, homepage | No leaked/stale article TOC in global hamburger, normal site menu still functional, Ctrl+K/public archive discovery preserved |
| Zoom 200%, keyboard, reduced motion | No lost focus, inaccessible closed menu, double page scroll or CTA obstruction |

**Test:** source unit tests for conditional visibility, route cleanup, heading selection; local typecheck, content validation (warnings recorded), build once after code settled, real Chrome CDP visual/screenshots correlated to 320/375/768/1024/1440 and 200% zoom, not simply asserted programmatically. Cover existing app routes and not just TDA. Block GA if actual consent behavior not yet proven. Do not submit forms.

## E. Decision/status

`RC_UX_01_PRIOR_AGENT_TESTS=PASS_REPORTED` but `OWNER_VISUAL_UX_ACCEPTANCE=FAIL_NEEDS_REFINEMENT`; `RC_UX_02_MOBILE_HAMBURGER_TOC=OWNER_RATIFIED_REQUIREMENT_NOT_IMPLEMENTED_YET`; `RC_UX_02_REMOVE_TWO_MOBILE_PILLS=PENDING`; `RC_UX_02_DESKTOP_SINGLE_RAIL=PENDING`; `W2_SEARCH_ARCHIVE=PRESERVE`; `WEBSITE_PHASE1_DOD=NOT_ACCEPTED`; `PHASE2=NOT_ACTIVE`.
