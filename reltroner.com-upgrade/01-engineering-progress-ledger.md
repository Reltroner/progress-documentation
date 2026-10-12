# Reltroner.com — Living End-to-End Engineering Progress & Risk Ledger

> As-of: 2026-10-12 Asia/Jakarta. Documented status is not a production certificate.
> Source authority: [README](./README.md) → [WEB ARCH contract](./00-ratified-frontend-architecture-contract-20261012.md) → [acceptance](./03-phase1-acceptance-and-invariant-traceability.md).
> Update this after every observed source/CI/preview/vendor/production change; retain dated history and mark evidence type.

## 1. Evidence rules

GIT-VERIFIED = GitHub source/ref/commit, not local runtime; OWNER-REPORTED = quoted operator status; UI-SNAPSHOT = screenshot of provider at one time; HISTORICAL = older document; PENDING = no evidence; BLOCKED = missing prerequisite; PASS_SCOPED = tested in named scope. Do not infer PASS from a design, screenshots, GitHub merge or billing tier marketing. Never fabricate counts or percent complete.

## 2. Entry snapshot and facts

| ID | Scope | Evidence | Status |
|---|---|---|---|
| WEB-E01 | progress-documentation/main initial | 73c24bcf0210b533020823c2d32680a2fea7eecb | GIT-VERIFIED, pre-ratification |
| WEB-E02 | reltroner-studio/main | 18b295f96ccb521b228a1855e79448158c09db15 | GIT-VERIFIED, at discovery |
| WEB-E03 | reltroner-studio-resource/main | 6c6fb38f8ff3376c0789c15bcfe4d0cafc4d057e | GIT-VERIFIED, at discovery |
| WEB-E04 | Studio primary Windows checkout | local HEAD d6969dd (11 commits behind Studio GitHub main 18b295f); exactly 14 protected untracked Markdown; zero tracked modifications | OWNER-REPORTED; cannot inspect local state via GitHub |
| WEB-E05 | Vercel | Hobby screenshots: deployed www.reltroner.com, apex 307 redirect, CDN/firewall dashboards, Speed Insights activation prompt | UI-SNAPSHOT; no actual billing/capacity acceptance |
| WEB-E06 | Site root implementation | app/layout.tsx loads CommandPalette, GoogleAnalytics, RouteAnalytics; app/page.tsx ecosystem gateway | GIT-VERIFIED at WEB-E02 |
| WEB-E07 | Contact source | app/contact/page.jsx + components/sections/ContactForm.jsx use Formspree endpoint and Google reCAPTCHA | GIT-VERIFIED at WEB-E02; actual submissions not tested |
| WEB-E08 | Public search/content | lib/utils/content.js uses published filter for collections; CommandPaletteDialog.tsx separate search; CollectionPageClient.tsx local filtering | GIT-VERIFIED at WEB-E02, no negative leak test |
| WEB-E09 | Image delivery | lib/assets/cdn.js uses @main, next.config.mjs remotePattern @main, ArchiveCardMedia.jsx bypasses optimization for jsDelivr | GIT-VERIFIED at WEB-E02; exact screenshot failures not root-caused |
| WEB-E10 | Markdown rendering | getCollectionEntry uses remark-html sanitize:false; embeds exist | GIT-VERIFIED at WEB-E02; untrusted HTML risk to audit |
| WEB-E11 | References | Skill-Wanderer contact uses browser Web3Forms; subscribe endpoint uses Resend Contacts then welcome email | GIT-VERIFIED public reference; **not** proof Reltroner integration |
| WEB-E12 | User requirements | Ratified expanded website Phase 1 UX+AI+contact+subscribe+zero-spend; no local file mutation | OWNER-RATIFIED design, source not implemented |

## 3. Current phase and gate

| Stage | State | Blockers/next evidence |
|---|---|---|
| Ratify website expanded Phase 1 | OWNER RATIFIED | Document commit verification required |
| W0-00 discovery | IN PROGRESS (READ-ONLY); multiple scoped receipts | Complete provider entitlements, privacy/UX, cost/release checks and owner disposition |
| W1-IA | HOLD | W0 content/map/route evidence |
| W2-Search/rails | HOLD | W0 shared index contract and responsive tests |
| W3-CDN | HOLD | W0 network/headers and existing no-cost deploy trigger |
| W4-Privacy/security | HOLD | W0 actual scripts/embeds provider map |
| W5-AI | HOLD | Actual no-spend provider entitlement, privacy, model tests |
| W6-Resend/Web3Forms | HOLD | Account, domain verification, quota, approval of provider config |
| W7-Release | HOLD | Preview/negative tests, rollback, owner release authority |
| Global Phase 1 / Phase 2 | NOT ACCEPTED / NOT ACTIVE | Independent final LMS and founder readiness gates |

## 4. Risk register (not resolved by documentation)

| Risk | Severity | Detection / mitigation gate |
|---|---|---|
| R01 untracked local authoring loss | CRITICAL | fresh local git status, no reset/clean, isolated worktree |
| R02 hidden vendor overspend or quota exhaustion | HIGH | read-only billing/free/auto-topup checks and server-side budget fail-closed |
| R03 AI canon/Earth mixing or unpublished disclosure | HIGH | publish-only index, epistemic type, negative retrieval/security tests |
| R04 third-party privacy statement false (GA already loaded) | HIGH | analytics + embed inventory, privacy-policy/config decision |
| R05 stale/broken CDN image despite same source filename | HIGH | HTTP/image tests and immutable SHA automation |
| R06 forms show false success / spam / inability to unsubscribe | HIGH | provider acceptance lifecycle, delivery not conflated with accepted |
| R07 Vercel Hobby compatibility with future commercial use | HIGH | terms/product placement review prior to paid activity |
| R08 shared VPS/HRM/LMS blast radius | CRITICAL | no resource allocation without independent authorization |
| R09 unsanitized HTML / iframe injection | HIGH | sanitize/allowlist and rendering-negative suite |
| R10 Scope creep delaying Phase 2 | HIGH | freeze accepted denominator, bounded PRs, owner-only exceptions |

## 5. Evidence receipts required for next append

For each new event: ID, timestamp, actor (Owner / ChatGPT reviewer / IDE implementation / provider UI), source exact SHA(s), change diff and affected invariants, command/test artifact or sanitized screenshot, status PASS/PARTIAL/BLOCKED/FAIL, deployment classification, cost impact, rollback, and next authorized operation. Avoid secrets, raw email addresses, IP logs and confidential inbound messages in this public repository.

## 6. First next step

Execute [W0-00 read-only discovery](./02-w0-00-read-only-discovery-work-order-20261012.md): no installs, no Git local mutations, no provider toggles, no releases. After W0 evidence and owner acceptance, write an exact W1 nonproduction work order; do NOT reinterpret ratified architecture as blanket permission to build/deploy anything.

## 7. Canonical engineering evidence archive — 2026-10-12 update

For the full reproducible, sanitized findings consult the [canonical progress archive](./progress-engineering-canonical/README.md) and its dated documents:

- [RC-W0-00 — original Vercel, GitHub, CDN and local evidence](./progress-engineering-canonical/RC-W0-00-vercel-and-provider-discovery-receipt-20261012.md); includes dated correction for a local ignored `public/images/background.webp` that was absent from deployed Git source.
- [RC-W0-01 — Cloudflare, Resend, Web3Forms, Vercel Usage and responsive UX](./progress-engineering-canonical/RC-W0-01-provider-and-mobile-ux-evidence-20261012.md). The underlying owner evidence contains UI snapshots, provider account screens and 320x480 mobile navigation/collection imagery; public receipts omit personal/account secrets.

Current W0 evidence disposition: **AC01 PASS_SCOPED, AC02 PASS_SCOPED, AC03 PARTIAL, AC04 PARTIAL, AC05 PARTIAL, AC06 PARTIAL, AC07 PARTIAL account access / UNKNOWN entitlement, AC08 PARTIAL / NOT_CONFIGURED, AC09 PARTIAL, AC10 PARTIAL, AC11 PARTIAL, AC12 PENDING.** Vercel `main` production still requires an independent technical release gate; no automatic merge into a release-tracked branch. Cloudflare Workers AI, Resend marketing and Web3Forms verification/quotas remain unproven. Retain W1–W7 on HOLD.

**Documentation commits in `progress-documentation` only** do not change `reltroner-studio`, resource files, Vercel, Cloudflare, Resend, Web3Forms, LMS/ERP, DNS, or production. Phase 1 NOT ACCEPTED; Phase 2 NOT ACTIVE.

## 8. Provider audit update + Gemini IDE QA decision (2026-10-12)

Canonical receipts: [RC-W0-02 — Provider entitlements, Resend Failed domain and Vercel metrics](./progress-engineering-canonical/RC-W0-02-provider-entitlement-domain-blocker-and-vercel-usage-20261012.md) and [RC-W0-AC10 — Gemini IDE Browser-QA work order](./progress-engineering-canonical/RC-W0-AC10-gemini-ide-browser-qa-protocol-20261012.md).

- **W0-AC08 PARTIAL / NOT_CONFIGURED:** Owner-supplied Web3Forms public pricing and account onboarding display Personal Free, 250 submissions/month, unlimited forms/domains, basic spam/hCaptcha. Pro lists Turnstile/reCAPTCHA; do not assume those included in Free. No live form or key provisioned.
- **W0-AC07 PARTIAL/BLOCKED_DOMAIN_FAILED:** Resend account billing lists Transactional 3,000 emails $0/month and Marketing 1,000 contacts $0/month; payment methods absent. 2 subscribers/0 unsubscribers. Sender `resend.reltroner.com` status **Failed**, so no assumption newsletter can send; per-record DNS diagnosis is a hard W6 prerequisite. Email metrics 0 in 15 days are no deliverability sample.
- **W0-AC06 PARTIAL:** 243 models displayed in Cloudflare catalogue, not a proof of any Free inference entitlement. Account/model usage/overage and Workers AI payment hard-stop still pending.
- **W0-AC05 PARTIAL:** Vercel ~30d displays 134,236 CDN requests, 712,452 ISR read units, 5.52GB/10GB Fast Origin Transfer, 164 Function invocations (156 success/8 user error), 34 successful builds/0 failed and ~4h/100h build time. Project breakdown is still **NOT VERIFIED**, even when page URL contains project slug: charts offer `Projects` tab and display `Total`.
- **W0-AC10 PARTIAL:** The owner proposes Gemini IDE QA under `npm run dev`. Agent source-only and public browser read-only observations are allowed; local Next dev generates `.next` and therefore needs an explicit scoped W0 generated-cache exception or future owner-authorized exact-SHA isolated worktree. Current primary local checkout has 14 protected untracked files and is 11 commits behind remote, so cannot be treated as production baseline. No Gemini browser run or localhost session is claimed to have executed.

**Status:** W0 remains IN PROGRESS; AC12 PENDING; W1–W7 HOLD; Phase 1 NOT ACCEPTED; Phase 2 NOT ACTIVE. No vendor changes, source edits or production deployment authorized or performed by the documentation receipts.

## 9. Gemini IDE browser QA received and independently reviewed (2026-10-12)

[RC-W0-03 — Independent Gemini IDE QA review](./progress-engineering-canonical/RC-W0-03-gemini-ide-browser-qa-review-20261012.md) is the sanitized reviewer receipt from the owner-supplied 08:45 WIB W0-AC10 agent report. The report declares zero tracked modifications and preservation of all 14 untracked Markdown files, source inspection, and production read-only route observations. These are **agent/owner supplied runtime observations**, distinct from GitHub source facts.

**Accepted scoped issues:** P1 observed `/contact` disabled due to missing reCAPTCHA public site key in deployed environment (source gate `canSubmit = isCaptchaConfigured && verified`); P1 first-contact Creator/Reader CTA absent in `EcosystemHero.tsx`; P2 `/images/background.webp` 404 consistent with absent remote tracking and local `.gitignore`; P2-candidate fixed mobile navbar may overlay focused/anchor content at deep scroll, impact not yet proven.

**Review correction / DO NOT MARK PASS:** 320x480 testing used a simulated isolated frame rather than true top-level 320 CSS-pixel viewport; it does not establish equivalence for viewport units, media queries and keyboard/touch. Agent claimed `15/15` and `100% route reproduction`, but focus restoration, zoom, overflow masked by `overflow-x-clip`, accessibility and negative cases were not fully evidenced. Record **W0-AC10 PARTIAL**, not full PASS or WCAG compliance. Contact failure is WEB-I11/WEB-AC18 in ratified workstream **W6**; Creator/Reader is **W1**, responsive navigation **W2**, image **W3**, privacy/security **W4**. Gemini's alternate workstream labels and WEB-AC08 contact mapping were incorrect and are not adopted.

**Next gated actions:** optional narrow read-only QA follow-up for native 320px, focus & anchor measurements; Resend failed-sending-domain per-record diagnostic; Cloudflare Workers AI entitlement/account billing; Vercel per-project usage. W0-AC12 still awaits explicit owner signoff, W1–W7 HOLD; source implementation, dev server in primary checkout, provider activation, merge/deployment all NOT AUTHORIZED. Documentation publication here does not advance execution gates.
