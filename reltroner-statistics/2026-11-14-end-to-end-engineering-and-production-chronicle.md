# Reltroner Statistics — End-to-End Engineering, Decision Intelligence and Production Activation Chronicle

> **Archive classification:** Consolidated engineering conversation and execution record, not a verbatim ChatGPT transcript.  
> **Record date:** 2026-11-14 (Asia/Jakarta, UTC+07:00).  
> **Coverage:** Initial Statistics concept; source-of-truth and intelligence architecture; interrupted/recovered AI-agent execution; decision-tree integration; RC-DEPLOY-01, RC-DEPLOY-02 and RC-DEPLOY-03; Windows PowerShell 5.1 recovery; Cloudflare Pages custom-domain publication; operational acceptance and residual gates.  
> **Implementation repository:** [Reltroner/reltroner-statistics](https://github.com/Reltroner/reltroner-statistics)  
> **Documentation repository:** [Reltroner/progress-documentation](https://github.com/Reltroner/progress-documentation/tree/main/reltroner-statistics)  
> **Production URL:** https://statistics.reltroner.com  
> **Dedicated Cloudflare Pages project:** `reltroner-statistics`  
> **Verified application commit:** `042aa46354b9253feb2c0d55e4c0ce1adbd3e7a6`  
> **Historical status at close:** Manual production publication and three-way commit identity passed; subsequent automatic-push publication was configured but had not been independently demonstrated on a *new* commit.

## 1. Executive record

Reltroner Statistics was designed as a production-first, read-only data and creative intelligence observatory for Reltroner Studio and the fictional Asthortera universe. Its purpose is larger than a statistics dashboard: it converts repository-backed information into deterministic comparisons, auditable observations, knowledge-graph connections, story-consistency findings, human-reviewable decision trees, bounded exploratory models and downloadable evidence reports.

The project progressed from an initial engineering concept through Creative Intelligence and Decision Intelligence integration, CI acceptance, dedicated Cloudflare Pages release isolation, Git synchronization repair, and a successful custom-domain deployment. The owner explicitly required that the Windows checkout (`C:\Projects\reltroner-statistics`), GitHub `main` and the public website use the same Statistics commit as their version identity. The owner also prohibited collateral mutation of the Studio, Learning, HRM, or shared DNS/nameserver configuration.

By the end of the recorded conversation:

- GitHub `main` was `042aa46354b9253feb2c0d55e4c0ce1adbd3e7a6`.
- The owner supplied Windows PowerShell output with `LOCAL_MAIN_1_TO_1_GITHUB: VERIFIED` and `STATISTICS_PUBLIC_SHA_PARITY: VERIFIED` for that SHA.
- The owner supplied Cloudflare screenshots showing the only Statistics Pages custom domain as `statistics.reltroner.com` with status **Active** and **SSL enabled**.
- The owner supplied a DNS inventory showing a `CNAME` named `statistics.reltroner.com` pointing to `reltroner-statistics.pages.dev`, **Proxied**, TTL **Auto**, without changes to the protected sibling records.
- GitHub Actions manual release run [#43587678915](https://github.com/Reltroner/reltroner-statistics/actions/runs/43587678915) passed its build, Pages target guard, static upload and live deployment verification.
- The previous bootstrap manual release run [#43574215880](https://github.com/Reltroner/reltroner-statistics/actions/runs/43574215880) had likewise passed to the `pages.dev` address.
- The dedicated automatic deployment job for eligible new pushes to `main` was implemented. Its actual success on a subsequent, newly pushed commit was **not** yet independently proven and remains a follow-up acceptance test.

**Important semantic distinction:** 1:1 means verified *source commit identity*, not byte-for-byte equivalence between a Git source tree and the generated HTML, PDFs, JSON and JavaScript published by Cloudflare. Source-derived observations are also separately pinned by their own source repository commit SHAs and semantic digest.

## 2. Problem statement and owner intent

### 2.1 Business and engineering problem

The owner maintains an expanding Reltroner Studio site and a distinct remodeling repository. Content and structural changes accumulate across Asthortera descriptions, factions, places, organizations, principles, laws and blog articles. Manual review alone is increasingly costly and risks:

1. Treating a proposal or draft as if it were production canon.
2. Missing changed or deleted sections and source-schema drift.
3. Breaking cross-file relationships or narrative consistency during remodeling.
4. Losing explainability for numerical observations and creative choices.
5. Issuing confident model or deployment claims without reproducible evidence.
6. Producing reports with different interpretations of the same underlying finding.
7. Creating an unnecessarily heavy runtime architecture for limited hosting capacity.

The target was an automated read-only observatory: a push or identified source change leads to a controlled ETL/validation/build pipeline; the resulting site exposes source identities, statistics, drift findings, graph relations, creative intelligence, decision options and reproducible reports.

### 2.2 User-facing outcomes

The conceptual outputs included whole-site structural visualization, consistency checks, cross-repository source-drift inspection, impact/dependency exploration, canon-remodeling recommendations, creative brainstorming grounded in text, and explainable decision-support trees. The intended export system covers **JSON, CSV, XLSX, TXT, Markdown, HTML, PDF and XML**, with ZIP packaging, manifest metadata and checksums where relevant.

The project name, website, and Git repository were to remain distinct from the Studio website itself. The implementation was not a request to alter canonical Studio content or to automatically ratify invented lore.

## 3. Source authority and provenance contract

| Surface | Role | Trust and mutation boundary |
| --- | --- | --- |
| `Reltroner/reltroner-studio`, `main` | Production repository source candidate for statistical observation | Read-only; must not be confused with a separately verified *deployed* Studio build |
| `Reltroner/reltroner-studio-remodeling`, `main` | Proposal/draft comparison source | Read-only; display proposals as proposals, not as accepted canon |
| Verified live Studio deployment, if evidence available | What is actually deployed on `reltroner.com` | Only asserted when tied to a checked live build identifier; historical Statistics manifest reported `DEPLOYMENT_UNVERIFIED` |
| `Reltroner/reltroner-statistics` | Observatory source code, analytical outputs, UI and exports | Writes only its own repo, generated artifacts and dedicated Pages target |
| `statistics.reltroner.com` | Published static Statistics application | Version identity must match its specific Statistics GitHub commit and build manifest |

Source identity is based on repository/commit/path/field evidence. The pipeline uses read-only GitHub API access and pinned commit SHAs while resolving inputs, verifies object/tree identities, and tracks a rules version and a semantic digest. Missing values are never silently coerced to zero. Unsupported causal claims, fake citations, invented business data, and synthetic ML results presented as canonical measurements are prohibited.

Statistics does not have authority to rewrite either source repository or to decide final story canon. Creator approval remains the authority for such decisions.

## 4. Technical architecture recorded in the conversation

~~~text
Read-only GitHub source resolution (Studio + Remodeling)
   |
   v
Pinned commit/tree/blob acquisition and source evidence
   |
   v
Deterministic comparator, JSON-field/Markdown-section drift, QA
   |
   +--> Civilizational observations and statistics
   +--> Typed knowledge/narrative graph and impact traversal
   +--> Creative Intelligence: extraction, audit, opportunities, refactor, remodeling
   +--> Decision Intelligence: explainable creative/review trees
   +--> Supervised decision trees: optional, gated, non-canonical estimates
   |
   v
Contract validation + Python analytics + evidence-backed report model
   |
   v
Astro + React static production build, pages, downloadable reports/PDFs
   |
   v
GitHub Actions: tests -> build -> visual evidence -> release artifact
   |
   v
GET-only Cloudflare project/domain preflight -> Wrangler Pages upload
   |
   v
statistics.reltroner.com + /build-info.json identity verification
~~~

**Implemented technology** includes Astro, TypeScript, React islands, Tailwind styling, React Flow, ECharts, Python/scikit-learn, locked Python dependencies, Playwright, Node's built-in test runner, GitHub Actions, Wrangler and Cloudflare Pages. The application has no requirement to run a separate continuously available analytics backend on the constrained Hostinger VPS.

Key implementation areas recorded from the repository:

- `src/domain/`: typed observations, canon status, decision-tree and graph contracts.
- `src/engine/`: comparator, evidence, graph construction, creative and decision intelligence.
- `src/engine/creative-intelligence/`: extraction, audit, opportunities, story refactor, remodel scenarios and deterministic AI boundary.
- `src/engine/decision-intelligence/`: decision tree building, evaluation, model conversion and helper kit.
- `analytics/python/reltroner_analytics/decision_tree.py`: supervised-tree sufficiency gates, training and hold-out evaluation.
- `src/pages/creative/decisions.astro` and `src/pages/statistics/decision-trees.astro`: distinct creative and statistical decision interfaces.
- `src/export/`: consistent multi-format reporting and ZIP output.
- `scripts/guard-pages-target.ts`, `scripts/verify-deployment.ts` and `scripts/sync-main-ff-only.ps1`: deployment identity guard and version parity.
- `.github/workflows/ci.yml` and `.github/workflows/release.yml`: automated CI and separately authorized release paths.

### Determinism and canonical data limitations

One earlier pinned source comparison was reported as **448 paths**: 393 identical, 41 changed, 1 production-only, 13 remodeling-only. This was a historical baseline pair, **not** a claim that subsequent source commits yield the same count. The repository's `verify:baseline` gate preserves the reference snapshot without substituting it for the latest resolved source SHAs.

Statuses used in the analytical domain distinguish observed/derived canon, model estimates, scenarios, proposals, archives and insufficient data. A current source SHA and a historical baseline SHA must be reported separately.

## 5. Creative Intelligence and Decision Intelligence execution history

### 5.1 Creative Intelligence foundations

The Creative Intelligence scope integrated source-backed entity extraction and graph relationships, consistency auditing, opportunity detection, story refactor planning, canon remodeling scenario exploration and creator-controlled ideation. An important narrative use case was the tension between Reltronland and Depcutland: they can remain political rivals while cooperating pragmatically on Henchoway/Nytherion threats. Such a joint response does not automatically imply permanent alliance, common sovereignty, or endorsement of each other's policies.

Evidence references were required to resolve to actual source passages. Verified relationships were differentiated from candidate or speculative connections, including in impact traversal and UI language. Proposed stories remain proposals and must not silently become accepted canon.

### 5.2 Decision Intelligence objective

The owner authorized extending those capabilities with **explainable Decision Trees**, including decision conditions, branch rules, outcomes, risk dimensions, missing-information states, and evidence/source citations. The solution was required to present potential creative paths without dictating a canonical winner.

A separate statistical path allowed `DecisionTreeClassifier` and `DecisionTreeRegressor` only when data quality permitted genuine supervised learning. The implementation uses explicit sufficiency and leakage checks. Important policy facts in the Python implementation include a minimum of 30 complete labeled observations, a minimum of 10 usable samples per feature, a nonconstant observed target, class sufficiency where classification is used, bounded depth, fixed random seed and hold-out evaluation. Cluster assignments/cohort labels are not silently promoted into observed labels. Synthetic tests are labeled as method checks and never presented as Asthortera facts. Insufficient data returns `INSUFFICIENT_LABELED_DATA` rather than a fabricated trained model.

### 5.3 AI-agent interruption and recovery

The conversation contains an agent interruption after a large implementation effort exhausted the agent's available token/usage window. The owner wanted the continuation to produce the *same engineering completion* expected from uninterrupted execution, in one standalone prompt wherever technically feasible.

The interrupted agent had already created or modified typed decision-domain files, a deterministic evaluator, evidence handling, narrative extraction/remodeling components, and decision fixtures/tests. Early local unit-test evidence included **12 passing decision-domain tests**. The working tree was partially modified: it was **not** a completed, committed production feature merely because some tests passed.

The review identified substantial historical evidence defects in an earlier Creative Intelligence artifact: **22 citation mismatches among 52 checked examples** and **23 dangling entity references**. An incorrect expansion of the abbreviation CBC and inconsistent numerical source readings were among the example classes of defects. These findings motivated strict quote-to-source verification, typed evidence status, and fail-closed narrative relationship rules; they were not treated as permission to invent replacement facts.

A continuation prompt instructed the agent to recover the actual workspace without discarding uncommitted work, repair evidence, complete both creative and supervised decision trees, integrate graph/UI/export contracts, run all tests, commit and push, then verify GitHub CI. The prompt explicitly noted that no single textual prompt can override a model's usage limits.

### 5.4 Completion acceptance

The eventual agent report and subsequent GitHub verification established Decision Intelligence on GitHub `main` at `eb4b99d657614548fd047e16d2c987630586b582`. The linked CI run [#43335686858](https://github.com/Reltroner/reltroner-statistics/actions/runs/43335686858) completed successfully.

Reported completion snapshot:

| Gate or artifact | Recorded result |
| --- | --- |
| Node unit tests | 76 passed |
| Python tests | 19 passed |
| Browser E2E | 255 passed, one intentional mobile-project skip |
| Static build | 530 pages and 541 PDF artifacts reported in later release inspection |
| Evidence integrity | Zero invalid cited evidence in accepted validation |
| TypeScript/Astro diagnostics | No reported errors |
| GitHub CI | Five passing jobs |
| Statistics site public deployment | **Not yet performed at that stage** |

The count and performance metrics are historical acceptance snapshots, not lifetime promises for a continually changing repository.

## 6. RC-DEPLOY-01 — Production readiness and visual acceptance

**Period:** 2026-11-13.  
**Purpose:** Secure publication isolation before any Cloudflare production activity, generate usable visual evidence, and ensure the Statistics release cannot target Studio/LMS/HRM.

The first deployment policy intentionally permitted only `reltroner-statistics.pages.dev` and **zero custom domains**; this was a bootstrap-era safety rule, not the final desired public domain. The later RC-DEPLOY-02 explicitly superseded the restriction for the one authorized Statistics hostname.

Implementation changes included a GET-only Cloudflare API preflight, strict Pages project identity checking, target URL allowlist, custom-domain inventory checks, fail-closed behavior, manual `workflow_dispatch` publication authorization, and guarded regression tests for protected hostnames. Build jobs remained distinct from actual publish jobs, and release artifacts could be created without publicly deploying.

Visual QA captured **48 screenshots**: six representative pages × four viewport profiles × two themes. The reviewer found duplicate Creative Intelligence section navigation on smaller screens. The interface was corrected, and a regression assertion prevented the duplicate navigation from recurring. Screenshot artifacts constituted visual review evidence, not a substitute for all possible human acceptance or real-user monitoring. An observed large Creative-page HTML payload (~2.85 MB uncompressed, ~326 KB compressed in one historical inspection) was logged as a performance improvement opportunity rather than falsely certified as optimized.

Verified GitHub record:

- [PR #1 — RC-DEPLOY-01](https://github.com/Reltroner/reltroner-statistics/pull/1), merged 2026-11-13 04:59:23 UTC.
- Merge commit `12fe65f98729bb23fd150f07fb51230415067f98`.
- [CI #43369021226](https://github.com/Reltroner/reltroner-statistics/actions/runs/43369021226), passed.

The outcome was **engineering readiness**, not yet Cloudflare production activation.

## 7. RC-DEPLOY-02 — Exact GitHub/local commit parity and custom-domain readiness

**Period:** 2026-11-14.  
**Purpose:** Allow the owner-authorized `statistics.reltroner.com` while retaining strict project isolation and safe one-way local synchronization.

The refined Pages guard recognized two phases:

1. Bootstrap: `https://reltroner-statistics.pages.dev` with zero custom domains.
2. Final production: `https://statistics.reltroner.com` with exactly one *active* custom domain, named `statistics.reltroner.com`.

It rejected unrelated Pages projects, apex/`www`/LMS/HRM names, incorrect hostnames, extra or pending domain associations, and stale or incomplete inventory checks. The preflight only uses GET requests to Cloudflare, rather than changing the account's DNS or nameserver configuration.

The production GitHub Actions path was configured to run on eligible `push` events to `main` **after** cross-platform and browser gates succeeded, download the exact successfully built artifact, reject a stale commit, guard Pages identity, deploy only to project `reltroner-statistics`, and compare the published `build-info.json` against the build. A manual release workflow remained available for bootstrap and recovery. Both publish paths target the same production environment and dedicated Pages project.

For the Windows workspace the repository added `scripts/sync-main-ff-only.ps1`, which rejects a wrong repository, wrong branch, unexpected remote, dirty working tree, and divergent/non-fast-forward history. The script never uses `reset --hard`, `git clean`, forced push, forced checkout or destructive rebase.

Evidence:

- [PR #2 — Custom-domain and parity contract](https://github.com/Reltroner/reltroner-statistics/pull/2), merged 2026-11-14 03:03:14 UTC.
- Merge SHA `0d0bc9af22e46bf0d74e98fba5c05942f070e37a`.
- [CI #43549582852](https://github.com/Reltroner/reltroner-statistics/actions/runs/43549582852), passed.
- Source reference: [RC-DEPLOY-02 contract](https://github.com/Reltroner/reltroner-statistics/blob/main/docs/RC-DEPLOY-02.md).

The implementation did **not** claim the Windows disk had changed or a Cloudflare account had been configured merely because source code was merged.

## 8. Windows PowerShell 5.1 incident, root cause and repair

### 8.1 First synchronization succeeded, then verification failed

The owner ran a safe fast-forward on `C:\Projects\reltroner-statistics` from `eb4b99d` to `0d0bc9a`. Git printed:

~~~text
Updating eb4b99d..0d0bc9a
Fast-forward
~~~

The subsequent call to `scripts/sync-main-ff-only.ps1` emitted:

~~~text
git.exe : From https://github.com/Reltroner/reltroner-statistics
At C:\Projects\reltroner-statistics\scripts\sync-main-ff-only.ps1:24
$result = @( & git @Arguments 2>&1 )
NativeCommandError
Final parity verification failed.
~~~

Crucially, the fast-forward itself had already completed. Normal Git fetch progress appeared on native stderr and Windows PowerShell 5.1 treated redirected stderr as an error record under `$ErrorActionPreference = 'Stop'`.

### 8.2 Fix and regression behavior

The wrapper was patched to capture **stdout only**, keep native stderr visible, and assess success using `$LASTEXITCODE`. The first Windows CI regression exercised an intentionally failing Git command to confirm real failures still throw; the test itself initially inherited the expected nonzero `$LASTEXITCODE` and made the job exit 1 despite printing its own PASS marker. That harness issue was corrected by running a known-successful Git command before the test exited.

The final PR included a Windows PowerShell 5.1 regression test using actual Git fetch progress and an intentional invalid-ref failure. All affected CI jobs then passed.

- [PR #3 — PowerShell 5.1 Git stderr repair](https://github.com/Reltroner/reltroner-statistics/pull/3), merged 2026-11-14 03:22:28 UTC.
- Final application SHA `042aa46354b9253feb2c0d55e4c0ce1adbd3e7a6`.
- [CI #43551304766](https://github.com/Reltroner/reltroner-statistics/actions/runs/43551304766), passed.

The owner then safely fast-forwarded `0d0bc9a..042aa46` and ran the patched script. The terminal explicitly reported:

~~~text
=== FETCH REMOTE MAIN (NO RESET, NO REBASE) ===
LOCAL_MAIN_1_TO_1_GITHUB: VERIFIED (042aa46354b9253feb2c0d55e4c0ce1adbd3e7a6)
=== LOCAL MAIN SYNCHRONIZED ===
~~~

This proved the local branch and fetched GitHub `main` shared the same commit with a clean working tree at the time of execution.

## 9. RC-DEPLOY-03 — GUI-driven Cloudflare Pages activation

**Date:** 2026-11-14.  
**Approach:** Owner-executed Cloudflare/GitHub GUI configuration, with deterministic guidance and screenshot checkpoints. No general-purpose Cloudflare account mutation tool was available to the assistant. The owner performed account-level changes directly. Details in this section record confirmed screen states and outcomes, not hypothetical operations.

### Checkpoint A — Existing platform discovered

Cloudflare Workers & Pages initially showed other existing applications, including `reltroner-studio-cf`, `lms-fe`, test API Pages projects and ERP Workers. There was **no existing** `reltroner-statistics` Pages project in that inventory. Cloudflare DNS for `reltroner.com` showed an already managed Cloudflare zone with protected apex/`www`/LMS/HRM-related records.

The chosen solution was a **new, dedicated Cloudflare Pages Direct Upload project**—not a shared Studio project, not a second Git-connected auto-build pipeline and not a Hostinger deployment.

### Checkpoint B — Dedicated Pages project created

From Workers & Pages → Create application → Continue to Pages → Direct Upload, the owner created `reltroner-statistics`. A minimal bootstrap HTML/ZIP asset was used to establish the project without uploading the entire Windows repository. The Cloudflare project displayed:

- Project: `reltroner-statistics`.
- Production branch/environment: `main` / Production.
- Bootstrap URL: `https://reltroner-statistics.pages.dev`.
- Initial status: successful bootstrap deployment.

The temporary bootstrap page was intentionally replaced by the verified GitHub Actions static build. Uploading the entire repository—with code, test fixtures, config and dependencies—was explicitly rejected as the wrong procedure.

### Checkpoint C — Cloudflare API token and GitHub credentials

The owner used **Account API Tokens → Create a token → Start from scratch → Developer Platform → Pages Write/Edit**. The review screen confirmed:

- Token name `reltroner-statistics-github-actions`.
- Permission: **Pages Write**; no DNS Edit or Workers Edit permission selected.
- Resource scope: **Entire Account** for the relevant Cloudflare account.
- Expiry displayed as **2027-11-14**.
- IP filtering: all addresses permitted, consistent with changing GitHub-hosted runner IPs.

**Security caveat:** Pages Write for an entire account can affect other Pages projects if the credential is misused. The workflow's project-name guard restricts what *this code* attempts, but it is not an account-side, project-scoped token boundary. Use GitHub secret protection, production branch restrictions and token rotation. The raw token value, account identifier and any secret payload are intentionally omitted from this public archive.

The owner then confirmed two **Repository secrets** in GitHub:

- `CLOUDFLARE_API_TOKEN`
- `CLOUDFLARE_ACCOUNT_ID`

Only their names/presence were shown; their values cannot be inspected after saving and were not disclosed.

### Checkpoint D — Repository variables and environment

The owner configured **Repository variables**:

| Variable | Bootstrap | Final |
| --- | --- | --- |
| `CLOUDFLARE_PAGES_PROJECT` | `reltroner-statistics` | Unchanged |
| `SITE_URL` | `https://reltroner-statistics.pages.dev` | `https://statistics.reltroner.com` |

The GitHub `production` Environment was created with **Selected branches and tags** allowing **`main` only**; the screenshot showed one allowed branch and zero allowed tags. Required reviewers and wait timer were not enabled in the recorded setup. The assistant distinguished repository secrets/variables from environment-level variables and avoided duplicating them.

### Checkpoint E — First verified Pages release

The owner manually invoked [`Analysis release — pipeline, gates, publication`](https://github.com/Reltroner/reltroner-statistics/actions/workflows/release.yml), branch `main`, source SHA fields left empty so the pipeline resolved current source tips, `publish_statistics=true`.

[Workflow run #43574215880](https://github.com/Reltroner/reltroner-statistics/actions/runs/43574215880) passed:

- Build and verify release candidate.
- Read-only project identity and zero-custom-domain guard.
- Publish to Cloudflare Pages.
- Verify the live published build identity.

The `Publication held` job was skipped **as expected** because manual publication was explicitly authorized. This run targeted `reltroner-statistics.pages.dev`.

### Checkpoint F — Custom domain associated and DNS record observed

In Cloudflare Pages → project `reltroner-statistics` → Custom domains → Set up a custom domain, the owner associated `statistics.reltroner.com`. The follow-up screenshot displayed **Active** and **SSL enabled**. A transitional page message still referred to DNS rechecking; the actual DNS view and live verification were subsequently used as independent evidence.

The owner later provided a DNS table showing **23 records in the zone** and the new row:

| DNS property | Observed value |
| --- | --- |
| Name | `statistics.reltroner.com` |
| Type | `CNAME` |
| Content | `reltroner-statistics.pages.dev` |
| Proxy status | **Proxied** |
| TTL | **Auto** |

The existing apex, `www`, `lms` and `hrm` entries remained visible in their respective configurations. No global nameserver or unrelated record modifications were required. This is evidence of the specific observed DNS state; it is not a full forensic before-and-after audit of every provider setting.

### Checkpoint G — Final-domain release and SHA parity

The owner changed repository `SITE_URL` to `https://statistics.reltroner.com` while leaving `CLOUDFLARE_PAGES_PROJECT` unchanged, then manually ran the same release workflow from `main` with `publish_statistics=true`.

GitHub's actual run [#43587678915](https://github.com/Reltroner/reltroner-statistics/actions/runs/43587678915) (created 2026-11-14 10:57:12 UTC) passed. Its **Publish to Cloudflare Pages** job reported success on the GET-only custom-domain guard, Wrangler upload and live build identity verifier. `Publication held` was skipped as intended.

The owner additionally executed:

~~~powershell
Set-Location 'C:\Projects\reltroner-statistics'
powershell.exe -NoProfile -ExecutionPolicy Bypass -File '.\scripts\sync-main-ff-only.ps1' -VerifyWebsite
~~~

And supplied this exact success evidence:

~~~text
=== FETCH REMOTE MAIN (NO RESET, NO REBASE) ===
From https://github.com/Reltroner/reltroner-statistics
 * branch            main       -> FETCH_HEAD
LOCAL_MAIN_1_TO_1_GITHUB: VERIFIED (042aa46354b9253feb2c0d55e4c0ce1adbd3e7a6)
STATISTICS_PUBLIC_SHA_PARITY: VERIFIED (042aa46354b9253feb2c0d55e4c0ce1adbd3e7a6)
~~~

This final verifier compares the GitHub/local Statistics commit against the public `/build-info.json` commit and confirms source identities/digest are present; the GitHub publish job additionally compares the full live build identity keys against its own freshly built manifest.

## 10. Release safety invariants

The owner repeatedly made the following *non-negotiable*:

1. **Do not alter** DNS/nameservers or deployments for `reltroner.com`, `www.reltroner.com`, `lms.reltroner.com` and `hrm.reltroner.com`.
2. Do not repoint existing protected CNAME, A, MX, TXT, Worker route or other service bindings as a shortcut.
3. Statistics must have its own Pages project and one explicitly authorized custom hostname.
4. Cloudflare account interaction must happen within the owner's intentionally approved GUI scope. The automated preflight is read-only.
5. An uncommitted/different local checkout must never be reset or silently overwritten to match GitHub.
6. Publish only the verified generated `dist/` artifact; never upload the whole local repository as a website.
7. Never claim a successful build artifact is itself proof of live deployment.
8. The live Statistics commit, analysis source commits, and Studio deployed build status are **three distinct identities**.
9. Creator control, intellectual property, and proposal/canon distinctions remain intact.
10. Never expose Cloudflare credentials or token contents in reports, commits, screenshots or support messages.

## 11. Final acceptance ledger as of 2026-11-14

| Contract | Result | Evidence |
| --- | --- | --- |
| Statistics Decision Intelligence integrated | PASS | `eb4b99d…`; [CI #43335686858](https://github.com/Reltroner/reltroner-statistics/actions/runs/43335686858) |
| RC-DEPLOY-01 isolated release/visual evidence | PASS | [PR #1](https://github.com/Reltroner/reltroner-statistics/pull/1); [CI #43369021226](https://github.com/Reltroner/reltroner-statistics/actions/runs/43369021226) |
| RC-DEPLOY-02 domain/parity source contract | PASS | [PR #2](https://github.com/Reltroner/reltroner-statistics/pull/2); [CI #43549582852](https://github.com/Reltroner/reltroner-statistics/actions/runs/43549582852) |
| PowerShell 5.1 native stderr regression | PASS | [PR #3](https://github.com/Reltroner/reltroner-statistics/pull/3); [CI #43551304766](https://github.com/Reltroner/reltroner-statistics/actions/runs/43551304766) |
| Dedicated Pages initial/bootstrap release | PASS | Owner Cloudflare screenshot; [run #43574215880](https://github.com/Reltroner/reltroner-statistics/actions/runs/43574215880) |
| Custom-domain Pages association / SSL | PASS (observed) | Owner Cloudflare Custom domains screenshot (`Active`, `SSL enabled`) |
| DNS CNAME to dedicated project | PASS (observed) | Owner Cloudflare DNS inventory screenshot |
| GitHub `SITE_URL` final canonical hostname | PASS (observed) | Owner GitHub Variables screenshot |
| Final-domain manual publish and live verifier | PASS | [run #43587678915](https://github.com/Reltroner/reltroner-statistics/actions/runs/43587678915) |
| Windows `main` = fetched GitHub `main` | PASS | Owner terminal `LOCAL_MAIN_1_TO_1_GITHUB` |
| Live website SHA = local/GitHub SHA | PASS | Owner terminal `STATISTICS_PUBLIC_SHA_PARITY` |
| Auto-deploy following a **new main push** | **NOT YET DEMONSTRATED** | Automation code configured, but no newly pushed release cycle was accepted in this conversation |
| Continuous runtime uptime, latency, accessibility and manual visual sign-off on the final hostname | **NOT FULLY ESTABLISHED** | CI and sampled screenshots exist; no continuous production monitoring claim |
| Verified *deployed Studio* build identity | **NOT ESTABLISHED** | Historical analysis manifest explicitly recorded `DEPLOYMENT_UNVERIFIED` |

## 12. Incident prevention and operational lessons

### 12.1 Safe synchronization is not destructive synchronization

A dirty local Git checkout is valuable work, not disposable drift. Branch mismatch, unexpected remote, local-ahead history or divergence must halt automation. The PowerShell wrapper is deliberately one-way fast-forward-only and independently checks cleanliness after the operation.

### 12.2 A native command's stderr is not its exit status

Git regularly uses stderr for progress. Windows PowerShell 5.1 plus redirection under Stop semantics can misclassify this as a terminating exception. Automated tests must reproduce the native process conditions, including a successful command with stderr and a genuinely failing command; negative tests must also clear the expected native exit code before completion.

### 12.3 Workflow allowlists do not replace provider-side least privilege

The owner-approved token had Pages Write permission at **account** scope, even though the automation performs strict Statistics-only checks. That difference is a residual security consideration; repository and environment protections, revocation, CI permissions, action pinning and rotation matter.

### 12.4 Deploy success needs observed external identity

The release workflow first tests/builds/exports, then uploads the build and checks `/build-info.json`. Success on `npm run build` or an uploaded GitHub artifact is never equated with a working website. Equally, a website responding with the expected Statistics SHA does not prove every source value matches a currently deployed Studio build.

### 12.5 The domain isolation contract evolved explicitly

RC-DEPLOY-01's initial "no custom domains" guard was appropriate for preflight/bootstrap. RC-DEPLOY-02 explicitly amended it to recognize the one authorized final hostname. The two rules should not be read simultaneously without their phase scope.

### 12.6 Review snapshots are bounded, not everlasting

Screenshot artifacts may expire after retention periods, and counts of pages, PDFs, tests, and source findings can change on later commits. Preserve links, SHA, timestamps, manifest digests and screenshots as evidence where appropriate; do not treat historical numbers as evergreen contracts.

## 13. Residual work and next acceptance

**RC-DEPLOY-04 — Automatic publish proof on a newly committed source change** remains the most meaningful follow-up. It should observe a harmless, reviewed change to `Reltroner/reltroner-statistics/main`, full CI success, the resulting `publish_statistics` job, Cloudflare Pages deployment and final-domain SHA parity *without touching unrelated DNS*. Also verify protected site availability and capture a rollback reference. This archive does not authorize making an unnecessary "proof commit" in the Statistics repository by itself.

Other follow-ups include production user-journey smoke tests, reasonable performance and bundle-size budgets for Creative/graph pages, release observability, secret rotation before 2027-11-14, ongoing provenance/evidence drift tests, and preserving reproducible visual evidence beyond short artifact retention windows.

No automatic canon ratification, model claim upgrading, source-repository mutation or infrastructure expansion follows from these acceptance results.

## 14. Source links and archival method

Primary implementation and evidence:

- [Reltroner Statistics implementation](https://github.com/Reltroner/reltroner-statistics)
- [Reltroner Statistics README](https://github.com/Reltroner/reltroner-statistics/blob/main/README.md)
- [RC-DEPLOY-01 implementation contract](https://github.com/Reltroner/reltroner-statistics/blob/main/docs/RC-DEPLOY-01.md)
- [RC-DEPLOY-02 implementation contract](https://github.com/Reltroner/reltroner-statistics/blob/main/docs/RC-DEPLOY-02.md)
- [GitHub CI workflow](https://github.com/Reltroner/reltroner-statistics/blob/main/.github/workflows/ci.yml)
- [GitHub manual release workflow](https://github.com/Reltroner/reltroner-statistics/blob/main/.github/workflows/release.yml)
- [Deployment target guard](https://github.com/Reltroner/reltroner-statistics/blob/main/scripts/guard-pages-target.ts)
- [Live build verifier](https://github.com/Reltroner/reltroner-statistics/blob/main/scripts/verify-deployment.ts)
- [PowerShell safe synchronization script](https://github.com/Reltroner/reltroner-statistics/blob/main/scripts/sync-main-ff-only.ps1)
- [PowerShell regression test](https://github.com/Reltroner/reltroner-statistics/blob/main/tests/windows/git-native-stderr.ps1)
- [Final production manual workflow #43587678915](https://github.com/Reltroner/reltroner-statistics/actions/runs/43587678915)
- [Public website](https://statistics.reltroner.com)
- [Public version identity endpoint](https://statistics.reltroner.com/build-info.json)

**Archival discipline:** This document synthesizes the substantive user instructions, assistant engineering decisions, console logs, screenshots, GitHub changes and acceptance outputs discussed in the project conversation. It is not a verbatim, timestamp-complete transcript; repetitive intermediate CI polling and transient progress messages are summarized. Screenshot claims are explicitly identified as owner-provided observations. CI and repository claims have linked GitHub evidence. Sensitive credentials, raw token values and private account configuration identifiers are deliberately not copied into this public repository.

For exact operational steps and deterministic acceptance commands, see [Operations and Recovery Runbook](./2026-11-14-operations-and-recovery-runbook.md). For the chronological evidence ledger and gate-to-claim traceability, see [Conversation and Evidence Ledger](./2026-11-14-conversation-and-evidence-ledger.md).
