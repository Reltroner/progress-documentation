# RC-W7-00 — Integrated Website Phase 1 Acceptance, Release and Operational Handoff (PLAN ONLY)

> **Status:** W7 acceptance matrix/exit sequence prepared. **W7 integration NOT EXECUTED**, no G3/4/5/6/7/8 approval. Source Studio `18b295f96ccb521b228a1855e79448158c09db15` is the currently reviewed main SHA, not a release candidate SHA.
> **Binding:** [WEB-AC01..27](../03-phase1-acceptance-and-invariant-traceability.md), [WEB-I01..18](../00-ratified-frontend-architecture-contract-20261012.md), [G0–G8 governance](../05-source-workspace-and-release-governance.md), [global Phase 1 exit & Phase 2 entry](../../all-in-reltroner-master-source-of-truth/05-phase1-phase2-exit-entry-and-reentry.md).

## 1. Acceptance is not a single green build

The ratified website target is a frontend-first **identity/discovery/knowledge/relationship gateway**, not a new LMS/ERP monolith. Required outcomes: Creator and Reader first-contact IA, secondary engineering/collaborator, six epistemic types, public-only knowledge index/shared search/reading rails, immutable same-file images, original branded Reltroner Navigator with *real bounded generative AI*, Resend opt-in newsletter, Web3Forms inquiry, truthful consent/privacy, security, WCAG 2.2 AA target, SEO, performance, privacy/operations and **Rp0 incremental spending**. LMS final DoD and operations must independently pass before global Phase 1 exits.

## 2. 27-criteria dependency and evidence matrix (all NOT YET ACCEPTED end-to-end)

| Range | Owner/workstream | Required proof |
|---|---|---|
| AC01–04 | W1 + W7 | Human first-time visitor comprehension, Creator framework and Reader spoiler-aware entry, secondary engineering |
| AC05–09 | W2 + W4 + W7 | Published canonical/aliases, six epistemic types, no draft leak, shared Ctrl+K/search revision/ranking and desktop/mobile rails |
| AC10–12 | W3 + W7 | Asset health, source SHA immutable same-name refresh, 404/timeout fallback and real rendered bytes |
| AC13–15 | W5 + W2 + W4 + W7 | Navigator accessibility, real cited Free AI explanation, public-only retrieval, abuse/model quota/error tests |
| AC16–18 | W6 + W4 + W7 | Resend opt-in/unsubscribe/suppression, correct free quotas and sender; Web3Forms intent/contact acceptance, spam/failure/recipient |
| AC19–20 | W4 + W7 | Clean-session GA preconsent/request/cookie controls; notice matches network; Markdown/iframe/XSS negatives |
| AC21–23 | W7 | Routes/canonical/sitemap/robots/structured SEO, representative WCAG 2.2 AA tests, LCP/INP/CLS targets (field p75 if available; lab is supplemental) |
| AC24–25 | W7 + all | CI on exact candidate source SHA, content/typecheck/negative/regression; no protected drafts; account-specific free quotas, hard stops, provider usage and no charges |
| AC26–27 | G4–G8 + owner | Exact approved preview/production deploy SHA+ID, smoke/security/cost/rollback, operations signoff, explicit website Phase 1 DoD |

No explicit versioned owner-approved waiver or revised denominator is recorded. **Do not turn “local W1 component PASS” into “WEB-AC01..04 DONE”.** All 27 must get a future field status/evidence receipt. This table is a test plan, not results.

## 3. Mandatory negative end-to-end tests

- Unpublished/draft fixtures (approved and synthetic) do not reach public index, static route/HTML, sitemap, Ctrl+K, AI retrieval or related content.
- Prompt injection, false citation/canon contamination, model timeout/paid-only/403/429, quota exhaustion, invalid inputs and isolation from LMS/HRM/Keycloak/secrets.
- Markdown/embed scriptable HTML/XSS and unsafe URL tests in local controlled test fixtures.
- Resend repeated opt-in/unsubscribe/re-subscribe/suppressed state, welcome vs active/verified truth, no mixing inquiry with newsletter; provider rejection and rate-limit.
- Web3Forms reject/timeout/bot/quota/recipient fallback; manual follow-up state truthful.
- GA network before and after consent, clean Incognito/no cookies/blocked tags before opt-in if strict basic mode; no other undisclosed third-party network calls.
- Images 404/timeout/wrong MIME and same-name R0→R1 refreshed immutable URL with visibly new bytes, cache stable rollback.
- A11y keyboard, focus, 200% zoom, 320/375 mobile drawer/readers/CTA, ARIA and reduced-motion; screen-reader sampled where available.
- Link/SEO/canonical/sitemap/robots, 404/redirect/alias/legacy anchors; sitemap no drafts; no silent unapproved provider preview.

## 4. Release sequence and stop gates

```text
W1..W6 scoped workstream proofs + independent review
  -> G3 exact source candidate PR and CI (owner grants separately)
  -> G4 preview/usage/privacy/security/no-spend tests (owner grants separately)
  -> G5 explicit merge authorization (check Vercel main auto-production!)
  -> G6 explicit production release authorization and rollback rehearsal
  -> G7 actual production HTTP/browser/privacy/provider/cost smoke and incident ownership
  -> G8 website 27/27 disposition + owner DoD sign-off
  -> independent LMS final DoD + operations handoff
  -> GLOBAL Phase 1 exit owner receipt
  -> founder readiness check
  -> explicit Phase 2 activation
```

If Vercel auto-deploys main on merge, do not conduct G5 until G6 deployment risk is understood and jointly authorized in an explicit release plan. Do not create Vercel Preview automatically via a G3 PR before pricing/usage posture is reviewed and authorized. Do not claim Vercel Hobby is necessarily viable for commercial monetization: official [Vercel Terms](https://vercel.com/legal/terms) and [Hobby plan](https://vercel.com/docs/plans/hobby) restrict Hobby use to personal/noncommercial purposes. Since this website is intended to support future monetization, **commercial use classification is a release/business-model constraint**, not a permission to upgrade or secretly pay. Owner must settle deployment entitlement or separately ratify a cost-neutral compliant alternative if actual site use exceeds Hobby's permitted scope.

## 5. Operational acceptance receipt schema

For each test/criterion record: `AC_ID | WEB_I_IDS | GATE | source_SHA | resource_SHA | build_ID | deploy_ID | URL | user_agent/viewport | execution_time | actor/tool | test_command/evidence | positive | negative | observed_cost | privacy | status | residual | rollback_owner`.

Evidence should be reproducible, sanitized, immutable by SHA and attached to canonical documentation or securely retained with accessible hash/path; no raw cookies, API secrets, email addresses or private author drafts in public GitHub.

### W7 current exit state

`W7_PLAN=PREPARED`, `W7_EXECUTION=NOT_STARTED`, `G3..G8=NOT_AUTHORIZED`, `WEBSITE_PHASE1_DOD=NOT_ACCEPTED`, `GLOBAL_PHASE1=NOT_EXITED`, `PHASE2=NOT_ACTIVE`. No claim W3/W5/W6 completed.
