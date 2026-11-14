# Reltroner Statistics — Team Capacity, Roles, Roadmap and Delivery Model

> **Document class:** Historical staffing and delivery **planning estimate**.  
> **Original planning reference:** November 2026.  
> **Archived:** 2026-11-14 (Asia/Jakarta).  
> **Status:** **Planning scenarios, not approved hiring, binding deadlines, actual timesheets or confirmed cost estimates.**  
> **Baseline analyzed:** Statistical/Data Intelligence scope (12-person balanced team).  
> **Expanded vision scenario:** Full Creative Intelligence scope could increase the capacity estimate to 14–16 people, conditional on scope ratification.  
> **Companion vision:** [Creative Intelligence & Worldbuilding Engineering](./2026-11-14-creative-intelligence-and-worldbuilding-vision-proposal.md).  
> **Related completed engineering chronology:** [End-to-End Engineering and Production Chronicle](./2026-11-14-end-to-end-engineering-and-production-chronicle.md).

## 1. Executive staffing model

The original November 2026 assessment estimated that completing the *full statistical/data-intelligence architecture* of Reltroner Statistics would benefit from a balanced team of **12 people**, operating at approximately **10–11 effective full-time equivalents (FTE)** over **8–12 months**, under favorable planning assumptions.

| Planning measure | Historical baseline estimate |
| --- | --- |
| Recommended members for the statistical/data scope | **12 people** |
| Effective allocation | **10–11 FTE** |
| Broad delivery estimate | **8–12 months** |
| Main engineering disciplines (original grouping) | **7** |
| Total aggregate effort, rough planning range | **70–110 person-months** |
| Scope | Statistical observatory, historical analytics, source integrity, drift, graph, UI, eight-format reporting and CI/CD |

**Interpretation:** these figures were estimates for comparative resourcing discussions, not measured labor, formal company staffing requirements or evidence that twelve employees were hired. A team can include several part-time allocations; one person may hold multiple competencies, with a corresponding impact on actual throughput.

The supplied analysis also considered a broader **Creative Intelligence & Narrative Systems** vision. In that expanded scenario, the speculative staffing envelope was revised to **14–16 people** to cover narrative systems, canon curation and possibly evidence-grounded AI/RAG work. The higher number should **not** be read as a later ratification of headcount or as a proven duration for the broader scope.

### 1.1 Why this is multidisciplinary

Reltroner Statistics is not merely a website with charts. Its intended product scope includes:

- Software product architecture and platform integration.
- Read-only GitHub source ingestion, integrity checking and versioned provenance.
- Data normalization, historical observations and quantitative validation.
- Computational statistics, visualization and optional ML.
- Typed knowledge graphs, dependency/impact analysis and semantic quality.
- Responsive UX, accessible interactions and visual analytics.
- Eight-format report generation and build artifact integrity.
- Cross-platform testing, CI/CD, Cloudflare release isolation and operational recovery.
- Canon governance, creator review and (in the expanded proposal) narrative analysis.

The need for a specialist depends on the work **and** on the availability of reliable cross-functional contributors. Avoid assuming that every role corresponds to one continuously full-time salaried employee throughout the entire program.

## 2. Historical initial repository maturity and its limitation

The supplied team assessment referenced an earlier repository snapshot at short commit prefix `39ecf272` with approximately **40 tracked files**. At that early checkpoint it reported a read-only GitHub adapter, deterministic comparator, source contracts, baseline regression tests and dependencies for Astro, React, ECharts, React Flow, Motion and Playwright.

The source described the project as having already moved beyond an empty starter repository while still facing substantial remaining effort in multi-page UI, statistical ML, graphs and export engine.

**Temporal warning:** this was an **early planning snapshot**, not the final November 14 production state. Subsequent engineering recorded in the [Engineering Chronicle](./2026-11-14-end-to-end-engineering-and-production-chronicle.md) implemented additional capabilities, merged production work and successfully deployed the Statistics site at a later SHA. Do **not** describe the deployed project as only 40 files or still missing all those modules on the basis of the older estimate.

The original short SHA and file count are preserved as *supplied historical planning context*, not independently re-measured current facts in this document.

## 3. Twelve roles in the baseline model

| # | Role | Headcount slot | Core accountability |
| --- | --- | --- | --- |
| 1 | **Product Owner / Canon Director** | 1 | Product scope, priority decisions, Asthortera canon ratification, acceptance and source-authority boundaries |
| 2 | **Principal Software Engineer / Tech Lead** | 1 | Architecture, TypeScript engineering, integration design, technical reviews and difficult system decisions |
| 3 | **Senior UI/UX Product Designer** | 1 | Design system, user journeys, responsive interaction, motion standards and accessibility |
| 4 | **Frontend Software Engineer** | 1 | Astro/React application, navigation, page composition, state management, theme, search and interaction |
| 5 | **Data Visualization Engineer** | 1 | Correct data-to-chart semantics, ECharts, scatter/treemap/time-series, axes, tooltips and interactive interpretation |
| 6 | **Backend / Platform Engineer** | 1 | GitHub API source retrieval, comparator, provenance, object caching, version integrity and platform contracts |
| 7 | **Data Engineer** | 1 | Structured ingestion, canonical identifiers, normalization, schemas, historical observations and valid unit/time metadata |
| 8 | **Data Scientist / ML Engineer** | 1 | Python analytics, descriptive statistics, K-Means/DBSCAN, outlier methods, model sufficiency and statistical validation |
| 9 | **Knowledge Graph Engineer** | 1 | Entity extraction, typed relationships, dependency/impact traversal, React Flow and graph evidence integrity |
| 10 | **Report Automation Engineer** | 1 | HTML-to-PDF and XLSX/CSV/Markdown/XML/JSON/TXT generation, ZIP archives and export consistency |
| 11 | **QA Automation Engineer / SDET** | 1 | Unit, integration, regression, end-to-end, cross-platform, browser, statistical and accessibility testing |
| 12 | **DevOps / Cloud Security Engineer** | 1 | GitHub Actions, Cloudflare Pages, release gates, token security, deployment observability and safe recovery |
| | **Total** | **12** | Balanced functional coverage, not necessarily 12 full-time allocations |

A condensed organizational restatement from the original analysis was: one Product Owner/Canon Director, one Tech Lead, one designer, **two frontend and visualization specialists**, one platform specialist, one data engineer, one data scientist, one graph specialist, one report specialist, one QA specialist and one DevOps/security specialist.

### 3.1 Product Owner and Tech Lead are complementary

The creator may hold the functions of:

- Product Owner.
- Canon Director.
- Technical Architecture Reviewer.

This concentration can be reasonable for intellectual-property direction, story ratification and product strategy. The historical analysis nevertheless recommends a dedicated **Tech Lead engineering function** for code architecture, integration, review and release quality so the Product Owner does not become a bottleneck on every technical decision.

That recommendation does not presume the founder has recruited a separate lead; the function could be fulfilled under an appropriate accountable staffing or collaboration arrangement.

### 3.2 Frontend and visualization are not interchangeable

**Frontend engineering** ensures that pages and user workflows exist and work: navigation, accessibility, state, form behavior, React composition and responsive layout.

**Visualization engineering** validates how quantitative meaning is encoded: logarithmic scales, missing-value presentation, bubble sizes, tooltip values, comparative axes, color/shape mappings and avoiding deceptive chart interpretation.

Combining these into one role is possible, but the visual correctness work still requires distinct review coverage.

### 3.3 Data engineering versus data science

**Data engineering** ensures each observation has a valid country/entity key, time period, unit, source SHA, field path and canon status; it owns schema consistency and reproducible source transformations.

**Data science** tests whether a conclusion is statistically defensible: sampling sufficiency, outlier interpretation, clustering stability, time-series coverage, leakage, evaluation and missing-data behavior.

A correctly rendered model can still be methodologically invalid if its input data or labels are wrong.

### 3.4 Knowledge graph is an evidence engineering discipline

The graph engineer must not conflate relationships such as `MENTIONS`, `DEPENDS_ON` and `DERIVED_FROM`. A textual mention is not proof of dependency or causation. Mixing these relation types can produce deceptive impact reports and spurious creative recommendations.

### 3.5 Report engineer, QA and security remain independent quality functions

Report generation must preserve the same analytical finding across eight formats; correct layout alone does not establish source integrity. QA must independently verify mathematical, data-contract, browser and export behavior. DevOps and security must ensure publishing cannot affect another Reltroner project or reveal secrets.

## 4. Workload distribution by engineering discipline

The historical assessment used the following **estimated work-share distribution**, not tracked hours:

| Workstream | Approximate share | Illustrative responsibilities |
| --- | ---: | --- |
| **Platform & Data Engineering** | **24%** | GitHub ingestion, normalization, evidence provenance, source QA rules |
| **Frontend & Visualization** | **23%** | Multi-page app, interaction, accessible charts, themes and animations |
| **Statistical Computing & ML** | **18%** | Historical analytics, clustering, outlier detection, reproducibility |
| **Graph & Report Engineering** | **17%** | Dependency graph, impact analysis and eight-format exports |
| **Quality, Security & Deployment** | **12%** | CI/CD, testing, accessibility, cloud secrets and production verification |
| **Product & Domain Validation** | **6%** | Requirements, canon authority, planning and acceptance |
| **Total** | **100%** | Illustrative allocation, not audited actual effort |

These six workstreams are a *workload grouping*; the original headline's **seven major engineering disciplines** is a separate way of describing expertise. They are not intended as matching counts of team roles or independent FTE allocations.

## 5. Four staffing scenarios and trade-offs

| Staffing scenario | People | Historical planning duration | Major trade-off |
| --- | ---: | --- | --- |
| **Solo engineer + AI agents** | 1 | **24–48+ months** | Single-person bottleneck, limited independent validation, accumulated integration responsibility |
| **Lean multidisciplinary team** | 6–8 | **12–20 months** | Many roles combined; must prioritize scope and manage coordination constraints |
| **Balanced specialist team** | **12** | **8–12 months** | Better specialization, integration and risk coverage at moderate team complexity |
| **Expanded delivery team** | 15–18 | **6–10 months** | Higher staffing cost and coordination overhead; more people do not guarantee linear speed gains |

The historical preference for **12 rather than 20–30** was grounded in the project's source scale and **static-first, batch-computation architecture**. It did not require a permanently running distributed-data platform or large real-time service fleet, so a much larger organization could introduce unnecessary overhead.

These durations are **conditional, comparative forecasts**, not deadlines or observed completion times. They assume experienced contributors, stable enough requirements, reasonably available canon data and no major infrastructure or review disruptions.

### 5.1 Planning effort versus time

The supplied conclusion estimated roughly **70–110 person-months** of aggregate effort. The separately stated 10–11 FTE and 8–12-month delivery scenario serves as another *order-of-magnitude planning view*, not a strict mathematically identical estimate.

No actual timesheets, cost quotes, salary assumptions, staffing start dates or delivery velocity measurements were provided; this document does not invent them or use the person-month range to assert a fixed budget.

## 6. Roadmap: illustrative ten-month delivery schedule

The source depicted a relative **10-month** roadmap beginning November 2026 and running approximately through August 2027, with overlapping workstreams and dependencies.

| Illustrative interval | Primary focus | Expected engineering outcome |
| --- | --- | --- |
| **November–December 2026** | Foundation and determinism | Source authority, read-only GitHub ingestion, core contracts, baseline tests |
| **January–February 2027** | UI/UX and data contracts | Astro/React design system, page structure, typed data agreements |
| **March–April 2027** | Statistics and historical analytics | Python computing, charts, historical model, reproducibility and validity checks |
| **May–June 2027** | Drift, graph and impact | Comparison, graph relation QA, dependency/impact exploration |
| **July–August 2027** | Exports, publishing and hardening | Eight formats, Pages integration, release security, E2E and acceptance |
| **Across phases, especially late stages** | Integration and quality hardening | Cross-platform reproducibility, accessibility, report integrity and final release checks |

The **10 months** was an illustrative calendar plan, **not** a contractual delivery date. Workstreams such as design-system scaffolding can begin while platform contracts are being developed, but data consumers must ultimately adopt stable, consistent source and schema contracts.

Source ingestion, evidence identity and typed data contracts should mature before a graph, statistical model or report renderer can be considered trustworthy.

No quality gate should be bypassed merely to preserve the estimated schedule:

- Cross-platform determinism.
- Mathematical/statistical correctness.
- Canon/source provenance.
- Export integrity and checksums.
- Accessibility and responsive behavior.
- CI, security and release acceptance.

**Historical perspective:** substantial engineering and Cloudflare deployment work was recorded as completed by 2026-11-14. Therefore this roadmap is preserved as a *prior planning scenario*, not a claim that all phases remained future work after the actual accepted release.

## 7. What "100% software engineering completion" means

A critical principle of the original assessment is that **100% software implementation is not equivalent to 100% fictional-history coverage**.

A technically complete system must be able to state that data is missing, sparse or insufficient rather than fabricate measurements to fill a visual chart or support an attractive narrative.

| Completion area | Measurable acceptance expectation |
| --- | --- |
| **Application** | All mandatory screens and user journeys exist and behave correctly |
| **Source Intelligence** | Read-only deterministic GitHub snapshots, source authority and reproducible identities |
| **Statistics** | Valid indicators, honest chart semantics and reproducible calculations |
| **Historical Analytics** | Sparse observations over **1010 BAC–Year 0** without invented intervening values |
| **Machine Learning** | Clustering/outlier workflows with correct validation and **insufficient-data** states |
| **Graph** | Relationships and impact paths traceable to evidence and type-safe relation meanings |
| **Reporting** | All eight formats plus ZIP packaging and integrity checks tested |
| **UI/UX** | Responsive, accessible, light/dark behavior and reduced-motion support |
| **Operations** | CI/CD, rollback approach, Cloudflare publish and monitoring readiness |
| **Governance** | No automatic canon ratification, clearly separated draft/proposal/publication authority |

### 7.1 Example: sparse historical coverage

Suppose the universe does not yet contain canon GDP observations for every year in the requested **1010 BAC through Year 0** interval. The application can still be functionally complete if it correctly reports gaps and insufficient historical observations, rather than generating false values for an entire 1,011-year inclusive sequence.

Creating all canonical annual measurements is a separate **research and worldbuilding production program**. Its scope and estimate should not be hidden within the software engineering effort.

### 7.2 Optional AI/RAG is a separately activated scope

GraphRAG or an AI assistant was described as **optional** in the statistical baseline. It should not silently become a mandatory completion criterion.

If explicitly activated later, it requires additional work on retrieval grounding, evidence provenance, privacy, evaluation, failure states, cost and review. The original analysis suggested an additional AI/RAG Engineer may be appropriate for that expansion. It did not authorize the integration merely by mentioning it.

### 7.3 No causal or canonical shortcuts

A statistics system must never manufacture data to make visualizations look complete. Likewise, the narrative expansion must not invent missing canon, confuse correlation with causation or treat a story proposal as an accepted historical event.

The credibility of the product depends on making unknown states visible, not hiding them.

## 8. Expanded Creative Intelligence team model (14–16, proposed)

The separate [Creative Intelligence & Worldbuilding Engineering Proposal](./2026-11-14-creative-intelligence-and-worldbuilding-vision-proposal.md) introduces seven narrative/creator-facing capabilities beyond the original statistical/data baseline:

- Narrative Ideation Engine.
- Worldbuilding Structure Explorer.
- Narrative Consistency Audit.
- Story Refactoring Engine.
- Canon Remodeling Laboratory.
- Narrative Impact Simulator.
- Creative Development Observatory.

To deliver *all seven as full end-to-end capabilities*, the historical suggestion increased the candidate team capacity from **12 to 14–16 people**.

| Incremental competency | Why it may be needed | Potential staffing model |
| --- | --- | --- |
| **Narrative Systems Designer / Story Editor** | Coherent dramatic arcs, motivation review, chronology, ambiguity, story restructuring | Dedicated role or shared with the creator/editorial team |
| **Worldbuilding Knowledge Curator** | Canon terminology, taxonomy, cross-document consistency, factual/narrative evidence quality | Dedicated curator or covered by the Canon Director plus graph/domain specialists |
| **AI/RAG Engineer (conditional)** | Evidence-grounded creative ideation, retrieval reliability and safe model interaction | Additional specialist only if AI/RAG is explicitly in scope |

This does not necessarily imply three net hires. Some functions overlap with the creator, the graph engineer, a systems architect, or an interdisciplinary AI engineer. The original proposal suggested **14–16** as a flexible range rather than rigidly adding three to the 12-person baseline.

**Do not infer that the original 8–12-month schedule remains valid for the expanded scope.** It would require an updated workload and dependency estimate, team availability and measurable capability acceptance.

## 9. Founder operating model and division of authority

The creator's leverage is strongest when responsible for:

- Vision and scope definition.
- Canon direction and ratification.
- Selection of story development opportunities.
- Product acceptance.
- Architecture review and strategic prioritization.

A Tech Lead may own day-to-day integration, reliability, code review and engineering sequencing. This delegation is a way to avoid turning every minor implementation detail into a founder-only bottleneck without transferring ownership of intellectual property or canon authority.

### Responsibility boundaries

| Decision | Primary authority |
| --- | --- |
| Asthortera lore/canon ratification | Creator / Canon Director |
| Product scope and value priorities | Product Owner |
| Technical design and engineering acceptance | Tech Lead, with owner review at material boundaries |
| Statistical method and integrity interpretation | Data Scientist / QA / relevant domain expert |
| Source versioning and ingestion correctness | Platform/Data Engineer |
| Narrative interpretation and ambiguity | Story editor/curator with Creator review |
| Production release, secrets and rollback | DevOps/Security within explicit approved boundaries |
| Writing back to Remodeling or Studio | **Separate explicit owner approval** |

The same person can hold more than one responsibility, but a role being assigned is not evidence that the person can perform all roles simultaneously without schedule or quality impact.

## 10. Planning assumptions, uncertainties and change controls

The numbers in this document were sensitive to assumptions such as:

1. Engineers with sufficient seniority and experience working across TypeScript, Astro/React, Python, data systems, CI and scientific validation.
2. Relatively stable initial requirements and source contracts.
3. Source repositories accessible by read-only GitHub API.
4. Canon gaps openly accepted instead of being filled with fabricated observations.
5. Static-first and batch-computation architecture remaining suitable.
6. Limited major disruptions to infrastructure and review cadence.
7. An independent quality function across statistics, exports and browser UI.
8. The Creator retaining final decision authority.
9. GraphRAG, private multi-user spaces and write-back excluded unless separately authorized.

These assumptions cannot be treated as confirmed facts about a hired team or operational throughput.

A fresh estimate would need an inventory of implemented versus unimplemented features, backlog/acceptance tests, dependencies, actual contributors, time availability, budget, and the quality of source data. The archived 2026 figures are a reference point—not a current staffing directive.

## 11. Historical baseline versus approved implementation status

The supplied staffing analysis sometimes uses phrasing such as **"full approved scope"** to refer to the statistical architecture under discussion. Its use of "approved" is preserved as a description of that historical planning baseline; it is not a new approval for staffing expenditure, deadlines or creative-scope expansion.

The separate product vision explicitly states that Creative Intelligence was at that moment a **proposed extension**, not a ratified new implementation requirement. Later repository evidence documents that many related modules were actually engineered, integrated and deployed; that later work should be evaluated against its **real GitHub SHA and acceptance gates**, rather than backdating the original staffing projection as an executed organizational plan.

### Conclusions the evidence supports

- A **12-person / 10–11-FTE** balanced team was the original recommended staffing scenario for the complete statistical/data scope.
- **8–12 months** and **70–110 person-months** were broad comparative estimates, not measured results.
- A fuller Creative Intelligence product might increase planned capacity to **14–16**, conditionally.
- Hiring, financial commitment, scope ratification and implementation completion are separate decisions.
- Software engineering can be accepted without authoring every missing Asthortera historical data point.
- Evidence quality, source authority and independent verification remain necessary regardless of team size.

## 12. Related records

- [Creative Intelligence & Worldbuilding Engineering — Proposed Product Vision](./2026-11-14-creative-intelligence-and-worldbuilding-vision-proposal.md)
- [End-to-End Engineering and Production Chronicle](./2026-11-14-end-to-end-engineering-and-production-chronicle.md)
- [Conversation and Evidence Ledger](./2026-11-14-conversation-and-evidence-ledger.md)
- [Operations and Recovery Runbook](./2026-11-14-operations-and-recovery-runbook.md)
- [Reltroner Statistics implementation repository](https://github.com/Reltroner/reltroner-statistics)

---

**Archive conclusion:** The baseline staffing assessment proposed **12 people with approximately 10–11 effective FTE** for the statistical/data system, and the subsequent creative vision considered **14–16** for a broader narrative-intelligence product. These are **capacity models**, not approvals or employment records. The lasting principle is that authority, data contracts, independent validation and the ability to distinguish *missing data from fabricated data* matter more than a raw developer count.
