# Reltroner Statistics — Post-Archive Production, Calculator & Scenario Intelligence Release Addendum

> **Recorded:** 2026-11-16 (Asia/Jakarta).  
> **Evidence window:** GitHub releases and owner-submitted operations on 2026-11-15.  
> **Category:** Evidence-backed extension of the 2026-11-14 engineering archive, **not** a rewrite of its historical acceptance snapshot.  
> **Application:** [Reltroner Statistics](https://statistics.reltroner.com) · [GitHub repository](https://github.com/Reltroner/reltroner-statistics).  
> **Observed GitHub `main` at preparation:** `54708b04d8a675d065ea30a18798877d057d4982`.  
> **Production verification:** [CI and publish run #43720463014](https://github.com/Reltroner/reltroner-statistics/actions/runs/43720463014).  
> **Source-of-truth rule:** The Statistics application commit, pinned Studio/Remodeling inputs, live Statistics deployment and live Studio deployment are distinct identities.

## 1. Why this addendum exists

The [2026-11-14 chronicle](./2026-11-14-end-to-end-engineering-and-production-chronicle.md), [evidence ledger](./2026-11-14-conversation-and-evidence-ledger.md) and [runbook](./2026-11-14-operations-and-recovery-runbook.md) correctly record that day's manual release and the then-unproven automatic push-to-publish loop. They remain historical artifacts. Three production feature/release changes and one dashboard-only configuration change occurred subsequently; they must not be silently backdated into the original archive.

This document records **later facts** with source and verification labels. Statements described as **GitHub verified** follow inspectable commits or CI logs; **owner observed/reported** follows the provided local-console/browser/Cloudflare GUI evidence; **not established** remains explicitly excluded. Counts and SHAs are snapshots, not perpetual service-level guarantees.

## 2. Subsequent release chronology

| Date (UTC unless stated) | Source / release | Verified result | Interpretation |
| --- | --- | --- | --- |
| 2026-11-15 04:54 | [Statistics merge commit `a00a07f`](https://github.com/Reltroner/reltroner-statistics/commit/a00a07f4d3292f3626f84a8c250e5f91d3b758ca) · [PR #5](https://github.com/Reltroner/reltroner-statistics/pull/5) | [Main CI #43678746193](https://github.com/Reltroner/reltroner-statistics/actions/runs/43678746193) succeeded | Species/ancestry, Spatial 3D, deterministic Assistant, scatter labels, GDP treemap, responsive QA, Platform Ecosystem |
| 2026-11-15 10:59 | [UI/UX commit `4f81f1a`](https://github.com/Reltroner/reltroner-statistics/commit/4f81f1a4feca47f2faff5444e5acf2d1ac6a3842) | Commit present in Statistics history | Inspection and comparison controls separated, land/resident panels differentiated, regression coverage added; no data or provenance changes |
| 2026-11-15 13:43 | [Calculator commit `54708b0`](https://github.com/Reltroner/reltroner-statistics/commit/54708b04d8a675d065ea30a18798877d057d4982) | [Push-triggered CI #43720463014](https://github.com/Reltroner/reltroner-statistics/actions/runs/43720463014), all six jobs successful | CALC-01–CALC-07 implemented on `main` |
| 2026-11-15 13:54 | Same Calculator CI publish job | `STATISTICS_DEPLOYMENT_VERIFIED`, exact published Statistics SHA `54708b04d8a675d065ea30a18798877d057d4982` | **RC-DEPLOY-04 automatic commit → CI → Pages publish → SHA verification demonstrated** |
| 2026-11-15, owner GUI | Cloudflare rule `RC-DEPLOY-05 - Disable Statistics RUM` | Owner screenshots: rule Active; hostname-specific filter; disabled RUM; empty browser Console and no beacon match in sampled Network capture | Statistics-specific analytics beacon/CSP error remediated operationally; not a source-code release |

**Important:** The initial 2026-11-14 statement "RC-DEPLOY-04 NOT YET DEMONSTRATED" remains truthful **as of that historical date**. The later successful main-push deployment supplies the missing proof; it is not an inconsistency to erase retroactively.

## 3. PR #5 feature baseline — delivered before Calculator

[Commit `a00a07f`](https://github.com/Reltroner/reltroner-statistics/commit/a00a07f4d3292f3626f84a8c250e5f91d3b758ca) brought seven requirements plus Spatial 3D:

1. **Species / primary ancestry:** production-pinned six-category ancestry; national shares and computed resident counts; representative 14-nation benchmark, **not** a measured 37-state census. The five development nations remain unassigned and the 18 deferred states are an aggregate.
2. **Statistics Intelligence Assistant:** deterministic source-grounded answers, explicit epistemic labels, immutable GitHub citations and insufficient-data handling; optional external explanation is disabled.
3. **Contact:** existing outbound link to Studio Contact preserved without duplicating it.
4. **Spatial 3D:** Remodeling-pinned terrestrial footprint and home-habitat shares labeled `PROPOSED`. Distinct land-area and resident denominators; polygons, volumes and unassigned marine/habitat-capacity quantities remain unknown.
5. **Scatter labels:** measured, boundary-aware label placement so right-edge country labels do not clip.
6. **GDP treemap:** small-tile country labels and percentages remain visible using in-tile labels or an external label rail; residual states remain grouped.
7. **Responsive/accessibility QA:** multiple viewport widths, both themes, wide-font overflow checks, accessible navigation and explicit "Platform Ecosystem / You are here" state.

Representative checked values (status depends on data role):

| Example | Computation / source | Meaning |
| --- | --- | --- |
| Beluftner Phantomkind | `91 B × 6% = 5.46 B` | Production ancestry-derived residents, not a separate species census |
| Reltronland land footprint | `58% / 15% / 14% / 13%` | Remodeling land-area distribution |
| Reltronland principal habitats | `70% / 22% / 2% / 6%` of 855 B residents | Remodeling resident distribution; 188.10 B underground |
| Beluftner area | Production 88 vs Remodeling 363 million km² | Distinct sources; denominators must never be mixed |

The subsequent `4f81f1a` commit reorganized Species/Spatial control flow: primary "Step 1 · Inspect" immediately precedes national detail; visually secondary "Step 2 · Compare" immediately precedes comparison. Spatial panels separately identify **land area** and **residents** using distinct accents, labels and written denominators. These UI edits do not change canonical observations.

## 4. Calculator & Scenario Intelligence — CALC-01 through CALC-07

**Implementation SHA:** [`54708b04d8a675d065ea30a18798877d057d4982`](https://github.com/Reltroner/reltroner-statistics/commit/54708b04d8a675d065ea30a18798877d057d4982)  
**Primary route:** [`/calculator/`](https://statistics.reltroner.com/calculator/)  
**Assistant route:** [`/assistant/`](https://statistics.reltroner.com/assistant/)  
**Release principle:** **one deterministic calculation engine, two interfaces**.

| Capability | Implemented behavior | Primary code |
| --- | --- | --- |
| CALC-01 — Deterministic calculation | Versioned formula allowlist, strict Zod request/result schemas, finite numeric and unit/denominator validation, pinned evidence, deterministic `evaluate()` | [`calculator.ts`](https://github.com/Reltroner/reltroner-statistics/blob/54708b04d8a675d065ea30a18798877d057d4982/src/domain/calculator.ts) · [`calculator-schemas.ts`](https://github.com/Reltroner/reltroner-statistics/blob/54708b04d8a675d065ea30a18798877d057d4982/src/domain/calculator-schemas.ts) |
| CALC-02 — Future scenarios | Conditional `baseline × (1 + annual_rate)^years`; user assumptions, `SCENARIO` status and separate source anchors; empirical forecast insufficiency declared | [`calculator.ts`](https://github.com/Reltroner/reltroner-statistics/blob/54708b04d8a675d065ea30a18798877d057d4982/src/domain/calculator.ts) |
| CALC-03 — Historical backcast | Conditional inverse growth from source anchors; existing BAC chronology and sovereign-foundation guards; no invented annual observed history | [`calendar.ts`](https://github.com/Reltroner/reltroner-statistics/blob/54708b04d8a675d065ea30a18798877d057d4982/src/domain/calendar.ts) · [`calculator.ts`](https://github.com/Reltroner/reltroner-statistics/blob/54708b04d8a675d065ea30a18798877d057d4982/src/domain/calculator.ts) |
| CALC-04 — Qualitative rubric | Three Reltronland–Depcutland cooperation alternatives; seven explicit criteria; user-entered ordinal scores and weights; missing scores remain unassigned | [`calculator.ts`](https://github.com/Reltroner/reltroner-statistics/blob/54708b04d8a675d065ea30a18798877d057d4982/src/domain/calculator.ts) |
| CALC-05 — Assistant tools | Existing deterministic Assistant invokes shared evaluation and supports EN/ID calculator questions; single-use session handoff; optional LLM endpoint stays fail-closed | [`assistant.ts`](https://github.com/Reltroner/reltroner-statistics/blob/54708b04d8a675d065ea30a18798877d057d4982/src/domain/assistant.ts) · [`handoff.ts`](https://github.com/Reltroner/reltroner-statistics/blob/54708b04d8a675d065ea30a18798877d057d4982/src/engine/calculator/handoff.ts) |
| CALC-06 — Compare and sensitivity | Bounded 2–3 scenario comparisons, controlled parameter sweeps; Spatial conditional share and full-composition closure checks | [`calculator.ts`](https://github.com/Reltroner/reltroner-statistics/blob/54708b04d8a675d065ea30a18798877d057d4982/src/domain/calculator.ts) |
| CALC-07 — UI, export & QA | Five responsive modes, results/tables/ECharts, keyboard navigation, JSON/CSV export with provenance and spreadsheet-formula neutralization | [`CalculatorWorkspace.tsx`](https://github.com/Reltroner/reltroner-statistics/blob/54708b04d8a675d065ea30a18798877d057d4982/src/features/calculator/CalculatorWorkspace.tsx) · [`export.ts`](https://github.com/Reltroner/reltroner-statistics/blob/54708b04d8a675d065ea30a18798877d057d4982/src/engine/calculator/export.ts) |

### 4.1 Calculation contract

The versioned result schema is `reltroner-calculator-result.v1`; handoff schema is `reltroner-calculator-handoff.v1`. The implementation records its formula/version, validated input and assumption values, units, output status, limitations and source references. Supported calculator statuses are `CANON_OBSERVED`, `CANON_DERIVED`, `SCENARIO`, `PROPOSED` and `INSUFFICIENT_DATA`. An invalid request is a failure, **not** a fictitious zero.

The underlying Statistics domain also has `MODEL_ESTIMATE` for suitable statistical models; the Calculator's current conditional growth scenarios **are not** empirical forecasts. A lack of sufficiently validated historical observations produces `INSUFFICIENT_DATA_FOR_EMPIRICAL_FORECAST` while the explicitly hypothetical calculation may still run.

The shared engine exposes the operations `calculate`, `projectScenario`, `reconstructScenario`, `compareScenarios`, `evaluateQualitativeScenario` and `analyzeSensitivity`. It does not run arbitrary user JavaScript, mutate source data or require external LLM inference.

### 4.2 Scenario and historical semantics

- Year 0 Reltronland population is **855 B** in the pinned baseline. A hypothetical +1% annual assumption over 100 years is labeled `SCENARIO`; the assumed growth rate is **not** a canonical demographic observation.
- Asthortera's `BAC` chronology is governed by [`src/domain/calendar.ts`](https://github.com/Reltroner/reltroner-statistics/blob/54708b04d8a675d065ea30a18798877d057d4982/src/domain/calendar.ts); older BAC values are earlier, and missing annual observations remain missing.
- Backcasts show canonical historical anchors separately from modeled values. They do not certify that the modeled path actually occurred.
- Qualitative scores are creator-supplied ordinal judgments. **Scores are neither probabilities nor verified geopolitical facts.** Incomplete alternative scores cannot silently become complete.
- A single-category Spatial example of underground share 27% at constant Reltronland population yields `855 B × 27% = 230.85 B` **as a conditional count only**. Retaining the other three shares would make the proposed entire composition 105%; a full distribution must reject that inconsistency or use a clearly specified reallocation totaling 100%.
- Remodeling-sourced spatial values remain `PROPOSED` as inputs; their hypothetical transformations are `SCENARIO` results with the underlying proposal attribution preserved.

### 4.3 Assistant and privacy boundary

The [published evidence index](https://github.com/Reltroner/reltroner-statistics/blob/54708b04d8a675d065ea30a18798877d057d4982/src/pages/data/assistant-index.json.ts) adds historical anchors and foundations to `reltroner-agent-index.v2`. The owner-reported live smoke check observed **367 facts, 2 anchors and 14 foundations** for this release. This is a version-specific snapshot.

Bidirectional `/calculator` ↔ `/assistant` handoff uses a validated, single-use `sessionStorage` payload (10-minute TTL) with safe fallback for blocked or malformed storage. No private draft text is encoded in public deep links. Generated LLM prose is **not** active; the owner-reported production `POST /api/assistant` returned HTTP **503** as intended. "Explain with Assistant" therefore means a deterministic grounded explanation, not undisclosed model inference.

### 4.4 Exports and UI

The Calculator exports reproducible **JSON and CSV** results; it does not implement a second global PDF/XLSX/ZIP report engine. The CSV layer preserves standardized columns, source identity/status, CRLF records and spreadsheet-formula injection protection. The single `/calculator` interface has five modes: Calculate, Future scenario, Historical backcast, Qualitative rubric, Compare & sensitivity. Other Statistics pages were not redesigned as part of this feature.

## 5. Release verification and evidence

### 5.1 Direct GitHub CI evidence

[Workflow #43720463014](https://github.com/Reltroner/reltroner-statistics/actions/runs/43720463014) was triggered by a **push to `main`** at Calculator SHA `54708b04d8a675d065ea30a18798877d057d4982`. All six jobs completed successfully:

1. P0R determinism — Ubuntu.
2. P0R determinism — Windows.
3. Python analytics — Ubuntu.
4. Python analytics — Windows.
5. Pipeline, static build and browser tests.
6. **Publish verified main SHA to Statistics custom domain.**

GitHub job logs independently show:

| Gate | At Calculator SHA |
| --- | --- |
| Node unit tests | **104 passed, 0 failed** |
| Python analytics tests | **24 passed** |
| Playwright browser tests | **415 passed, 1 pre-existing viewport-scoped skip** |
| Baseline comparator | `BASELINE_VERIFIED` |
| Publish target preflight | `ISOLATED_STATISTICS_PAGES_VERIFIED` |
| Site deployment verification | `STATISTICS_DEPLOYMENT_VERIFIED` |
| Live Statistics application SHA reported by publish verifier | `54708b04d8a675d065ea30a18798877d057d4982` |

The owner-supplied final local verification additionally reported: `schemas:check` pass; typecheck **0 errors, warnings or hints**; full build **558 pages, 565 PDFs, 32,313 internal links**; `415/415` actually executed E2E tests; clean local tree and `sync-main-ff-only.ps1 -VerifyWebsite` parity. These local-console assertions are **owner-reported**, not direct access to the Windows disk.

**Two digest scopes must not be conflated.** The deterministic pinned baseline check reported `8f3ddad3f264130aa35ccf1a7d8202f5deed13fcbf943a590d7c2702694ea7d5`; the owner-reported later live `/build-info.json` showed semantic digest `d1d034fcaf03d221992c646d4e9114d04122e70364a152147288c9ab77fef082`. They describe different verification contexts/snapshots, and their inequality alone does **not** establish a production defect.

### 5.2 Source snapshot on the observed Calculator release

The owner-reported `/build-info.json` at that release identified:

| Identity | Value |
| --- | --- |
| Statistics application | `54708b04d8a675d065ea30a18798877d057d4982` |
| Production source | `ad895e6d9184f09281a7cc14ccd7867c47acd29e` |
| Remodeling source | `2c970f4c51ef14e610a554ec4127d5bc25cefa9c` |
| Rules | `P0R-2.0.0` |
| Statistics deployment | Verified by the push-triggered publish job |

This identifies the **input repository snapshots**, not a proven SHA of the **separately deployed Studio website**.

### 5.3 RC-DEPLOY-04 — automatic publishing demonstrated

Prior archival limitation: the 2026-11-14 manual release proved target isolation and live parity, but had not exercised an entirely new `main` push.

Later directly evidenced lifecycle:

```text
Calculator commit 54708b0… pushed to main
  → CI run #43720463014 (push event)
  → deterministic/unit/Python/site gates pass
  → only reltroner-statistics Pages project and custom domain allowed
  → Pages deploy
  → /build-info.json exact commit verification
  → STATISTICS_DEPLOYMENT_VERIFIED
```

Deployment logs show `custom_domains:["statistics.reltroner.com"]`, `dns_mutations:0` and `nameserver_mutations:0`. The workflow guard is a meaningful safety property; it is **not** proof that the provider-side API token has been restricted to one Pages project.

## 6. RC-DEPLOY-05 — Cloudflare Web Analytics / CSP

**Decision:** Disable injected Cloudflare Real User Monitoring for the Statistics hostname only, instead of weakening the site's Content Security Policy.

**Owner dashboard evidence (2026-11-15):**

- The Web Analytics dashboard had a zone-wide `reltroner.com` Automatic setup entry. Disabling that whole zone entry would be too broad.
- The owner created **Configuration Rule** `RC-DEPLOY-05 - Disable Statistics RUM`.
- Exact filter: `(http.host eq "statistics.reltroner.com")`.
- Action: **Disable Real User Monitoring (RUM)**.
- Rule state shown: **Active**.
- Subsequent sampled mobile browser Network search showed no matching beacon, browser Console was empty, and the response still showed a CSP header.
- No Git commit, `_headers` relaxation, redeploy, DNS or nameserver change was needed.

**Verification classification:** Configuration and browser evidence are **owner-observed screenshots**, not an authenticated Cloudflare API read from this archive. Exact-hostname matching excludes other hostnames by rule scope; continuous behavior of sibling services and uptime was not independently measured.

**Recovery guidance:** If a beacon CSP error returns, first re-inspect this hostname-specific Cloudflare rule and any Pages-project Web Analytics setting. Do **not** disable the `reltroner.com` zone-wide analytics entry or loosen CSP merely to hide the error.

## 7. Operational checklist for future Calculator releases

1. Inspect `git status -sb`, `git worktree list`, local `HEAD`, `origin/main`, and GitHub `main`. Preserve local-ahead work; do not run the FF-only sync command when local is ahead.
2. Run `npm run verify:baseline`, `npm run schemas:check`, `npm run typecheck`, `npm test`, `npm run test:py`, `npm run pipeline`, `npm run build`, `npm run test:e2e`; verify final exit status and exclusions.
3. Ensure the exact current `main` commit is the release candidate. Use normal non-forced pushes; never reset to manufacture parity.
4. Check the **push-triggered** CI job `publish_statistics`, its project/domain GET-only guard, the static artifact SHA and `STATISTICS_DEPLOYMENT_VERIFIED`.
5. After publish, run from the **clean, in-sync** Windows checkout: `powershell.exe -NoProfile -ExecutionPolicy Bypass -File '.\\scripts\\sync-main-ff-only.ps1' -VerifyWebsite`.
6. Smoke-test `/calculator/`, `/assistant/`, `/statistics/species/`, `/statistics/spatial/`, `/build-info.json`; confirm deterministic Calculator results, JSON/CSV downloads, the fail-closed optional AI endpoint and unchanged CSP.
7. Confirm no unrelated Pages projects, DNS records or nameservers were changed. Record actual commit, source pair, date, CI URL and exceptions.

**Do not** use `sync-main-ff-only.ps1` as a push tool or as a repair for diverged local history. It intentionally synchronizes **local from remote** only when safe.

## 8. Explicit non-claims and remaining boundaries

- A successful automatic release proves the **specific** CI/deploy lifecycle, not permanent production availability.
- The owner-supplied browser checks prove sampled behavior; they are not ongoing RUM, performance or accessibility monitoring.
- The Assistant's external LLM explanation is still disabled; enabling it requires a separate approved provider, server-side secrets, rate limiting and privacy disclosure.
- Calculator scenario forecasts are **conditional**, not time-series validated probabilistic forecasts. Their outputs are not canon.
- Missing Asthortera population trajectories, geographic polygons, habitable `km³` and related unassigned values remain unassigned.
- Independent verification of **Studio's own deployed commit** remains separate from verified Statistics Pages deployment.
- Existing historical staffing estimates and expanded Creative Intelligence vision remain proposals; CALC-04's **bounded** qualitative rubric delivery does not ratify the entire vision.
- Cloudflare API permissions, secret rotation and provider-side least privilege continue to require normal operational oversight.

## 9. Source references

- [Original 2026-11-14 archive index](./README.md)
- [Historical chronicle](./2026-11-14-end-to-end-engineering-and-production-chronicle.md)
- [Conversation and evidence ledger](./2026-11-14-conversation-and-evidence-ledger.md)
- [Operations and recovery runbook](./2026-11-14-operations-and-recovery-runbook.md)
- [Creative Intelligence proposal — historical vision](./2026-11-14-creative-intelligence-and-worldbuilding-vision-proposal.md)
- [Species/Spatial/Assistant + seven requirements: PR #5](https://github.com/Reltroner/reltroner-statistics/pull/5)
- [Post-merge UI/UX commit](https://github.com/Reltroner/reltroner-statistics/commit/4f81f1a4feca47f2faff5444e5acf2d1ac6a3842)
- [Calculator CALC-01–07 commit](https://github.com/Reltroner/reltroner-statistics/commit/54708b04d8a675d065ea30a18798877d057d4982)
- [GitHub CI and deployed SHA verification #43720463014](https://github.com/Reltroner/reltroner-statistics/actions/runs/43720463014)
- [Public Calculator](https://statistics.reltroner.com/calculator/) · [Public Assistant](https://statistics.reltroner.com/assistant/) · [Version endpoint](https://statistics.reltroner.com/build-info.json)

**Archive integrity:** This addendum does not claim to be a complete verbatim conversation export and never includes Cloudflare tokens, account IDs, private session content or other credentials. The dated primary documents remain intact; later evidence is explicitly additive.
