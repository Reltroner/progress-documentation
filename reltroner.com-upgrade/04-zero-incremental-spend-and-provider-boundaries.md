# RC-WEB-COST-001 — Zero-Incremental-Cash, Third-Party, Privacy & Security Boundary

> OWNER RATIFIED: New website capabilities must target **Rp0 additional spending** without secretly degrading essential functional/nonfunctional acceptance.
> As of 2026-10-12: free-plan availability and actual account quota **NOT VERIFIED**; this is a contract, not invoice proof.
> No paid selection, plan activation, card/auto-topup/overage change or product key generation is authorized by documenting a preferred candidate.

## 1. Financial invariants and allocation strategy

- Reuse existing frontend hosting and free/static infrastructure before introducing new running services.
- No Vercel Pro, Vercel AI Gateway purchase, paid AI credits, new VPS, Redis/PostgreSQL service, SMTP hosting, subscription, automatic billing or hidden paid AI inference. A free promotional credit is not assumed indefinitely renewable.
- New third-party API may be activated only if official current pricing, **account-specific entitlement**, no-upgrade behavior, authorization and worst-case abuse response are verified. Rates are mutable, so do not make historical pricing a binding guarantee.
- Distinguish **free provider quota**, existing sunk cost, resource contention and economic opportunity cost. Spending Rp0 does not permit stealing CPU from HRM/LMS.
- If quota exhausted or blocked: return accurate unavailable/throttled state, deterministic browse/search/email fallback; do not fabricate success or use a paid pathway.

## 2. Provider placement / status

| Concern | Preferred boundary | Contractual role | Decision gate |
|---|---|---|---|
| Website | Existing Vercel Hobby deployment | Frontend-first static/content render | Verify current plan and commercial-use terms, budget and build usage |
| Edge key custody | Existing Cloudflare Worker Free (candidate) | Resend server-only key, optional AI endpoint | Verify worker quotas and rate-limit controls, CORS/origin/CSRF/abuse model and hard no-bill behavior |
| AI inference | Cloudflare Workers AI Free (preferred candidate; **not yet selected for deployment**) | Public evidence-based explanation only | Model test, Indonesian/English quality, quota/cost and privacy; fail closed |
| Contact | Web3Forms Free (ratified provider requirement) | Contact inquiry delivery only | Existing account and free limitations, recipient ownership, spam defenses, success handling |
| Newsletter | Resend Free (ratified provider requirement) | Opt-in contacts / welcome-confirmation / unsubscribe | Domain authentication, free plan quotas, user consent, suppression, API key safety |
| Images | GitHub source + jsDelivr immutable commit URL (candidate delivery implementation) | Versioned public assets | Confirm URL behavior, build trigger on same-name update and free build budget |
| LMS/VPS/Keycloak/DB | Existing independently owned infrastructure | No website inference/default API core | Never mutate without independent authority |

Do not interpret 'Workers AI Free' as unlimited chat. Requests/neuron usage depends on model and context; no model is authorized from this document alone. A public AI endpoint needs meaningful abuse controls even if inference nominally free. Any account that allows silently paid overage without an enforceable hard stop is **BLOCKED** for Phase 1 zero-spend use.

## 3. Resend newsletter data lifecycle

1. Explicitly state topics, frequency expectation, privacy link and unsubscribe; contact form consent is NOT mailing-list consent.
2. Client .tsx posts minimal normalized email + consent/source to a protected server-side endpoint. Never use NEXT_PUBLIC/committed Resend API secret.
3. Guard with schema validation, request limits, bot mitigation, duplicated request handling and provider response classification.
4. Contacts enrollment accepted does not imply welcome delivered, verified address, or marketing permission unless consent/verification conditions actually fulfilled.
5. Returning subscriber and suppressed/unsubscribed contacts must not be silently reactivated. Idempotent welcome delivery and suppression reconciliation needed.
6. Unsubscribe/erasure path must work without requiring the user to expose sensitive personal data to an open source issue. Email lists remain with provider, not public Git.
7. On failure or quota exhaustion return clear result; no retry storms and no auto-upgrade.
8. No outbound marketing community campaign until Phase 2 is expressly active; minimal Phase 1 tests and setup are not marketing activation.

## 4. Web3Forms contact lifecycle

- Separate intent paths for collaboration, creativity/worldbuilding and learning. Common accessible controls: name, reply email, topic and free text; do not require unnecessary sensitive data.
- Submit only to confirmed correct recipient; show 'accepted by provider' vs actual manual follow-up separately; record non-PII request reference where available.
- Client-facing Web3Forms access key is not equivalent to private Resend server API secret. Still protect abuse using the free features **verified on the actual plan**, not falsely assume premium controls are included.
- Prevent duplicate sends; handle timeout, vendor rejection, quota exhausted and offline states. Offer real monitored alternative mailto address (owner verifies before release).
- No automatic conversion from contact lead to newsletter list, no user-account creation and no implied calls/free prototypes/agency services.

## 5. Privacy and third-party inventory

Code baseline (Studio 18b295f): app/layout.tsx imports GoogleAnalytics and RouteAnalytics; GoogleAnalytics.jsx emits the GA script in production; some markdown HTML is converted with sanitize:false. Before publishing 'essential cookies only / no tracking / no advertising / no profiling', verify and remove or properly consent-gate nonessential GA and third-party trackers. Examine iframes/YouTube, remote CDN requests, forms, and AI data processing/retention. Document actual processors (Resend, Web3Forms, optional Cloudflare AI), purposes, data minimization, deletion and contact method; do not claim third-party services receive zero information when they do receive submitted details.

Cookie banner: informational only if **no optional cookies/tracking are loaded**. Otherwise require meaningful pre-consent control and reject nonessential cookies until consent. Cookie preferences/counter should not themselves reintroduce an unnecessary vendor. WCAG/keyboard support mandatory.

## 6. Threat model and quality non-goals

Protect against prompt injection, private/unpublished source retrieval, cross-domain canon contamination, API token leakage, data exfiltration, contact spam, newsletter list pollution, cross-origin abuse, callback URL abuse, untrusted Markdown HTML and compromised embeds. No arbitrary agent tools, SQL, shell, external unrestricted HTTP, Keycloak admin or privileged LMS capabilities.

Existing KVM1 1-vCPU snapshot is **not** free inference capacity; frozen LMS placement prohibits its local-LLM inference. Never deploy another model daemon or open a new VPS port to avoid provider fees.

## 7. Cost verification worksheet and STOP rules

For each provider record: timestamp, current account plan, card/billing configuration without sensitive identifiers, hard limit behavior, monthly/daily quota, alerts, expected request volume, production cost (cash and existing-resource), free entitlement expiry, fallback UX, operator ownership. If unsupported by evidence mark UNKNOWN, not $0 CERTIFIED. STOP if provider needs payment method with no enforceable hard cap, plan restrictions conflict with use, or current usage could degrade existing service.

Result classification: FREE_VERIFIED, FREE_CONDITIONAL, UNKNOWN, REQUIRES_PAYMENT, BLOCKED, DISABLED. **FREE_VERIFIED does not guarantee future terms; set recurring manual review before activation and during Phase 2.**

