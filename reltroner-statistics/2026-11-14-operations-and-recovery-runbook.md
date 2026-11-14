# Reltroner Statistics — Production Operations, Git Synchronization and Recovery Runbook

> **Archived:** 2026-11-14 (Asia/Jakarta).  
> **Audience:** Owner/operator, release engineer, QA reviewer and future AI engineering agents.  
> **Live entrypoint:** https://statistics.reltroner.com  
> **GitHub source:** https://github.com/Reltroner/reltroner-statistics  
> **Local Windows workspace:** `C:\Projects\reltroner-statistics`  
> **Cloudflare Pages project:** `reltroner-statistics`  
> **Current verified Statistics commit at archival close:** `042aa46354b9253feb2c0d55e4c0ce1adbd3e7a6`  
> **Change control:** This document is a record and manual. It does not authorize DNS/nameserver changes, modifications to unrelated applications or destructive Git operations.

## 1. Canonical production topology

~~~text
Developer Windows workspace C:\Projects\reltroner-statistics
       | clean main; fast-forward-only synchronization
       v
Reltroner/reltroner-statistics  [GitHub main]
       | test/contract/determinism/Python/E2E gates
       v
GitHub Actions (static site + PDFs + artifacts)
       | GET-only Cloudflare project/domain preflight
       v
Cloudflare Pages project: reltroner-statistics
       | published dist/ artifact only
       +--> reltroner-statistics.pages.dev
       +--> statistics.reltroner.com  (the sole active custom hostname)
       |
       v
/build-info.json (commit SHA, digest, rules version, source identities)
~~~

The application statically reports observations of `Reltroner/reltroner-studio` and `Reltroner/reltroner-studio-remodeling` at pinned source commits. The origin website's deployed build is a *separate* claim from those repository snapshots. The Statistics Pages target is unrelated to the Hostinger VPS, existing Studio Pages project and LMS Pages project.

## 2. Protected boundary and allowed writes

| Object | Permitted | Explicitly not permitted |
| --- | --- | --- |
| Statistics repository | Reviewed source changes, tests, CI builds | Force-push or destructive overwrite merely to achieve superficial parity |
| Local Statistics checkout | Clean fast-forward from `origin/main` | `git reset --hard`, `git clean`, forced checkout, unapproved rebase, automatic stash of owner work |
| Cloudflare Pages | Upload to project `reltroner-statistics` only | Upload to `reltroner-studio-cf`, `lms-fe`, ERP Workers or other projects |
| DNS | The owner-authorized `statistics` CNAME association, already completed | Repointing apex, `www`, `lms`, `hrm`, identity/email/ERP records, wildcard routes or nameservers |
| Source content | Read-only source resolution from Studio and Remodeling | Automatically editing canon, mutating source repos, or treating drafts as deployed truth |
| Credentials | GitHub Actions encrypted repository secrets; account-scoped Pages Write token | Plaintext tokens in Markdown, source code, browser screenshots, prompts or commit logs |

**Important:** the Cloudflare token reviewed during setup had Pages Write for the whole Cloudflare account. This does not grant DNS write privileges, but it is not a Pages-project-level access restriction. Keep the token secret, minimize GitHub workflow permissions and rotate before its 2027-11-14 expiry.

## 3. Configuration baseline — GitHub and Cloudflare

At archival close, GitHub repository variables were reported as:

| Repository variable | Value |
| --- | --- |
| `CLOUDFLARE_PAGES_PROJECT` | `reltroner-statistics` |
| `SITE_URL` | `https://statistics.reltroner.com` |

Repository secret *names* (values hidden):

- `CLOUDFLARE_API_TOKEN`
- `CLOUDFLARE_ACCOUNT_ID`

GitHub environment `production` allowed only branch `main` (one branch, zero tags). No Required reviewers or wait timer were enabled in the operator's screenshot. This means branch/environment scope exists, but the archived evidence must **not** claim that human approval is forced on every deployment.

Cloudflare Pages:

- Project: `reltroner-statistics`.
- Pages hostname: `reltroner-statistics.pages.dev`.
- Authorized custom domain: `statistics.reltroner.com` only.
- Custom domain status shown in dashboard: **Active**.
- SSL shown: **enabled**.
- DNS: `CNAME statistics → reltroner-statistics.pages.dev`, **Proxied**, TTL **Auto**.
- Do not add a duplicate DNS record, re-create the project or replace existing Pages assets manually.

## 4. Safe local synchronization (Windows PowerShell 5.1)

### 4.1 Standard command

From PowerShell 5.1:

~~~powershell
Set-Location -LiteralPath 'C:\Projects\reltroner-statistics'
powershell.exe -NoProfile -ExecutionPolicy Bypass -File '.\scripts\sync-main-ff-only.ps1'
~~~

The checked-in script:

1. Requires the exact local repository path and `main`.
2. Checks that origin points to `Reltroner/reltroner-statistics`.
3. Refuses any tracked or untracked local changes.
4. Fetches `origin/main`.
5. Checks that the local HEAD is an ancestor of the fetched remote `main`.
6. Merges with `--ff-only`.
7. Confirms local HEAD equals remote HEAD and the working tree remains clean.
8. Reports `LOCAL_MAIN_1_TO_1_GITHUB: VERIFIED` only if the contract holds.

If the script itself is outdated and errors before updating, run this *only when the current tree is clean and local HEAD is an ancestor of origin/main*:

~~~powershell
Set-Location -LiteralPath 'C:\Projects\reltroner-statistics'
git status --short
git fetch --no-tags origin main
git merge-base --is-ancestor HEAD origin/main
if ($LASTEXITCODE -ne 0) { throw 'Local main is ahead or diverged. Do not reset it.' }
git merge --ff-only origin/main
if ($LASTEXITCODE -ne 0) { throw 'Git fast-forward failed.' }
powershell.exe -NoProfile -ExecutionPolicy Bypass -File '.\scripts\sync-main-ff-only.ps1'
if ($LASTEXITCODE -ne 0) { throw 'Parity verification failed.' }
~~~

**Safety precondition:** the compact fallback prints `git status --short` but does not by itself refuse a dirty tree. When operating from an unknown workspace, use the full preconditioned script below instead, or explicitly inspect and protect all local work. Never use the compact fallback to override the script's clean-worktree gate.

### 4.2 Full preconditioned recovery command

~~~powershell
& {
    $ErrorActionPreference = 'Stop'
    $Repo = 'C:\Projects\reltroner-statistics'

    Set-Location -LiteralPath $Repo

    $Root = (git rev-parse --show-toplevel).Trim()
    if ($LASTEXITCODE -ne 0 -or $Root.Replace('/', '\') -ine $Repo) {
        throw 'Incorrect Git workspace.'
    }

    $Branch = (git branch --show-current).Trim()
    if ($LASTEXITCODE -ne 0 -or $Branch -ne 'main') {
        throw 'Only local main is permitted.'
    }

    $Origin = (git remote get-url origin).Trim()
    if ($LASTEXITCODE -ne 0 -or $Origin -cnotmatch '^(https://github\.com/Reltroner/reltroner-statistics(\.git)?|git@github\.com:Reltroner/reltroner-statistics(\.git)?)$') {
        throw 'Unexpected Git origin.'
    }

    $Changes = @(git status --porcelain=v1 --untracked-files=all)
    if ($LASTEXITCODE -ne 0 -or ($Changes -join '').Trim().Length -gt 0) {
        throw 'Uncommitted local work exists. No files were modified.'
    }

    git fetch --no-tags origin main
    if ($LASTEXITCODE -ne 0) { throw 'Fetch failed.' }

    git merge-base --is-ancestor HEAD origin/main
    if ($LASTEXITCODE -ne 0) {
        throw 'Local main is ahead or diverged; refusing destructive sync.'
    }

    git merge --ff-only origin/main
    if ($LASTEXITCODE -ne 0) { throw 'Fast-forward failed.' }

    powershell.exe -NoProfile -ExecutionPolicy Bypass -File '.\scripts\sync-main-ff-only.ps1'
    if ($LASTEXITCODE -ne 0) { throw 'Patched verification failed.' }
}
~~~

Avoid redirecting Git native stderr with `2>&1` inside a helper that also uses `$ErrorActionPreference = 'Stop'` under Windows PowerShell 5.1; normal Git progress can be misclassified as a terminating error.

### 4.3 Verify the live domain at the same time

~~~powershell
Set-Location -LiteralPath 'C:\Projects\reltroner-statistics'
powershell.exe -NoProfile -ExecutionPolicy Bypass -File '.\scripts\sync-main-ff-only.ps1' -VerifyWebsite
~~~

Observed passing result for the archived commit:

~~~text
LOCAL_MAIN_1_TO_1_GITHUB: VERIFIED (042aa46354b9253feb2c0d55e4c0ce1adbd3e7a6)
STATISTICS_PUBLIC_SHA_PARITY: VERIFIED (042aa46354b9253feb2c0d55e4c0ce1adbd3e7a6)
~~~

The website check reads the live `/build-info.json`. It fails on SHA mismatch or missing digest/source identity. The CI release verifier is more rigorous: it compares exact local build and live fields `statistics_commit`, `semantic_digest`, `rules_version` and `sources`.

**Expected transient case:** immediately after a new GitHub commit is pushed, `-VerifyWebsite` may fail until CI publishes it. That is version drift during release propagation, not justification to reset Git or edit DNS.

## 5. Reproduce a Statistics build in the repository

The checked-in `package.json` and workflows define the executable commands; do not substitute guessed build steps.

~~~powershell
Set-Location -LiteralPath 'C:\Projects\reltroner-statistics'
npm ci
npm test
npm run schemas:check
npm run verify:baseline
npm run test:py
npm run pipeline
npm run typecheck
npm run build
npm run test:e2e
~~~

Notes:

- Python analytics depends on a Python environment and locked requirements; the README documents `python -m venv .venv` and a hash-verified install from `analytics/python/requirements.lock`.
- CI runs tests on Ubuntu and Windows, including a separate PowerShell 5.1 native stderr regression on Windows.
- The pipeline fetches the latest Studio and Remodeling `main` SHAs and pins them for analysis; source snapshot identity can change even when the Statistics source commit is stable.
- Building static HTML and PDFs requires Chromium/Playwright tooling. Published `dist/` is derived output; it is not the Git source root.
- If any check fails, do not bypass it by weakening provenance or inventing data.

## 6. Release process — manual maintenance or recovery

Open [Analysis release workflow](https://github.com/Reltroner/reltroner-statistics/actions/workflows/release.yml).

1. Select **Run workflow**.
2. Use `Branch: main`.
3. Leave `production_sha` and `remodeling_sha` blank for latest-source resolution; provide pinned source commits only when the release specifically requires a reproducible older snapshot.
4. Select `publish_statistics=true`.
5. Run and inspect three jobs.

| Expected job | Target result |
| --- | --- |
| Build and verify release candidate | Success |
| Publish to Cloudflare Pages | Success |
| Publication held — explicit authorization required | Skipped |

The publish job downloads its matching release artifact, requires Cloudflare secrets, verifies account/project/custom-domain identity using **GET only**, refuses stale GitHub commits, deploys `dist/` through Wrangler to `reltroner-statistics`, and verifies the live `build-info.json`.

If the release builds but the publish job is **skipped**, check the manual trigger input, `main` branch, repository variables, custom-domain guard and `production` environment. If the publish job **fails**, inspect its specific step and Cloudflare account permissions before changing anything else.

Successful historical manual runs:

- [#43574215880 — Pages bootstrap URL](https://github.com/Reltroner/reltroner-statistics/actions/runs/43574215880).
- [#43587678915 — final custom domain](https://github.com/Reltroner/reltroner-statistics/actions/runs/43587678915).

These runs deployed Statistics commit `042aa46354b9253feb2c0d55e4c0ce1adbd3e7a6`.

## 7. Release process — automatically after eligible main pushes

The checked-in [CI workflow](https://github.com/Reltroner/reltroner-statistics/blob/main/.github/workflows/ci.yml) contains a separate job `publish_statistics`. Its eligibility is intentionally strict:

- Trigger: a new `push` on `main` (not a PR).
- Repository variable project must be exactly `reltroner-statistics`.
- Repository variable `SITE_URL` must be exactly `https://statistics.reltroner.com`.
- All prerequisite Ubuntu/Windows determinism and Python jobs, site pipeline, typecheck, PDF/static build, Playwright/E2E and artifact upload must pass.
- The job downloads the artifact named with the exact current `github.sha`.
- A freshness check rejects a commit that has been superseded by a newer `main` commit.
- The same Cloudflare target/custom-domain guard and live build verifier apply.
- The job is serialized in a Statistics production concurrency group.

**Archival status:** this mechanism is implemented and has passed CI workflow syntax/regression acceptance. A *new-commit automatic publication lifecycle* had **not been directly exercised** in the conversation. Its future success cannot be inferred solely from the manual release jobs.

To complete a future RC-DEPLOY-04 proof, choose a legitimate reviewed Statistics source change, push/merge to `main`, observe the actual `publish_statistics` job, compare live SHA, and check protected sibling sites. Do not create a meaningless commit only to generate a green badge without appropriate owner intent.

## 8. Cloudflare Pages GUI reconstruction (already completed in 2026-11-14 session)

This historical procedure is retained for disaster recovery; it is **not an instruction to create a second project**.

### Phase A — Create the Pages project

1. Cloudflare → **Workers & Pages** → **Create application**.
2. Use **Continue to Pages** / legacy Pages flow if shown.
3. Select **Upload assets / Direct Upload**, not a competing Git-connected deployment.
4. Name the project exactly `reltroner-statistics`; Cloudflare offers `reltroner-statistics.pages.dev`.
5. Upload only a minimal bootstrap `index.html` (ZIP or folder), not `C:\Projects\reltroner-statistics`.
6. Deploy the bootstrap and enter the dedicated project's overview.
7. Run the GitHub release workflow to replace bootstrap content with tested real `dist/` output.

### Phase B — Create credential for GitHub Actions

1. Cloudflare account → **API Tokens → Create a token → Start from scratch**.
2. Name it `reltroner-statistics-github-actions`.
3. In **Developer Platform**, select **Pages → Write/Edit** only.
4. Review the effective access scope. The original configuration used the entire relevant Cloudflare account; this is an account-level power, not a project-only role.
5. The original setup selected one-year expiration (until 2027-11-14) and did not restrict runner IPs.
6. Store the generated value in GitHub repository secret `CLOUDFLARE_API_TOKEN` and the separate Cloudflare Account ID in `CLOUDFLARE_ACCOUNT_ID`.
7. Do not copy raw values into public docs, Slack, commits or AI chats.

### Phase C — Set variables and production restrictions

1. GitHub repository → **Settings → Secrets and variables → Actions → Variables**.
2. Set `CLOUDFLARE_PAGES_PROJECT=reltroner-statistics`.
3. For first bootstrap, set `SITE_URL=https://reltroner-statistics.pages.dev`.
4. GitHub repository → **Settings → Environments** → create `production`.
5. Under selected deployment branches/tags, allow `main` only.
6. Manually run the Analysis release with `publish_statistics=true`; confirm real build and live bootstrap Pages URL.

### Phase D — Attach only the custom domain

1. Cloudflare Workers & Pages → `reltroner-statistics` → **Custom domains → Set up a custom domain**.
2. Enter `statistics.reltroner.com`.
3. Confirm the change concerns only this subdomain and does not collide with an existing record/Worker route.
4. Inspect the proposed CNAME: name `statistics`, target `reltroner-statistics.pages.dev`.
5. For the owner-provided screenshot the result was `CNAME`, **Proxied**, TTL **Auto**.
6. Confirm Pages shows **Active** and **SSL enabled**, then verify public HTTPS independently.
7. Change GitHub `SITE_URL` from `pages.dev` to `https://statistics.reltroner.com`.
8. Manually release once more with `publish_statistics=true`. The new guard now requires the **sole active** custom domain.
9. Check `/build-info.json` and PowerShell `-VerifyWebsite`.

The sequence avoids creating DNS records in advance, attaching the hostname to a wrong Pages project, or changing the zone's nameservers.

## 9. Expected public smoke tests

| Request | Expected property |
| --- | --- |
| `https://statistics.reltroner.com/` | HTTPS homepage, no temporary bootstrap placeholder |
| `https://statistics.reltroner.com/statistics/decision-trees` | Statistical Decision Tree screen and truthful sufficiency/model status |
| `https://statistics.reltroner.com/creative/decisions` | Creator-controlled explainable decision trees |
| `https://statistics.reltroner.com/creative/audit` | Evidence-backed narrative audit and provenance |
| `https://statistics.reltroner.com/reports` | Report Center and available export formats |
| `https://statistics.reltroner.com/build-info.json` | Valid JSON with `statistics_commit`, `semantic_digest`, `rules_version` and source identities |

Public HTTPS is not proof of the deployed Studio source identity. Confirm the final hostname's commit and digest rather than guessing that an existing artifact or a GitHub green tick guarantees publication.

### Read-only PowerShell inspection

~~~powershell
& {
    $ErrorActionPreference = 'Stop'
    $Url = 'https://statistics.reltroner.com/build-info.json'
    $Info = Invoke-RestMethod -Uri $Url -Method Get -TimeoutSec 20 -Headers @{
        'Cache-Control' = 'no-cache'
    }
    $Info | ConvertTo-Json -Depth 20
}
~~~

For authoritative parity against local and GitHub, use the checked-in `-VerifyWebsite` command instead of eyeballing a shortened commit hash.

## 10. Known incidents and deterministic response

### 10.1 `NativeCommandError` after a successful Git fetch

**Signature:** PowerShell 5.1 shows normal `From https://github.com/...` as a terminating native stderr exception in the old script. **Cause:** `git @Arguments 2>&1` under `$ErrorActionPreference='Stop'`. **Fix:** use the patched script introduced by [PR #3](https://github.com/Reltroner/reltroner-statistics/pull/3), verify actual native exit code, and do not rewrite local history. The owner subsequently confirmed a successful same-SHA sync.

### 10.2 No Pages project / wrong project

**Signature:** Cloudflare preflight fails `ISOLATION_BLOCKED` or Pages project not found. **Action:** confirm the separate project `reltroner-statistics` exists in the expected Cloudflare account, that its Pages hostname matches, and GitHub variables reference the same project. Do not point the release at Studio/LMS to bypass the guard.

### 10.3 Custom domain pending / unverified

**Signature:** Pages domain not Active, SSL pending, or domain inventory unexpected. **Action:** inspect the Stats-only Pages custom domain and its CNAME; do not bypass domain checks, edit unrelated records or change nameservers. Once active, retry the *current* main manual release.

### 10.4 CI build green but deployment skipped

**Signature:** scheduled source analysis or PR validation uploads artifacts but does not run Pages publishing. **Interpretation:** expected if not manually authorized for the release workflow, or if CI's push-only production job eligibility is not met. Inspect event type, input flag, source branch, exact vars and production environment.

### 10.5 `STALE_RELEASE_BLOCKED` or `STALE_DEPLOY_BLOCKED`

**Signature:** another commit advanced GitHub `main` after the candidate started. **Action:** do not deploy an obsolete artifact. Run a fresh release on current `main`. No forced Git ref changes required.

### 10.6 `STATISTICS_DEPLOYMENT_UNVERIFIED` / site SHA drift

**Signature:** network, TLS or `build-info.json` mismatch, or missing source/digest keys. **Action:** compare the current `main` commit and most recent successful Pages publish run. Verify the domain project association and release credentials. Remember that a just-pushed commit can briefly precede the production update. Do not reset local work or change DNS to hide an actual publication failure.

### 10.7 Pages token expiry or overbroad credential concern

**Action:** generate a replacement limited to necessary Pages permissions, update GitHub secret, validate in a safe authorized release, then revoke the old token. Do not request raw token material in conversation and do not grant DNS/Workers Edit merely to fix a Pages upload issue.

### 10.8 Visual regression or large graph payload

**Action:** run the 4-viewport × 2-theme visual suite and review the screenshot artifact. Specific historical issue: duplicate Creative Intelligence navigation, fixed in RC-DEPLOY-01. Large Creative HTML output remains a performance follow-up; do not imply all performance budgets have been proved just because CI passed.

## 11. Rollback and recovery

Cloudflare Pages keeps deployment history for a project. If a Statistics-only production release is defective:

1. Identify the bad Statistics SHA, run ID, Pages deployment ID and predecessor that was known good.
2. Confirm the issue truly affects `reltroner-statistics`, not Studio, LMS, HRM or another origin.
3. Use the **Statistics project's own** Cloudflare deployment-history rollback/restore controls, with operator authorization and evidence capture.
4. Verify the restored site and its `build-info.json`; note that an intentional rollback will no longer match a newer GitHub `main` until reconciled through a new approved release.
5. Investigate and correct the current code on `main` through a normal reviewed PR or revert; do not silently force a GitHub branch backward or alter unrelated DNS.
6. Record incident, cause, impacted routes, exact source/build SHAs, run IDs, and remediation.

A Pages rollback changes the deployed content. It does not automatically change the GitHub commit or the local checkout; a temporary three-way parity mismatch after rollback is expected and must be reported truthfully.

## 12. Evidence preservation and operating cadence

Recommended checks around each material release:

1. Record the GitHub `main` SHA and CI run link.
2. Capture source production/remodeling pinned SHAs, rules version and semantic digest.
3. Record Pages target project/hostname, deployment ID and screenshot of Active/SSL status when domain settings change.
4. Execute and archive clean local/GitHub parity, publish success, and final live SHA parity.
5. Smoke-test representative routes, browser accessibility, security headers, graphs and exports.
6. Preserve visual evidence outside expiring short-retention CI artifacts if the owner needs a durable audit.
7. Recheck that sibling sites and DNS remain unaffected.
8. Record exceptions, skipped tests, pending reviewer decisions and incident repairs rather than reporting blanket success.

**GitHub artifact retention in the archived workflows:** screenshot evidence generally 14 days; release artifact 90 days; failure-only Playwright report 7 days. Those periods are workflow configuration snapshots and can be changed in later commits.

## 13. Evidence and authoritative references

- [End-to-end engineering chronicle](./2026-11-14-end-to-end-engineering-and-production-chronicle.md)
- [Conversation and evidence ledger](./2026-11-14-conversation-and-evidence-ledger.md)
- [RC-DEPLOY-01 source contract](https://github.com/Reltroner/reltroner-statistics/blob/main/docs/RC-DEPLOY-01.md)
- [RC-DEPLOY-02 source contract](https://github.com/Reltroner/reltroner-statistics/blob/main/docs/RC-DEPLOY-02.md)
- [Manual release #43587678915](https://github.com/Reltroner/reltroner-statistics/actions/runs/43587678915)
- [Final GitHub CI #43551304766](https://github.com/Reltroner/reltroner-statistics/actions/runs/43551304766)
- [Implementation README](https://github.com/Reltroner/reltroner-statistics/blob/main/README.md)

**Archival rule:** if a later build, host, account setting or source commit differs from this historical record, use the latest verified live evidence for operation and preserve this document as the dated historical trace. Do not retroactively rewrite a past success/failure without an explicit correction note.
