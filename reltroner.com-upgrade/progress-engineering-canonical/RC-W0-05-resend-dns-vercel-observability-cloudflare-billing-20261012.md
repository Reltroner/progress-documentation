# RC-W0-05 — Read-only Resend DNS, Vercel Observability, Cloudflare Billing & Privacy Audit Navigation

> Observed: 2026-10-12 Asia/Jakarta, from owner-provided dashboard screenshots. **W0 IN PROGRESS; NOT a new permission for provider changes**.
> Provenance: OWNER-UI-SCREENSHOT for Resend/Vercel/Cloudflare, WEB-PUBLIC-REFERENCE for vendor pricing and Chrome DevTools instructions. This canonical receipt is deliberately sanitized; no account IDs, full DNS key values, invoice addresses, cookies or HTTP payloads.
> Source context: Studio GitHub main production at last confirmed `18b295f96ccb521b228a1855e79448158c09db15`; documentation HEAD before this receipt `24296231d1ca6cf873a40a46b50fee2c9f58b676`.
> Authority: [W0 read-only work order](../02-w0-00-read-only-discovery-work-order-20261012.md) · [WEB acceptance](../03-phase1-acceptance-and-invariant-traceability.md) · [living ledger](../01-engineering-progress-ledger.md).

## 1. W0-AC07 — Resend sender domain: failure narrowed to 3 DNS records

Owner's Resend domain details page for `resend.reltroner.com` displays **domain Failed**, provider **Hostinger**, sending region **Tokyo (ap-northeast-1)**, **Enable Sending** toggle on and **Enable Receiving** off. All three on-screen required DNS records have **Failed** statuses:
- DKIM TXT record (under a `_domainkey` hostname): Failed.
- Sending/mail feedback MX record (`send.resend` sublabel): Failed.
- Sending SPF TXT record (`send.resend` sublabel): Failed.

These are status observations, **not yet a proof that entries are missing, changed, incorrectly scoped, or served by the displayed DNS provider**; authoritative DNS/name-server queries and expected/actual record comparison have not been run. Provider label does not prove authoritative DNS control. No restart/reverify, Auto configure, change toggle, DNS edits, mail send, or new form/email creation. `Enable Sending` toggle on does **not** override failed verification.

**Exit evidence needed:** read-only DNS management showing record type/host and public-value fingerprints (sanitized) and authoritative DNS trace; classify missing vs mismatch vs stale vs wrong zone with owner permission before eventual correction. W6 send readiness **BLOCKED_DOMAIN_FAILED**.

## 2. W0-AC05 — Vercel project-specific Observability (12-hour scoped)

Owner opened **project** `reltroner-studio` → Observability → Fast Data Transfer and ISR. UI shows filter `All environments` and time window `Last 12 hours`:
- Fast Data Transfer: approximately **69 MB outgoing / 4 MB incoming** in last 12h. Visible top routes include `/`, `/404`, `/blog/[slug]`, `/principles/[slug]`, `/places/[slug]`, `/philosophies/[slug]`. `/404` is a tracked route here; it is not automatically evidence that every such request is a distinct user incident.
- ISR: approximately **23K read units / 0 write units** in last 12h; Request Caching panel around **2.4K**. Revalidations shown as zero in screenshot time range. Routes include `/blog/[slug]`, `/principles/[slug]`, `/places/[slug]`.
- These are **project-observability time-slice metrics**, not replacements for earlier rolling 30-day billing/team totals; the time range and metric units differ. Retain `PROJECT_ATTRIBUTED_12H_PASS_SCOPED`; **30-day project attribution and traffic trend not yet verified**.
- Prior 30-day Function Invocations 164 (156 success / 8 User Error) still need request classification; neither dashboard proves site-wide failure.

## 3. W0-AC06 — Cloudflare billing: wrong page for Free neuron quota

Owner Cloudflare Manage Account → Billing → **Billable usage** screenshot shows `Billable usage notification`, estimated usage feature and `Spectrum — No data` on this displayed portion. It does not show Workers AI neuron consumption, account Workers Free/Paid subscription, or spend hard stop. It is not evidence of zero Workers AI neurons.

Deterministic read-only next route:
1. From that exact Billing screen click **Subscriptions** tab to inspect account Workers/AI subscriptions (not `Upgrade`).
2. From dashboard sidebar magnifying-glass Search enter **Workers AI** and choose AI → Workers AI (Cloudflare 2026 AI top-level section). Locate **Usage/Analytics** only if present; earlier owner `/ai/workers-ai/usage` showed onboarding rather than usage chart. If no meter, record `WORKERS_AI_USAGE_UI_NOT_EXPOSED`, do not create a Worker/inference to populate it.
3. Document **account-specific Free/Paid plan** separately from **public pricing**. Public Cloudflare Workers AI docs dated 2026-10-09 state Workers Free receives 10,000 Neurons/day reset 00:00 UTC; Workers Free over-limit calls fail, whereas Workers Paid can incur usage charges. Some listed models require Paid or prepaid Gateway credits. The previously viewed catalogue of 243 mixed Cloudflare-hosted/third-party models is not a 243-model free-entitlement declaration.

Relevant public sources:
- https://developers.cloudflare.com/workers-ai/platform/pricing/
- https://developers.cloudflare.com/billing/manage/billable-usage/
- https://developers.cloudflare.com/changelog/post/2026-02-19-ai-dashboard-experience-improvements/

## 4. W0-AC09 — Chrome DevTools privacy inspection: reproducible read-only sequence

On `https://www.reltroner.com/` in Chrome:
1. **F12 → Network → All**; enable **Preserve log**, **Disable cache**; click Clear log then **Ctrl+R**.
2. To get external traffic in one view: **Network → More filters → 3rd-party requests**. For named probes in the Filter field, use `domain:google-analytics.com`, `domain:googletagmanager.com`, `domain:cdn.jsdelivr.net`, `domain:google.com`, `domain:formspree.io`; clear each between probes. Absence on homepage not proof absent on /contact or article embeds.
3. **Application** tab (if hidden, **>> → Application**) → **Storage → Cookies** → click first-party site origin. Record cookie names/domain/flags, redact **Value**, no deletion or modification.
4. **Elements → Ctrl+F → iframe**, then check loaded `src`, `title`, `sandbox` where present. Repeat for `/contact`. Do **not** solve CAPTCHA or submit form.
5. **Console** tab → check errors/warnings. Sanitize all URLs and headers before screenshot/receipt.

Public DevTools references:
- https://developer.chrome.com/docs/devtools/network/reference/
- https://developer.chrome.com/docs/devtools/security/
- https://developer.chrome.com/docs/devtools/application/cookies/

Observation vs risk: production Google Analytics had previously been observed, and R1 Gemini agent later reported active public reCAPTCHA iframe. Neither alone proves privacy disclosure compliance, consent correctness, or absence of another embed. **W0-AC09 PARTIAL** pending request/cookie/iframe inventory and final privacy text comparison.

## Gate dispositions

| Gate | Result |
|---|---|
| AC05 Vercel | PARTIAL; project-specific 12h metric observation PASS_SCOPED, 30-day attribution pending |
| AC06 Cloudflare | PARTIAL / account AI entitlement not proven; billable usage screenshot not Neuron meter |
| AC07 Resend | BLOCKED_DOMAIN_FAILED: DKIM TXT, feedback MX and SPF TXT each shown Failed |
| AC09 Privacy | PARTIAL; deterministic operator procedure ready; evidence not yet collected |
| AC11 zero-spend | PARTIAL; no proof of broad provider hard billing control |
| AC12 W0 final | PENDING owner disposition |

**No** source changes, Git fetch/pull/reset, provider activation, DNS mutation, email send, AI inference, Vercel deployment or payment setup are authorized by this publication. W1–W7 HOLD, Phase 1 NOT ACCEPTED, Phase 2 NOT ACTIVE.
