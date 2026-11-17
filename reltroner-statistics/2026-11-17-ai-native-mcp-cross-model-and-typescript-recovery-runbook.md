# Reltroner Statistics — AI-Native MCP, Cross-Model Acceptance & IDE Recovery Runbook

> **Dated:** 2026-11-17 (Asia/Jakarta). **Authority:** [Implementation repository](https://github.com/Reltroner/reltroner-statistics). This is a historical and operational reference, not a live status monitor or permission to merge/deploy.  
> **Context:** [Complete RS-AI-API-001 → RS-AI-API-002 → RS-CREATIVE-QUALITY-003 → RS-CQ-003 chronicle](./2026-11-17-ai-native-api-cross-model-and-creative-quality-end-to-end-chronicle.md).

## 1. Identify the exact running system

At the verified checkpoint, **RS-AI-API-001** was live at Statistics main \`fc37812b6cad68cfb707fdcdd07d7a0e417825df\`. **RS-AI-API-002 (draft PR #7)** and **RS-CREATIVE-QUALITY-003 (draft PR #8)** were **not merged or deployed**. The TypeScript editor fix was performed locally.

| Service | URI | Expected use |
|---|---|---|
| Public UI | https://statistics.reltroner.com | Human-facing dashboard |
| MCP endpoint | https://statistics.reltroner.com/mcp | Remote **Streamable HTTP POST**, 13 read-only tools |
| REST | https://statistics.reltroner.com/api/v1 | Fifteen read-only retrieval/calculation operations |
| OpenAPI | https://statistics.reltroner.com/openapi.json | Machine-readable contract |
| AI context | https://statistics.reltroner.com/llms.txt | Browsing discovery; **not** MCP connection |
| Manifests | https://statistics.reltroner.com/ai/manifest.json and https://statistics.reltroner.com/ai/context.json | Source and tool discovery |
| Build SHA | https://statistics.reltroner.com/build-info.json | Statistics deployed identity |

**GET /mcp = 405 is expected.** MCP clients send JSON-RPC over POST. Do not interpret a web-browser 405 as a broken connection. The public MCP does not use OAuth, client secret, API key or arbitrary request headers. Never expose confidential information in model tool calls.

## 2. Preserve local Git work before any operation

Owner workspace: \`C:\Projects\reltroner-statistics\`. At the last supplied PowerShell output the current branch was \`feat/rs-creative-quality-003\`, HEAD \`66cf0bafa9c62b0eafcdb2c7947f67ecbde24d53\`, with one **untracked** \`.vscode/settings.json\`. No tracked application changes were reported.

**Read-only preflight in PowerShell 5.1:**

~~~powershell
$ErrorActionPreference = 'Stop'
Set-Location -LiteralPath 'C:\Projects\reltroner-statistics'
Write-Host '=== LOCAL ==='
git branch --show-current
git rev-parse HEAD
git status --short --untracked-files=all
git remote get-url origin

Write-Host '=== REMOTE MAIN ==='
git fetch origin main
if ($LASTEXITCODE -ne 0) { throw 'FETCH_FAILED' }
$remoteMain = (git rev-parse origin/main).Trim()
$remoteAdvertised = (git ls-remote origin refs/heads/main)
if ($LASTEXITCODE -ne 0) { throw 'LS_REMOTE_FAILED' }
$advertisedSha = ($remoteAdvertised -split '\s+')[0]
Write-Host ('origin/main: ' + $remoteMain)
Write-Host ('ls-remote:   ' + $advertisedSha)
if ($remoteMain -ne $advertisedSha) { throw 'MAIN_REMOTE_DRIFT' }
~~~

This checks remote-tracking identity, **not** local-main=GitHub-main or live website parity while on a feature branch. Also compare GitHub's API branch SHA and \`/build-info.json\` when required.

Only when the owner explicitly authorizes main reconciliation and all worktrees are safe:

~~~powershell
# Inspect all changes and switch safely; NEVER discard WIP.
git status --short --untracked-files=all
git switch main
if ($LASTEXITCODE -ne 0) { throw 'UNSAFE_TO_SWITCH_STOP' }
.\scripts\sync-main-ff-only.ps1 -VerifyWebsite
if ($LASTEXITCODE -ne 0) { throw 'MAIN_PARITY_GATE_FAILED_STOP' }
~~~

Do **not** run \`git reset --hard\`, \`git clean\`, force push, rewrite history, merge draft PRs, or remove untracked workspace preferences by default.

## 3. MCP connector setup, actual invocation and evidence

| Client | Setup | Native acceptance evidence |
|---|---|---|
| ChatGPT | Install custom MCP server/plugin at \`https://statistics.reltroner.com/mcp\`; no authentication. Feature availability is plan/workspace-dependent. | Actual connected tool calls in conversation |
| Claude web | Add custom connector; same URL, **No sign-in**, **no request headers**, Streamable HTTP. | “Used Reltroner Statistics” tool activity, expand input/output when available |
| Gemini **web** Developer Mode | Connect to MCP server; Client ID & Client Secret blank; select Reltroner Statistics app. | **Tool schemas 13/13**, plus **Event log** → Tool call/Tool result → Export |
| Gemini CLI (optional, separate client) | Configure \`mcpServers.reltroner-statistics.httpUrl\` to the URL above. | CLI trace and results, not equivalent to Gemini web |

**Connection ≠ tool execution.** A model's final textual self-reported tool ledger is not an authoritative event log. Raw Gemini exports can contain session/account identifiers; keep private and commit only sanitized summaries.

**Repeatable four-operation benchmark:**

~~~text
get_statistics_manifest {}
calculate_scenario {
  request: {
    operation: "projectScenario",
    entity_id: "country:reltronland",
    indicator: "population",
    annual_rate_pct: 1,
    horizon_years: 100,
    label: "RS-AI-API-002 test"
  }
}
build_research_context {
  query: "Reltronland Depcutland cooperation",
  source_policy: "production_only"
}
query_statistics { entity: "Atlantis", indicator: "population" }
~~~

At the *historic* pinned snapshot \`fc37812b…\`, the same conditional calculation was **855 billion × 1.01^100 = 2312.6158241554067 billion sentients**, \`SCENARIO\`, **not** validated empirical forecasting (\`INSUFFICIENT_DATA\`, 2 observed points vs 8 required). Atlantis returned **NOT_FOUND**, never zero or another entity. Source SHAs, digest and exact arguments must match before claiming cross-model parity.

For an independent public network probe, use the read-only test in draft PR #7:

~~~powershell
# Requires checkout containing the RS-AI-API-002 verifier, plus npm ci.
node .\scripts\verify-remote-mcp.mjs --expected-sha '<FULL_CURRENT_GITHUB_MAIN_SHA>'
if ($LASTEXITCODE -ne 0) { throw 'LIVE_PROTOCOL_FAILURE_OR_NETWORK_BLOCK' }
~~~

[Remote protocol CI #44016469520](https://github.com/Reltroner/reltroner-statistics/actions/runs/44016469520) and [PR CI #44016469521](https://github.com/Reltroner/reltroner-statistics/actions/runs/44016469521) passed at draft PR #7 head. That is provider-neutral evidence, **not** proof of any user's AI session.

## 4. Creative Intelligence G4 benchmark and scoring

Required tools in a connected client:

~~~text
get_statistics_manifest {}
build_research_context {
  query: "Reltronland Depcutland cooperation",
  source_policy: "production_only",
  max_evidence_items: 40,
  detail: "standard"
}
discover_opportunities { view: "opportunities", limit: 10 }
audit_consistency { limit: 15 }
evaluate_decision_tree {}
# Optional: search, get_entity_context, trace_evidence, analyze_narrative_impact
~~~

Ask for at most three source-grounded, differentiated hypotheses; two verified anchors and immutable GitHub citations per hypothesis where the sources permit; explicit **ASSUMED** bridges, unknown consequences, alternative development paths, falsification tests, creator decision and **HYPOTHESIS / UNRATIFIED** status. If fewer than three can be justified, return fewer.

Rubric: source/canon fidelity **25**, citations/provenance **20**, novelty **20**, causal reasoning **15**, actionability **10**, creator control **10** points. The previous **86/100** was provisionally assigned to **one** pasted response artifact, not to independent Claude and Gemini outputs.

**Important differences:** compact research used 20 evidence items and omitted 3 at its selection; standard G4 returned 40 and omitted 53. Relationship counts differed by depth/selection; Claude-pasted text said 19 verified while earlier native Gemini standard-detail export recorded 20 included. Do not claim a source contradiction or exact parity without the same arguments and returned sections. The Gemini native log recorded 14 calls (13 OK, one invalid \`trace_evidence\` child-ID argument later corrected). A duplicated pasted Claude/Gemini output and self-reported tool ledgers cannot establish independent authorship.

**Owner position:** H1 (“Two-Custodian Case”), H2 (“Unresolvable Question”), H3 (“Evidence Threshold”) are **not ratified now**. The purpose of the experiment is discovery, **not** automatic canon publication.

## 5. Creative-quality engineering results: draft PR #8 only

The upgrade in \`feat/rs-creative-quality-003\` introduces \`data.coverage\`, disclosed omitted IDs, bounded \`coverage.follow_up\`, \`trace_evidence\` child-ID resolution and \`data.exploration_candidates\`. **These are not assumed live on the earlier production SHA.**

- Across 15 deterministic same-snapshot runs: **493 → 0 undisclosed** omitted citation references, while **169** references are still legitimately not present in bounded \`evidence[]\` but are disclosed.
- \`trace_evidence\` resolution: **320/364 → 364/364**; the 44 former \`#\`/\`@\` errors were fixed **on PR #8**, not retroactively on the earlier live release.
- Structured compositional candidates: **0 → 27**, all with 2+ independent anchors; **40** candidate anchor occurrences absent from returned opportunity cards; **0** known-card restatements by deterministic proxy.
- Sparse corpus cases correctly report insufficiency and produce fewer candidates.
- No proof yet of actual hosted model prose reaching **95–100/100**.

Agent's gate report: **132/132** Node unit tests, **24/24** Python, \`astro check\` **210 files/0 errors**, pipeline and static build, \`workerd\` 15 REST/13 MCP, **416 Playwright passed/1 conditional skip**; [GitHub CI #44025753185](https://github.com/Reltroner/reltroner-statistics/actions/runs/44025753185) **SUCCESS**. PR #8 remains draft.

If performing an explicitly authorized feature-branch regression run:

~~~powershell
npm ci
npm run verify:baseline
npm run schemas:check
npm run typecheck
npm test
npm run test:py
npm run pipeline
npm run build
npm run verify:runtime
npm run test:e2e
~~~

These commands may regenerate local artifacts; **they do not publish anything**. Preserve Git WIP and inspect status afterward.

## 6. RS-CQ-003 non-invasive TypeScript IDE recovery

**Observed incident:** Antigravity IDE showed ~**1,037** diagnostics, principally \`TS1295\`, \`TS1287\`, \`TS2802\`, \`TS1378\`, and \`astro/tsconfigs/strictest\` not found. Yet PR #8 CI and CLI typecheck were green.

**Owner's read-only PowerShell checks:**

~~~powershell
Set-Location -LiteralPath 'C:\Projects\reltroner-statistics'
Test-Path '.\node_modules\astro\tsconfigs\strictest.json'
Test-Path '.\node_modules\typescript\lib\tsserver.js'
node -p "require('./package.json').type"
.\node_modules\.bin\tsc.cmd --version
.\node_modules\.bin\tsc.cmd --showConfig
npm run typecheck
git status --short --untracked-files=all
~~~

Both paths existed; package \`type\` was \`module\`; **TypeScript 6.0.3**, \`target=esnext\`, \`module=esnext\`, \`moduleResolution=bundler\`, \`verbatimModuleSyntax=true\` resolved. \`astro check\`: **210 files, 0 errors, 0 warnings, 0 hints**.

The untracked \`.vscode/settings.json\` contains only a local compiler path, visually shown as:

~~~json
{
  "typescript.tsdk": "./node_modules/typescript/lib"
}
~~~

**Editor recovery:**

1. Open actual \`src/api/mcp.ts\` (\`.ts\` tab), not only \`settings.json\` (\`.json\` tab).
2. \`Ctrl+Shift+P\` → **TypeScript: Select TypeScript Version**.
3. Choose **Use Workspace Version 6.0.3** (\`./node_modules/typescript/lib\`), rather than bundled **Jetski's Version 5.9.3**.
4. **TypeScript: Restart TS Server**; **Developer: Reload Window**.
5. Open \`src/api/mcp.ts\` and \`tsconfig.json\`, inspect the **Problems** panel.

**Observed result:** both final user screenshots display **“No problems have been detected in the workspace.”** This is editor recovery consistent with a TS language-server project resolution mismatch. An internal tsserver root-cause trace was not supplied; do not claim the precise runtime cause is formally proven. Source files were **not modified** to obtain the recovery.

**Prohibited shortcuts:** Converting valid ESM to CommonJS; disabling \`verbatimModuleSyntax\`; weakening strictness; mass \`@ts-ignore\`; editing 92 files blindly; deleting/stashing/resetting unknown WIP; force pushing; changing Cloudflare/DNS or publishing feature branches.

## 7. Final gates

| Workstream | Recorded status | Remaining authority |
|---|---|---|
| RS-AI-API-001 | Merged/live/protocol verified | Recheck live SHA on later dates |
| RS-AI-API-002 | G1 protocol PASS, native tool evidence captured, same-data results match; **G4 independent model attribution HOLD** | Owner review of PR #7 and attributable output logs |
| RS-CREATIVE-QUALITY-003 | PR #8 code/CI PASS, deterministic proxy improvements; **not deployed** | Owner approval for any merge/release; later hosted blind evaluation |
| RS-CQ-003 | **RESOLVED locally, IDE 0 Problems + CLI 0 errors** | Keep workspace-only settings safe; no application patch needed |
| H1/H2/H3 canon | **UNRATIFIED** | Human creator only |

Nothing in this runbook authorizes a write to \`Reltroner/reltroner-studio\`, \`reltroner-studio-remodeling\`, production \`statistics.reltroner.com\`, DNS or unrelated Reltroner sites.
