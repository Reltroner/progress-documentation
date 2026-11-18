# RS-AI-PAGE-004 + RS-DEPLOY-SHA-005 — Cross-Milestone Acceptance and Provenance Ledger

> **Checkpoint:** 2026-11-18 UTC/WIB. **Records are pinned to linked commits and workflow runs.**  
> **Status:** PAGE-004 released; SHA-005 merged and published; live deployment + 16-tool protocol PASS. Native-client G8 remains PENDING.  
> **Implementation main:** `ed3abce95fd5c6f4371bd5e957ff7aa4d680909c`.  
> **Primary release run:** [Statistics main CI #44254064537](https://github.com/Reltroner/reltroner-statistics/actions/runs/44254064537), publication job `134635454324` **SUCCESS**.

## 1. Evidence-class policy

| Class | Meaning / admissible conclusion |
| --- | --- |
| `SOURCE_CONTRACT` | code, Zod, tests and version-pinned implementation docs; describes intended/implemented behavior |
| `CI_LOCAL` | test result obtained in a feature PR, workerd, or developer checkout; does not establish public deployment |
| `CI_PRODUCTION` | completed main-push pipeline and publication job, including exact-SHA live verification |
| `LIVE_PROTOCOL` | actual production tool/REST calls; protocol works at tested snapshot, not necessarily in every AI client |
| `OWNER_REPORTED` | screenshot/CLI observation supplied by owner, not independently re-executed by this archive |
| `MODEL_SELF_REPORT_ONLY` | AI claims about tool use, not independently proven by client-native telemetry |
| `HYPOTHESIS` | plausible cause, future feature or creative idea; cannot be silently promoted to observation |
| `PENDING` | no sufficiently grounded final acceptance evidence |

Do not merge evidence types. In particular, a Statistics production SHA is not Studio frontend deployment parity; an MCP `tools/list` pass is not native ChatGPT/Claude/Gemini G8 completion; an owner-ratified architecture is not a canon amendment.

## 2. Sequential release ledger

| Stage | Git identity | Gate result / historical qualification |
| --- | --- | --- |
| RS-AI-API-001 | [PR #6](https://github.com/Reltroner/reltroner-statistics/pull/6), `fc37812b6cad68cfb707fdcdd07d7a0e417825df` | first publicly verified 15 REST + 13 MCP architecture |
| RS-AI-API-002 | [draft PR #7](https://github.com/Reltroner/reltroner-statistics/pull/7) | client acceptance workstream remains separate and unmerged at this checkpoint |
| RS-CREATIVE-QUALITY-003 | [PR #8](https://github.com/Reltroner/reltroner-statistics/pull/8), merge `5b5473875f81b16d9f47ac0dc52f6d49e30a0861` | creative exploration/evidence improvements deployed; previous draft state superseded |
| RS-AI-PAGE-004 | [PR #9](https://github.com/Reltroner/reltroner-statistics/pull/9), merge `1dbca25ff3b8e12b1919038967bbfb23f8a4bfce` | all eligible pages mirrored; +3 REST/+3 MCP; original main push failed on **metadata default assertion**, not on payload correctness |
| Page-tool verifier correction | [PR #10](https://github.com/Reltroner/reltroner-statistics/pull/10), merge `92ad608e1d22193120a2fb9a0b42993271797a84` | SDK-omitted default accepted only with live MCP/REST behavior tests; next main-push failed on **early custom-domain SHA check** |
| RS-DEPLOY-SHA-005 | [PR #11](https://github.com/Reltroner/reltroner-statistics/pull/11), feature head `f32b67c142f10360e02f6ff5654b9681421ae8f6`, merge `ed3abce95fd5c6f4371bd5e957ff7aa4d680909c` | feature CI [#44251870217](https://github.com/Reltroner/reltroner-statistics/actions/runs/44251870217) SUCCESS and production [#44254064537](https://github.com/Reltroner/reltroner-statistics/actions/runs/44254064537) SUCCESS |

Historical failure workflows remain **failed as originally executed**, despite later remediation: [PR #9 publication #44104975078](https://github.com/Reltroner/reltroner-statistics/actions/runs/44104975078), [PR #10 publication #44111759840](https://github.com/Reltroner/reltroner-statistics/actions/runs/44111759840). Do not retroactively mark them green.

## 3. PAGE-004 acceptance matrix

| Gate | Assertion | Evidence | Recorded status |
| --- | --- | --- | --- |
| G0 Git safety | isolated worktrees, local/remote parity, owner staged files untouched | [PAGE acceptance](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-AI-PAGE-004-ACCEPTANCE.md) and later SHA-005 preflight | **PASS at recorded runs** |
| G1 Census | each eligible built HTML has exactly one JSON + Markdown mirror | initial 608/607; later release 635 HTML/634 eligible, 625 FULL and 9 PARTIAL | **PASS in build/workerd** |
| G2 Exact URLs | strict canonical origin, exact registry lookup, stable refusal codes and no substitution | URL test matrix, 4,000 invalid inputs, live page URL negative tests | **PASS** |
| G3 Semantic fidelity | HTML/headings/island data represented; browser-only state clearly PARTIAL | 617 mirror values compared in workerd; nine pages PARTIAL with reason | **PASS for published coverage** |
| G4 Epistemic fidelity | PROPOSED vs canon, nulls, two spatial denominators and source SHA never conflated | live spatial page verification and source policy cases | **PASS** |
| G5 REST/MCP compatibility | original 13/15 preserved, 3/3 page tools added, 16/18 total, read-only | [live protocol step](https://github.com/Reltroner/reltroner-statistics/actions/runs/44254064537) and combined workerd tests | **PASS** |
| G6 Non-functional | no added browser JS; bounded generated assets; PDF and visual routes retained | [PAGE regression](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-AI-PAGE-004-REGRESSION-AND-PERFORMANCE.md), SHA-005 bundle parity | **PASS at tested snapshots** |
| G7 Combined regression | build/test/workerd/browser | [combined PR #9 CI #44101213896](https://github.com/Reltroner/reltroner-statistics/actions/runs/44101213896), [SHA-005 PR CI](https://github.com/Reltroner/reltroner-statistics/actions/runs/44251870217) | **PASS** |
| G8 Cross-provider native use | ChatGPT, Claude, Gemini each use actual connected page tools, with native logs and evidence fidelity | seven test prompts prepared in PAGE security doc; no completed multi-provider native G8 ledger in source | **PENDING** |

**Page source and coverage:** On the successful main-push snapshot `ed3abce…`, independent live MCP manifest reports Stats commit `ed3abce…`, production SHA `ad895e6…`, remodeling SHA `33ea8fa…` and digest `4119d30…`. These are anchored identities, not floating "latest" guarantees.

## 4. SHA-005 acceptance matrix

| Gate | Requirement | Evidence | Status |
| --- | --- | --- | --- |
| D0 Root cause | stale HTTP 200 must be retried, not treated as terminal | replay old loop with captured previous snapshot; incident timeline | **PASS** |
| D1 Exact artifact | unique URL from same Wrangler job, exact full identity | `e037afc4.reltroner-statistics.pages.dev`, one matching read | **LIVE PASS** |
| D2 Canonical convergence | two consecutive exact identity matches separated by 5 seconds | production job canonical reads `MATCH` + `MATCH` and `CUSTOM_DOMAIN_CONVERGED` | **LIVE PASS** |
| D3 Git main | before and after verification equal expected main SHA | `main_ref.state=MAIN_EQUALS_EXPECTED` | **LIVE PASS** |
| D4 Full identity | commit, semantic digest, rules and both source SHAs | `STATISTICS_DEPLOYMENT_VERIFIED` `reason=VERIFIED` `mismatches=[]` | **LIVE PASS** |
| D5 Negative and security | redirects, malformed identities, stale forever, timeouts, wrong digest/URL/ref fail closed | 33 deterministic new tests + mutation checks on feature branch | **CI PASS** |
| D6 Protocol after verification | 13 legacy + 3 new MCP, 18 REST, exact page/context/sections, invalid inputs | `RS-AI-API-002` `status=PASS`, `page-aware-v1` profile | **LIVE PASS** |
| D7 Non-regression | existing web, PDF, API, read-only and browser bundles intact | 180 Node, 9 protocol, 24 Python, typecheck 230, workerd, 441 E2E + 1 expected skip | **PR CI PASS** |
| D8 Provider-native G8 | signed-in chat clients prove real tool invocation, not just protocol | distinct from deploy; remains with owner | **PENDING** |

**Production publication details (UTC 2026-11-18):**

- `06:59:02` Statistics Pages guard: `ISOLATED_STATISTICS_PAGES_VERIFIED`, exact project/domain; zero DNS/nameserver mutations.
- `06:59:32` Wrangler announced deployment URL `https://e037afc4.reltroner-statistics.pages.dev`.
- `06:59:39` full SHA verifier reported `STATISTICS_DEPLOYMENT_VERIFIED`; unique artifact verified in **one** read, canonical domain matched in **two** successive reads ~5 seconds apart; `main` unchanged at `ed3abce…`.
- `06:59:43` live PAGE-004 protocol report `RS-AI-API-002: PASS`, including `MCP_TOOL_COMPATIBILITY_AND_STRICT_DISCOVERY`, `PAGE_URL_EXACT_RESOLUTION`, `PAGE_CONTEXT_PROVENANCE_AND_TWO_DENOMINATORS`, `PAGE_MCP_DEFAULT_TRUE_AND_EXPLICIT_FALSE_RUNTIME_PARITY`, `PAGE_SECTIONS_REAL_DATA_AND_REST_MCP_PARITY`, `PAGE_PROPOSED_WITHHELD_WHEN_PRODUCTION_ONLY` and negative unknown-key/foreign-URL checks.

Source: [main push CI #44254064537, publication job `134635454324`](https://github.com/Reltroner/reltroner-statistics/actions/runs/44254064537).

## 5. Current epistemic/production state at recorded checkpoint

~~~text
RS-AI-PAGE-004                 MERGED + DEPLOYED + LIVE PROTOCOL PASS
RS-DEPLOY-SHA-005              MERGED + DEPLOYED + LIVE_POST_MERGE_ACCEPTANCE PASS
STATISTICS_APP_COMMIT          ed3abce95fd5c6f4371bd5e957ff7aa4d680909c
PRODUCTION_SOURCE_SHA          ad895e6d9184f09281a7cc14ccd7867c47acd29e
REMODELING_SOURCE_SHA          33ea8fa5472a723d640f1adbea35f686a65b3e27
SEMANTIC_DIGEST                4119d30b2c2d7ea14b95fe08c2d53365de966acaeb343a2a772e26d42a28e08d
RULES_VERSION                  P0R-2.0.0
REST_OPERATIONS                18
MCP_TOOLS                      16 (13 legacy + 3 PAGE)
PAGE_MIRRORS                   634 (625 FULL; 9 PARTIAL) in pinned build
STUDIO_DEPLOYMENT_STATUS       DEPLOYMENT_UNVERIFIED (separate source frontend)
PROVIDER_NATIVE_G8             PENDING
H1_H2_H3                       HYPOTHESIS / UNRATIFIED
AUTOMATIC_CANON_WRITEBACK      NONE
~~~

No fresh inference should overwrite these pinned observations. For the actual running revision, recheck the GitHub main ref, the public `build-info.json`, and the live MCP manifest independently.

## 6. Explicit unresolved gates and release boundaries

1. **G8 user-side native cross-model acceptance:** run the seven prompts in [PAGE security/operator instructions](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-AI-PAGE-004-SECURITY-AND-OPERATIONS.md). Capture client-native call args, snapshot identity, refusal behavior, exact outputs and epistemic fidelity; do not call model self-report a provider trace.
2. **Studio deployment identity:** `studio_deployment_status` in Statistics evidence is not a live frontend attestation. Keep this separate even though Statistics site release is verified.
3. **Future build variation:** HTML/mirror/page counts depend on pinned source revisions and must be recalculated per build. Static mirror assets are public and unaffected by the REST/MCP kill switch.
4. **Owner control and canon:** no automated changes to `reltroner-studio` or `reltroner-studio-remodeling`. New story directions, including H1, H2 and H3, require creator review and ratification.

**Linked archive documents:** [PAGE full design](./2026-11-18-rs-ai-page-004-universal-page-aware-intelligence-architecture.md), [SHA-005 incident/fix](./2026-11-18-rs-deploy-sha-005-deployment-sha-parity-debugging.md) and [operational runbook](./2026-11-18-rs-page-deployment-operations-runbook.md). 
