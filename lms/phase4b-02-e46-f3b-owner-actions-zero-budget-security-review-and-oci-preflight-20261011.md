# Reltroner LMS Phase 4B-02 — E46-F3B Owner Actions Security & Zero-Dollar Budget GUI Review; Read-Only OCI Digest Preflight

> **Record:** `LMS-P4B02-E46-F3B-GUI-20261011` | **Scope:** owner-provided screenshots + official GitHub/Docker documentation; no settings Save, no first sandbox commit, no Actions jobs/OCI layers/DB launched.
> **Current:** `F3A=PASS_VERIFIED_EMPTY_PUBLIC_LAB`; `F3B_GUI_DISCOVERY=PASS_SCREENSHOT_SCOPE`; `F3B_POLICY_HARDENING=RECOMMENDATION_NOT_APPLIED`; `F3B_OCI_DIGEST=NOT_VERIFIED`; `F3B_WORKFLOW_BOOTSTRAP=NOT_AUTHORIZED`; `F3C_MANUAL_RUN=NOT_AUTHORIZED`; `PG-R01..10=0/10`; `T02=0/86`; `D02=HOLD`.
> **Authoritative references:** [canonical README and clarity-first process](./README.md), [E46-F2 controls](./phase4b-02-e46-f2-owner-github-actions-policy-billing-evidence-and-manual-pg18-redis8-sandbox-contract-20261011.md), [verified empty repository](./phase4b-02-e46-f3a-github-empty-lab-live-acceptance-and-f3b-workorder-20261011.md), frozen infrastructure/logical contracts.
> **No inference:** browser screenshot = observed state before Save, not proof that changes were subsequently applied. PR #46 is documentation-only and remains OPEN. No LMS-BE/LMS-FE/VPS/production changes.

## 1. Owner screenshot evidence accepted

**Screenshot A** `github.com/Reltroner/lms-trust-sandbox/settings/actions`:
- `Allow all actions and reusable workflows` **SELECTED**. Security posture = broad external action execution allowed by repository policy if referenced in later workflow; this does NOT mean a workflow has run.
- `Require actions to be pinned to a full-length commit SHA` **UNCHECKED**.
- `Check, workflow run, status, artifact and log retention` **90 days**; no change saved in screenshot.

**Screenshot B** same repository Actions General page:
- `Require approval for first-time contributors` **SELECTED**; future fork PR approval policy, NOT a security gate for the planned manual-only initial workflow.
- Default workflow permissions `Read repository contents and packages permissions` **SELECTED** (not write).
- `Allow GitHub Actions to create and approve pull requests` **UNCHECKED**.
- Each visible `Save` button does not prove a click or persisted change.

**Screenshot C** `github.com/settings/billing/budgets` owner personal billing:
- Five **account budgets** displayed: `Codespaces`, `Packages`, `Actions`, `Git LFS`, `All AI Credit SKUs`.
- Each **$0 spent / $0 budget** and **Stop usage = Yes**, including specifically `Actions` (previously unverified).
- `Included usage alerts: On`.
- This is stronger than gross billed usage `$1.82` less discounts `$1.82` net-zero snapshot or Actions-specific `$0 billable` alone: a product-specific **zero-dollar stop-usage budget is observed**.
- **Do not overclaim:** this is a point-in-time GUI screenshot, not a contractual no-charge guarantee or a test of the budget stop mechanism. Per GitHub Docs, applicable exhausted stop-usage budgets can block additional metered operations and sometimes hosted runners. If this blocks an otherwise-free public-standard runner later, STOP AND DOCUMENT; **do not automatically raise/disable the $0 budget**. Actions in public standard runners remain described as free by official GitHub billing docs.

References (externally checked 2026-10-11):
- https://docs.github.com/en/billing/how-tos/set-up-budgets
- https://docs.github.com/en/billing/concepts/product-billing/github-actions
- https://docs.github.com/en/actions/how-tos/write-workflows/choose-where-workflows-run/choose-the-runner-for-a-job
- https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository

## 2. Recommended new-sandbox-only hardening (NOT YET OWNER-APPROVED/APPLIED)

Since `lms-trust-sandbox` has ZERO refs/workflows/actions runs, this is the right time to narrow policy **before a first executable workflow**, unlike the existing `LMS-BE` workflow with tagged `actions/checkout@v4` and `shivammathur/setup-php@v2`. Do **not** change existing `LMS-BE` Actions settings.

Recommended initial option for a **zero external `uses:` first workflow**:
- `Actions permissions` → **Allow Reltroner actions and reusable workflows**. This blocks GitHub-authored `actions/checkout` and other external actions; the first lab MUST contain zero external `uses:` if choosing this policy. If a maintainable test harness requires `actions/checkout`, revise to narrowly-allowlisted **Allow Reltroner, and select non-Reltroner actions**, review its exact upstream commit SHA and allowlist, then seek separately scoped approval BEFORE saving changes or uploading a workflow. **Never silently weaken policy to get CI green.**
- Enable **Require actions to be pinned to a full-length commit SHA**. Compatible with an initial workflow containing zero `uses:`; any later action must have a verified full upstream SHA. The checkbox is not a substitute for digest pinning container images, which are separate supply-chain artifacts.
- Change retention **90 → 30 days** as a proportional proposal (GitHub check/status/log data is ephemeral; durable sanitized result/evidence goes into this documentation ledger). No artifacts/cache uploaded. Owner may retain 90 days if investigation windows warrant it; there is no proven additional bill from this 90-day setting alone.
- Leave fork first-time approval, default read-only `GITHUB_TOKEN`, and create/approve-PR disabled **unchanged**. Every future workflow additionally sets `permissions: {}` or minimum read as technically necessary.

**GUI steps only AFTER owner approves these exact new-repo setting changes:**
1. Open https://github.com/Reltroner/lms-trust-sandbox/settings/actions; visually confirm page belongs to sandbox not LMS-BE.
2. Select `Allow Reltroner actions and reusable workflows` and check full-length SHA. Click the **first Save** for these controls.
3. Change retention to `30` days and click that section's own **Save**.
4. Refresh page. Verify the two security selections are persisted and 30-day retention persists; capture redacted screenshot.
5. Leave all other sections unchanged, especially GitHub Billing budgets ($0 / Stop usage Yes). Do not create a workflow, PR, commit, secret, runner, repository action or payment resource.

**This document is NOT approval to press Save.** Owners' earlier approvals were specifically creation-only, not blanket future state changes.

## 3. OCI manifests: reader-proof and supply-chain boundary

The following optional Windows PowerShell 5.1 **copy-paste candidate** performs ONLY authenticated-to-public anonymous **GET** requests for Docker Official Image manifest JSON and public bearer pull-scope tokens. It does not download layers, start Docker Desktop, use CLI/docker daemon, start CI, access production, install tools, submit owner secrets or create/edit GitHub resources. Network traffic to `auth.docker.io` and `registry-1.docker.io` is required, so it is **not** offline and must be used only if owner authorizes the network-only discovery. It prints no bearer tokens.

The source below is DESIGN-PREPARED and **NOT YET EXECUTED on owner PowerShell 5.1**. It is NOT sufficient to ratify the final workflow: actual job image command/client support and server binary versions must be checked separately. A correct digest is NOT an assertion an image is benign.

```powershell
& {
$ErrorActionPreference = "Stop"
$oldProtocol = [Net.ServicePointManager]::SecurityProtocol
try {
    [Net.ServicePointManager]::SecurityProtocol = $oldProtocol -bor [Net.SecurityProtocolType]::Tls12
    function Read-PublicRegistryManifest {
        param([string]$Name, [string]$Reference, [string]$Token)
        $url = "https://registry-1.docker.io/v2/library/$Name/manifests/$Reference"
        $request = [System.Net.HttpWebRequest]::Create($url)
        $request.Method = "GET"
        $request.Timeout = 15000
        $request.ReadWriteTimeout = 15000
        $request.Headers["Authorization"] = "Bearer $Token"
        $request.Accept = "application/vnd.oci.image.index.v1+json, application/vnd.docker.distribution.manifest.list.v2+json, application/vnd.oci.image.manifest.v1+json, application/vnd.docker.distribution.manifest.v2+json"
        $response = $request.GetResponse()
        try {
            $memory = New-Object System.IO.MemoryStream
            try {
                $response.GetResponseStream().CopyTo($memory)
                $raw = $memory.ToArray()
            } finally { $memory.Dispose() }
            $reported = [string]$response.Headers["Docker-Content-Digest"]
        } finally { $response.Dispose() }
        if ($reported -notmatch "^sha256:[0-9a-fA-F]{64}$") { throw "STOP: no valid registry SHA256 digest for $Name" }
        $sha = [System.Security.Cryptography.SHA256]::Create()
        try { $actual = ([BitConverter]::ToString($sha.ComputeHash($raw))).Replace("-","").ToLowerInvariant() }
        finally { $sha.Dispose() }
        if ($reported.ToLowerInvariant() -ne ("sha256:" + $actual)) { throw "STOP: digest mismatch for $Name" }
        $payload = ([System.Text.Encoding]::UTF8).GetString($raw) | ConvertFrom-Json
        return [pscustomobject]@{ Digest=("sha256:" + $actual); Body=$payload }
    }
    foreach ($item in @(
        @{ Name="postgres"; Tag="18" },
        @{ Name="redis"; Tag="8" },
        @{ Name="ubuntu"; Tag="24.04" }
    )) {
        $scope = [uri]::EscapeDataString("repository:library/$($item.Name):pull")
        $tokenUrl = "https://auth.docker.io/token?service=registry.docker.io&scope=$scope"
        $auth = Invoke-RestMethod -Method Get -Uri $tokenUrl -TimeoutSec 15
        if ([string]::IsNullOrWhiteSpace([string]$auth.token)) { throw "STOP: registry token unavailable" }
        $index = Read-PublicRegistryManifest -Name $item.Name -Reference $item.Tag -Token $auth.token
        if ($null -eq $index.Body.manifests) { throw "STOP: no multiarch manifest index for $($item.Name)" }
        $platformMatches = @($index.Body.manifests | Where-Object { $_.platform.os -eq "linux" -and $_.platform.architecture -eq "amd64" })
        if ($platformMatches.Count -ne 1) { throw "STOP: expected one linux/amd64 manifest for $($item.Name), got $($platformMatches.Count)" }
        $childReference = [string]$platformMatches[0].digest
        if ($childReference -notmatch "^sha256:[0-9a-fA-F]{64}$") { throw "STOP: invalid child digest" }
        $child = Read-PublicRegistryManifest -Name $item.Name -Reference $childReference -Token $auth.token
        if ($child.Digest -ne $childReference.ToLowerInvariant()) { throw "STOP: linux/amd64 child digest mismatch" }
        Write-Output ("VERIFIED_IMAGE=" + "docker.io/library/" + $item.Name + "@" + $index.Digest)
        Write-Output ("VERIFIED_PLATFORM=linux/amd64 MANIFEST=" + $child.Digest)
        Write-Output ("TAG_AT_TIME_OF_CHECK=" + $item.Name + ":" + $item.Tag + " (informational only)")
    }
    Write-Output "E46_F3B_REGISTRY_MANIFEST_PREFLIGHT=PASS_DIGEST_BYTES_AND_AMD64_DESCRIPTOR"
    Write-Output "RUNTIME_ENGINE_VERSION=NOT_TESTED"
    Write-Output "WORKFLOW_OR_CONTAINER_EXECUTION=NOT_AUTHORIZED"
} catch {
    Write-Output ("E46_F3B_REGISTRY_MANIFEST_PREFLIGHT=STOP_" + $_.Exception.GetType().Name)
    throw
} finally {
    [Net.ServicePointManager]::SecurityProtocol = $oldProtocol
}
}
```

**Expected PASS:** three paired index/image and linux/amd64 descriptor digests (`postgres:18`, `redis:8`, and candidate job base `ubuntu:24.04`), with `E46_F3B_REGISTRY_MANIFEST_PREFLIGHT=PASS_DIGEST_BYTES_AND_AMD64_DESCRIPTOR`. These are public registry metadata, not production material. Record exact index digests as candidate immutable image references only AFTER owner results; this document invents **zero** digest values. Confirm current image/software versions and job/client capability in a future owner-approved test; no release number is assumed from major tags.

**STOP if** HTTP/TLS error, non-index tag manifest, missing/ambiguous linux/amd64 descriptor, missing Docker-Content-Digest, byte-level SHA mismatch, or different mutable tag-to-index mapping after earlier review. Failed discovery never authorizes fallback to unpinned mutable tags.

## 4. F3-B proposed workflow architecture acceptance — still non-executable

- `on: workflow_dispatch` only, on a new default-branch `main` created exclusively after another owner approval. No push, PR or schedule trigger.
- `runs-on: ubuntu-24.04` standard public 4 vCPU / 16 GiB / 14 GB SSD; one job; `timeout-minutes: 10`; `permissions: {}` unless minimal checkout scopes separately approved; no deployments/environments, secrets, caches or artifacts.
- Use a **job container** and PostgreSQL/Redis **service containers** on the same GitHub job network, **NO `ports:` mapping** at all. Distinct service hostnames `postgres` and `redis`, not `localhost` and no user/VPS endpoint. No `--entrypoint` or `--network` in `container.options`, both unsupported by GitHub Actions.
- Immutable `@sha256:<observed actual registry index digest>` on job image, PostgreSQL18 image, Redis8 image; runtime major checks `server_version_num >= 180000 and < 190000`, Redis `INFO server` version major 8. Configured resources must fit ephemeral standard VM; fail closed on health/readiness.
- **Unresolved pre-run engineering blocker:** job container must have **audited clients** for BOTH PostgreSQL18 SQL sessions and Redis8 protocol commands, with reproducible package provenance. Merely picking `ubuntu:24.04` does NOT supply `psql` or `redis-cli`. Do not casually `apt install` unpinned dependencies, assume `postgres` server image runs correctly as a job container, or rely on unsupported Docker options. Prefer an explicit audited standalone harness with deterministic client source and allowed minimal egress. No runnable workflow source is approved at this point.
- First real tests only PG-R01 (SQL durable duplicate concurrency), PG-R02 (atomic two-proof reservation with conflict ROLLBACK), PG-R03 (real disposable Redis8 FLUSHDB with independent PostgreSQL replay authority). Rejected duplicate must have no protected side effects. PASS demands **actual** HTTP/SQL/Redis evidence, two independent nonce identities, zero ambiguous success, exact exit codes, runtime versions and bounded logs.
- PG-R04..10 remain separate coverage (process restart, SQL unavailable, PostgreSQL restart, standby failover, expiry/cleanup, load, owner DB grant parity). Redis-only silent nonce loss remains **UNSAFE**. T02 canonical HTTP 0/86 is independent and no lab-only SQL experiment can silently increase that counter.
- If workflow file is placed on default branch, it becomes a dispatchable executable resource. Its **initial bootstrap commit** is therefore a separately authorized state transition; and **first dispatch** is yet another gate. Merely having a branch or workflow is not permission to run.

Official technical references:
- https://docs.github.com/en/actions/tutorials/use-containerized-services/use-docker-service-containers
- https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax
- https://docs.github.com/en/actions/reference/security/secure-use
- https://distribution.github.io/distribution/spec/api/

## 5. Decision/evidence register and next operator action

| Gate | Current status | Exit |
|---|---|---|
| E46-F3A public empty repo created and live-checked | **PASS** | Owner GUI + connected GitHub verified |
| E46-F3B-A owner Actions GUI review | **PASS_SCREENSHOT_ONLY** | Screen A+B; no changed/saved settings implied |
| E46-F3B-B billing screenshot: Actions $0/Stop Yes | **PASS_SCREENSHOT_ONLY** | Screen C; budget enforcement not live-tested |
| E46-F3B-C hardening plan | **READY_FOR_OWNER_DECISION** | Owner approves specific sandbox-only GUI settings |
| E46-F3B-D OCI index/platform digest discovery | **PREPARED_NOT_EXECUTED** | Copy-paste PS5.1 script output |
| E46-F3B-E dual client / harness topology | **DESIGN_GAP** | Source and exact hash reviewed before workflow |
| E46-F3B-F first commit on default branch | **NOT AUTHORIZED** | Explicit owner authorization, new separate gate |
| E46-F3C first manual CI run | **NOT AUTHORIZED** | Explicit owner authorization after reviewed workflow |
| Real PG-R01..10 / canonical T02 | **0/10 / 0/86** | No false PASS via model/SQLite |
| D02 design owner ratification; production | **HOLD** | Evidence and separate owner gates |

**Safest next action:** owner decides sandbox-only GUI hardening scope, then runs read-only OCI metadata preflight on Windows if they permit those external GET requests. Avoid risking the active LMS backend, local RAM-constrained Docker, Keycloak and production.
