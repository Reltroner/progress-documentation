# RC-W1-17 — Direct ZIP/PNG Evidence Review: Visual Desktop Pass, Viewport Screenshot Mismatch, Invalid WebP Recording

> **Source:** Owner-uploaded binary ZIP attachment `RC-W1-16-Browser-QA-Evidence-20261012.zip`; archive SHA-256 `11e753dbaf9939cec948e1123cc55e8ab481d304a2c5969ec8b1ab5787a51cd4`; archive size **980,248 bytes**.
> **Review execution:** Independent reviewer actually opened ZIP, checked zip integrity, decoded all **four PNGs**, compared file SHA-256 against `manifest.txt`, decoded optional WebP and inspected RIFF chunks and rendered content. This is **DIRECT_FILE_CONTENT_VERIFICATION**, not an agent-only written assertion. No Studio application source modifications.
> **Previous receipts:** [RC-W1-16 independent QA review based on owner-agent browser report](./RC-W1-16-independent-browser-qa-acceptance-review-and-residuals-20261012.md); [RC-W1-15 successful owner restoration & browser QA readiness](./RC-W1-15-one-file-restore-pass-browser-qa-ready-20261012.md); [original W1-IA01..12 acceptance contract](./RC-W1-01-proposed-g2-first-contact-creator-reader-ia-work-order-20261012.md).
> **Current disposition:** `ZIP_INTEGRITY=PASS`, `PNG_4_OF_4=DECODABLE_HASH_MATCH`, `DESKTOP_VISUAL=PASS_SCOPED`, `MOBILE_AND_TABLET_SCREENSHOT_PROVENANCE=INCONSISTENT`, **`WEBP_RECORDING=INVALID_AS_QA_RECORDING`**, `BROWSER_AGENT_MEASUREMENTS=REPORTED_NOT_INDEPENDENTLY_REPLAYED`, `W1_IA07=PARTIAL_PENDING_TARGETED_RECAPTURE`, `G3..G8=HOLD`.

## 1. ZIP integrity and artifact proof

Python's `ZipFile.testzip()` returned no corrupt entries. There are 6 expected archive members: 4 PNG screenshots, `manifest.txt` and optional WebP. The four PNG's hashes and byte sizes match the manifest (case-insensitive SHA-256 comparison).

| Manifest target | Actual decoded PNG pixel dimensions | Byte size | SHA-256 first 16 |
|---|---:|---:|---|
| VP01: 320×480 | **628×484** | 131,681 | `10da6167151dc8f4` |
| VP02: 375×812 | **628×899** | 203,670 | `94e138e1db901f43` |
| VP03: 768×1024 | **944×985** | 270,867 | `db02b56fc7f0f972` |
| VP04: 1440×900 | **1784×985** | 371,852 | `f44ad1ed935bf57b` |

**Critical distinction:** Screenshot raster dimensions need not equal CSS viewport when display scaling / devicePixelRatio / full-window screenshot including chrome differs. Therefore the mismatch alone does not prove that the browser agent failed to set CSS viewport metrics. However, the images themselves contain additional contradictions with the agent's simultaneous claimed responsive state; as provided, these are **insufficient independent screenshot proof of the labeled CSS viewport states**. Manifest conjecture about “Windows Chromium minimum-window-frame width limits” is **not an independently verified capture explanation**.

## 2. Direct visual findings

**VP04 desktop screenshot:** Both `For Creators` and `For Readers` cards are shown side-by-side with consistent geometry, clear high-contrast headings and full CTA buttons, equivalent prominence, legible English explanatory copy, and explicitly labeled Reader lore preview. Search bar and desktop navigation visible. This independently supports `W1-IA01=PASS_SCOPED_DESKTOP_VISUAL` and the *visual presence* of a spoiler-aware disclaimer; it does not alone prove keyboard behavior, semantic ARIA association or browser HTTP navigation.

**VP01 screenshot labeled 320×480:** actual canvas 628×484; mobile navigation visible; hero and only the **top portion of the Creator card** is in the capture. Reader is not shown. On-image layout/text span approximately the same 628px capture width as VP02, not a separately distinguishable 320px screenshot. This cannot independently establish Creator/Reader reachability under actual 320px CSS viewport or full card/CTA accessibility on a 480px-tall viewport. Vertical scroll is legitimate; absence of Reader on initial fold is not by itself a defect.

**VP02 screenshot labeled 375×812:** actual canvas 628×899; mobile navigation and stacked cards visible, but Reader card disclosure/button extends beyond bottom of capture. Comparing the top 484 pixel rows to VP01 shows nearly the same rendered layout and wrapping, consistent with a *same-width screenshot capture* with different heights rather than clear evidence of two distinct CSS widths. Do not claim it proves 375px responsive state just from filename.

**VP03 screenshot labeled 768×1024:** actual canvas 944×985; it visibly has the **mobile hamburger/header** and single-column stacked Creator/Reader cards. The prior browser agent report described this viewport as **two equal 352px-wide cards in a two-column grid** with desktop behavior. The **image and reported state are inconsistent**. The frozen source `MobileNavbar.tsx` uses Tailwind `md:hidden` for the mobile header, further suggesting the screenshot was not captured at the same CSS responsive state as the purported 768px measurements (given standard Tailwind md threshold; source project config could override). Do NOT infer application bug from this mismatch; targeted browser screenshot instrumentation must correlate CSS viewport, media-query result, DPR and actual image geometry in one atomic capture.

**VP01/02/03 verdict:** No obvious clipping of the *portion that is visible*, text is legible, dark contrast readable, and CTA color is high-contrast in VP02/03. But viewport claims are not independently verifiable from these screenshots and not all CTA actions fit in crop. `W1-IA07` should be downgraded from unqualified PASS_SCOPED to **PARTIAL_EVIDENCE_CONFLICT** pending minimal corrected screenshots. No source fix indicated.

## 3. Optional WebP is NOT a recording — confirmed

Manifest claims `browser_qa_w1_1791819452181.webp` is a valid animation of full QA. Direct decoding proves otherwise:
- WebP size 11,800 bytes; canvas 960×960; PIL `n_frames=1`.
- RIFF chunks: `VP8X`, `ICCP`, `VP8 `; **no `ANIM` or `ANMF` animation chunks**.
- The only image is a gray placeholder displaying the text **“Error generating recording”**.

Thus `WEBP_DECODABLE=TRUE`, **`WEBP_IS_BROWSER_RECORDING=FALSE`**, and the manifest's recording claim is factually incorrect. Do not keep `W1-IA12` full acceptance based on that file. The four screenshots remain useful visual evidence and were not fabricated merely because the optional recorder failed.

## 4. Revised independent acceptance relevance

- `W1-IA01`: **PASS_SCOPED_DESKTOP**, mobile screenshot evidence PARTIAL. First-time visitor-comprehension test still missing (WEB-AC01).
- `W1-IA03`: Reader disclaimer visibly truthful on desktop; ARIA association and page navigability remain agent-reported, not proven by static PNG.
- `W1-IA06`: keyboard/zoom remains **AGENT_REPORTED_PASS_SCOPED**, not independently visible; 4 screenshots do not prove 200% zoom or Tab behavior.
- `W1-IA07`: **PARTIAL_EVIDENCE_CONFLICT** because VP01, VP02, VP03 screenshot capture states do not corroborate their reported 320/375/768 geometries. Original browser-agent scrollWidth measurements remain *reported* but not independently correlated to screenshot viewports.
- `W1-IA12`: **PARTIAL**; 4 image artifacts validated, but no usable browser recording and capture provenance contradicts labels; rollback/candidate SHA not yet established.
- `W1-IA05`: **PARTIAL**, known `/#knowledge` and `/#roadmap` baseline, broader nav interaction not evidenced.
- `W1-IA10`: **PARTIAL**, unpublished negative fixture missing.
- Prior npm ci, typecheck, content validation and one successful 440/440 Next build remain PASS_SCOPED. No new patch-level browser regression has been independently demonstrated.

## 5. Minimal targeted corrective action (no repeat full QA)

Use already-installed Antigravity browser agent on the same localhost production build. **Do not redo install, build, all routes or full W1 flow**.

Capture **only VP01 (320×480), VP02 (375×812), VP03 (768×1024)** using browser viewport/CDP emulation (not resizing browser outer window), and collect in the same frame/capture session:

1. `window.innerWidth`, `document.documentElement.clientWidth`, `document.documentElement.scrollWidth`, `window.devicePixelRatio`, `window.visualViewport.width`, and `window.matchMedia('(min-width: 768px)').matches`.
2. Computed `display`, DOM bounding rectangles of primary Creator/Reader cards (and whether layout is single or two-column), and navbar mobile/desktop visibility.
3. Capture viewport screenshot using true browser page/viewport screenshot API, ideally `deviceScaleFactor=1` so PNG intrinsic width equals emulated CSS viewport. **Do not rely on Win32 OS window screenshot** or naive screenshot filename. Correlate screenshot file SHA256 and telemetry recorded immediately before the image capture.
4. If browser tool cannot supply true viewport image, report `SCREENSHOT_CAPTURE_UNVERIFIABLE`; do not mislabel.
5. Copy three new screenshots and one text manifest with these actual browser metrics into one ZIP under Downloads; keep originals intact. Human owner should only attach one ZIP to the current conversation, no source files or providers.

Do not claim a real browser recording or spend time repairing recorder. The optional WebP is a deterministic failure artifact; only screenshot QA needed for this evidence gap.

## 6. Release and security boundary

This RC-W1-17 report is a **documentation-only revision**. Source application main remains unchanged at frozen SHA as previously verified; local three TSX W1 changes remain not committed/pushed. No code edit, npm install/build, network provider config, billing, PR, Vercel Preview, merge or deployment. Browser agent must not read unrelated home/Windows files or upload evidence outside the owner-selected ChatGPT channel. **G3 requires separate owner decision.** Full 27 WEB-AC (including privacy consent, unpublished negative suite and WCAG 2.2 AA) remain mandatory. `WEB_PHASE1=NOT_ACCEPTED`, `PHASE2=NOT_ACTIVE`.
