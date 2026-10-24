# 06 — UI/UX Acceptance Criteria, Test Scenarios and Evidence Protocol

> Status: PROPOSED ACCEPTANCE SPEC — owner-approved design intent, criteria subject to final bounded implementation review.  
> Baseline: existing website obligations are **not replaced** by the additional criteria below.  
> No fabricated measurement baseline, uplift percentage or release PASS status.

## 1. Acceptance philosophy

Tests should measure real **relevance, causal understanding, retained insight, navigation, agency and trust** rather than aesthetics in isolation. The rule of three constrains primary message hierarchy, never deep content or functional controls.

Treat **source review, automated checks, rendered manual inspection and production evidence as different classes**. A source commit is not production acceptance; a mockup is not deployed UI; a positive test result is not proof of learning efficacy.

## 2. Proposed acceptance matrix

| ID | Dimension | Observable pass condition | Evidence |
| --- | --- | --- | --- |
| TED-AC01 | Home purpose | New visitor can summarize the studio's basic role without internal terminology | Recorded first-visit paraphrase |
| TED-AC02 | Two routes | Home distinctly offers creator and reader choices with truthful destinations | Keyboard/click route test |
| TED-AC03 | Emotional relevance | Target visitor identifies one relevant concern or story choice on entry | Task observation and paraphrase |
| TED-AC04 | Novel causality | Visitor explains **why** one choice or rule changed an outcome | Cause→effect comprehension probe |
| TED-AC05 | Memorable insight | Visitor recalls one relevant takeaway after a bounded delay | Consistent optional recall task; time recorded |
| TED-AC06 | No cardinality damage | Existing six-step method, narrative lenses, WOS depth and Explore intents remain accessible | UI + source coverage check |
| TED-AC07 | Creator usability | Visitor can run a small creative example without mandatory sign-in/paid tool | End-to-end guest walkthrough |
| TED-AC08 | Creator artifact | User can inspect/copy/export their own meaningful result where existing feature supports it | Worksheet/export test |
| TED-AC09 | Mental-model prompt | User can identify one reasoning pattern separate from fictional nouns | Answer from use-case prompt |
| TED-AC10 | Transfer safety | Any real-world analogy names mismatches/needed evidence and stays low-risk/optional | Editorial and scenario review |
| TED-AC11 | Reader experience | Person-level stakes precede macro classification | Reading-order inspection |
| TED-AC12 | Narrative consistency | Current Lore, Backstory, Wiki/World Guide explain compatible aspects of same preview | Scenario continuity QA |
| TED-AC13 | Epistemic integrity | Hypothetical/non-canon content is not labelled as published Asthortera events | Copy and metadata audit |
| TED-AC14 | Explore discovery | Existing curiosity intents/collections remain reachable; no silent exclusion by new filters | Multi-path navigation test |
| TED-AC15 | About credibility | Founder/capability claims align with inspectable sources and do not imply unevidenced credentials | Claim provenance review |
| TED-AC16 | Contact honesty | Inquiry intent, provider acknowledgement and likely follow-up are accurately explained | Form success/error/duplicate as relevant |
| TED-AC17 | Privacy/consent | No automatic newsletter sign-up, tracking or notebook AI transmission introduced | Static/runtime privacy audit |
| TED-AC18 | Accessibility | Keyboard focus order, focus visibility, semantic headings, readable contrast and reduced motion preserved | Mobile + desktop assistive checks |
| TED-AC19 | Responsive | No overlapping header, hidden CTA, clipping or unreadable paragraphs on selected viewports | Owner screenshot review |
| TED-AC20 | Navigation continuity | Global menu/search/Navigator/reading path retain latest accepted behavior | Regression across all six routes |
| TED-AC21 | Images/media | Existing artwork/critical media stay correct, legible and current; source URLs honest | Source/asset render QA |
| TED-AC22 | Performance | Proposed change does not cause an unreviewed critical regression; budget set from observed baseline | Repeatable performance comparison |
| TED-AC23 | Security/cost | No new secret exposure, privileged LMS call, vendor spend or required service introduced | Change diff, dependency/provider audit |
| TED-AC24 | Release evidence | Current code SHA, build, relevant tests, actual page acceptance and rollback path are recorded | Versioned release receipt |

**Interpretation:** A candidate may satisfy a criterion through *existing unchanged code* if the observed behavior already passes. Do not create features merely to tick a document row.

## 3. Example user task probes

### Probe A — First-time creator

Give a first-time participant the /creators page with no technical preamble. Ask them to find a way to move forward from a single fictional idea, identify what changes, and state the next question. Then optionally ask which abstract pattern they used. Record whether they could access the actual working feature and keep their artifact.

### Probe B — First-time reader

Open /readers; ask what decision the fictional person faces, how an institutional response may change the stakes, and what uncertainty remains. Ask whether they understood the preview's **hypothetical/noncanonical** status.

### Probe C — Mixed curiosity

Open /; ask participants what Reltroner Studio does, where they would go to make a world versus discover one, and how they would find deeper material without reading a whole manifesto.

### Probe D — Trust and contact

Open /contact; ask what they may submit, whether this subscribes them to anything, what confirmation really means, and whether a guaranteed immediate live call was promised. Use test-safe provider behavior; never flood or spend on live sends.

### Probe E — Lightweight recall

After a predeclared short gap and without showing the page, ask participant to state one idea, one change, and what new possibility followed. Log the exact interval and response; do not present one recall result as universal memory science.

## 4. UX research data minimization

For usability observations, keep only necessary anonymous notes and consented data. Do not collect identifiable drafts, private creative IP or recordings by default. If recording or quoting a participant, obtain separate permission. Avoid unconsented analytics event insertion under the pretext of research.

## 5. Quality review dimensions

- **Message fidelity:** relevance/novelty/memorability without manipulating the visitor.
- **Causal fidelity:** consequence derives from premise, actor, conditions and interactions.
- **Educational honesty:** fictional example, articulated model, near transfer and cross-domain transfer kept distinct.
- **Production honesty:** release statuses, services, published content and CTA availability checked against actual evidence.
- **Non-regression:** same or better guest navigation, accessibility, privacy, asset correctness and responsiveness.

## 6. Evidence protocol and status labels

For each accepted change: ID, route, source commit SHA, file/section, baseline observation, test environment, tested date, automated suite status, manual viewport evidence, user scenario evidence if collected, outstanding limitation, reviewer, rollback and final owner acceptance. Status terms: **NOT_RUN / FAIL / PARTIAL / PASS_SCOPED / OWNER_ACCEPTED / PROD_ACCEPTED**. Never label a route “PROD_ACCEPTED” merely because a build passed.

Existing WEB-I01–I18, 27 WEB-AC and subsequent accepted changes retain precedence. This TED-specific test package is supplementary, **not a reset of frozen production definitions**.

## 7. Go / no-go rule

**GO for a bounded patch** only with appropriate owner scope, current HEAD and available safe validation. **GO for public release** only with affected-route regressions cleared, truthful claims, accessibility/security/privacy/cost compliance, and explicit release acceptance. If the page already meets intent, leave it unchanged and record why.
