# RC-W0-06 — Cloudflare Workers Free & Browser Privacy Evidence (2026-10-12)

> **W0-AC06 / AC09 / AC10 / AC11: scoped evidence review, not W0 closure.**
> Observation date: 2026-10-12 Asia/Jakarta. Evidence: owner-provided Chrome DevTools and Cloudflare dashboard screenshots, not independent browser reproduction.
> Source context: Studio deployed GitHub main `18b295f96ccb521b228a1855e79448158c09db15` from earlier W0 verification; doc baseline `70a4f232aa9ba8286a097d86d5a104e1c220ad85`.
> PUBLIC DOCUMENT: No screenshot bytes/raw HTTP URLs, Google auth cookies, cookie values, reCAPTCHA token/iframe parameters, GA hit payloads, session/account IDs, secrets or private contact data have been copied here.
> Governing docs: [W0 Work Order](../02-w0-00-read-only-discovery-work-order-20261012.md), [Architecture Contract](../00-ratified-frontend-architecture-contract-20261012.md), [Traceability](../03-phase1-acceptance-and-invariant-traceability.md), [Progress Ledger](../01-engineering-progress-ledger.md).

## 1. W0-AC06: Cloudflare account subscription baseline (PASS_SCOPED FREE; AI usage still UNKNOWN)

Owner dashboard **Manage Account → Billing → Subscriptions → Subscribed** explicitly lists:
- `Workers` → **Workers Free, Active**;
- `reltroner.com` → **Free Plan, Active**;
- payment method panel: **No payment method on file**;
- Invoices and documents: **No invoices** in displayed view;
- paid upgrade is offered, **not enabled**.

This closes the prior unknown of account Workers subscription tier. It does **not** prove that any one of the 243 Cloudflare model-catalog entries is compatible with zero-cost AI, that AI usage is zero, that all account products have universal zero billing exposure, or that AI inference has ever been successfully invoked. The owner separately inspected the Workers AI dashboard and reports **`WORKERS_AI_USAGE_UI_NOT_EXPOSED`**: no account-specific neuron usage meter was available in shown UI. Treat as **account Workers Free PASS_SCOPED / Workers AI model entitlement PARTIAL-UNKNOWN / no usage UI**. Avoid repeatedly searching for the same unavailable graph or probing paid models. The public free allocation is a design input, not account-evidence of AI runtime readiness.

**Zero-spend posture:** Free active + no card + no invoice observed is a strong scoped baseline, not an absolute provider-wide hard-stop proof. No paid plans, billing setup, upgrade or external inference are authorized.

## 2. W0-AC09: Google Analytics request and first-party cookies (PARTIAL, actual tracking confirmed)

Owner Chrome DevTools Network, on `https://www.reltroner.com/`:
- `www.googletagmanager.com/gtag/js` → **HTTP 200 GET**; Google tag script loaded;
- `www.google-analytics.com/.../collect` → **HTTP 204 POST** for at least two requests; the site generated analytics events. Request URLs and payloads are NOT reproduced.
- Chrome Application → Cookies lists **`_ga` and one `_ga_*` cookie** scoped to `reltroner.com` in owner session.
- On the home page, some individual domain filters (`cdn.jsdelivr.net`, `google.com`, `formspree.io`) showed **No matches found** in that captured request window. This cannot be generalized to other pages or a complete external dependency inventory; other screenshots already prove resource CDN access on content routes and Google reCAPTCHA under `/contact`.
- **No clean-profile, before-interaction consent experiment** is present; a populated browser profile may have existing cookies. Thus `TRACKING_CONFIRMED` does NOT establish `CONSENT_REQUIRED_VIOLATION` or `CONSENT_COMPLIANT`. Must match the website privacy notice, actual script initialization, cookies and user-choice model in **W4 / WEB-I13 / WEB-AC19**.

### Information exposure handling

Screenshots of Chrome Application → Cookies showed **actual cookie Value columns**, including Google-account-related cookies in the contact browser profile; other image captures included long Analytics collect URLs and reCAPTCHA iframe/token-related DOM. These are sensitive browser-session artifacts and must **never** be committed raw to the public documentation repository, sent to third-party QA agents, or copied to issue descriptions. Sanitize at source (hide `Value`, remove full query strings/tokens, crop personally sensitive account UI). This receipt records only cookie names/categories and statuses. The user may consider invalidating affected Google sessions if these images have been shared publicly; mere screenshots in the present chat are not evidence of public compromise.

## 3. W0-AC09/10: reCAPTCHA on contact and 320px layout

Owner Chrome Elements screenshot at `/contact` showed a loaded **Google reCAPTCHA iframe**, with its embedded challenge and auxiliary hidden iframe/textarea elements. This further supports [RC-W0-04 correction](./RC-W0-04-gemini-qa-targeted-revalidation-review-20261012.md): absent reCAPTCHA configuration was not proven by the initial Gemini report. The **Send Message** button remained grey/disabled before verification, consistent with source `canSubmit = isCaptchaConfigured && verified`. **No submit**, no solved CAPTCHA, no Formspree delivery and no POST to contact provider were executed; sender availability remains **UNVERIFIED**.

At browser DevTools device emulation labelled `iPhone 4 320 × 480`, the reCAPTCHA challenge appears **wider than the visible content/card region and clipped at its right edge**. Classify **`MOBILE-320-CAPTCHA-CLIPPING / visually observed candidate`**; determine exact widget/card bounding rectangles and keyboard/touch reachability in a gated W2/W6 or W7 QA. Existing app/page `overflow-x-clip` and fixed mobile shell may mask clipping; do not call page overflow PASS merely because `document.scrollWidth == clientWidth`. Avoid shrinking an interactive third-party captcha via CSS without an owner-approved usability/accessibility test; W6's ratified Free Web3Forms/hCaptcha pathway may replace this widget later.

Chrome Console on `/contact` shows `GET /images/background.webp 404 Not Found`. This corroborates already archived W3 missing source-tracked static asset issue; not a new separate incident.

**Iframe inventory is route-dependent:** homepage Elements `iframe` search showed 0 matches in that captured state, while `/contact` shows reCAPTCHA nested frames. No proof that all pages have been exhaustively searched.

## 4. Remaining work and gate disposition

| Gate | Status | Evidence/remaining actions |
|---|---|---|
| W0-AC06 Workers subscription | **PASS_SCOPED** | Workers Free Active; reltroner.com Free Active; no card/invoices shown |
| W0-AC06 Workers AI inference entitlement | **PARTIAL / UI_NOT_EXPOSED** | Specific Cloudflare-hosted text model Free eligibility, free-inference fail-closed design and permitted no-spend deployment not tested |
| W0-AC09 external requests/cookies | **PARTIAL / TRACKING_CONFIRMED** | GA tag GET 200, collect POST 204, `_ga*` cookies; pre-consent clean profile and privacy-text congruence still untested |
| W0-AC10 contact responsive | **PARTIAL / CLIPPING_CANDIDATE** | reCAPTCHA visible at 320, right edge outside card/visible content; no box measurements, touch/keyboard/zoom QA |
| W0-AC11 zero-spend | **PARTIAL with Cloudflare Free account proof** | Free plan presence ≠ universal guarantee; Web3Forms/Resend/production release costs independently gated |
| W0-AC12 owner acceptance | **PENDING** | Owner must explicitly accept W0 with scoped gaps and later workstream owners or request more discovery |

**Do not re-run completed provider screen navigation.** Remaining high-value W0 is read-only Resend authoritative DNS comparison for 3 failed record statuses, W0 privacy notice/source truth matrix and optional clean-profile consent observation, plus bounded risk/owner deferral decisions. Browser QA can later be allocated to W2/W4/W6/W7 and must remain production-safe.

No GitHub Studio source, local protected content, Cloudflare/Resend/Web3Forms/Vercel configuration, DNS, sent mail, deployed build, or paid API was changed or authorized by this receipt. **W0 IN PROGRESS; W1–W7 HOLD; Phase 1 NOT ACCEPTED; Phase 2 NOT ACTIVE.**
