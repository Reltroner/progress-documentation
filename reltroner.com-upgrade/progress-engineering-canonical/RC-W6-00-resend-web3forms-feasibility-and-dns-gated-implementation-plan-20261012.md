# RC-W6-00 — Read-Only Resend & Web3Forms Feasibility, DNS Blocker and Free Contact/Newsletter Plan

> **Status:** `PUBLIC_PROVIDER_RESEARCH=COMPLETE_SCOPED`; `RESEND_SENDER=BLOCKED_DNS_VERIFICATION`; `WEB3FORMS=NOT_CONFIGURED`; **no** DNS write, provider form creation, email sent, key creation, billing or source change authorized by this report.
> Contracts: [WEB-I11/12/13/14](../00-ratified-frontend-architecture-contract-20261012.md), [WEB-AC16..19/25](../03-phase1-acceptance-and-invariant-traceability.md), [cost](../04-zero-incremental-spend-and-provider-boundaries.md), [owner W0 DNS facts](./RC-W0-08-authoritative-dns-timeouts-and-cloudflare-zone-absence-20261012.md).

## 1. Public vendor quotas as of 2026-10-12 (not entitlement proof)

- [Resend official pricing](https://resend.com/pricing) Free transactional tier advertises **3,000 emails/month**, **100/day** and **3 sending domains**. Its marketing/broadcast product has a **distinct pricing model/quota dimension**, so do not treat 3,000 transactional emails as unlimited newsletter broadcasts or infer subscriber limits without checking the active marketing product. Resend says on paid plans overage can be enabled; **owner must verify no pay-as-you-go and account not on paid billing**.
- [Web3Forms official pricing](https://web3forms.com/pricing) Personal Free advertises **250 submissions/month**, unlimited forms/domains, advanced spam protection and **hCaptcha integration**. Features such as reCAPTCHA/Cloudflare Turnstile, autoresponders, restrict-to-domains, webhooks and multiple recipients appear under paid tiers; **do not design a “free” contract requiring Pro-only features**.
- Historical owner W0 screenshots separately showed Resend Free / failed sender and Web3Forms onboarding Free. New public pricing does not certify the owner's account balance, receiver address, correct DNS or permitted verification steps.

## 2. Exact current blockers

**Resend:** sender domain `resend.reltroner.com` marked Failed, with DKIM/SPF/MX verification incomplete. Owner Cloudflare zone GUI found no corresponding records; 1.1.1.1 and 8.8.8.8 failed to resolve requested records. Direct queries to the delegated authoritative nameservers timed out even for SOA, so **cannot claim proven authoritative NXDOMAIN**. Resend dashboard may display “Hostinger” provider while public NS delegation points to Cloudflare. Before any DNS edit, owner must inspect **current** active zone, absolute vs relative FQDN, exact record types, hostnames, priorities and conflicts. Do not expose DKIM TXT value in docs.

**Web3Forms:** onboarding/personal free state, no verified recipient or live accepted form receipt. `components/sections/ContactForm.jsx` currently relies on Formspree and reCAPTCHA, not Web3Forms. Existing contact at narrow viewport had reCAPTCHA candidate clipping; migrating may fix dependency but must not be called fixed until observed.

## 3. Separate journeys and truthfulness

Newsletter is **opt-in marketing consent**, not contact messages. Server-only Resend credential (never `NEXT_PUBLIC`), normalized email validation, source/consent timestamp, dedupe/idempotency, known subscriber vs verified vs welcome delivered, unsubscribe/suppression and safe failure states. No silent reactivation or contact-to-newsletter enrollment. Require owner-reviewed unsubscribe/erasure handling and no spam/mass marketing while Phase 2 inactive.

Web3Forms is **contact inquiry** with intent `collaboration`, `creative/worldbuilding`, `learning`, reachable fallback monitored mailbox, name/reply email/body minimization and explicit manual asynchronous follow-up expectation. Show `provider accepted` vs `owner replied` separately; 429/timeout/rejection/offline/error should not show success. Select only confirmed Free antibot features (hCaptcha according to provider docs) and allow testing without live external submission until separately approved. Avoid paid-restriction dependence and address harvesting.

## 4. Operator-gated sequence

| Gate | Narrow owner action | Output / STOP |
|---|---|---|
| W6A | Read-only Resend account: transactional vs marketing Free entitlement, domains, sender DNS exact **redacted** labels, quotas, paid overage off; Web3Forms recipient and Free dashboard | Account-specific `FREE_VERIFIED` or `UNKNOWN/BLOCKED`, no API key in chat |
| W6B | Owner separately approves exact Cloudflare DNS record **write set** and rollback; only after no conflicts and blast-radius analysis | Resend domain verified; no DNS edit before separate approval |
| W6C | Owner approves exact source file allowlist and scoped provider config; establish protected Worker handler vs client-side Web3Forms access key distinction | TypeScript implementation / no secret in client or repository |
| W6D | One bounded email/contact test per owner-approved sender/recipient, opt-in/unsubscribe/duplicate/error/limit negatives with redacted PII | Provider accepted vs delivered status, unsubscribe functional, anti-spam |
| W6E | W7 preview/security/privacy/e2e/prod with no-spend proof | WEBSITE DoD evidence only after production |

**No workarounds:** do not replace newsletter with bare `mailto:` while claiming Resend Done; `mailto:` may be fallback contact, not equivalent to server-side newsletter. No mixing contact and subscription records, no trial upgrade. Existing user data/production mail config changes require a new owner-approved change plan.

**Current:** `W6_FEASIBILITY_PUBLIC_RESEARCH_SCOPED`, `W6_RESEND_BLOCKED`, `WEB3FORMS_NOT_CONFIGURED`, `W6_IMPLEMENTATION_NOT_AUTHORIZED`, `WEB-AC16/17/18=PENDING`.
