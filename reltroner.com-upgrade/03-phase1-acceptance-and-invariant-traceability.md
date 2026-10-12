# RC-WEB-AC-001 — Phase 1 Website Acceptance Matrix & Invariant Crosswalk

> **2026-10-13 OWNER AMENDMENT — [RC-WEB-ADR-008](./08-owner-execution-authority-and-dedicated-creator-reader-tsx-adr-20261013.md):** The owner explicitly requires the homepage Creator/Reader CTAs to enter **new independent TSX onboarding pages** `/start/creators` and `/start/readers`, with existing Markdown documents only as later optional reading. WEB-AC01–04 now evaluate the **two-step** homepage → TSX orientation → published article/series path, not direct jump to an MD-derived article. Previous W1 acceptance evidence is historical for older CTA destinations; two new routes require a fresh code/test receipt. Owner may direct cross-workstream order without ceremonial permission loops, but 27 WEB-AC, objective evidence and no-spend remain binding; none of the acceptance states in the table below is silently promoted to PASS.


> Date: 2026-10-12 Asia/Jakarta. STATUS: **RATIFIED CONTRACT / TESTS NOT YET EXECUTED**.
> Owner ratification sets feature scope, not PASS results. Exact thresholds are **initial test targets** until a W0 measurement and owner-approved benchmark receipt.
> All status entries below are PENDING by default; mark PASS_SCOPED only with an immutable source/runtime proof.

## 1. Acceptance principles

1. **Two different exits**: (a) website Phase 1 production DoD; (b) overall Reltroner Phase 1, including independent LMS and operational handoff; then explicit founder Phase 2 activation.
2. Evidence is layered: design accepted != implemented != CI tested != preview tested != production verified != owner final sign-off.
3. A public feature that requires optional free third-party inference must be proven functional, **not** represented as AI if only deterministic FAQ works. Free quota exhaustion must fail honestly without paying.
4. No feature may silently be deferred after ratification. A deferral or revised scope needs owner-signed amendment, with the consequence to Phase 1 exit recorded.

## 2. End-to-end web acceptance criteria (WEB-AC01..WEB-AC27)

| AC | Requirement / intended proof | State |
|---|---|---|
| WEB-AC01 | First-time visitor identifies what Studio offers, creator vs reader route and actual availability; comprehension test observed | PENDING |
| WEB-AC02 | Creator journey to concrete Creative Compound framework/proof works with keyboard/mobile | PENDING |
| WEB-AC03 | Reader journey to spoiler-safe Asthortera, with canon/speculative boundary, works | PENDING |
| WEB-AC04 | Third real-world/engineering collaborator lens is discoverable without conflating with fiction or making unoffered commercial promises | PENDING |
| WEB-AC05 | Every indexed public entry has canonical route, publication status, epistemic type and preserved permalink/redirect | PENDING |
| WEB-AC06 | unpublished/private/draft source never surfaces in static search, AI retrieval, public routes, sitemap or HTML output (negative suite) | PENDING |
| WEB-AC07 | Ctrl+K and archive sidebar use compatible ranking/index/version and keyboard focus behavior | PENDING |
| WEB-AC08 | Desktop left reading path, center bounded editorial prose, right archive explorer; no keyboard traps | PENDING |
| WEB-AC09 | Mobile rails collapse into usable drawers; no overflow, content blocking or conflicting chatbot | PENDING |
| WEB-AC10 | Critical images load, have semantic alt/fallback and predictable geometry, with representative device/network test | PENDING |
| WEB-AC11 | Same-name asset push results in website URL referencing newest immutable resource SHA through controlled no-cost automation | PENDING |
| WEB-AC12 | Image fault injection: broken origin/network/404 shows meaningful placeholder; core navigation remains usable | PENDING |
| WEB-AC13 | Navigator launcher visible across all publicly accepted layouts; reset, quick prompts and accessible keyboard/mobile interaction | PENDING |
| WEB-AC14 | Generative AI answers grounded in public approved sources, links correct pages, respects fiction/nonfiction separation and uncertainty | PENDING |
| WEB-AC15 | AI abuse, prompt injection, private source access, oversize input, quota exhaustion and provider failure tests; no privileged tool access | PENDING |
| WEB-AC16 | Subscription with Resend: explicit opt-in, provider accepted vs welcome email sent/verification states separated, no duplicate activation | PENDING |
| WEB-AC17 | Subscription unsubscribe/re-subscribe and suppression behavior verified; direct contact submissions do not enter mailing list | PENDING |
| WEB-AC18 | Web3Forms accepted/rejected/timeout/spam handling and correct manual reply expectation; reachable fallback email | PENDING |
| WEB-AC19 | Privacy notice, cookies, analytics, third-party assets, embeds, contact and AI processing statements match production requests | PENDING |
| WEB-AC20 | Markdown HTML/iframe sanitization/allowlist negative security tests; no XSS regressions on known safe embeds | PENDING |
| WEB-AC21 | All known public routes, links, SEO metadata, canonical, sitemap/robots and relevant structured data verified | PENDING |
| WEB-AC22 | WCAG 2.2 AA **target** across representative critical pathways: headings, contrast, labels, input errors, focus, motion | PENDING |
| WEB-AC23 | Core Web Vitals **target** p75 LCP <=2.5s, INP <=200ms, CLS <=0.1 on meaningful real-user evidence where available; Lighthouse/lab supplemental, not claim of real-field p75 | PENDING |
| WEB-AC24 | Typecheck/build/content-validate and regression suite succeed on exact release candidate SHA; no protected local file stage | PENDING |
| WEB-AC25 | Zero incremental spending verified for deployed vendors/plans, provider quotas and hard-stop/fallback, no forced upgrade | PENDING |
| WEB-AC26 | Preview-to-production release receipt: exact SHA, deploy ID, domain, smoke checks, rollback, incident ownership | PENDING |
| WEB-AC27 | Owner explicit website Phase 1 DoD sign-off; global Phase 1 and Phase 2 separate and still gated | PENDING |

## 3. Invariant-to-acceptance crosswalk

| WEB invariant | Primary acceptance |
|---|---|
| I01 strategic gates | AC26, AC27 |
| I02 TS/TSX frontend-first | AC24 |
| I03 two strategic audience paths | AC01, AC02, AC03, AC04 |
| I04 epistemic types | AC03, AC04, AC05, AC14 |
| I05 Git published-only truth | AC05, AC06, AC14 |
| I06 shared search | AC07 |
| I07 adaptive rails | AC08, AC09 |
| I08 immutable images | AC10, AC11, AC12 |
| I09 branded assistant | AC13 |
| I10 bounded AI | AC06, AC14, AC15 |
| I11 Web3Forms | AC18 |
| I12 Resend | AC16, AC17 |
| I13 privacy | AC19, AC20 |
| I14 Rp0 additional spend | AC15, AC25 |
| I15 local file protection | AC24 |
| I16 LMS isolation | AC15, AC20, AC25 |
| I17 nonfunctional production evidence | AC19–AC26 |
| I18 separate authorization gates | AC26, AC27 |

## 4. Workstream checkpoints

| Workstream | Required inputs | Exit/output |
|---|---|---|
| W0 Discovery | Source, user local status, billing/cost and UI/network evidence | W0-AC01..12 scoped receipt, gaps and owner-approved next work order |
| W1 IA | W0 taxonomy/route inventory | Creator/Reader journeys, labels, route compatibility, IA tests |
| W2 Search/rails | W1 metadata and public index | AC05–09 |
| W3 Assets | W0 asset/cache/build evidence | AC10–12 |
| W4 Security/privacy | W0 real external requests/scripts | AC06, AC19–20 |
| W5 AI | W0 free provider entitlement and public index | AC13–15, AC25 |
| W6 Subscribe/contact | W0 vendor account/domain evidence | AC16–18, AC19, AC25 |
| W7 Integrated acceptance | All scoped workstream receipts | AC21–27, cost and owner release receipt |

## 5. Test evidence format

For every AC: ID, version/date, goal, inputs (source SHA/resource SHA/provider config class), tool/actor, reproducible execution or sanitized test artifact, actual outcome, exact negative cases, applicable WEB-I IDs, costs observed, decision PASS_SCOPED/PARTIAL/BLOCKED/FAIL/N/A_WITH_REASON, reviewer, unresolved risk. Final summary must enumerate **27/27 statuses**; never invent all-pass. A build PASS is not domain runtime/cost/privacy PASS.

## 6. Release and rollback gate

Release requires all mandatory accepted ACs either PASS_SCOPED with integration evidence or an explicit owner-approved scope amendment and disclosure. Approvals in order: source changes reviewed → preview smoke/security and usage → **separate owner production authorization** → controlled deployment → post-deploy verification → website DoD receipt → independent overall Phase 1 exit. Never auto-activate Phase 2.

