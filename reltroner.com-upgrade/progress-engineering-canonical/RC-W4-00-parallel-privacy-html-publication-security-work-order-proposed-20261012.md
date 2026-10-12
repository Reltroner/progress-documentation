# RC-W4-00 — W4 Parallel Privacy, Publication Security & Consent Work Order

> **Status:** read-only source review completed for named components; **W4 implementation NOT AUTHORIZED**. W4 is a mandatory Phase 1 security/privacy workstream, not deferred indefinitely merely because W1 passes.
> Parents: [WEB-I05, I13, I17](../00-ratified-frontend-architecture-contract-20261012.md), [WEB-AC06, AC19, AC20, AC22](../03-phase1-acceptance-and-invariant-traceability.md), [W0 provider/browser evidence](./RC-W0-09-final-discovery-disposition-and-proposed-w1-entry-20261012.md).
> Public source verified at `Reltroner/reltroner-studio` `18b295f96ccb521b228a1855e79448158c09db15`. Zero source edits made by this report.

## 1. Confirmed baseline from source and owner evidence

- `app/layout.tsx` mounts `GoogleAnalytics` and `RouteAnalytics` unconditionally inside public app shell.
- `components/GoogleAnalytics.jsx` in production registers `next/script` `gtag/js?id=G-VZ7QYLZPF0` and `gtag('config')` with `afterInteractive`, **without an in-component consent condition**. Prior W0 clean/Incognito browser owner evidence reports analytics collection before visible consent, including `_ga` cookies/collect request. Treat as **P1 unresolved data-processing/consent requirement**, not a final jurisdiction-specific legal verdict.
- `lib/utils/content.js` uses Markdown HTML conversion with previously inspected unsafe `sanitize:false` behavior; inspect exact render and embed paths plus `processVideoDirectives`/`injectVideoEmbeds` in W4 before approving broad index/AI retrieval. Do not execute malicious content on public production.
- `components/sections/ContactForm.jsx` currently uses Formspree and Google reCAPTCHA; migration to Web3Forms belongs W6 with W4 privacy review.
- The W1 browser session *locally blocked analytics with interception*; that demonstrates QA containment only, **not** a consent fix.

## 2. Bounded target security design

**Proposed privacy decision (owner review needed):** default to no optional tracking until explicit consent, or disable GA entirely until there is a genuine reason to collect it. Google provides a *basic consent mode* that prevents tags from loading before consent; advanced consent mode can still generate cookieless pings, so **“consent denied” in advanced mode does not automatically mean zero requests**. For a strict pre-consent zero-outbound requirement, choose basic (load only after grant) or remove analytics entirely, then verify network and cookies in a clean browser. [Official Google consent mode guide](https://developers.google.com/tag-platform/security/guides/consent); [Google basic vs advanced behavior](https://developers.google.com/tag-platform/security/concepts/consent-mode).

No misleading cookie notice: include processors, optional analytics, third-party media/embed, Resend form/newsletter, Web3Forms submissions and Cloudflare optional AI when they become operational. Language must describe actual requests and consent choice. Consent UI keyboard/focus handling and rejection path must not regress navigation.

**Markdown security:** derive public-only publication predicate shared with W2; sanitize/restrict raw HTML, scriptable URI schemes, dangerous attributes, iframes and embeds; preserve explicitly approved safe video embeds with origin/allowlist and no active script injection. Test using synthetic fixtures in an isolated test environment; do not publish XSS payloads or probe production visitors. Distinguish indexed excerpt sanitization from full rendered HTML sanitization. Reject malformed dangerous input (fail closed), preserve safe legacy Markdown where explicitly approved.

## 3. Suggested safe tests / owner decisions

| Case | Required observation |
|---|---|
| Fresh browser / optional analytics undecided | No GA tag/collect and no `_ga` cookie under **basic** blocked mode; browser request log |
| Reject consent | Remains no GA outgoing analytics; preference persisted appropriately |
| Accept consent | Only then permitted GA script/collect; consent status captured without sensitive IDs |
| Revoke/return visitor | No new tag before permission; state and privacy text match |
| Accessibility | Keyboard, focus, dismiss, no modal trap at 320/375/768/1440 |
| Markdown safe cases | Known images/video embeds survive controlled allowed origins |
| Markdown negative | Dangerous HTML/script scheme not executable or indexed/served |
| Draft negative | Unpublished fixture absent from index, static HTML/route/sitemap/AI source |
| CSP/headers | Document actual source and any Vercel/CSP behavior; do not invent headers |

**Do not add an analytics CMP subscription, send cookies or credentials to public evidence, or claim security PASS before actual browser/negative tests**.

## 4. Phased owner-gated execution

W4A **READ-ONLY discovery now**: exact source path inventory; sanitize/HTML flows, network/cookie baseline class; choose basic-consent vs temporarily disable GA. W4B requires explicit owner-approved TS/TSX source allowlist and test fixtures. W4C local synthetic negative tests, clean-browser consent captures, no source-related public deploy. W4D G3/G4 separate PR/preview/privacy/security review and W7 integration.

### Blockers/STOP

No blanket source rewrite or fourth W1 file; `W4_PRIVACY=OPEN_P1`, `W4_HTML_SECURITY=NOT_ACCEPTED`, `WEB-AC06/19/20=PENDING`. No public analytics/cookie changes, deployment or provider modifications authorized by this document.
