# RC-W0-04 — Independent Review: Gemini RC-W0-AC10-R1 Targeted Revalidation

> Date: 2026-10-12 Asia/Jakarta; owner-supplied agent timestamp `2026-10-12T08:54:30+07:00`.
> **Disposition:** NEW TARGETED EVIDENCE ACCEPTED WITH QUALIFICATIONS; W0-AC10 **PARTIAL**; W0 and Phase 1 gates unchanged.
> Source baseline independently inspected: `Reltroner/reltroner-studio` GitHub `main` at `18b295f96ccb521b228a1855e79448158c09db15`. Agent's historical local Windows checkout remained `d6969ddfbc5e7d98d49b1523259785125159e722` (11 commits behind remote).
> Evidence class: OWNER-SUPPLIED GEMINI IDE BROWSER/TERMINAL REPORT, with independently verified GitHub source control logic. Browser DOM dimensions and GUI account state were **not** rerun independently by the reviewer.
> Parent: [RC-W0-03 initial independent review](./RC-W0-03-gemini-ide-browser-qa-review-20261012.md), [RC-W0-AC10 QA protocol](./RC-W0-AC10-gemini-ide-browser-qa-protocol-20261012.md), [W0 order](../02-w0-00-read-only-discovery-work-order-20261012.md), [acceptance crosswalk](../03-phase1-acceptance-and-invariant-traceability.md).
> **Privacy and secrets:** ReCAPTCHA public site-key literal, browser profile/account identifiers and private contact identifiers intentionally omitted. No form POST, CAPTCHA solution, delivery test, changes to source/providers or production are claimed.

## 1. Delta against RC-W0-03: reclassifications required

### W0QA-01 — Contact CAPTCHA gate: earlier P1 malfunction claim NOT CONFIRMED

The original Gemini audit reported an absent reCAPTCHA public site key plus an unconfigured warning. **The later R1 agent directly contradicts that observation**, reporting a configured reCAPTCHA v2 iframe in the production browser and **no unconfigured-warning text**. GitHub `components/sections/ContactForm.jsx` independently confirms:

```javascript
const isCaptchaConfigured = Boolean(recaptchaSiteKey);
const canSubmit = isCaptchaConfigured && verified;
// button: disabled={!canSubmit}
```

Therefore **a disabled Send Message button before a user completes CAPTCHA is expected initial UI behavior, not a confirmed production form outage**. Reclassify W0QA-01 from `P1 CONFIRMED_CONTACT_FAILURE` to `EXPECTED_CAPTCHA_GATING / DELIVERY_UNVERIFIED`. Do **not** assert that Google reCAPTCHA is unconfigured on current production based on the superseded initial report. Exact causes of the conflicting observations (time/config change, agent error, browser timing) remain unknown.

Actual unresolved W6 requirements: legacy Formspree endpoint, independent Web3Forms Free contact path, missing apparent direct fallback in the page body (agent found only footer recruiter link, not independently checked across every site route), anti-spam behavior, provider accepted/rejected/timeout handling, truthful success vs delivered state and privacy disclosure. These remain **W6 / WEB-I11 / WEB-AC18** (and privacy WEB-I13/WEB-AC19), **not** WEB-AC08. No successful CAPTCHA+form submission was attempted; form availability after solve remains UNKNOWN.

### W0QA-05 — Fixed mobile navbar: scoped anchor non-obstruction, NOT blanket failure

Agent-reported production browser measurements at **502 CSS px top-level viewport** and selected `/philosophies/agile-vs-waterfall-analogy` anchor `#analogi-kota-dan-jembatan`:

| Measurement | Reported value |
|---|---:|
| Header top / bottom / height | 0 / 60 / 60 CSS px |
| Heading top / bottom after anchor jump | 60 / 100 CSS px |
| ScrollY before → after | 0 → 620 CSS px |

For this **specific heading at this specific width**, heading.top `>=` header.bottom and no overlap is measured. Supersedes suspicion of a proven obstruction for that case. The existence of a fixed bar during deep-scroll remains ordinary design behavior, not automatically an accessibility defect. Other headings, native 320px/375px, browser zoom, browser text scaling, focus-driven scrolling and screen-reader reading experience are **NOT VERIFIED**. Do not mandate hide-on-scroll or label WEB-AC09/22 PASS from one rect comparison.

## 2. Remaining R1 execution evidence

| Test | Reviewer conclusion | Limitation |
|---|---|---|
| Desktop top-level 1440x900 and tablet 768x1024 | PASS_SCOPED_AGENT_REPORTED for visited route/layout observations | Not all accessibility/performance/privacy/negative cases |
| Native mobile top-level 320x480, 375x812 | **NOT_EXECUTED_BY_IDE** | Chromium Windows tool minimum top-level `window.innerWidth=502`; earlier operator DevTools 320px captures exist but do not automatically prove the full test matrix |
| Drawer open, keyboard Tab/Shift+Tab, Escape focus return | PASS_SCOPED_AGENT_REPORTED at 502px | Agent reports `document.activeElement` returns to hamburger; no independent replay or native 320px |
| Drawer → Command Palette after event/200ms → input focus | PASS_SCOPED_AGENT_REPORTED at 502px | Specific interaction only |
| Anchor jump (one heading) | PASS_SCOPED_AGENT_REPORTED at 502px | See measurements above |
| Root viewport width / intentional breadcrumb rail | PASS_SCOPED_AGENT_REPORTED at 502px: root 502=502; breadcrumb 470 client vs 582 scroll | `overflow-x-clip` can mask offscreen descendants; need clipping/focus negative cases in later acceptance |
| Semantic landmarks / labels / focus ring spot check | PARTIAL_POSITIVE_AGENT_REPORTED | Not WCAG 2.2 AA certification |
| 200% browser zoom | **NOT_EXECUTED** | Browser automation has no native zoom facility |
| Contact form DOM & CAPTCHA iframe | PARTIAL / CAPTCHA_CONFIG_REPORTED; submit intentionally disabled initially | No CAPTCHA solved, no POST or delivery; prior agent observation contradicted |
| Contact fallback | PARTIAL_GAP_AGENT_REPORTED | No direct contact email in form/page body observed; footer recruiter link is not equivalent to guaranteed alternative channel |
| Git source protections | PASS_SCOPED_AGENT_REPORTED | Post-audit `git status --porcelain=v1 --untracked-files=all` reported no tracked edits and exactly 14 expected untracked Markdown paths; does not hash file contents or prove no ignored caches were written |

Agent report's final `W0-AC10 PASS_SCOPED` is **not adopted as a full acceptance gate**: the output explicitly labels native mobile and 200% zoom `NOT_EXECUTED`, and the contact flow remains untested end-to-end. Record **W0-AC10 PARTIAL** at the workstream level, with PASS_SCOPED for precisely stated subtests. The earlier six-route matrix was wider but not an end-to-end certification.

## 3. Correct workstream and severity crosswalk

- W0QA-01: **NOT A PROVEN P1 OUTAGE**. W6 contact/newsletter, WEB-I11, WEB-AC18; preserve a missing-fallback and legacy-provider readiness concern; do not remove W6 scope.
- W0QA-02: **P1 design-contract gap** confirmed by `EcosystemHero.tsx` at inspected remote Studio SHA: Creator vs Reader primary first-contact hero paths absent → **W1**, WEB-I03, WEB-AC01–04.
- W0QA-03: **P2 confirmed 404**, `ShellBackdrop.tsx` references absent remote asset, `.gitignore` excludes local `public/images/` → **W3**, WEB-I08, WEB-AC10–12.
- W0QA-04: **TOOL CAPABILITY**, not product defect. Native 320/375 IDE check remains unexecuted.
- W0QA-05: **P2 UX preference/other-anchor negative-test candidate**, NOT confirmed obstruction in measured case → **W2**, WEB-I07, WEB-AC09 and WEB-AC22.
- **W4 remains privacy/security**, specifically analytics, Markdown sanitization, embedded content, published-only negative cases. It is not renamed to `Content Governance & Pipeline Baseline` by the agent's latest suggestion. Local authoring protection applies cross-workstream under WEB-I15.
- W5 Navigator AI and W7 integration retain their ratified scope; no resequencing/urgent source fix without a separately approved change order.

## 4. Next gate / execution policy

There is now sufficient **scoped W0 discovery** to specify W1 IA risks and the W2 mobile QA follow-up. Do not keep repeating the same viewport/read-only QA indefinitely. W0-AC10 may be presented for **owner acceptance as PARTIAL with explicitly scheduled W2/W7 negative tests**, but cannot be silently marked PASS. Native mobile and 200% zoom validations must occur by W7 (or earlier on owner-approved isolated exact-SHA source) before website production DoD. Current evidence uses prior owner DevTools 320px screenshots separately from agent's 502px CSS environment.

More urgent unresolved W0 provider/cost items before W0-AC12 owner acceptance: per-record diagnostics for failed Resend sending domain, Workers AI Free account-specific quota and billing posture, Vercel per-project (not total) consumption, privacy analytics/third-party inventory, published-only trust risk and Rp0 fail-closed treatment. Any resulting W0 deferral must be owner-approved and explicitly connected to later WEB-AC identifiers.

**No changes to Studio source, any application branch, customer data, DNS, vendor dashboard, or production are authorized or implied by this documentation. W0 IN PROGRESS; W1–W7 HOLD; Phase 1 NOT ACCEPTED; Phase 2 NOT ACTIVE.**
