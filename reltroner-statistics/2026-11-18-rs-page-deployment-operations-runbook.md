# Reltroner Statistics — PAGE-004 + DEPLOY-SHA-005 Production Operations Runbook

> **Evidence checkpoint:** 2026-11-18 (Asia/Jakarta).  
> **Applies to:** Statistics implementation main `ed3abce95fd5c6f4371bd5e957ff7aa4d680909c` and later releases, subject to contract changes.  
> **Audience:** owner, release reviewer and authorized operator.  
> **Rule:** checks are **read-only by default**. This document is not authorization to merge, publish, change Cloudflare settings, overwrite worktrees or ratify Asthortera canon. **Current hard owner policy:** [only one local Statistics checkout; no new worktrees](./2026-11-18-permanent-single-checkout-no-worktree-policy.md), superseding historical recommendations below.

## 1. Distinguish five identities before debugging

| Identity | Evidence / purpose |
| --- | --- |
| Local working branch and HEAD | `git branch --show-current` and `git rev-parse HEAD`; may be a feature branch and contain WIP |
| Local `refs/heads/main` | local main branch *ref*, distinct from active checkout |
| Remote GitHub `refs/heads/main` | `git ls-remote origin refs/heads/main` plus GitHub API; can advance independently |
| Statistics published application | `https://statistics.reltroner.com/build-info.json` and `/api/v1/manifest`, with `statistics_commit`, both source SHAs and digest |
| Source-site deployment | `studio_deployment_status`, which can remain `DEPLOYMENT_UNVERIFIED` even when Statistics has correctly deployed |

A passing `LOCAL_MAIN_1_TO_1_GITHUB` check does not establish website parity; a green PR CI does not establish main publication. Treat each release as a pinned snapshot, not a general live-state assertion.

### Safe PowerShell 5.1 diagnostic preflight (does not modify refs)

~~~powershell
$ErrorActionPreference = 'Stop'
Set-Location -LiteralPath 'C:\Projects\reltroner-statistics'
git --no-optional-locks branch --show-current
git --no-optional-locks rev-parse HEAD
git --no-optional-locks rev-parse refs/heads/main
git --no-optional-locks status --short --untracked-files=all
git remote get-url origin
git ls-remote --exit-code origin refs/heads/main
if ($LASTEXITCODE -ne 0) { throw 'REMOTE_MAIN_UNAVAILABLE' }
~~~

**Important:** this command intentionally does **not** fetch, merge, reset, stash or switch. Never run a destructive clean/reset in the owner's original workspace, particularly when `.vscode/settings.json` or `public/reltroner-statistics-logo.webp` is staged/untracked. The November 18 SHA-005 agent used a separate sibling worktree and verified both owner's files by SHA-256 against external backups. Preserve the original working tree when later editing release tooling.

**CURRENT HARD OWNER RULE (2026-11-18):** Secondary local Statistics worktrees and clones are prohibited. Use only `C:\Projects\reltroner-statistics`, with clean in-place Git branches, pinned GitHub/main identity, and strict protected-file hash/index checks. If in-place work risks owner WIP, STOP; do not create an isolated worktree. See the [permanent single-checkout policy](./2026-11-18-permanent-single-checkout-no-worktree-policy.md). Do not force-push `main` or silently "repair" local refs.

## 2. Inspect live read-only service identity

The following are ordinary HTTP read-only requests; success depends on network/client availability:

~~~powershell
$Base = 'https://statistics.reltroner.com'
$Urls = @(
  "$Base/build-info.json",
  "$Base/llms.txt",
  "$Base/ai/manifest.json",
  "$Base/ai/context.json",
  "$Base/openapi.json",
  "$Base/ai/pages/index.json",
  "$Base/ai/pages/statistics/spatial.json",
  "$Base/ai/pages/statistics/spatial.md"
)
foreach ($url in $Urls) {
  try {
    $r = Invoke-WebRequest -UseBasicParsing -Method Get -Uri $url -TimeoutSec 20
    Write-Host ($r.StatusCode.ToString() + ' ' + $url)
  } catch {
    Write-Warning ($url + ' — ' + $_.Exception.Message)
  }
}
~~~

Inspect the **body** of `build-info.json` rather than just its HTTP 200. The same-build registry, mirror and API manifest must agree with that identity. A local analysis `semantic_digest` matches its pinned source inputs; it does not prove Studio's live deployment.

For the recorded successful 2026-11-18 run, exact identity was:

~~~text
statistics_commit     ed3abce95fd5c6f4371bd5e957ff7aa4d680909c
production_source_sha ad895e6d9184f09281a7cc14ccd7867c47acd29e
remodeling_source_sha 33ea8fa5472a723d640f1adbea35f686a65b3e27
semantic_digest       4119d30b2c2d7ea14b95fe08c2d53365de966acaeb343a2a772e26d42a28e08d
rules_version         P0R-2.0.0
~~~

These exact values are **historical acceptance evidence**; do not hardcode them into a generic current-main verification script.

## 3. PAGE-004 client access paths

**Browser-only:** offer the human page `https://statistics.reltroner.com/statistics/spatial/` and, if the browser cannot render/extract it, the public semantic mirror `https://statistics.reltroner.com/ai/pages/statistics/spatial.md` or `.json`. Browser failure remains a browser failure, even if MCP works in another chat.

**REST capable:** call `GET /api/v1/pages/resolve?url=<URL>`, then `GET /api/v1/pages/context?path=/statistics/spatial/`, then `GET /api/v1/pages/section?path=/statistics/spatial/&section=data-spatial-home-habitat` as needed. Encode parameters correctly; inspect `result_status` and source status, not just HTTP 200.

**MCP connected:** configure the owner's client to `https://statistics.reltroner.com/mcp` using the client-supported stateless Streamable HTTP mechanism; do not fabricate OAuth credentials for a public no-login server. Confirm the client displays **16 read-only tools**. Then use `resolve_statistics_page`, `read_statistics_page` and `read_statistics_section`. Provider connection success does not prove the client will choose the tool for every URL.

Example request, explicitly grounded and unratified:

> Resolve `https://statistics.reltroner.com/statistics/spatial/` using the connected Reltroner Statistics tools, read the page and the two spatial sections, then evaluate AI-assisted local housing and hardware production as a **HYPOTHESIS**. Separate production canon, remodeling proposals, computed scenario results and unknown values. Cite original source identities and state uncertainty.

### Page-specific acceptance checks

- URL resolves exactly to `/statistics/spatial/`; an unknown `/statistics/spatial-3d/` must not be substituted.
- Spatial surface-footprint denominator = national terrestrial land; resident habitat denominator = unique usual residents; both are `PROPOSED`. Do not invent a 3D volume or capacity.
- `source_policy=production_only` withholds remodeling table rows, without changing their source role.
- `include_sections` omitted behaves like `true`, while `false` excludes inlined content, with REST/MCP parity.
- Output identifies snapshot SHA/digest and `coverage.status`, including `PARTIAL` limitations where applicable.
- Provider-native G8 requires **actual client tool telemetry** (ChatGPT activity, Claude tool cards or Gemini Developer Mode), not a model's self-reported ledger.

## 4. Automated release-gate order

[Main CI](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/.github/workflows/ci.yml) on a verified main push:

1. Determinism (Ubuntu + Windows), analytics (Ubuntu + Windows), pipeline/site build, workerd and E2E; publish depends on passing predecessors.
2. Reject stale main; verify required Cloudflare credentials and the exact Statistics-only Pages project and active custom domain via GET-only guard.
3. Upload build artifact with Wrangler. Capture **exactly one** unique deployment URL from *this invocation's* Wrangler output; never use a manually guessed project alias as proof.
4. Check the artifact's own `build-info.json` on the unique URL, validate the expected commit/digest/rules/sources.
5. Poll canonical custom domain with bounded retries until it returns two consecutive matching identities five seconds apart, and verify GitHub main remains the expected SHA.
6. Only after `STATISTICS_DEPLOYMENT_VERIFIED`, run the live `page-aware-v1` strict 16-tool REST/MCP acceptance.

The independent [explicit release workflow](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/.github/workflows/release.yml) requires an owner-authorized dispatch and its configured production gate. It applies the same validation sequence; this archive does not instruct bypassing approvals.

### Commands for an already-built, exact-SHA checkout

These are **not** valid from an arbitrary dirty or feature-branch workspace with an unrelated `dist` artifact:

~~~powershell
# Run only where dist/build-info.json was generated for the expected SHA.
$ExpectedSha = '<40-character main commit SHA>'
$DeployUrl   = 'https://<8-lowercase-hex>.reltroner-statistics.pages.dev'
node scripts/verify-deployment.ts https://statistics.reltroner.com --expected-sha $ExpectedSha --deployment-url $DeployUrl --require-current-main
if ($LASTEXITCODE -ne 0) { throw 'DEPLOYMENT_NOT_VERIFIED' }
node scripts/verify-remote-mcp.mjs --expected-sha $ExpectedSha --profile page-aware-v1
if ($LASTEXITCODE -ne 0) { throw 'LIVE_PAGE_AWARE_PROTOCOL_FAILED' }
~~~

When executing inside GitHub CI, use the validated deployment URL from the capture step's environment, and the workflow's exact `github.sha`. Don't interpolate an untrusted URL into a shell command. The verifier's one-argument legacy mode remains supported but does not provide the full unique-artifact + current-main release evidence.

## 5. Failure triage — always fail closed

| Failure / state | Interpretation and safe action |
| --- | --- |
| `DEPLOYMENT_URL_UNAVAILABLE` | Wrangler log did not yield exactly one valid unique URL; inspect the current job log and capture parser, not another release's URL |
| `EXPECTED_IDENTITY_INVALID` | expected artifact or commit incomplete/malformed; rebuild or select the correct verified artifact; never bypass digest checks |
| `DEPLOYMENT_ARTIFACT_MISMATCH` | unique immutable URL serves a different identity; investigate wrong artifact, project or captured URL |
| `PROPAGATING` | well-formed prior release temporarily returned at canonical domain; retry occurs automatically **only within bounds** |
| `TIMED_OUT` / `UNREACHABLE` | convergence not demonstrated within deadline; inspect last observed commit, cache headers and Cloudflare deployment status read-only; do not mark green |
| `MALFORMED` / `REDIRECT_REFUSED` | unexpected format or routing; investigate without following a redirected host |
| `STALE_DEPLOY_BLOCKED` / `MAIN_REF_UNRESOLVED` | main moved or couldn't be verified; refer to newest main run, not an old deployment as current |
| API `API_DISABLED` (503), `RATE_LIMITED` (429) | explicit kill switch or configured limiter; do not disable controls to force tests green |
| `PAGE_NOT_FOUND` / `UNKNOWN_SECTION` | no exact registry entry; never substitute similar route/section |
| `SOURCE_POLICY` withholding | proposal data intentionally withheld by production-only request; not equivalent to zero |
| 16-tool protocol verifier failure after publication | inspect tool schema, readonly hints, SDK defaults, three new page calls, REST/MCP parity and refusal cases separately; no assertion suppression |

A green build or successful upload is not permission to purge caches or reroute. Cache purges, rollbacks, re-runs, workflow dispatches and manual Cloudflare changes require owner authorization.

## 6. Full non-regression suite for a source change

Use these commands only in the owner's **single authorized checkout** `C:\Projects\reltroner-statistics`, with a safe Git branch and correct dependencies; no second clone/worktree is permitted by the [2026-11-18 permanent owner policy](./2026-11-18-permanent-single-checkout-no-worktree-policy.md):

~~~powershell
node --version
npm --version
npm ci
npm run verify:baseline
npm run schemas:check
npm run typecheck
npm test
node --test tests/protocol/mcp-contract-profile.test.mjs
npm run test:py
npm run pipeline
npm run build
npm run verify:runtime
npm run test:e2e
~~~

Check exit code after **each command**; don't count an unrun gate as pass. Compare with pinned source/digest and deliberate build timestamps, not raw HTML bytes alone. For verifier-only changes, ensure JS/CSS browser assets remain byte-identical; confirm exact 18 REST / 16 MCP / 3 page operations, source roles, static mirror coverage, no write tools and negative security tests. Preserve `RS_API_DISABLED`, rate limiting, origin guards and custom domain isolation.

## 7. Operational boundaries and recordkeeping

- **No autonomous canon ratification.** H1, H2 and H3 remain HYPOTHESIS / UNRATIFIED. `PROPOSED` spatial data must not be presented as production canon.
- **Static mirror kill switch caveat.** `RS_API_DISABLED` blocks REST/MCP only, not publicly served `/ai/pages/*`. Removing public mirrors requires a new build; emergency deny rules require explicit owner authorization.
- **No unattended local ref alteration or extra worktrees.** Preserve WIP, index, ignored/untracked files and protected assets. The single-checkout policy **forbids** creating/using sibling Statistics worktrees; use a safe in-place Git branch or STOP if local owner changes cannot be preserved.
- **No secrets in logs or docs.** Use names of GitHub encrypted secrets, never values, access tokens or credential-helper stderr.
- **No fabricated runtime status.** A dated PR report marked PENDING may be superseded by a later verified main-push; link both, and explicitly timestamp the update rather than silently rewriting historical evidence.

### Canonical reference set

[PAGE architecture](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-AI-PAGE-004-ARCHITECTURE.md) · [PAGE contracts](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-AI-PAGE-004-CONTRACTS.md) · [PAGE security + seven G8 scenarios](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-AI-PAGE-004-SECURITY-AND-OPERATIONS.md) · [SHA-005 architecture](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-DEPLOY-SHA-005-ARCHITECTURE.md) · [SHA-005 incident](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-DEPLOY-SHA-005-INCIDENT.md) · [Main-push production acceptance](https://github.com/Reltroner/reltroner-statistics/actions/runs/44254064537).

**Archive companions:** [PAGE-004 full chronicle](./2026-11-18-rs-ai-page-004-universal-page-aware-intelligence-architecture.md) · [DEPLOY-SHA-005 full chronicle](./2026-11-18-rs-deploy-sha-005-deployment-sha-parity-debugging.md) · [acceptance ledger](./2026-11-18-page-aware-and-deployment-acceptance-ledger.md).
