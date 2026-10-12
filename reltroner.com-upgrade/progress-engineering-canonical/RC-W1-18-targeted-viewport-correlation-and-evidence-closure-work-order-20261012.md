# RC-W1-18 — One-Session Targeted W1 Viewport Evidence Closure (Owner-Approved G2 QA Scope Only)

> Status: **WORK ORDER PREPARED / NOT EXECUTED**. Browser QA scope is already owner-authorized, but the assistant has no direct control over the operator's Windows Antigravity browser or localhost. This document does **not** mark W1 evidence closed.
> Source: [RC-W1-17 directly inspected screenshot mismatch](./RC-W1-17-direct-png-evidence-review-viewport-capture-mismatch-and-invalid-webp-20261012.md); [RC-W1-16 acceptance matrix](./RC-W1-16-independent-browser-qa-acceptance-review-and-residuals-20261012.md).
> Allowed runtime: existing production `next start` on **127.0.0.1:3101** from isolated `C:\Projects\reltroner-studio-w1-ia`. Frozen HEAD `18b295f96ccb521b228a1855e79448158c09db15` and exactly three modified TSX paths. No new npm installation, builds, source writes, provider calls, PR/preview/deployment or primary-worktree reads.

## Fault isolated

Previous Antigravity agent report claimed Chrome CSS viewports 320×480, 375×812, 768×1024, and a two-column 768px layout. Directly inspected PNG captures had intrinsic image dimensions **628×484**, **628×899**, **944×985**, with mobile header/stacked cards in the labeled 768px screenshot. Recorded CSS metrics and image artifacts are not coherently correlated. `browser_qa_w1_1791819452181.webp` is only one frame saying “Error generating recording”, **not a QA video**. No app regression or environment viewport manipulation has been proven.

## Single small QA session

**Only three** targets: VP01 320×480, VP02 375×812, VP03 768×1024. Existing VP04 desktop evidence can remain accepted. Agent must use real page viewport/CDP emulation via its actual supported browser tool, **not** outer-window resizing, browser UI screenshots, or changing screenshot dimensions in an editor. Fix `deviceScaleFactor=1` if possible; if not, explicitly report actual devicePixelRatio. Before first localhost navigation, block `*googletagmanager.com*`, `*google-analytics.com*`, `*analytics.google.com*` and related trackers, and verify intercept enabled; do not call providers.

For **each** of the three viewports, in the *same browser page context immediately before capture*, record:

```js
{
  viewportLabel: "VP01 | VP02 | VP03",
  innerWidth: window.innerWidth,
  innerHeight: window.innerHeight,
  docClientWidth: document.documentElement.clientWidth,
  docScrollWidth: document.documentElement.scrollWidth,
  dpr: window.devicePixelRatio,
  visualViewportWidth: window.visualViewport?.width,
  mediaMd: window.matchMedia("(min-width: 768px)").matches,
  creator: document.querySelector('a[href="/blog/no-copypaste-worldbuilding"]')?.getBoundingClientRect().toJSON(),
  reader: document.querySelector('a[href="/blog/asthortera-glossary"]')?.getBoundingClientRect().toJSON(),
  visibleMobileHeader: [...document.querySelectorAll('header')].some(e => getComputedStyle(e).position === "fixed" && e.getBoundingClientRect().width > 0),
  capturedAt: new Date().toISOString()
}
```

The selectors target CTA anchors and **not necessarily full cards**; if agent can reliably identify both card containers, record separate card boxes and computed CSS `gridTemplateColumns`. Never label anchor bounds as full card bounds.

Screenshot via the browser's **actual viewport/page screenshot method**, capture dimensions from decoded resulting PNG file, SHA-256, and associate with exactly that metrics JSON by filename. No screenshots of browser outer window. Evidence PASS only when CSS viewport metrics match target and PNG pixel dimensions are consistent with method and DPR; 768px must report `mediaMd=true` for standard Tailwind md, and responsive header/grid state must agree. At 320/375, the Reader CTA may legitimately require vertical scroll; perform a second scroll or full-page capture only if first capture cannot show Reader reachability. Do not require both entire mobile cards above fold.

## Stop / output

If viewport emulation / screenshot API inaccessible, `SCREENSHOT_CAPTURE_UNVERIFIABLE` and STOP; **do not loop endlessly**, reinstall browser tool, record fake values or reshoot all previous QA. Only a single controlled attempt is authorized for this work order; any retry needs a specific reason and owner decision. Do not chase failed WebP recorder.

Package **three verified PNGs plus one metrics/manifest text or JSON** in one ZIP in user's Downloads, preserving original files, no cloud upload. Operator uploads one ZIP into this conversation. For each VP report screenshot pixel size, devicePixelRatio, DOM client/scroll width, `mediaMd` and user-visible Creator/Reader state. Recheck read-only Git: exactly three TSX modified, `next-env.d.ts` unmodified, same HEAD; stop server only at owner convenience. No personal/Windows host-file reads.

Evidence closure decision by reviewer only AFTER uploaded ZIP: `W1_IA07=PASS_SCOPED_CORRELATED` or `PARTIAL_TOOL_LIMITATION` or `FAIL_REAL_RESPONSIVE_REGRESSION`. W1-IA05 (broader nav) and W1-IA10 (unpublished negative fixture) remain separate outstanding proofs. **No G3 grant implied.**
