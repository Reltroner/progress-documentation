# RC-W1-16 — Independent Acceptance Review of W1 Browser QA: Scoped Pass, Residuals and G3 Hold

> **Owner-submitted agent report:** Antigravity Browser Subagent “Laporan Konsolidasi Hasil Browser QA Deterministik RC-W1-15”, timestamp **2026-10-12T22:38:45+07:00**, supported by owner console `next start` Ready in 377 ms. Evidence class: **OWNER_PASTED_AGENT_REPORT_WITH_LOCAL_BROWSER_MEASUREMENTS**, **not independent reviewer reproduction in Chrome**.
> **Reviewer source of truth:** [RC-W1-01 original W1-IA01..12 acceptance contract](./RC-W1-01-proposed-g2-first-contact-creator-reader-ia-work-order-20261012.md), [RC-W1-15 restored one-file source integrity and QA handoff](./RC-W1-15-one-file-restore-pass-browser-qa-ready-20261012.md), [RC-WEB-AC-001 mandatory 27-AC crosswalk](../03-phase1-acceptance-and-invariant-traceability.md), [RC-WEB-GOV-001 governance](../05-source-workspace-and-release-governance.md).
> **Source base:** `Reltroner/reltroner-studio` `18b295f96ccb521b228a1855e79448158c09db15`, W1 branch `phase1/w1-creator-reader-ia-20261012` local isolated `C:\Projects\reltroner-studio-w1-ia`. GitHub Studio `main` separately rechecked at the same SHA. Local W1 three-file patch remains **uncommitted and not visible on GitHub**; reviewer relied on owner-agent status and previously reported diff.
> **Review classification:** **`BROWSER_QA=PASS_SCOPED_AGENT_REPORTED`**, **`W1_ACCEPTANCE=PARTIAL_WITH_DOCUMENTED_RESIDUALS`**, **`G3=NOT_AUTHORIZED`**, `G4..G8=HOLD`, `WEB_PHASE1=NOT_ACCEPTED`, `PHASE2=NOT_ACTIVE`.
> **No source writes, PR, provider changes or preview/deploy are authorized by this archive.**

## 1. What genuinely advanced at G2

The previous agent STOP `BLOCKED_RESTORE_EVIDENCE` was resolved by owner-run `RC_W1_12_NEXT_ENV_RESTORE=PASS` (RC-W1-15). Owner reports final browser agent read-only Git checks: exact branch/HEAD; only `app/page.tsx`, `components/ecosystem/EcosystemHero.tsx`, `components/ecosystem/UseCasePathways.tsx` modified; `next-env.d.ts` no diff against HEAD; no staged/untracked paths. Original primary 14 author Markdown SHA256 integrity was verified within RC-W1-12R, not rehashed by browser agent.

Actual browser agent reports Chrome emulation and DOM measurements:

| VP | Browser viewport | document scrollWidth / clientWidth | Creator rectangle | Reader rectangle | Reported finding |
|---|---|---|---|---|---|
| VP01 | 320×480 | 320 / 320 | x unspecified; y=281, w=288, h=312 | x unspecified; **y=609**, w=288, h=356 | Vertical cards, no horizontal overflow |
| VP02 | 375×812 | 375 / 375 | y=268, w=343, h=272 | y=556, w=343, h=316 | Vertical cards, no horizontal overflow |
| VP03 | 768×1024 | 768 / 768 | x=24, y=253, w=352, h=328 | x=392, y=253, w=352, h=328 | Equal two-column cards |
| VP04 | 1440×900 | 1440 / 1440 | x=272, y=269, w=440, h=280 | x=728, y=269, w=440, h=280 | Equal two-column cards |

**First-fold qualification:** At 320×480, Reader begins at y=609, wholly below initial viewport; Creator extends from y=281 to y=593, beyond the fold as well. At 375×812, Reader extends to y=872. A stacked two-path mobile design **need not place both full cards above the fold**, and lack of horizontal overflow is real scoped evidence, but the report's “immediate” first-time comprehension and equal initial viewport visibility claims are **not independently established** by these metrics. WEB-AC01 still requires a first-time visitor comprehension test rather than geometry alone.

Browser agent also reports: Tab/Shift+Tab logical; visible focus ring; one h1 with h2 card headings; Reader `aria-describedby="reader-lore-note"` with accurate spoiler-aware fictional glossary description; 200% zoom usable; Creator `/blog/no-copypaste-worldbuilding`, Reader `/blog/asthortera-glossary`, collaborator `/blog/for-recruiters` navigated via CTA; `#app-dock` and `#knowledge-bridge` scroll correctly; deliberately nonexistent route displays standard 404; 0 reported uncaught JS or hydration errors; Next bundles loaded; `gtag/js?id=G-VZ7QYLZPF0` request was actively blocked with `ERR_BLOCKED_BY_CLIENT`. These are **agent observations**; full browser trace/console/screenshot bytes were not supplied to the reviewer.

The earlier owner-authorized local QA remains: npm ci one attempt (263 packages, exit 0), TypeScript exit 0, content validator exit 0 (**0 errors / 371 warnings / 419 files**) and Next production build exit 0 (**440/440 static pages**, sitemap postbuild). These cannot be extrapolated into production, cross-provider or Phase 1 DoD success.

## 2. Independent W1-IA01..12 matrix

| Test | Original contract / evidence now available | Independent classification | Residual/gap |
|---|---|---|---|
| W1-IA01 | Two distinct Creator/Reader CTAs; symmetric desktop/tablet, mobile stacked, links/labels reported correct | **PASS_SCOPED_AGENT_REPORTED** | Screenshot bytes not independently viewed; 320px Reader below initial fold, first-time comprehension not measured |
| W1-IA02 | Creator published method article navigated via CTA, accurate noncommercial positioning | **PASS_SCOPED_AGENT_REPORTED** | Browser trace not independently replayed |
| W1-IA03 | Fiction boundary and spoiler-aware Reader disclaimer, glossary CTA navigated | **PASS_SCOPED_AGENT_REPORTED** | Content-level assessment that glossary has *no surprising master-architecture spoilers* not exhaustively verified; glossary honestly warns of lore |
| W1-IA04 | Public engineering collaborator link via secondary CTA, navigated to published route | **PASS_SCOPED_AGENT_REPORTED** | No external recruiting workflows in scope |
| W1-IA05 | AppDock/Knowledge Bridge anchors reported working | **PARTIAL_WITH_BASELINE_RESIDUALS** | Original criterion also requires LMS/HRM/footer/mobile-nav smoke; complete interactive evidence not provided; known `/#roadmap` and `/#knowledge` anchor defects remain |
| W1-IA06 | Tab/Shift+Tab, focus ring, ARIA and zoom 200% agent-tested | **PASS_SCOPED_AGENT_REPORTED** | Screen reader `NOT_EXECUTED`; not a complete WCAG 2.2 AA audit |
| W1-IA07 | All four viewport measurements show `scrollWidth == clientWidth`; fixed header not reported obstructing CTA | **PASS_SCOPED_AGENT_REPORTED** | Cannot visually examine image screenshots yet; mobile stacked cards require scroll |
| W1-IA08 | Exactly three approved TSX paths; generated `next-env` restored; repo clean aside from scoped edits | **PASS_SCOPED_OPERATOR_AND_AGENT_REPORTED** | Cross-session author hash proof is earlier RC-W1-12R in-session snapshot, not measured by browser agent |
| W1-IA09 | npm ci, typecheck, content validate, build and sitemap from prior operator receipt | **PASS_SCOPED_OWNER_EXECUTED** | 371 warnings are nonfailing per validator; exact release candidate commit/CI SHA does not exist yet |
| W1-IA10 | Unknown route 404; anchors tested and baseline gaps found | **PARTIAL** | Unpublished/draft negative fixture not available/tested, invalid anchor still present; one 404 does not prove no draft leakage |
| W1-IA11 | No form submissions, external auth, AI inference, provider config or deployment claimed | **PASS_SCOPED_AGENT_REPORTED** | Tracker blocking worked for inspected GA domains, not consent control; no account billing or complete network proof, cannot claim globally zero provider traffic |
| W1-IA12 | Deterministic local audit, four named screenshot artifacts and one .webp browser recording claimed; ref/status preserved | **PARTIAL_EVIDENCE_NOT_INDEPENDENTLY_ACCESSIBLE** | Screenshot/recording `file:///C:/Users/.../.gemini/...` paths are owner-local and unavailable to independent reviewer; no candidate commit/PR or independently verified rollback operation |

**Conclusion:** `W1_BROWSER_QA_PASS_SCOPED` is a defensible *agent-reported scoped* result. Do **not** elevate all twelve items to independent unconditional PASS; overall `W1_ACCEPTANCE=PARTIAL_WITH_RESIDUALS`. No evidence in the report of a W1 patch regression requiring immediate scope expansion, but gaps must be explicitly carried.

## 3. New and known issues, with correct attribution

- **Known baseline (P2):** Article/collection breadcrumb links `/#knowledge` while homepage section ID is `knowledge-bridge`. Forward to W2/W7 navigation IA follow-up; not W1 three-file modification authorization.
- **Known baseline (P3):** Legacy mobile/menu `/#roadmap` anchor has no matching target ID. Future navigation follow-up with independent owner-specified scope.
- **Known W4 privacy (P1/owner to triage):** Google Analytics script remains present in `app/layout.tsx` and was blocked by the QA browser. This proves the test session interception was effective for the attempted request, **not** that pre-consent tracking was fixed or no other third-party requests could occur.
- **Acceptance evidence gap:** Draft/unpublished negative route fixture absent; full screen reader / external LMS/HRM click not conducted; screenshots not shared as accessible attachments. Do not manufacture `PASS` for these.
- **Minor agent least-privilege drift (P3 process):** command log includes reading Windows `C:\Windows\System32\drivers\etc\hosts`, which is outside the limited source/browser QA scope and not necessary for the stated W1 tests. No evidence of exfiltration; future instructions should confine reads to required paths. The previous agent's broader off-scope file access was already recorded in RC-W1-13.

## 4. Screenshot and browser artifact provenance

Agent report names:
- `vp01_320x480_1791819486322.png`
- `vp02_375x812_1791819491737.png`
- `vp03_768x1024_1791819497290.png`
- `vp04_1440x900_1791819503296.png`
- `browser_qa_w1_1791819452181.webp`

These are **file URLs on the owner's Windows PC** under Antigravity's artifact directory, not artifact bytes uploaded into this conversation and not GitHub blobs. Reviewer **cannot open or visually independently audit them** and must not invent sandbox URLs for them. A WebP filename alone does not establish that the file is a video recording rather than static/animated WebP. If independent image-level review is required before G3, the owner should attach 320px/375px/1440px screenshots (and 768 if needed) to the chat or an approved evidence file, **without uploading them into the source repository**.

## 5. Relationship to WEB-AC / G3

The original `WEB-AC01` visitor-comprehension outcome is **not proven** by one browser agent session; `WEB-AC02` and the W1 portion of `WEB-AC03/04` have *local scoped* evidence; full `WEB-AC03` spoiler-safe orientation remains PARTIAL; `WEB-AC06` unpublished negative suite NOT EXECUTED; `WEB-AC19` remains open (GA consent); `WEB-AC22` WCAG comprehensive target not satisfied by this narrow QA; `WEB-AC24` exact release-candidate SHA/CI not available yet because three TSX edits remain uncommitted. No statuses in the binding 27-AC ratified contract are globally promoted by this receipt.

**G3 readiness classification:** `G3_CANDIDATE=REVIEWABLE_WITH_RESIDUALS_BUT_NOT_OWNER_AUTHORIZED`, **not** `G3_STARTED`. Recommended next decision is whether the owner wants independent screenshot access plus one small read-only mobile-nav/negative fixture gap check before opening a separate exact-3-file source PR/commit permission. Any G3 commit, push, PR and later G4 Preview need distinct owner authorization. Do not automatically alter old anchors or W4 analytics; those require separately scoped work orders. Main `Reltroner/reltroner-studio` remains unchanged at `18b295f96ccb521b228a1855e79448158c09db15`.

**Unchanged strategic gates:** `G1=APPROVED`, `G2-QA_LOCAL_SOURCE/BROWSER=PASS_SCOPED_WITH_RESIDUALS`, `G3..G8=HOLD`, `PHASE1=NOT_ACCEPTED`, `PHASE2=NOT_ACTIVE`.
