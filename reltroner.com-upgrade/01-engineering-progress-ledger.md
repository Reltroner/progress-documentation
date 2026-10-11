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
| WEB-E04 | Studio primary Windows checkout | main up to date, 14 untracked files (12 music, 2 places) | OWNER-REPORTED; cannot inspect local state via GitHub |
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
| W0-00 discovery | START AUTHORIZED (READ-ONLY) | Complete W0 checks and owner disposition |
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
