# 05 — Scoped Delivery Workstreams, Sequencing and Risk Register

> Status: OWNER-APPROVED A + B DESIGN STRATEGY / **ENGINEERING EXECUTION NOT CLAIMED**  
> Financial principle: **Rp0 additional spend** under existing website contract until expressly changed.  
> Delivery philosophy: smallest useful refinement; preserve existing architecture and separate release evidence.

## 1. Alternatives considered and decision

| Alternative | Rough relative allocation | Status and reason |
| --- | --- | --- |
| **A — Communication / hierarchy refinement** | Low | **P0**: clarity of headline, CTA, audience selection, repeated copy and proof ordering |
| **B — Experience-led component refinement** | Low–moderate | **P1**: connect existing interaction to human relevance and retained takeaway; targeted educational bridge |
| **C — Fully immersive interactive storytelling platform** | High | **DEFER**: cost, maintenance and proof of need not established |

Relative comparisons are architecture judgments, **not cost estimates or ROI forecasts**.

## 2. P0 — Source-aware audit and editorial hierarchy

**Goal:** make the present experience intelligible before designing new UI.

**Tasks:**
1. Read current app pages and relevant shared components; capture current mobile and desktop state and confirm route destinations.
2. Recheck Studio Master, latest owner ADRs, Communication Framework, WOS release evidence and relevant security/provider docs.
3. Map each public section to page responsibility, target audience, emotional hook, causal mechanism, evidence and voluntary CTA.
4. Mark duplicated promises and contextless jargon; edit minimum necessary copy or section arrangement.
5. Verify all candidate copy against actual availability, fiction status, SEO, accessibility and language localization.
6. Preserve non-participating sections unless an identified defect requires changes.

**Deliverable:** reviewed, minimal source diff + route-by-route pre/post screenshots + comprehension QA evidence.  
**Gate:** owner-scoped engineering change, no broken links/route behavior, zero regression on required flows, QA of meaningful message recall.  
**Stop rule:** if source conflicts with an existing ratified contract, do not improvise—record and resolve via controlled decision.

## 3. P1 — Existing-component experience refinement

**Goal:** let the user *experience* cause and consequence.

**Candidate tasks** (must be individually scoped and source-verified):
- Connect the creator lighthouse before/after to a short, optional “what mental model did you use?” reflection.
- Where appropriate, make an existing notebook result summarize one changed state and the inherited next question; keep export/ownership unchanged.
- Ensure reader Current Lore / Backstory / World Guide and micro/meso/macro views refer to one internally consistent hypothetical case.
- Add curated, verified causal cross-links within Explore instead of adding graph/recommendation infrastructure.
- Refine About narrative ordering and Contact copy without new complex controls.
- Preserve existing Navbar/Navigator and approved media/image delivery.

**Gate:** no new authentication, account DB, required AI/third-party transfer, automatic canon mutation or fabricated LMS enrollments; test every modified component.  
**Stop rule:** if meaningful improvement requires a new vendor, charge, privacy capability or incompatible LMS change, log it as **BLOCKED / separate decision**.

## 4. P2 — Usability and trust validation

**Goal:** distinguish attractive design from demonstrated user comprehension.

**Candidate methods:** voluntary first-visit walk-throughs; record what a creator and a reader infer; request one paraphrase of the new idea; verify real accessible CTA navigation; inspect feature fallback and performance. Report qualitative responses as samples, not statistically validated evidence.

**Gate:** publish findings with date, environment, tested version, user/task counts if collected, observed defects and accepted/deferred follow-ups. No arbitrary adoption/retention threshold is created retroactively.

## 5. Rollback and change control

Before implementation, record:
- exact source branch/commit and release environment;
- changed files and why each is necessary;
- screenshot and functional baseline for each affected route;
- rollback path for a site behavior regression;
- proof that unrelated provider keys, LMS runtime, canonical content and deployment infra are not affected.

Use a separate worktree/branch where applicable and protect local untracked author files. Avoid sweeping formatting, dependency installs, generating unrequested artefacts in source repo, resetting dirty trees or pushing without source-governance compliance. Do not amend historic receipts to imply today's production gate passed.

## 6. Risk register

| ID | Risk | Impact | Mitigation and gate |
| --- | --- | --- | --- |
| R01 | Three-part motif becomes literal “only three elements” doctrine | Functional loss and false cognitive science | Treat as message scaffold; retain deep structures |
| R02 | Designer writes elaborate fiction before canon approval | Canon contamination | Fiction-canon vs hypothetical label in page and metadata |
| R03 | WOS mental-model transfer advertised as guaranteed real expertise | Misleading education claim | Distinguish W/M/N/X evidence; separate low-risk assessment |
| R04 | Homepage/Creators/Readers become duplicative | Cognitive noise | One primary experience per route, cross-link to depth |
| R05 | Motion and image updates harm mobile access and performance | UX regression | Reuse assets, reduced motion, responsive screenshots |
| R06 | Contact/newsletter microcopy breaks consent or provider truths | Privacy/security and trust | Freeze transport unless separately scoped; provider tests |
| R07 | Old 12–13 Oct docs override current mobile nav decisions | Navigation regression | Reinspect later ADRs and actual source before edits |
| R08 | LMS lessons implied shipped or enrollment promised | False availability | Validate actual public routes/material; omit unverified CTA |
| R09 | New feature implies data collection/server spend | Financial/privacy boundary breach | No new provider/backend; dedicated owner change request |
| R10 | Cosmetic improvement mistaken for production acceptance | False certification | Explicit acceptance gate and observed runtime QA |
| R11 | Source drift between documentation and implementation | Incorrect file/route edits | Refresh HEAD, component imports and visual baseline |
| R12 | Fictional complexity oversimplified into slogans | Loss of studio differentiation | Preserve cause-and-effect mechanism and optional L5 depth |

## 7. Workstream success policy

Completion means **accepted user experience** with preserved constraints, not maximum UI additions or maximal number of sections changed. A decision not to edit a well-functioning current element can be the correct engineering outcome.

## 8. Deferred backlog

Interactive world-simulation platform; graph database/recommendation engine; automatic model scoring; cross-user artifact accounts; community/membership/payments; aggressive animation rebuild; personalized real-time learning AI; new analytics pipeline. Each needs separate demonstrated user need, scope, risk, privacy, cost and owner acceptance.
