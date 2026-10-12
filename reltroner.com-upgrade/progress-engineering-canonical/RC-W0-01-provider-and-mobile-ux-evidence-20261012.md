# RC-W0-01 — Provider, Vercel Usage & Responsive UX Discovery Receipt

> Date: 2026-10-12 Asia/Jakarta. Status: **W0 IN PROGRESS; READ-ONLY EVIDENCE**.
> Scope: W0-AC03/05/06/07/08/09/10/11. Documentation evidence only; not W1 implementation or production approval.
> Parent: [W0 work order](../02-w0-00-read-only-discovery-work-order-20261012.md), [ratified contract](../00-ratified-frontend-architecture-contract-20261012.md), [engineering ledger](../01-engineering-progress-ledger.md).
> Previous snapshot: [RC-W0-00 interim receipt](./RC-W0-00-vercel-and-provider-discovery-receipt-20261012.md).
> Evidence provenance: owner-supplied Cloudflare / Web3Forms / Resend screenshots, Chrome desktop / 320x480 mobile screenshots, owner-provided Vercel Usage page text; GitHub code read at named Studio HEAD. Sensitive account identifiers, email addresses, access keys, tokens and personal data deliberately omitted.

## Immutable source authority for this receipt

- Documentation GitHub main before this documentation receipt: `d56e28b206f31e5cb9631d18499aa87861cb980b`.
- Studio GitHub main: `18b295f96ccb521b228a1855e79448158c09db15`.
- Studio resource GitHub main: `6c6fb38f8ff3376c0789c15bcfe4d0cafc4d057e`.
- Local Windows snapshot (historical 2026-10-12T07:35:31+07:00): `d6969ddfbc5e7d98d49b1523259785125159e722`; origin correct, no tracked changes, exactly 14 protected untracked Markdown files, one primary worktree. Local HEAD 11 commits behind remote. **Do not synchronize or mutate the protected primary checkout during W0.**

## W0-AC06 — Cloudflare Workers & Pages (PARTIAL)

Owner account UI displayed **5 existing applications** (two ERP Workers and three Pages apps including LMS and course-related sites); those resources are **outside the new website workload allocation**. Account dashboard showed Workers Requests Today `0 / 100,000`, October 1–12 Requests `4.15K`, CPU Time `144.82K ms` and Workers Build Minutes `0`. These are scoped owner-UI observations and **not** evidence of spare dedicated capacity, Workers AI Free account entitlement, billing hard cap, current model availability, or Turnstile activation.

**Remaining:** read-only Workers AI model/quota/usage; account billing/payment/overage posture; Turnstile plan/status; domain/zone relationships; potential LMS/ERP blast radius. **No** Worker creation, inference probing, secret generation, DNS changes, or API calls.

## W0-AC07 — Resend (PARTIAL for account access, UNKNOWN for free newsletter entitlement)

Resend profile/dashboard for the owner team is accessible. The screenshot provides **no** plan/quota, sending-domain verification, contact capacity, marketing/broadcast entitlement, suppression/unsubscribe state, or billing hard-limit evidence. Account profile access is **not** provider-readiness or sending authorization.

**Remaining:** metadata-only screenshots of Settings/Billing, Domains verification, Usage, Audience contacts count and unsubscribe/suppression capabilities. Never publish recipient email addresses, subscriber records or API credentials.

## W0-AC08 — Web3Forms (NOT_CONFIGURED / PARTIAL discovery)

Authenticated Web3Forms UI displayed `Create Your First Form` onboarding with an empty/initial form configuration and text stating a unique access key would be generated in the next step. **No form creation or recipient validation was shown.** Public free pricing alone does not prove the actual account's limits. Do not press `Create Form` during W0. Required data: free entitlement and quotas, verified recipient workflow, spam controls, handling of rejections/timeouts, and a confirmed existing non-sensitive fallback contact pathway.

## W0-AC05 — Vercel Usage supplementary evidence (PARTIAL)

Owner supplied the Vercel Usage screen text for `Last 30 Days`. It reports Fast Data Transfer `2.62 GB / 100 GB`, Fast Origin Transfer `5.52 GB / 10 GB`, CDN Requests `133,989 / 1,000,000`, CDN Request CPU `47s / 1h`, ISR Reads `712,526 / 1,000,000`, ISR Writes `0`, Function Invocations `164 / 1,000,000`, Build Time `4h / 100h`, Build Minutes `0s`, Build CPU Minutes `7h 14m`. **Project filter attribution was not demonstrated** by the supplied export; do not claim all usage belongs to Studio.

ISR Reads ~71.3% and Fast Origin Transfer ~55.2% of the displayed allowance merit monitoring, not automatic optimization or upgrade. The discrepancy between Build Minutes and Build CPU Minutes is a metrics-definition question, not itself evidence of error. The account remains Hobby with no payment method reported; commercial-use eligibility and independent production release gate remain unresolved. Previous production build completed at `18b295f` with 440/440 static pages; green build does not imply browser/UX/security/quotas PASS.

## W0-AC10 — Desktop and 320x480 mobile UX (PARTIAL)

Observed desktop home has working ecosystem hero presentation, global search entry and navigation, but first-contact hero explicitly promotes `Explore Ecosystem`, `Browse Knowledge Base` and `Open LMS`. **The two ratified primary paths for Creators and Readers are not yet explicit in that hero** (WEB-I03 / WEB-AC01–03). This is a present-information-architecture gap, not proof those audiences cannot find content anywhere.

320px mobile captures show: fixed mobile navbar and working navigation drawer/search entry; homepage CTAs stack vertically; `/philosophies` shows breadcrumb, category, reported count `27 records`, archive search, taxonomy signals, images and linked cards. Multiple screenshots show the fixed navbar covering scrolled content visually and unusually tall tag pills occupying a large fraction of the 320px viewport. **Accessibility/overlap impact is a remediation candidate**, not yet an automated keyboard/focus or scroll-reachability failure. The source `components/MobileNavbar.tsx` confirms `fixed inset-x-0 top-0 z-[100]`, an initial compensating spacer, and a scrollable dialog drawer. Initial spacer does not guarantee that scrolled headings remain visible. Need scroll-to-anchor, 200% zoom, keyboard and 320px overflow tests before claiming AC09 or AC22 PASS/FAIL.

The local collection's search uses `CollectionPageClient.tsx` filtering, while global Command Palette uses another ranking/index mechanism; shared-search contract (WEB-I06) not yet implemented. Screenshot evidence does not prove the publication provenance and epistemic categories of all listed cards; WEB-I04/05 are still gated.

## Related unresolved security and image risks

- Vercel `/images/background.webp` produced HTTP 404; Studio `ShellBackdrop.tsx` references it, and the Studio `.gitignore` contains `public/images/`. Windows read-only inventory confirmed the file exists locally, but GitHub remote tree did not track it: evidence strongly supports a **Git-ignored local-only asset missing from production**. No CDN purge recommended.
- Three jsDelivr `@main` image requests returned HTTP 200 with `max-age=604800`, `s-maxage=43200`, `Age=61`, and cache HIT. Same-filename freshness not proven; immutable commit-addressed URLs remain a scoped W3 design candidate.
- Production Google Analytics network request and `collect` response observed. Consent/cookies/third-party requests require further W0-AC09 audit. No unsupported privacy claims.
- `getCollectionEntry()` publication filtering and Markdown `sanitize:false` require a **negative suite**. Dynamic-route `dynamicParams=false` exists in route pages; do not assert an exploitable draft leak without representative runtime tests.

## Acceptance / gate matrix (interim, not full W0 PASS)

| W0 AC | Current status | Outstanding |
|---|---|---|
| AC01 | PASS_SCOPED | Fresh remote SHA recheck at future write gate |
| AC02 | PASS_SCOPED | Protected 14 local files, checkout still behind |
| AC03 | PARTIAL | Published-only tests, metadata & route/index consistency |
| AC04 | PARTIAL | CDN freshness test and browser console inventory |
| AC05 | PARTIAL | Project-specific usage, noncommercial eligibility, independent release gate |
| AC06 | PARTIAL | Workers AI, billing hard stop, Turnstile and zone eligibility |
| AC07 | PARTIAL_ACCOUNT_ACCESS / UNKNOWN_ENTITLEMENT | Resend sending domain/free quotas/contact lifecycle |
| AC08 | PARTIAL / NOT_CONFIGURED | Web3Forms key/form not created; quota and recipient requirements unverified |
| AC09 | PARTIAL | Cookies, tracking scripts, iframe, consent truth |
| AC10 | PARTIAL | Creator/Reader journey and mobile interaction & accessibility negative tests |
| AC11 | PARTIAL | Cross-provider cost matrix, security/threat and W1 allowlist |
| AC12 | PENDING | Final W0 owner disposition and separate G2 source authorization |

## Execution limits and next batched observation

Read-only Cloudflare account Workers AI, billing, Turnstile and zones; Resend billing/domains/audience metrics; Web3Forms public free requirements without onboarding creation; Vercel exact project filter; UX keyboard/zoom/scroll behavior and browser privacy request inventory. One sanitized batch is preferred to many small rounds. Do not enter or disclose API keys, account emails, subscriber names, payment data or secrets. This is **documentation only** in the canonical archive; no authorization for Studio edits, application PR, preview activation, main merge, deployments, AI inference, LMS/ERP mutations, or costs. Phase 1 NOT ACCEPTED, Phase 2 NOT ACTIVE.
