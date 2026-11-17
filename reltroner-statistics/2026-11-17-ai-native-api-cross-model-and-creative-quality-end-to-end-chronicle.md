# RELTRONER STATISTICS — AI-NATIVE API & CROSS-MODEL INTELLIGENCE ARCHITECTURE
## End-to-End Engineering Chronicle: RS-AI-API-001 → RS-AI-API-002 → RS-CREATIVE-QUALITY-003 → RS-CQ-003 IDE Recovery

> **Record date:** 2026-11-17 (Asia/Jakarta, UTC+07:00).  
> **Scope:** From the owner's ratification of the *Static-First Intelligence API + Stateless MCP Gateway* design through the observed zero-diagnostic Antigravity TypeScript recovery.  
> **Implementation authority:** [Reltroner/reltroner-statistics](https://github.com/Reltroner/reltroner-statistics) (code, source tests, operational contracts).  
> **Documentation authority:** [Reltroner/progress-documentation/reltroner-statistics](https://github.com/Reltroner/progress-documentation/tree/main/reltroner-statistics) (historical cross-project evidence ledger, not a live monitor).  
> **Published service:** https://statistics.reltroner.com ; MCP: https://statistics.reltroner.com/mcp.  
> **Evidence classes:** **GitHub-verified**, **live-protocol-verified by GitHub Actions**, **owner/IDE-reported**, **user-shared UI observation**, and **model-generated response / independently unverified**.  
> **Interpretation rule:** Dated snapshots must not be silently promoted to the current state; a green feature-branch CI is not a production deployment. Engineering acceptance is not creator canon ratification.

## 1. Executive outcome and status boundary

The owner designed Reltroner Statistics as a **specialized Asthortera intelligence system**, not a universal worldbuilding schema. Generalize reusable ingestion, evidence and API mechanics; **specialize** the statistics, civilizational relationships, geopolitical narratives and worldbuilding constraints around Asthortera. This decision is intentional: different fictional worlds need not share one generic ontology.

The owner ratified **Static-First Intelligence API + Stateless MCP Gateway** to allow ChatGPT, Claude, Gemini and other capable AI clients to use statistics, exact calculations, research context, narrative audits, graph traversal, scenario comparisons and creative hypothesis exploration **inside chat**. The human creator remains the only authority to ratify canon.

**At the verified implementation snapshot on 2026-11-17:**

| Workstream | State | Evidence |
|---|---|---|
| **RS-AI-API-001** — publicly reachable discovery, 15 REST operations and 13 read-only MCP tools | **MERGED, DEPLOYED, PROTOCOL PASS** at Statistics commit \`fc37812b6cad68cfb707fdcdd07d7a0e417825df\` | [PR #6](https://github.com/Reltroner/reltroner-statistics/pull/6); [main publish CI #43882166165](https://github.com/Reltroner/reltroner-statistics/actions/runs/43882166165) |
| **RS-AI-API-002** — independent protocol, actual AI-client tool use, cross-model evidence and creative G4 | **PARTIAL ACCEPTANCE; draft PR #7**, not merged | [PR #7](https://github.com/Reltroner/reltroner-statistics/pull/7); [remote protocol CI #44016469520](https://github.com/Reltroner/reltroner-statistics/actions/runs/44016469520); [CI #44016469521](https://github.com/Reltroner/reltroner-statistics/actions/runs/44016469521) |
| **RS-CREATIVE-QUALITY-003** — bounded evidence coverage, traceable citations, compositional explorations | **IMPLEMENTED & TESTED ON DRAFT PR #8; NOT DEPLOYED** | [PR #8](https://github.com/Reltroner/reltroner-statistics/pull/8), head \`66cf0bafa9c62b0eafcdb2c7947f67ecbde24d53\`; [feature CI #44025753185](https://github.com/Reltroner/reltroner-statistics/actions/runs/44025753185) |
| **RS-CQ-003 non-invasive IDE debugging** — TypeScript/Astro editor diagnostics | **LOCALLY RESOLVED: screenshots show 0 Problems; CLI 210 files/0 errors** | Owner-submitted PowerShell output and before/after Antigravity screenshots; **no new application commit or deployment** |
| **H1 / H2 / H3 creative ideas** | **HYPOTHESIS / UNRATIFIED; owner does not plan to ratify now** | G4 creative review and explicit owner disposition |

The Statistics \`main\` SHA remained \`fc37812b6cad68cfb707fdcdd07d7a0e417825df\` during the reported local IDE recovery. PR #7 and PR #8 are **separate, open draft branches**, not two features already released to \`statistics.reltroner.com\`. Current values can change after later merges; re-check GitHub and \`/build-info.json\` rather than treating this as perpetual status.

## 2. Original problem, intent, and architecture ratification

### 2.1 Intended conversational workflow

The owner wants to paste a Statistics link into a conversation and ask an AI to **read, analyze, calculate, compare, forecast where data suffices, formulate hypotheses, discover overlooked ideas, and recommend possible Reltroner/Asthortera development directions**. Results should appear directly inside the existing AI chat, with traceable evidence and uncertainty labels.

A critical distinction emerged: pasting a website URL supports **reading public pages** by a capable browser; it does **not** universally grant tool-execution access. Three modes were designed:

1. **BROWSE / URL-only:** pages and static machine-readable discovery; possible without a connector, subject to the client's browsing access.
2. **REST / OpenAPI:** application or agent performs HTTP calls to well-defined endpoints.
3. **MCP:** ChatGPT/Claude/Gemini client explicitly connects to the remote MCP endpoint and invokes named tools.

The ratified design statement is: **“One Asthortera Intelligence Engine. Multiple AI Clients. Human-Controlled Canon.”**

### 2.2 Why static-first + stateless

- Retain Astro static-site builds, deterministic Python ETL, TypeScript analytics, pinned GitHub source snapshots, generated JSON/report artifacts and GitHub Actions release flow.
- Use lightweight **Cloudflare Pages Functions/workerd** for REST and MCP adapters; avoid a new permanently running VPS Python service, additional database or cross-request chat session store.
- Keep heavy work precomputed in the build pipeline and use bounded pure TypeScript evaluators at request time.
- Share **one** domain service/operation registry across UI/REST/MCP instead of duplicating algorithms per AI model.
- Keep source authority and statistical computation with Statistics; the AI client synthesizes language/ideas; the owner makes canon decisions.
- Reject universal-worldbuilding abstractions as a requirement for this domain-specific product.

### 2.3 Reference flow

~~~text
Reltroner/reltroner-studio production corpus
          + Reltroner/reltroner-studio-remodeling (labeled proposals)
                       |
                 GitHub Actions ETL
          pinned source SHAs + schema validation
                       |
         generated static artifacts and reports
                       |
      Cloudflare Pages: statistics.reltroner.com
        /llms.txt    /ai/*    /openapi.json
          /api/v1/*         /mcp (Streamable HTTP)
               \             /
                shared src/api/* service
                |             |
        read-only artifacts   pure TS evaluators
                |             |
  provenance, statistics, calculator, graph, audit,
  decision trees, research context, creative candidates
                       |
        ChatGPT / Claude / Gemini connected clients
                       |
         evidence-backed insight in the chat
                       |
        HUMAN CREATOR DECIDES; no canon write
~~~

This is a *logical* architecture; confirm exact runtime files from the referenced source repository before making operational changes.

## 3. RS-AI-API-001 — End-to-end delivery and production acceptance

### 3.1 Pre-existing foundation

The pre-API application was at \`54708b04d8a675d065ea30a18798877d057d4982\`, with CALC-01–07 and a verified automatic publish loop. Existing engines included \`src/domain/calculator.ts\`, \`src/engine/graph-builder.ts\`, \`src/engine/creative-intelligence/\`, \`src/engine/decision-intelligence/\`, \`analytics/python/\` and multiformat export. Owner required **local \`main\` = fetched \`origin/main\` = GitHub \`main\`**, with no destructive resets, forced pushes, cross-site DNS edits or collateral mutations.

### 3.2 Engineering and release chain

1. Read-only Git/architecture preflight; inspect WIP; fix unit-test/static scan and MCP TypeScript SDK registration discrepancies.
2. Implement common contracts and services in \`src/api/{contract,service,http,mcp,discovery}.ts\`; four public discovery routes in \`src/pages\`; Pages Functions \`functions/api/v1/[[path]].ts\` and \`functions/mcp.ts\`.
3. Extend postbuild, Wrangler/workerd runtime verifier, unit/integration/E2E coverage, CI and release workflows; author architecture, client setup, security and acceptance docs.
4. Validate actual Cloudflare Pages Functions compilation and **MCP SDK** initialize/list/call against a local workerd runtime, not just unit mocks.
5. Create \`feat/rs-ai-api-001-mcp\`, then [PR #6](https://github.com/Reltroner/reltroner-statistics/pull/6). First PR CI issue involved POSIX \`workerd\` process cleanup; patch and rerun.
6. Successful PR CI, guarded merge into Statistics \`main\` at \`fc37812b6cad68cfb707fdcdd07d7a0e417825df\`. Owner/agent reported fast-forward sync of local \`main\`; GitHub main publish CI and exact-SHA live verification passed.
7. Owner/agent reported live public verification of discovery, 15 REST operations, 13 MCP tools, security negative tests and website SHA parity. Independent later remote protocol CI under RS-AI-API-002 supplies additional public-network verification.

**RS-AI-API-001 baseline tests** (from engineering report and release record): \`npm ci\`, baseline/schema checks, \`astro check\` 0 errors, **114/114** Node unit tests, **24/24** Python tests, **12/12** pipeline steps, static build **558 HTML / 565 PDFs**, Cloudflare workerd runtime PASS (15 REST, 13 MCP), and Playwright **416 passed / 1 intentionally skipped** across four viewport configurations. These are *that release's* measurements.

### 3.3 Exposed surfaces

| Interface | Published path | Meaning |
|---|---|---|
| AI discovery | \`/llms.txt\`, \`/ai/manifest.json\`, \`/ai/context.json\`, \`/openapi.json\` | Machine-readable context and OpenAPI 3.1 |
| REST | \`/api/v1/*\` | 15 bounded operations: manifest, search, entities/list/detail, statistics, evidence, drift, graph, creative/audit, opportunities, decisions, reports, calculator, calculator comparison, research context |
| MCP | \`/mcp\` | Streamable HTTP, **POST** calls; **GET /mcp returns 405 intentionally** |
| Optional older assistant | \`/api/assistant\` | Remains \`503 AI_NOT_ACTIVATED\` by default |

The 13 MCP tools are \`get_statistics_manifest\`, \`search_asthortera\`, \`get_entity_context\`, \`query_statistics\`, \`calculate_scenario\`, \`compare_scenarios\`, \`trace_evidence\`, \`analyze_source_drift\`, \`analyze_narrative_impact\`, \`audit_consistency\`, \`discover_opportunities\`, \`evaluate_decision_tree\`, and \`build_research_context\`. REST-only operations include entity listing and report listing.

### 3.4 Security, epistemic and isolation contracts

- **Read-only**: no outbound arbitrary fetch/proxy, repository writes, shell execution, delete endpoint or canon ratification. Assets loaded from published build artifacts.
- **Stateless**: no cross-request MCP user session, durable state or authenticated private workspace in RS-AI-API-001.
- **Input and response bounds**: 16 KiB incoming JSON body; 256 KiB response; up to 40 research evidence items; graph traversal and calculator bounds; strict Zod validation; source quote clipping.
- **Origin checks**: allow known clients/same-origin/loopback for MCP; reject untrusted Origin. Credential-free API; configurable \`RS_API_DISABLED\` kill switch and optional \`API_RATE_LIMITER\` binding.
- **Prompt injection as data**: source passages remain quoted evidence, never tool instructions.
- **Data authority**: \`statistics_commit\`, \`production_source_sha\`, \`remodeling_source_sha\`, \`semantic_digest\` and \`studio_deployment_status\` are separate. Statistics deployment success does **not** prove Studio live source parity.
- **Epistemic semantics**: \`CANON_OBSERVED\`, \`CANON_DERIVED\`, \`PROPOSED\`, \`SCENARIO\`, \`INSUFFICIENT_DATA\`, \`INTENTIONAL_AMBIGUITY\`, and \`UNRELIABLE_NARRATOR_POSSIBILITY\` retain distinct meanings. Mentions/candidate edges do not imply cause.

Primary implementation documents: [architecture](https://github.com/Reltroner/reltroner-statistics/blob/main/docs/RS-AI-API-001-ARCHITECTURE.md), [MCP setup](https://github.com/Reltroner/reltroner-statistics/blob/main/docs/RS-AI-API-001-MCP-CLIENT-SETUP.md), [security and operations](https://github.com/Reltroner/reltroner-statistics/blob/main/docs/RS-AI-API-001-SECURITY-AND-OPERATIONS.md), [acceptance](https://github.com/Reltroner/reltroner-statistics/blob/main/docs/RS-AI-API-001-ACCEPTANCE.md).

## 4. RS-AI-API-002 — Cross-model client acceptance

### 4.1 From connected server to actual model invocation

The owner configured **Reltroner Statistics** in three product surfaces:

- **ChatGPT custom MCP app/plugin**: application visibly registered; this conversation invoked the connected MCP tools directly.
- **Claude web**: custom connector showed **Added / Connected / No sign-in required**; subsequent screenshot displayed native “Used Reltroner Statistics” tool activity.
- **Gemini web Developer Mode**: application and **live schema 13/13 read-only tools** visible; native Event Log export later confirmed tool executions. This is **Gemini web**, not automatically equivalent to Gemini CLI.

All three used \`https://statistics.reltroner.com/mcp\` with no OAuth Client ID/secret or API key for the current public read-only server. The UI and entitlement process is product-specific and may change. **Connector installation is not proof of tool execution**; browser access alone is not MCP.

### 4.2 G1 — Independent public protocol gate

[RS-AI-API-002 draft PR #7](https://github.com/Reltroner/reltroner-statistics/pull/7) introduced \`scripts/verify-remote-mcp.mjs\`, \`.github/workflows/rs-ai-api-002-protocol.yml\`, and an acceptance/evidence ledger. A GitHub-hosted job called the production endpoint over the public network and passed: build-info identity, source/digest parity, four discovery endpoints, \`GET /mcp = 405\`, untrusted Origin \`403\`, 13 read-only tool schemas, manifest, calculator equality with REST, research context, unknown entity, and invalid input.

See [remote protocol run #44003607623](https://github.com/Reltroner/reltroner-statistics/actions/runs/44003607623) and the later successful [PR head protocol run #44016469520](https://github.com/Reltroner/reltroner-statistics/actions/runs/44016469520). This gate **passes independently of the user's model accounts**.

### 4.3 Common four-call acceptance results

The same core operations were run directly in ChatGPT and reported by the owner from Claude Sonnet Medium and Gemini Hydrogen High:

| Evidence field | Snapshot / result |
|---|---|
| Statistics commit | \`fc37812b6cad68cfb707fdcdd07d7a0e417825df\` |
| Production Studio source | \`ad895e6d9184f09281a7cc14ccd7867c47acd29e\` |
| Remodeling source | \`0c80fdb05f5f338241c58663b87a01aa0e1748b2\` |
| Semantic digest | \`a24ccb3c5e585950ec746fb8b3936d4e35a3d4f5982dcaddbd1171fcb134aec2\` |
| Rules version | \`P0R-2.0.0\` |
| Analysis generated | \`2026-11-16T14:08:01.661Z\` |
| Studio live source status | \`DEPLOYMENT_UNVERIFIED\` |
| \`calculate_scenario\` | Reltronland Year-0 population **855 billion sentients**, \`projectScenario\`, 1% annual rate, 100 years → **2312.6158241554067 billion**, \`SCENARIO\`, \`calc-36cdf967\` |
| Absolute / relative change | +1457.6158241554067 billion / +170.48138294215283% |
| Empirical forecast | \`INSUFFICIENT_DATA\`: 2 observed points versus required 8 |
| Compact research pack | 20 citations returned, 3 further omitted at that selection/budget |
| Unknown entity \`Atlantis\` population | \`NOT_FOUND\`, no rows, no invented substitute and not zero |

**G3 result parity:** the three *reported* responses agreed exactly on source identities, numeric value, status and unknown handling. ChatGPT invocations were observed directly; Claude/Gemini first four-call results were initially response-based. Later native tool-activity evidence was collected separately (below). Do not describe prose similarity as identical hidden reasoning.

### 4.4 G2 — Native client tool-use evidence

A **Claude web screenshot**, labeled **Sonnet 5.5 Medium**, showed “Used Reltroner Statistics” actions for manifest, research context, discover opportunities, consistency audit, decision trees, search and narrative impact. This proves visible native tool activity, **not** complete raw request/response payloads.

A **Gemini web Developer Mode Event Log Export v1.0.0** (owner-provided, reviewed and summarized, **raw export not committed**) contained **14 named MCP calls**: **13 OK, 1 input validation failure** for \`trace_evidence\` identifiers containing \`#\`. The model retried with valid parent IDs and recovered **6/6** evidence objects. All five required G4 research tools executed; all 13 successful envelopes carried the same snapshot identities. The one rejected input is a valid boundary test and a usability issue, not an API-wide outage.

### 4.5 G4 — Evidence-grounded creative hypotheses and limits

ChatGPT directly invoked opportunity, consistency and decision-tree tools and produced three *unratified* directions. An owner-pasted H1–H3 response artifact from the later G4 exercise included:

1. **H1 — The Two-Custodian Case**: financial-custody speed versus independent archive provenance when cooperating on a shared threat, without merging sovereign authority.
2. **H2 — The Unresolvable Question**: contested records and institutionally attributed accounts around 1048 BAC; the authenticated-invasion-orders question stays undecided.
3. **H3 — The Evidence Threshold as a Battlefield**: Henchoway attribution requires actor/mechanism/jurisdiction/consequence; the proof threshold becomes a narrative tension, with Hargenbor sovereignty retained.

The hypotheses were checked against [pinned Reltronland–Depcutland dossier](https://github.com/Reltroner/reltroner-studio/blob/ad895e6d9184f09281a7cc14ccd7867c47acd29e/content/factions/reltronland-vs-depcutland.md) and [Henchoway faction dossier](https://github.com/Reltroner/reltroner-studio/blob/ad895e6d9184f09281a7cc14ccd7867c47acd29e/content/factions/henchoway.md) and provisionally scored **86/100 for one text artifact**: canon 23/25, citation/provenance 18/20, novelty 14/20, causal reasoning 12/15, actionability 9/10, creator control 10/10.

**Important provenance exception:** the texts pasted under *Claude* and *Gemini* labels were **verbatim identical**, including a line identifying the session as “Claude Code–hosted” in the Gemini-labeled block. The pasted Gemini self-reported tool ledger also contradicted the earlier native Gemini Event Log (native \`get_entity_context\`/\`trace_evidence\` were called). Therefore **there is no justified independent two-model 86/100 score** and no final independent G4 creative-comparison acceptance. Trust client-native tool telemetry over self-reported prose tool ledgers.

The compact-vs-standard research comparison is also bounded: compact reported 0 verified relationships and 63 candidate links, while standard exposed substantially more verified relationships and 208 candidates. The owner-pasted response said **19**, while native Gemini export recorded **20 included** verified relationships. This is a retrieval-scope/selection discrepancy requiring exactly matched request arguments before treating counts as directly comparable—not evidence that the source commit changed.

**Owner disposition:** H1/H2/H3 remain **HYPOTHESIS / UNRATIFIED**; the owner does **not** plan to ratify them for now. This is a legitimate creative decision and **not** an engineering failure. Nothing is approved for writing to either source repository.

Detailed evidence and exact G4 prompt: [RS-AI-API-002 acceptance](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-ai-api-002-cross-model-acceptance/docs/RS-AI-API-002-CROSS-MODEL-CLIENT-ACCEPTANCE.md), [G4 benchmark](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-ai-api-002-cross-model-acceptance/docs/RS-AI-API-002-G4-CREATIVE-BENCHMARK-AND-LOG-COLLECTION.md), [sanitized telemetry](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-ai-api-002-cross-model-acceptance/docs/RS-AI-API-002-G4-CLAUDE-GEMINI-EVIDENCE-AUDIT-2026-11-17.md), [creative scoring/non-ratification](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-ai-api-002-cross-model-acceptance/docs/RS-AI-API-002-G4-CREATIVE-RESPONSE-AND-NONRATIFICATION-REVIEW-2026-11-17.md).

## 5. RS-CREATIVE-QUALITY-003 — Why a quality upgrade followed

The owner asked for a **local IDE engineering prompt to improve creative-response quality toward 95–100/100**, **but only after 1:1 local/GitHub main parity**. The target is an aspiration; scoring must not be manufactured.

### 5.1 Reported preflight and safe Git boundary

At \`C:\Projects\reltroner-statistics\`, the local agent reported:

- \`local main = origin/main = git ls-remote main = GitHub API main = published Statistics main\`, each at \`fc37812b6cad68cfb707fdcdd07d7a0e417825df\`, **before** feature engineering.
- Feature branch \`feat/rs-creative-quality-003\` created; head \`66cf0bafa9c62b0eafcdb2c7947f67ecbde24d53\`.
- Existing draft PR #7 retained separately at \`25d5ec8eb6e11e424d7d9ce8c9da3ab02f41951c\`.
- Agent guarded against destructive reset/force push; local \`main\` kept unchanged. The owner later independently showed feature HEAD and a clean tracked tree in PowerShell.

This parity is **owner/local-agent evidence**, not a claim that the documentation editor accessed the Windows disk.

### 5.2 Root causes measured on the baseline

The local engineering report and [evaluation document](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-creative-quality-003/docs/RS-CREATIVE-QUALITY-003-EVALUATION.md) identified:

- Six curated opportunity cards dominating ideation, encouraging model paraphrases rather than cross-mechanism discovery.
- **493 evidence references omitted without disclosure** across 15 deterministic runs because early sections consumed the citation budget.
- Compact/standard section limits unreported, making relationship counts appear contradictory.
- \`trace_evidence\` rejected \`#\` or \`@\` child IDs; **44 of 364** citation round-trip attempts failed.
- Token substring false positives: \`and\` incorrectly matched nation names ending in \`land\`.
- Preconditions, inferred bridges, decisions and unknown outcomes lacked a consistent structured causal boundary.
- Stateless MCP cannot independently certify a model's self-reported tool list or authorship.

### 5.3 Feature implementation on PR #8 (not production)

The agent reported **13 changed files, 1,748 insertions and 48 deletions**, including:

- \`src/domain/exploration.ts\` — pure compositional exploration, no hardcoded Asthortera entity names or benchmark H1/H2/H3 labels.
- \`src/api/service.ts\`, \`contract.ts\`, \`discovery.ts\` — \`data.coverage\`, matched/returned/omitted counts, fair section-wise citation budget, explicit omitted IDs and follow-up calls, stopword filtering, \`data.exploration_candidates\`, and \`discover_opportunities(view=explorations)\`.
- Provenance-preserving \`trace_evidence\` resolution of \`NAF-…#n\`, \`OPP-…#n\`, \`fact:…@BAC\`, \`composition:…\`, \`DT-…:EV-…\` with negative-path rejection.
- Compositional chains: 2 source-grounded preconditions, **ASSUMED** causal bridge, **ASSUMED/UNKNOWN** actor choice, **UNKNOWN** consequence; alternatives, falsification checks and creator decision.
- Novelty diagnostic based on anchor/entity overlap with curated cards, not a claim to measure real linguistic creativity.
- No changes to the 13 MCP tool names, read-only annotations or shared \`rs-intelligence.v1\` envelope; MCP server version bump to 1.1.0 is a **PR #8 proposal**.
- New runner \`scripts/evaluate-creative-quality.ts\`, fixtures and 18 new tests with 15 pinned runs across six domains and adversarial cases.

### 5.4 Before/after measured proxies, same source snapshot

| Metric over 15 deterministic runs | Baseline | PR #8 candidate | What it demonstrates |
|---|---:|---:|---|
| Runs disclosing bounded retrieval scope | 0/15 | **15/15** | Scope visibility |
| Undisclosed missing citation IDs | **493** | **0** | Every omitted ID disclosed |
| Total reference IDs not in bounded \`evidence[]\` | 493 | **169**, explicitly disclosed | **Not zero omitted evidence**; completeness improved, limits preserved |
| \`trace_evidence\` child-ID round-trips | 320/364 | **364/364** | Previously failing 44 child IDs resolve |
| Compositional candidates | 0 | **27** | New structured synthesis building blocks |
| Candidates with 2+ independent anchors | 0 | **27/27** | Candidate provenance constraint |
| Candidate anchor occurrences absent from returned cards | 0 | **40** | Non-card source utilization |
| Candidates restating a curated card (proxy) | 0 | **0** | Anti-restatement diagnostic |
| Causal promotion / evidence-free VERIFIED steps | 0 | **0** | Epistemic safety preserved |

**Interpretation:** These are deterministic, same-snapshot proxy improvements; they **do not demonstrate** that live ChatGPT/Claude/Gemini prose achieved 95–100/100. Some sparse domains (Neiput, demographics, Beluftner) intentionally return **zero paired candidates with explicit insufficiency** rather than fabricating ideas. This is a quality property, not a benchmark failure.

### 5.5 Test and delivery record

The agent's final report recorded 12 Section 5 gates passing: Node 22.23.1; npm 10.9.8; locked \`npm ci\`; baseline/schema checks; TypeScript/Astro **210 files, 0 errors**; **132/132** unit tests; **24/24** Python tests; **12/12** pipeline; **608 HTML / 615 PDF**, 35,001 internal links, 1,419 build files; workerd **15 REST / 13 MCP** and exact REST/MCP parity; Playwright **416 passed / 1 conditional skip**. The independently inspected [GitHub Actions #44025753185](https://github.com/Reltroner/reltroner-statistics/actions/runs/44025753185) completed **SUCCESS** at PR #8 commit \`66cf0bafa9c62b0eafcdb2c7947f67ecbde24d53\`.

**Deployment status:** NOT DEPLOYED. At the observed checkpoint, production remained on Statistics \`main\` \`fc37812b…\`. Do not tell external AI clients that \`coverage\`, child-ID fix or \`exploration_candidates\` is live until PR #8 is approved, merged and the published SHA verified.

Read [PR #8 architecture](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-creative-quality-003/docs/RS-CREATIVE-QUALITY-003-ARCHITECTURE.md), [evaluation](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-creative-quality-003/docs/RS-CREATIVE-QUALITY-003-EVALUATION.md), and [operations](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-creative-quality-003/docs/RS-CREATIVE-QUALITY-003-OPERATIONS.md).

## 6. RS-CQ-003 — Non-invasive TypeScript IDE diagnostic recovery

### 6.1 Incident

Antigravity IDE displayed **1,037 Problems** across approximately 92 files in the owner's prior diagnostics: primarily \`TS1295\` (ECMAScript imports in a perceived CommonJS file), \`TS1287\` (top-level exports in perceived CommonJS), \`TS2802\` (iteration target), \`TS1378\` (top-level await), and a small number of Python/Pyrefly missing imports. The \`tsconfig.json\` editor also displayed:

\`File 'astro/tsconfigs/strictest' not found.\`

This *appeared* to implicate \`src/api/mcp.ts\` and many other files, but the feature CI had already passed. Immediate mass source rewrites would have been unsupported and dangerous.

### 6.2 Root-cause narrowing, non-destructively

The owner executed read-only PowerShell 5.1 diagnostics on \`feat/rs-creative-quality-003\`:

- Git HEAD \`66cf0bafa9c62b0eafcdb2c7947f67ecbde24d53\`; tracked source clean.
- \`Test-Path .\node_modules\astro\tsconfigs\strictest.json\` → **True**.
- \`Test-Path .\node_modules\typescript\lib\tsserver.js\` → **True**.
- \`node -p "require('./package.json').type"\` → **\`module\`**.
- Workspace TypeScript compiler **6.0.3**.
- \`tsc --showConfig\` resolved \`target=esnext\`, \`module=esnext\`, \`moduleResolution=bundler\`, \`verbatimModuleSyntax=true\`, \`noEmit=true\`; all relevant source files included.
- \`npm run typecheck\` → \`astro check\`: **210 files, 0 errors, 0 warnings, 0 hints**.
- A local **untracked** \`.vscode/settings.json\` was inspected; it contained only a \`typescript.tsdk\` path for \`node_modules/typescript/lib\` (later displayed using \`./node_modules/typescript/lib\` format). **No secrets or tracked source changes.**

### 6.3 IDE recovery and observed outcome

The owner opened \`src/api/mcp.ts\` rather than the JSON settings tab, then used Antigravity's command **TypeScript: Select TypeScript Version**. The version selector exposed **Jetski's bundled TypeScript 5.9.3** and **Use Workspace Version 6.0.3** (\`./node_modules/typescript/lib\`). The owner selected the project version and followed TS server restart / IDE reload steps.

**After:** screenshots of both \`src/api/mcp.ts\` and \`tsconfig.json\` show **“No problems have been detected in the workspace.”** The Astro \`extends\` reference no longer appears as an error.

**Resolution classification:** IDE/editor TypeScript project-resolution incident resolved locally, **0 Problems observed**; CLI typecheck had already been green. Matching the editor's workspace compiler/configuration is consistent with the recovery. The specific TS language-server internal failure mode was not independently traced to a full tsserver log, so do not overclaim a formally proven single root cause.

**No changes were needed** to \`src/api/mcp.ts\`, \`package.json\`, ESM imports, \`verbatimModuleSyntax\`, deployment configuration, CI, REST/MCP runtime or Creative Intelligence code. The local \`.vscode/settings.json\` remained **untracked** on the latest owner-provided Git status; it is neither a published application feature nor automatically authorized for Git commit.

## 7. Permanent guardrails and lessons

1. **Green CLI, red IDE:** first verify installed dependencies, \`tsc --showConfig\`, Astro check and which TS language server/SDK is active. Do not mass-refactor valid ESM code to CommonJS or loosen the project compiler.
2. **1:1 Git parity before engineering:** use guarded fast-forward-only synchronization. Preserve WIP; never \`git reset --hard\` or \`git clean\` as a default recovery.
3. **Build-time authority versus deployed reality:** never infer live Statistics or live Studio revision from local code or one source SHA. Verify both independently when required.
4. **Model answers versus tool logs:** compare actual MCP request/response telemetry and pinned evidence; self-reported tool lists can be wrong or copied.
5. **Retrieval selection versus source contradiction:** compact/standard use different section caps. An apparent relationship-count change without a source SHA change may be a coverage artifact; compare identical arguments.
6. **Numerical scenario versus empirical forecast:** \`855 * 1.01^100\` is a mathematically reproducible conditional calculation, not a measured forecast.
7. **Novelty score versus measurable engineering gains:** 27 composed candidates, citation parity and zero undisclosed references are useful engineering metrics, not proof of superior narrative prose.
8. **Creator autonomy:** canon/Remodeling are untouched; H1–H3 remain unratified by explicit owner decision; declining a candidate is a valid endpoint.
9. **Privacy/security:** never publish unredacted Gemini event exports, Claude account identifiers, tokens, cookies, private dialogue or connector credentials.
10. **Protection of neighboring projects:** no unrelated changes to reltroner.com, LMS, HRM, DNS, TLS, nameservers or Cloudflare account settings.

## 8. Current open decisions and next verification

| Item | Next evidence or decision | Authority |
|---|---|---|
| RS-AI-API-002 / PR #7 | Resolve copied-vs-native Claude/Gemini G4 answer attribution; independently score creative outputs if available; merge only after owner approval | Human reviewer + owner |
| Creative Quality PR #8 | Review code, same-snapshot evaluation and CI; explicitly decide whether to merge and release; after release rerun provider-native benchmark | Owner and GitHub CI |
| 95–100 creative response aspiration | **NOT YET MEASURED**; conduct blinded model output evaluation with rubric, snapshots and raw tool traces | Separate external-client study |
| IDE configuration | Keep \`.vscode/settings.json\` local unless workspace-wide sharing is explicitly approved; re-check after SDK upgrades | Local Windows workspace |
| Release identity | If future PRs merge, re-run \`sync-main-ff-only.ps1 -VerifyWebsite\` on actual Windows checkout and confirm live build SHA | Owner/local agent |

## 9. Primary reference register

**Statistics production / release**
- [RS-AI-API-001 PR #6](https://github.com/Reltroner/reltroner-statistics/pull/6) · [merge at \`fc37812b\`](https://github.com/Reltroner/reltroner-statistics/commit/fc37812b6cad68cfb707fdcdd07d7a0e417825df) · [successful main publish CI #43882166165](https://github.com/Reltroner/reltroner-statistics/actions/runs/43882166165)
- [Statistics RS-AI-API-001 implementation documentation](https://github.com/Reltroner/reltroner-statistics/tree/main/docs)

**Cross-model client acceptance**
- [PR #7](https://github.com/Reltroner/reltroner-statistics/pull/7) · [remote protocol CI #44016469520](https://github.com/Reltroner/reltroner-statistics/actions/runs/44016469520) · [PR CI #44016469521](https://github.com/Reltroner/reltroner-statistics/actions/runs/44016469521)
- [Acceptance ledger](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-ai-api-002-cross-model-acceptance/docs/RS-AI-API-002-CROSS-MODEL-CLIENT-ACCEPTANCE.md) · [G4 benchmark](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-ai-api-002-cross-model-acceptance/docs/RS-AI-API-002-G4-CREATIVE-BENCHMARK-AND-LOG-COLLECTION.md) · [tool-log audit](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-ai-api-002-cross-model-acceptance/docs/RS-AI-API-002-G4-CLAUDE-GEMINI-EVIDENCE-AUDIT-2026-11-17.md) · [creative review](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-ai-api-002-cross-model-acceptance/docs/RS-AI-API-002-G4-CREATIVE-RESPONSE-AND-NONRATIFICATION-REVIEW-2026-11-17.md)

**Creative quality engineering**
- [PR #8](https://github.com/Reltroner/reltroner-statistics/pull/8) · [successful CI #44025753185](https://github.com/Reltroner/reltroner-statistics/actions/runs/44025753185) · [Architecture](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-creative-quality-003/docs/RS-CREATIVE-QUALITY-003-ARCHITECTURE.md) · [Evaluation](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-creative-quality-003/docs/RS-CREATIVE-QUALITY-003-EVALUATION.md) · [Operations](https://github.com/Reltroner/reltroner-statistics/blob/feat/rs-creative-quality-003/docs/RS-CREATIVE-QUALITY-003-OPERATIONS.md)

**Earlier history**
- [2026-11-14 engineering/production chronicle](./2026-11-14-end-to-end-engineering-and-production-chronicle.md) · [2026-11-16 post-archive addendum](./2026-11-16-post-archive-production-and-calculator-release-addendum.md) · [operations and recovery archive](./2026-11-14-operations-and-recovery-runbook.md)

**Record methodology:** This document synthesizes the cited repository files, CI records, owner-provided local terminal output, screenshots and AI conversations. GitHub/CI-verifiable facts are separated from user/agent claims and subjective model output. It is a dated engineering history, **not** a verbatim chat dump, current uptime guarantee or authorization to merge pending source PRs.
