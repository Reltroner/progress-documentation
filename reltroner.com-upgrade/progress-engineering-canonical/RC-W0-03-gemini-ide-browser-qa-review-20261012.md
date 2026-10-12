# RC-W0-03 — Independent Review of Gemini IDE Browser QA (2026-10-12)

> **Receipt classification:** REVIEWED_WITH_QUALIFICATIONS / W0-AC10 **PARTIAL**.
> **Phase:** Reltroner.com Phase 1 → W0 read-only discovery IN PROGRESS, not W0 owner acceptance.
> **Owner-supplied evidence:** Gemini IDE QA transcript/reported audit dated `2026-10-12T08:45:00+07:00`. The full report was submitted as a generated pasted text artifact in the conversation; this published receipt is **sanitized and reviewer-normalized**, not a verbatim replication of unverified browser measurements.
> **Evidence boundary:** GitHub source independently inspected by ChatGPT at Studio SHA `18b295f96ccb521b228a1855e79448158c09db15`; GitHub resource previous baseline `6c6fb38f8ff3376c0789c15bcfe4d0cafc4d057e`. **Browser actions, screenshots, DOM metrics, and local Git status are reported by Gemini agent, not independently executed by ChatGPT.**
> **Governance:** [W0 work order](../02-w0-00-read-only-discovery-work-order-20261012.md) · [Architecture](../00-ratified-frontend-architecture-contract-20261012.md) · [WEB acceptance](../03-phase1-acceptance-and-invariant-traceability.md) · [IDE QA protocol](./RC-W0-AC10-gemini-ide-browser-qa-protocol-20261012.md).
> **Cost:** No paid provider action reported. This documentation update does not authorize any source/provider mutation.

## 1. Operator report provenance and preserved state

Gemini reports a read-only git preflight and post-audit at `C:\Projects\reltroner-studio`, origin `https://github.com/Reltroner/reltroner-studio.git`, branch `main`, local HEAD `d6969ddfbc5e7d98d49b1523259785125159e722`, zero tracked edits, one primary worktree, and all 14 prior protected untracked Markdown files intact (12 music / 2 places). This is **OWNER-SUPPLIED_AGENT_REPORT**; individual local file hashes and direct independent terminal verification from this exact run were not available. The historical local checkout remains 11 commits behind inspected remote production SHA, and the report correctly distinguishes source inventory as `HISTORICAL_LOCAL`.

The agent lists visits to six public routes: `/`, `/philosophies`, `/philosophies/agile-vs-waterfall-analogy`, `/contact`, `/about` and `/places`. It reports browser capability through preinstalled Chromium/Playwright-style automation, but **native window could not be resized under approximately 502 CSS px**. A purported `320x480` isolated frame test was used instead. The iframe emulation's relationship to top-level viewport CSS media queries, visual viewport dimensions, focus behavior, viewport units, and mobile touch semantics was not established. Do not upgrade that simulated frame observation to native 320px end-to-end PASS.

No source modifications, `npm run dev`, installation, provider operations, form POST, or production changes are reported. The agent's unqualified wording `ZERO WRITE` refers to tracked/visible Git state, not proof that no untracked build/cache/browser files were touched; no cache/filesystem audit is provided.

## 2. Finding classification (preserve report facts, correct acceptance mapping)

| ID | Claimed defect / observation | Reviewer classification | Source and evidence | Ratified owner mapping |
|---|---|---|---|---|
| W0QA-01 | Production `/contact` renders reCAPTCHA unconfigured warning and disabled `Send Message` | **CONFIRMED_IN_SCOPE / P1 USER JOURNEY**; does NOT mean permanently broken in all environments | GitHub `components/sections/ContactForm.jsx`: `isCaptchaConfigured = Boolean(NEXT_PUBLIC_RECAPTCHA_SITE_KEY)`, `canSubmit = isCaptchaConfigured && verified`, disabled button. Public observed state is agent-reported, not independently replicated | **W6**, WEB-I11, **WEB-AC18**; privacy WEB-AC19. Agent incorrectly mapped it to WEB-AC08 (reading rails) and WEB-I10 (AI) |
| W0QA-02 | Creator/Reader first-contact paths absent from homepage hero | **CONFIRMED SOURCE GAP / P1 IA** | `components/ecosystem/EcosystemHero.tsx` exposes Explore Ecosystem, Browse Knowledge Base, Open LMS. `UseCasePathways.tsx` provides later `For builders` and `For lore readers`, insufficient by itself for approved first-contact two-route specification. Comprehension/real user testing remains pending | **W1**; WEB-I03, WEB-AC01–04 |
| W0QA-03 | `/images/background.webp` request returns HTTP 404 | **CONFIRMED_BROWSER_EVIDENCE / P2** | `components/layout/ShellBackdrop.tsx` explicitly references image; production 404 previously documented via owner network capture. Studio `.gitignore` contains `public/images/`, and local owner discovery saw image present locally but absent in remote tree; likely ignored local-only asset omitted at deploy. | **W3**, WEB-I08, WEB-AC10–12; W0-AC04. It is not proven to be a jsDelivr edge-cache bug. |
| W0QA-04 | Native Chromium browser window cannot reach 320px | **TOOL_CAPABILITY_LIMIT, not product defect** | Agent reports lower bound ~502 CSS px and fallback via isolated frame | W0-AC10 test evidence limitation; not product P2 issue |
| W0QA-05 | Fixed header overlays upper viewport while deep-scrolling | **UX OBSERVATION / P2_CANDIDATE**, not conclusive accessibility failure | `MobileNavbar.tsx` uses `fixed top-0 z-[100]` plus first-fold spacer. A fixed overlay can be intentional; need element rects and focus/anchor target measurements to prove obstruction/unreachability. | **W2** responsive rails, WEB-I07, WEB-AC09, WEB-AC22 spot checks |

Additional concern: report labels 320px `PASS_SCOPED` when it relied on iframe and does not show equivalent top-level viewport results, and labels `PASS_SCOPED` for routes with known 404 and incomplete keyboard/zoom coverage. Interpret such PASS statements narrowly (load/render or selected interaction observed), not as full route acceptance. Likewise, `15/15 categories` and `100% reproduction coverage` are **unsupported aggregates**: a route matrix contains mixed simulated viewport conditions, unmeasured accessibility subtests and unexecuted localhost mode.

## 3. Detailed negative test and security caveats

- **Horizontal overflow**: `documentElement.scrollWidth === clientWidth` is useful, but `overflow-x-clip` in `app/layout.tsx` may mask cut-off descendants. Must additionally inspect out-of-viewport element bounding boxes, clipped focus targets, long tags, reachable breadcrumb scroll and narrow viewport screenshots. Do not infer `WEB-AC09 PASS` from zero document-level scroll alone.
- **Keyboard / dialog**: the source includes accessible button names and Headless UI / cmdk dialog primitives. The agent reports desktop Ctrl+K, focus input and Escape close, as well as drawer open/close, but **no complete tab-order/focus-restoration/keyboard-trap trace per route and viewport**. Pending focused-element evidence after closing and switching drawers.
- **Contact form**: current submit gate is disabled in the observed production environment. Zero sends and disabled form do not prove all error pathways; no provider accepted/rejected/timeout or anti-spam validation was performed. Agent's blanket conclusion `no security/privacy risk` is not proven; avoid collecting data before W6 acceptance. No reCAPTCHA/private keys should be pasted.
- **Other unresolved cross-cutting**: draft route/publication negative fixtures, Markdown `sanitize:false`, external embeds/GA cookies, AI scope/inference, sitemap truth and performance cannot be marked PASS by this browser spot audit.
- **WCAG 2.2 AA**: heading/ARIA/tap-target spot checks are progress evidence, **not** WCAG conformance or complete zoom/focus/contrast/motion acceptance. The report did not demonstrate 200% zoom end-to-end.

## 4. Correct ratified workstream priority, no unauthorized resequencing

The agent recommendation names were **incompatible with the ratified architecture** (`W1 Contact`, `W2 IA`, `W4 Assets`). Correct original scope:
- **W1 Information Architecture / taxonomy** → Creator/Reader first-contact design; preserve content routes/slugs. Confirm owner W1 scoped authorization after W0 acceptance.
- **W2 navigation/search/sidebars** → mobile rails, focus, command-palette and content navigation after W1 public index contract.
- **W3 asset freshness & rendering** → background 404, immutable jsDelivr resource pin, fallbacks, screenshot/network tests.
- **W4 privacy/security** → GA/iframe/unsafe Markdown and security negative suite.
- **W5 Navigator AI** → provider quota, public grounding and no-spend fail-closed tests.
- **W6 contact and newsletter** → Web3Forms Free contact and Resend account/domain readiness, acceptance vs delivery states; Resend sender `resend.reltroner.com` still `Failed` in owner screenshot.
- **W7 E2E/release** → independent preview, build, accessibility, cost, browser and production gates.

Severity assignment is pragmatic review triage, not proof of end-user impact frequency. The architecture's W6 gating cannot be silently moved to W1 because contact fails today; if a safety/availability emergency requires an exception, use an explicit owner-ratified change order before mutating source.

## 5. Acceptance disposition

| Item | Result | Residual |
|---|---|---|
| Local source protection / preflight | PASS_SCOPED_AGENT_REPORTED | Actual source file integrity not independently hashed; 14 paths currently reported preserved |
| Production desktop route/navigation spot checks | PASS_SCOPED_AGENT_REPORTED | Limited routes/interactions; do not treat as W7 acceptance |
| 768px tablet spot check | PARTIAL_AGENT_REPORTED | No complete matrix of focus/zoom/privacy tests |
| Native mobile 375px / 320px automated end-to-end | **NOT_EXECUTED_AS_NATIVE** | 320px isolated iframe is an indication only; operator Chrome DevTools screenshots from earlier session exist |
| Contact user journey | **FAIL_OBSERVED / P1** | Disabled in observed production, eventual W6/provider verification needed |
| Creator/Reader first-contact IA | **FAIL_SPEC / P1** | No ratified two-path explicit CTA in hero |
| Broken image | **FAIL_OBSERVED / P2** | missing Git-tracked deploy asset, future W3 |
| Mobile overlay accessibility / focus | **PARTIAL** | exact focus/anchor overlap trace pending |
| Fully enumerated WCAG/negative suite, 200% zoom | **NOT_VERIFIED** | full accessibility assurance belongs later W7 |
| Overall W0-AC10 | **PARTIAL — DISCOVERY SUFFICIENT TO RECORD DEFECTS** | Need remaining evidence or owner-approved W0 deferral; **not** website PASS |

## 6. Operator next steps (only within existing W0)

1. Ask IDE Gemini to append a narrow **read-only supplemental QA result**, not rerun all six routes. Explicitly separate native browser CSS viewport `320x480` from an embedded `320px` iframe. Never claim browser width 320 if top-level CSS viewport remains 502.
2. Verify mobile focus restoration after Escape, anchor scroll positions versus fixed header, 200% zoom and genuine visible clipping using existing browser DevTools. If browser automation cannot achieve native mobile viewport, mark native as NOT_EXECUTED and rely on human Chrome Device Mode evidence. Do not install drivers or use new source tooling.
3. Keep W1–W7 on HOLD. No local `npm run dev` in the primary checkout; exact remote source SHA isolated worktree can be used only after separate authorization. Never use the existing historical local checkout as production parity.
4. Continue W0 account/provider hard blockers (Resend failed domain diagnostics, Cloudflare Workers AI entitlement and Vercel per-project attribution). W0-AC12 final owner acceptance still pending.

**Receipt decision:** accept the agent's useful observed defects as evidence, reject overstated universal PASS/coverage claims, and keep W0-AC10 **PARTIAL**. No fixes executed. No W1, vendor, merge or production authorization granted.

## 2026-10-12 superseding correction — R1 browser revalidation

**Read before relying on the W0QA-01 P1 claim in this historical document.** Gemini's later read-only browser revalidation reports an **active reCAPTCHA v2 iframe and no missing-site-key warning on production**; the `Send Message` button remained disabled because CAPTCHA was deliberately not solved during W0. GitHub code `canSubmit = isCaptchaConfigured && verified` confirms that disabled-by-default is intended gate behavior and **does not prove the public form broken**. Therefore the first agent's assertion of missing reCAPTCHA configuration is contradictory and **the contact-outage P1 designation is withdrawn pending real authorized delivery testing**. The legacy Formspree/Web3Forms and fallback-contact requirements remain W6 gaps. No secret/site-key literal is reproduced here.

The R1 measurement of one anchor at 502 CSS px found header.bottom = heading.top = 60px, so that heading was not obscured in that case. R1 additionally reported focus restoration on Escape and the drawer-to-palette focus transition as scoped positives. Native 320/375 CSS px and 200% zoom remained **NOT_EXECUTED**, and W0-AC10 remains **PARTIAL**. These superseding findings and precise provenance are archived in [RC-W0-04 independent R1 review](./RC-W0-04-gemini-qa-targeted-revalidation-review-20261012.md). Historical initial results above are retained for audit traceability rather than silently rewritten.
