# 10 — Decision Register, Evidence State, Risks & Open Questions

> Archive checkpoint: 2026-10-12. This register intentionally distinguishes **ratified**, **frozen**, **reported**, **candidate** and **unknown**. It is not a live task runner.

## Ratified strategic decisions
| ID | Status | Decision | Authority |
|---|---|---|---|
| ST-01 | RATIFIED | Intellectual product is Creative Compound Machine plus civilizational simulation; tech is a medium | Studio Master v2.3 |
| ST-02 | RATIFIED | Creator-facing outcomes emphasize agency, less stagnation and enjoyable continuity; no guaranteed burnout or fan growth outcome | Studio Master §§2, 55 |
| ST-03 | RATIFIED | Unpublished narrative seasons remain mutable; public canon has stricter release/change controls | Studio Master §§48–50 |
| ST-04 | RATIFIED | Phase 1 = accepted full LMS production DoD + reltroner.com landing UX + operational handoff | Studio Master §55 |
| ST-05 | RATIFIED | Phase 2 active community branding only after Phase 1 exit and founder readiness | Studio Master §55 |
| ST-06 | RATIFIED | Phase 2 engineering is maintenance-first, except real incidents and approved business-driven requests | Studio Master §55 |
| ST-07 | RATIFIED | No unearned publishing/crowdfunding authority; no revenue/retention claims without evidence | Studio Master §§52, 55 |

## Frozen external-to-archive technical decisions
| ID | Status | Decision | Authority |
|---|---|---|---|
| TECH-01 | FROZEN | LMS 6-service microservice topology and API trust/permission model | LMS logical contract |
| TECH-02 | FROZEN | Only LMS API Gateway publicly exposed, learner/admin separate Cloudflare frontends | LMS placement contract |
| TECH-03 | FROZEN | Keycloak canonical issuer/realm and LMS OIDC audiences/clients | LMS logical contract |
| TECH-04 | FROZEN | Source-controlled course catalog, owner-specific Postgres persistent state, Redis replaceable runtime | LMS contracts |
| TECH-05 | FROZEN | Assistant/Knowledge are noncanonical derived access surfaces, Audit append-only authority | LMS logical contract |

## Current evidence bounds
As of the 2026-10-11 source checkpoint:
- Phase 3 nonproduction source/contract acceptance does not mean runtime PASS.
- Phase 4A read-only discovery closed conditionally with residual issues, not an unqualified 18/18 pass.
- Phase 4B G03 source metadata alignment in backend `main=617dadc0d0d627071d713ceb729df6658202b43e` with 7/7 CI does not authorize production or certify Keycloak/Redis/live trust.
- No verified paid-mentorship customers, conversion rate or sales revenue in the reviewed project materials.
- This archive's creation is documentation work, **not** LMS implementation, account provisioning, deploy, Phase 1 freeze or Phase 2 activation.

For more recent evidence, refresh [LMS README](../lms/README.md) and [ledger](../lms/engineering-end-to-end-progress-ledger.md).

## Historical decisions and supersession
Earlier discussion considered simultaneous distribution, freelancing experiments and creator monetization. The later 11–12 October founder decisions prioritize existing LMS work and landing closure before active multi-channel community work. Keep prior debates in the historical source without silently converting them into active orders. The history also reports a possible **6 December 2026 career program plan**, not confirmed enrollment, outcome or guaranteed resource availability. Re-evaluate any collision using current evidence, not a dated forecast.

## Unresolved questions requiring real discovery
- What precise LMS final product DoD and runtime/security gates remain at the latest ledger checkpoint?
- Does the current frontend implementation fully match the frozen OIDC client/issuer and privilege architecture? Which gaps have receipts?
- What is accepted production landing page contract for reltroner.com (content, responsive, SEO/accessibility, test reports)?
- What owner-approved budgets and provider accounts exist for outbound WhatsApp, meeting integrations and inference?
- Is learner profile/account UI integration best served by Keycloak theming, account console customization or a separate approved ADR?
- Which initial curriculum exercises best prove Creative Compound Machine transferability?
- When does founder readiness make Phase 2 participation sustainable?
- Which communities allow which types of contribution/promotion currently?
- Can learners independently use the method and do any observed outcomes justify claims about enjoyment/continuity/fan engagement?
- Is paid one-on-one diagnostic/mentorship actually demanded, affordable and deliverable at the desired price?
- Does a new AI runtime solve a verified need beyond existing Knowledge/Assistant/n8n capability?

## Risk register
| Risk | Consequence | Guardrail |
|---|---|---|
| Infinite Phase 1 scope | community work never starts | 100%=accepted frozen scope, new ideas go to backlog |
| Premature Phase 2 | fragmented attention/context loss | mandatory owner Phase 1 exit and readiness |
| Engineering contract drift | production insecurity and distributed monolith | ADR/contract authority, six-service boundaries |
| Branding guru overclaim | distrust, unmet expectations | evidence ladder and caveats |
| Narrative canon leakage | loss of rewrite freedom | draft status and selective spoiler-safe disclosure |
| Expensive AI/tool proliferation | VPS instability and recurring cost | cost/benefit, capacity, overlap and explicit owner approval |
| Trust/engagement confusion | wrong business decisions | evidence states, actual transactions and retention |
| Public sensitive data | privacy/security harm | no secrets or learner data in docs/case studies |

## Standard decision record template
~~~yaml
id: REL-DECISION-YYYY-NNN
date: YYYY-MM-DD
domain: studio-strategy | LMS | canon | marketing | finance
status: CANDIDATE | OWNER_RATIFIED | FROZEN | SUPERSEDED
claim: ...
evidence: [links/to/sources]
assumptions: [...]
not_implied: [...]
scope: [...]
resource_cost: ...
owner_authorization: ...
review_trigger: ...
~~~

Do not insert placeholder “approved” decisions without the human owner's explicit action.
