# Reltroner LMS Phase 4B-02 — E46-F3B-R5A First Main Commit Accepted; Separate First-Run Owner Decision

> **Record:** `LMS-P4B02-E46-F3B-R5A-FIRST-BOOTSTRAP-20261011`
> **Current status:** `FIRST_BOOTSTRAP=PASS_VERIFIED` | `WORKFLOW_RUN_COUNT=0` | `R5A_FIRST_MANUAL_RUN=HOLD_PENDING_SEPARATE_OWNER_DECISION` | `R5B=LOCKED` | `REAL_PG-R01..10=0/10` | `T02_HTTP=0/86` | `D02_OWNER_TRUST_DESIGN=HOLD`.
> **Authority:** [Canonical README](./README.md), [frozen placement contract](./master-infrastructure-placement-contract.md), [frozen logical service/API contract](./logical-service-boundary-api-contract.md), [R5 staged design/proof](./phase4b-02-e46-f3b-r5-isolated-readonly-diagnostic-and-withheld-destructive-workorder-20261011.md). This is a verifiable operational receipt, not a frozen contract amendment.
> **Change control:** user explicitly requested final review and authorization of **first commit containing only R5-A diagnostic**, with NO CI run; a new and independent YES/NO decision is required to start a runner.

## 1. Source review provenance and scoped pre-commit remediation

Original owner Windows `R5_ZIP_INTEGRITY=PASS` was based on exact R5 ZIP SHA-256 `91b8cd9bd7750a81ab1489362741c3e27ec6aca0ee0fb5e37e0d303909818125`. Assistant revalidated the mounted ZIP and its internal SHA256SUMS. Original archived R5-A candidate YAML sha256 `3d61fb43f5b9f4c3f6c1b759ccdbb682b731459568b711c653e4327adcd7a25e`.

The **final bootstrapped YAML differs intentionally** from R5 ZIP source by only two assertion improvements:
- PostgreSQL query also reads `transaction_read_only` and requires both `default_transaction_read_only=on` and `transaction_read_only=on` in the same read-only SELECT session.
- Redis version parsing requires the complete numeric `8.major.patch` format (`^8\.[0-9]+\.[0-9]+$`), rejecting suffixes/malformed versions.

**Final exact YAML UTF-8 SHA256:** `1e318115f31d15fc5feb7d0af0cb18c704a62c1e8d94f030809dbb1b2e4e10a4`. Final Bash source SHA256 `db5ac3390f9262d726d68ca772722399980104c781e6498706aaf1d034d84f7f`. Static `bash -n` PASS; PyYAML BaseLoader read the single manual trigger, single job, zero external actions, zero host `ports:`, explicit `permissions: {}`, `ubuntu-24.04`, `timeout-minutes: 10`; standalone Bash equals YAML step body. Local synthetic RESP endpoint tests **4/4 PASS**: Redis8/empty accepted, Redis7/empty rejected, Redis8/nonempty rejected, Redis8/malformed version rejected. Mock endpoint `127.0.0.1` only, no production, not Redis runtime acceptance. ShellCheck/actionlint NOT RUN, real image binaries/runtime NOT VERIFIED.

Security model: job container = digest-pinned PostgreSQL18 client environment, PostgreSQL18 disposable service, Redis8 disposable service on internal job Docker network; job/service container IDs/network equality from GitHub job contexts; no external `uses`, package install, uploaded artifact/cache, self-hosted runner, host-mapped DB ports, checkout, prod secret, production endpoint, DNS mutation, SSH or privileged deploy. Only SQL SELECT and Redis PING/INFO/DBSIZE; PostgreSQL service may initialize internal disposable files, so "read only" describes diagnostic-issued business commands, NOT zero container bootstrap filesystem writes.

## 2. First sandbox GitHub commit — completed and independently verified

- Repository: https://github.com/Reltroner/lms-trust-sandbox (PUBLIC, owner Reltroner).
- Branch: `main`, **one branch ref**; first commit `3f8f923bf444f18b7ed5eed8ab738345f9b1a728`, **zero parents**, no preexisting baseline.
- Commit message: `ci(lms-trust-sandbox): bootstrap manual-only read-only PG18 Redis8 diagnostic (NO RUN)`.
- **Exactly one leaf file** in Git tree: `.github/workflows/e46-f3b-r5a-diagnostic.yml`. No README, R5-B, other workflow, secret or deployment file.
- GitHub file blob SHA (Git object SHA1): `d2f616c72e7c225431b54b2fa51d0e5b7b4139b8`.
- GitHub file content fetched **after** commit and SHA256 recomputed independently from its bytes: `1e318115f31d15fc5feb7d0af0cb18c704a62c1e8d94f030809dbb1b2e4e10a4`, **exactly equal** to locally audited final source. Length 7199 bytes.
- The workflow has **only `workflow_dispatch`**; no `push`, PR, cron, reusable `workflow_call` trigger.
- Connected GitHub Actions runs endpoint reports **`total_count=0`** after commit. **NO runner/container, DB start, registry layer pull or Redis/PG operation performed by the assistant** as part of the commit.
- Current GitHub source SHA proof verifies repository state at inspection, not immutable future settings nor evidence of executed tests.

**Gate decision:** `F3B_R5A_FIRST_MAIN_COMMIT=PASS_VERIFIED_EXACT_SOURCE`. This permission **has been consumed** and never authorizes running or modifying the workflow later.

## 3. Separate F3-C first diagnostic run — analytical GO/NO-GO matrix

| Control | Verified as of gate | First-run effect |
|---|---|---|
| R5-A source byte-for-byte pinned to first main commit | PASS | Prevent source drift before execution; re-verify HEAD |
| Manual-only event and exactly one bounded standard job | PASS static | No automatic run from initial commit |
| Repo public, GitHub Actions $0 budget with Stop usage=Yes | PASS owner GUI snapshot, **not live spend cap stress test** | Standard public runner expected $0 incremental compute; if blocked, STOP and do not change budget |
| Allow Reltroner actions only + required full SHA | PASS owner post-refresh GUI snapshot | Zero `uses:`; OCI images pinned separately by verified Docker manifest index SHA |
| No production secrets, env, tokens or DB target | PASS source/static | Synthetic-only and fail-closed repo/event/ref/network gates |
| Non-destructive diagnostic statements | PASS source/static | Only PostgreSQL SELECT and Redis read commands; fresh services still initialize |
| Runtime `psql`/`bash`/`timeout` and real PG18/Redis8 versions | UNKNOWN **by design** | Diagnostic may FAIL safely; failure is new evidence, not permission to edit live YAML or rerun automatically |
| Actual GitHub context IDs, image entrypoint, health checks | UNKNOWN **by design** | Must validate via one controlled run; network metadata not cryptographic Redis peer authentication |
| Future R5-B SQL mutation/Redis FLUSHDB | **FORBIDDEN** | Completely outside any R5-A runtime authorization |
| Action logs / retention / costs | 90-day owner setting; no artifact uploads | Record run ID, conclusion, SHA, redacted markers and budget snapshot; do not log credentials |

**Engineering decision: `CONDITIONAL_GO_FOR_ONE_R5A_READ_ONLY_RUN_IF_OWNER_APPROVES`.** This is a *recommendation*, not executable authorization. Residual risk is low but nonzero: fetching official public OCI image layers, running ephemeral third-party binaries, Docker networking and per-job service initialization consume transient compute/network and may expose GitHub-hosted runner runtime defects. No production endpoints/credentials/keys or cross-service write grants are in scope. There is no absolute zero-risk guarantee.

Before any run, require simultaneously:
1. Owner explicitly states `ALLOW_F3C_R5A_FIRST_MANUAL_DIAGNOSTIC_RUN=YES`, authorizing **one dispatch only**, on `main@3f8f923bf444f18b7ed5eed8ab738345f9b1a728`, no R5-B, no subsequent rerun without fresh evidence/approval.
2. Check `main` is still exact SHA and YAML exact SHA256; `workflow_dispatch` only; `permissions: {}`; standard `ubuntu-24.04`; job timeout 10 minutes, zero external `uses:`, immutable OCI references, no `ports:` and no host networking.
3. Check no existing in-progress Actions run; `Actions $0 / Stop usage Yes` budget and `Public` repository remain as observed (owner recheck if setting changes or drift detected). Do not upgrade runner, create secrets/artifacts or turn off stop budget to bypass policy.
4. Run **only** R5-A once via GitHub UI on `main`; no blanket permission for re-run.
5. Capture actual run URL/ID, `head_sha`, job attempt/conclusion, tool version markers and sanitized logs; report `PASS/FAIL/BLOCKED` with root cause. Do not classify real PG-R01..10 or HTTP T02 as executed by a pure diagnostic. If blocked by GH budget, image pull, context, health, runtime tools or code bug, **STOP and audit**; do not re-dispatch or change production.

**Hard NO-GO** if any source HEAD mismatch, previously unseen auto trigger, nonpublic repo, paid runner, new credentials, service port mapping, preexisting unexpected run, $0 stop budget changed, owner authorization absent, or inability to prove R5-B absent.

## 4. Trust program continuation

After a separately authorized and actually **PASSING** R5-A diagnostic: consider R5-B source risk review, owner permission for SQL-only fault tests and separately Redis loss/FLUSHDB in disposable isolated topology. Redis-only silent nonce-loss remains UNSAFE. PG-R01..10 **0/10 real** and T02 HTTP **0/86** until their own executable acceptance evidence exists. D02 owner design ratification and production remain HOLD.

**Next owner decision requested:** "Saya menyetujui satu kali eksekusi `workflow_dispatch` R5-A diagnostik read-only pada `Reltroner/lms-trust-sandbox/main@3f8f923bf444f18b7ed5eed8ab738345f9b1a728`, runner standard `ubuntu-24.04`, satu job maksimum 10 menit, dengan budget Actions $0 Stop usage Yes tetap, tanpa menjalankan R5-B dan tanpa perubahan production." Affirmation is required only if they wish to activate F3-C.
