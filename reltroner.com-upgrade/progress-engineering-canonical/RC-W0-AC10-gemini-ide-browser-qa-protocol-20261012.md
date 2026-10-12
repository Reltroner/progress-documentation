# RC-W0-AC10 — Gemini IDE Browser-QA Protocol (Agent Prompt + Scope Gates)

> 2026-10-12 Asia/Jakarta. **PROPOSED QA WORK ORDER**, documentation-only; W0 remains read-only. This work order is not a source edit, agent permission expansion, new worktree authorization, or `npm run dev` exception.
> Binding documents: [W0](../02-w0-00-read-only-discovery-work-order-20261012.md), [Workspace/release governance](../05-source-workspace-and-release-governance.md), [WEB AC crosswalk](../03-phase1-acceptance-and-invariant-traceability.md).
> Studio remote GitHub baseline: `18b295f96ccb521b228a1855e79448158c09db15`; Windows primary checkout baseline: `d6969ddfbc5e7d98d49b1523259785125159e722` (11 commits behind), 14 protected untracked Markdown files. Verify live SHA anew before any code work.
> Owner preference: delegate QA to Gemini IDE rather than many manual screenshots. No claims about installed IDE agent browser tooling.

## Boundary between W0 and later browser tests

**Now permitted by existing W0:** source inspection without edits, Git read-only status/source comparison, inspection of user-supplied screenshots, and read-only browser exploration of existing public website (if an existing browser control capability is available), without submitting forms, sending analytics test events intentionally, changing cookies/privacy settings, or activating services. Normal page loads may generate ordinary production requests.

**Deferred until new explicit owner authorization:** running `npm run dev` in a newly isolated worktree at a verified remote exact SHA. Next.js dev mode generates/updates `.next` and may create files; doing so in protected primary checkout conflicts with strict W0 no-writes policy. Even after authorization, npm `install`, `update`, `npx`, broad source edits, fixture creation, Git writes and provider actions remain independently gated. Starting a localhost server from historical local HEAD cannot be labeled production parity.

## Full single-paste prompt for Gemini IDE agent

~~~text
ROLE: QA investigator (NOT coding agent). PROJECT: reltroner.com Phase 1, RC-W0-AC10.
LANGUAGE: Report in Indonesian with precise technical terms. MODE: STRICT READ-ONLY DISCOVERY.
YOUR DUTY: Run one comprehensive, traceable, non-destructive audit. DO NOT implement fixes.

AUTHORITATIVE CONTRACTS:
- https://github.com/Reltroner/progress-documentation/blob/main/reltroner.com-upgrade/02-w0-00-read-only-discovery-work-order-20261012.md
- https://github.com/Reltroner/progress-documentation/blob/main/reltroner.com-upgrade/03-phase1-acceptance-and-invariant-traceability.md
- https://github.com/Reltroner/progress-documentation/blob/main/reltroner.com-upgrade/05-source-workspace-and-release-governance.md
- https://github.com/Reltroner/progress-documentation/tree/main/reltroner.com-upgrade/progress-engineering-canonical
Remote studio expected at entry: 18b295f96ccb521b228a1855e79448158c09db15.
Local primary historical HEAD: d6969ddfbc5e7d98d49b1523259785125159e722.

HARD NO: No edit, no patch, no format, no create/delete files in Studio checkout. Do not run git fetch/pull/reset/clean/checkout/worktree/add/commit/push, npm install/update/npx, build/clean/content scripts, deployment/redeploy, HTTP POST, form submit, production email, create provider credentials, DNS edits, paid APIs or Cloudflare AI inference. Never stage 14 untracked Markdown under content/music and content/places. No secret or .env reading/output. Do not claim browser checks passed if browser control is unavailable.

PRE-FLIGHT A: SOURCE SNAPSHOT
1. Read-only git -C C:\Projects\reltroner-studio remote get-url origin; branch --show-current; rev-parse HEAD; status --porcelain=v1 --untracked-files=all; worktree list --porcelain.
2. Require correct origin/branch, zero tracked modifications, 14 previously protected untracked Markdown. If changed, STOP and only report.
3. Note local HEAD differs from remote 18b295f. Label all locally derived source results HISTORICAL_LOCAL, not production.
4. Inspect existing source files only (do not modify): components/MobileNavbar.tsx, CommandPalette dialog, CollectionPageClient.tsx, ContentEntryPage.tsx, global layout, app/contact, and shared content and route definitions. Cite source path/line.

PRE-FLIGHT B: BROWSER CAPABILITY
Check whether your IDE has a *pre-installed* browser automation/DevTools interface. If absent, report BLOCKED_BROWSER_AUTOMATION and provide exact reproducible manual DevTools operations. Do not install Playwright/Puppeteer/browser drivers or spawn a separate browser through npx. Do not improvise unseen screenshots or DOM outputs.

RUN MODE 1 — READ-ONLY PRODUCTION BASELINE, AVAILABLE NOW
Use https://www.reltroner.com/ only through existing browser capabilities, with no forms submitted and no privacy-setting modifications. Production results are an observation at deployed source baseline, not proof of all accepted paths.

CRITICAL ROUTES:
- /
- /philosophies
- /philosophies/agile-vs-waterfall-analogy
- /contact
Optional, if present and public: /places, one /places/[slug], /blog, /about.

DEVICE MATRIX (measure actual CSS viewport; do not substitute physical screen pixels):
- 320x480 iPhone 4 emulation
- 375x812 mobile representative
- 768x1024 tablet
- 1440x900 desktop

FOR EACH ROUTE/VIEWPORT:
1. Capture path, mode, viewport width/height, timestamp, effective URL, and whether route navigated successfully.
2. Detect root/body horizontal overflow; document element.scrollWidth vs clientWidth and any scrollable descendants that force page-level overflow. Do not conflate intentionally scrollable breadcrumb/chip rail with unintended page overflow.
3. Inspect fixed mobile header: overlap with heading, breadcrumb, focused links, article text and CTA at scrollTop 0, 50%, and deep-scroll. Header may intentionally overlay background, but must not make interactive content unreachable or hide focused controls.
4. Inspect mobile drawer open/close, ESC, overlay click, focus-entry, focus-return, background scroll lock, scrollable drawer content, search transition, and any keyboard trap. Mark interaction untested if browser keyboard isn't available.
5. Check search launcher Ctrl+K desktop and mobile search icon; keyboard and focus behavior; no independent fake search results. Do not use unpublished strings as probes against public production.
6. Breadcrumb legibility / clipping at 320px, accessible text, navigation links, and wrapping.
7. Archive taxonomy chips: readability, excessive multi-line chips, tap targets, wrapping and focus.
8. Article title, anchor navigation/ReadingPath, focus/scroll behavior and prose width. Verify same article accessible from collection.
9. Hero Creator vs Reader pathways and actual destinations; mark absent or ambiguous, do not invent a website feature.
10. Image load/404 behavior and alt/fallback (only inspect loaded public network, no purge). Record exact HTTP statuses without tokens.
11. Console errors and uncaught exceptions, distinguishing pre-existing expected 404 from new route errors.
12. Basic WCAG 2.2 AA targets: semantic landmarks/headings, keyboard, focus visible, tap targets ~24 CSS px minimum with 44px usability preference, contrast signals, prefers-reduced-motion if inspectable, and 200% zoom (if browser supports it). Do not claim full WCAG compliance from spot checks.
13. On /contact, inspect field labels, required markers, submit disabled/error states without submitting; never send a real message.
14. On other pages, do not activate Open LMS links to private/account workflows; only inspect href and active/planned labels.
15. No screenshots of browser account tabs, API keys, private subscribers, Resend billing address, cookies or authorization headers.

MEASUREMENTS: Use actual UI and DevTools outputs. For example, scrollWidth/clientWidth, boundingClientRect of nav/heading and focused item, document.activeElement, performance/resource request summaries. If tool capability absent, report NOT_EXECUTED, do NOT assume.

RUN MODE 2 — LOCAL DEV QA, DEFERRED:
The owner proposes npm run dev. This is NOT authorized by the W0 read-only contract in the protected primary checkout: Next dev creates/updates .next. Do not run it now. After separate owner approval for a clean isolated worktree created from an exact verified remote main SHA, and preinstalled node_modules/tooling verified, the human operator may start:
  npm run dev
with localhost-only binding, explicitly recording the port, compile status and generated cache path. Never install missing dependencies automatically. Rerun the same device/route matrix against localhost and compare with production. Note local dev may behave differently from production; report differences, don't infer production behavior. No public provider forms/email tests.

OUTPUT CONTRACT (NO FILE WRITES IN PRIMARY):
Header: RC-W0-AC10; timestamp, actor, browser capability, tested URL modes, Git HEADs, local status, deployment SHA if known.
Table per route/viewport: navigation, horizontal overflow, sticky/fixed overlay, keyboard, focus, drawer, anchors, images, console, and result PASS_SCOPED / PARTIAL / FAIL / BLOCKED / NOT_EXECUTED.
Issue ledger: ID, severity P0/P1/P2, exact reproduction, expected vs actual, screenshot/DOM evidence, likely owning source file(s), WEB-I/WEB-AC references, scope/false-positive caveats, security/privacy impact.
P0 = public draft/security or unreachable critical workflow; P1 = mobile nav clipping/keyboard trap/broken required CTA; P2 = excessive spacing/tag visual polish.
Exit receipt: #checks observed/blocked (not guessed), reproduction coverage, unchanged Git status after, protected 14-file integrity, zero provider configuration changes, zero incremental billing activation, residuals and recommended W1/W2/W4 engineering fixes. STOP if source drift or status unexpected.
Do NOT mark all PASS merely because npm build is green. No PR, no implementation, no merge, no deploy.
~~~

## Operator guidance

1. In Gemini IDE, paste the entire prompt and request **Run Mode 1 only** while W0 is open.
2. If Gemini lacks a browser tool, source-only inspection can be recorded but browser test remains NOT_EXECUTED; use ordinary Chrome DevTools as a separate operator.
3. To conduct Run Mode 2, finish/approve the W0 gate and create an independently authorized exact-SHA isolated worktree first; do not run `npm run dev` or `npm install` on primary checkout during current W0. Document any narrower exception explicitly if the owner later chooses it.
4. Deliver redacted report into the conversation; reviewer will classify it and archive sanitized evidence to [canonical folder](./README.md) without publishing private screenshots.

## Acceptance mapping

WEB-I03 / WEB-AC01–04: Creator/Reader entry and collaborator lens.
WEB-I06 / WEB-AC07: shared archive/index search.
WEB-I07 / WEB-AC08–09: responsive rails, focus, mobile navigation.
WEB-I08 / WEB-AC10–12: asset loading/fallback.
WEB-I13 / WEB-AC19/20: third-party and embed safety (only observe).
WEB-AC22: accessibility target, not certification.
W0-AC10 remains PARTIAL until real tested evidence and owner review.
