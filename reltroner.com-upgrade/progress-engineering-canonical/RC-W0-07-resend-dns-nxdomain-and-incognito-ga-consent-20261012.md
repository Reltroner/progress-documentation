# RC-W0-07 — Resend DNS NXDOMAIN & Fresh-Session Google Analytics Consent Evidence

> **Status:** EVIDENCE RECEIVED / W0 IN PROGRESS / W0-AC07 BLOCKED / W0-AC09 PARTIAL WITH P1 PRIVACY GAP. No provider modifications or Studio source changes authorized.
> **Observation:** 2026-10-12T09:44:41+07:00 for owner-provided Windows PowerShell 5.1 DNS probes; clean/Incognito Chrome privacy test reported afterward on 2026-10-12 Asia/Jakarta without a separate event timestamp.
> **Evidence classes:** `OWNER_POWERSHELL_OUTPUT`, `OWNER_CLEAN_SESSION_REPORT`, `INDEPENDENT_GITHUB_SOURCE_REVIEW`. No independently executed DNS queries or browser tests by reviewer in this receipt.
> **Immutable Studio baseline:** `Reltroner/reltroner-studio` GitHub `main` SHA `18b295f96ccb521b228a1855e79448158c09db15`, checked for relevant analytics components. Initial documentation main before receipt: `d37cdd0df2dbef4b1e464dd0edc015247851b66e`.
> **Authority:** [W0 read-only work order](../02-w0-00-read-only-discovery-work-order-20261012.md), [WEB architecture](../00-ratified-frontend-architecture-contract-20261012.md), [WEB acceptance](../03-phase1-acceptance-and-invariant-traceability.md), [prior RC-W0-05 DNS failed](./RC-W0-05-resend-dns-vercel-observability-cloudflare-billing-20261012.md), [prior RC-W0-06 observed tracking](./RC-W0-06-cloudflare-free-and-browser-privacy-evidence-20261012.md).
> **Publication redaction:** Do not commit session cookies, cookie values, full analytics request URLs/parameters, browser account IDs, contact addresses, raw reCAPTCHA DOM tokens or full provider verification secrets. This receipt contains only public DNS QNAMEs, NS labels and summary of observations.

## 1. W0-AC07 — Resend email DNS: recursive DNS lookup absence

The owner ran the previously authorized public DNS discovery batch in Windows PowerShell 5.1 without changing local Git or DNS.

**Domain delegation from 1.1.1.1 NS lookup:** `reltroner.com` advertises `nicolas.ns.cloudflare.com` and `millie.ns.cloudflare.com` (TTL displayed 86400 seconds). These identify the **publicly delegated authoritative DNS provider**, distinct from Resend's dashboard's provider label `Hostinger`. A Resend-configured provider label is not itself proof of active delegated authoritative DNS.

Both publicly recursive resolvers, `1.1.1.1` and `8.8.8.8`, returned PowerShell `DNS name does not exist` on the requested RR types:

| Resend purpose | Full queried QNAME | RR type | 1.1.1.1 | 8.8.8.8 |
|---|---|---|---|---|
| DKIM | `resend._domainkey.resend.reltroner.com` | TXT | LOOKUP FAILED / DNS name does not exist | same |
| Sending SPF | `send.resend.reltroner.com` | TXT | LOOKUP FAILED / DNS name does not exist | same |
| Sending feedback MX | `send.resend.reltroner.com` | MX | LOOKUP FAILED / DNS name does not exist | same |

These full names are constructed from the previous owner Resend UI relative host labels **as interpreted in the earlier approved script**. The missing results reliably show these RR queries were not satisfied by either resolver when checked, strongly supporting the earlier Resend statuses **DKIM Failed + SPF Failed + MX Failed**. However, it is not yet an independent **authoritative DNS query** and the exact record FQDN interpretation is not independently cross-checked against the Resend detail UI. `Resolve-DnsName` exception strings alone do not distinguish all DNS protocol negative response types. Do not claim authoritative NXDOMAIN proofs, exact DNS-server misconfiguration cause, SPF policy mismatch, or a required edit value until authoritative direct query / Cloudflare DNS Records read-only GUI comparison is complete.

**Scoped conclusion:** `RESEND_SENDER_UNVERIFIED` / `DNS_HOSTS_NOT_FOUND_FROM_TWO_PUBLIC_RESOLVERS`; likely missing records in the active Cloudflare zone or incorrect record host naming/provider migration. **No email send, no DNS edit, no provider Restart/Auto configure, no DKIM key generation, no account upgrade or re-verification run as part of W0.**

**Next one-batch read-only verification:** Cloudflare Dashboard → Websites → `reltroner.com` → DNS → Records, inspect TXT/MX names for `resend._domainkey.resend` and `send.resend`, with entries redacted. Independently issue type-specific lookup directly to `nicolas.ns.cloudflare.com` and `millie.ns.cloudflare.com` if needed, not modifying records; confirm current Resend expected hostnames under its Domain → Records view. If zone is absent, STOP and report discrepancy. Changes to Cloudflare DNS are a separate explicit owner authorization with rollback/record-conflict analysis and site/email blast-radius awareness.

## 2. W0-AC09 — New Incognito browser consent observation

Owner reported a fresh Chrome Incognito website test, without interacting with any consent mechanism:
- `_ga` cookie **found** on `www.reltroner.com`;
- Google Analytics `collect` request **found**;
- user-facing consent UI **did not appear**.

This is stronger than an ordinary previously used browser session, because it examines initial browser behavior in a newly opened private context. It is still an **owner self-report**, not a reviewer-observed replay, and it does not demonstrate an exhaustive browser/region/consent-management or regulatory legal assessment. No raw cookie values or collection URLs reproduced.

**Independently checked remote GitHub source at exact Studio main SHA:**

- `app/layout.tsx` includes `<GoogleAnalytics />` and `<RouteAnalytics />` globally in the page shell.
- `components/GoogleAnalytics.jsx` renders Next.js `<Script src="https://www.googletagmanager.com/gtag/js?..."` using `strategy="afterInteractive"` in production, plus inline `gtag('js', new Date())` / `gtag('config', ...)`. There is **no consent check inside this component**.
- `components/RouteAnalytics.jsx` fires `pageview(pathname)` on production client route changes without an in-component consent state condition.
- `lib/gtag.js` `pageview()` and `event()` merely check that `window.gtag` exists, **not** a consent flag. The source alone does not prove every consent mechanism elsewhere is absent; owner fresh-session observation indicates an effective gate was not surfaced in the tested experience.

**Strong risk conclusion:** `TRACKING_ON_FRESH_SESSION_WITHOUT_VISIBLE_CONSENT_UI` is **P1 privacy implementation/remediation candidate** against ratified `WEB-I13` and `WEB-AC19`. This is **not** a definitive conclusion of a specific jurisdiction's legal violation; applicable consent requirements, lawful basis, user location, and a transparent choice/notice mechanism still require review. The product contract expressly requires removing or consent-gating nonessential tracking before any `no tracking` assertion.

Avoid conflating (1) observed tracking on clean session, (2) current privacy notice legal accuracy, and (3) future W4 owner-approved remedy. They are different claims. No GA tag changes or production redeploy is authorized during W0.

## 3. Source/product risks inherited from previous receipts

- `/contact` Google reCAPTCHA iframe is present; disabled Send before CAPTCHA solve is expected behavior, **not** proof of contact outage. Native 320px screenshot indicates reCAPTCHA visual clipping, to be measured during W2/W6/W7.
- Existing `/images/background.webp` HTTP 404 remains a W3 fix candidate, not a jsDelivr purge request.
- Resend account Free entitlements remain source evidence but **failed sending-domain verification blocks newsletter readiness**. Web3Forms Personal Free is documented but form not configured.
- Cloudflare Workers Free Active account status is verified, while Workers AI per-model Free entitlement remains `UNKNOWN / UI_NOT_EXPOSED`. The catalog alone is not proof of free inference.
- Studio source remains unchanged by this evidence-only receipt and owner-local 14 untracked Markdown are protected. No read-only Git re-preflight included with this DNS/proxy command batch; previous integrity receipts remain historical snapshots.

## 4. Updated acceptance / owner disposition

| Gate | Result | Owner disposition needed |
|---|---|---|
| W0-AC06 | Cloudflare Workers Free **PASS_SCOPED**, Workers AI **PARTIAL/UNKNOWN** | Accept no model-inference probing under W0, defer model selection/gating to W5 with no-spend constraint |
| W0-AC07 | **BLOCKED** sender: 3 record lookups missing at 2 recursive resolvers | Read-only Cloudflare DNS/source of authority inspection, then W6 work order; no DNS edit until separately approved |
| W0-AC09 | **PARTIAL/P1_CONSENT_RISK_CONFIRMED_IN_SESSION** | Owner acknowledges observed GA tracking before any displayed consent UI; W4 gate for privacy notice, remove or consent-gate nonessential GA |
| W0-AC10 | PARTIAL | 320px reCAPTCHA clipping issue to W2/W6/W7 with native viewport/zoom QA |
| W0-AC11 | PARTIAL | Cross-provider zero-incremental-cost fallback/trust/risk matrix and final W1 allowlist |
| W0-AC12 | PENDING | Explicit owner acceptance and recorded deferrals before separate W1 source authorization |

W0 may eventually close with **complete discovery and accepted residual workstream blockers**, not only when all later W1–W7 implementations are fixed. However, the owner must explicitly accept known P1/privacy and W6 sender risks and keep those as mandatory W4/W6/W7 exit criteria; do not falsely mark individual ACs PASS. Current owner has not yet granted W0 final sign-off or W1 G2 source authorization.

**Next:** direct authoritative DNS/provider host comparison, then W0-AC12 owner closure/risk register review. No edits, payments, DNS, deploys or Git Studio mutations occur in this work.
