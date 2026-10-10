# Reltroner LMS — E46-F3C R5-A Owner One-Time Manual Diagnostic Run Approval and STOP-Safe Handoff

> **Record:** `LMS-P4B02-E46-F3C-R5A-OWNER-APPROVAL-20261011`  
> **Final current state at inspection:** `OWNER_FIRST_RUN_APPROVAL=YES_ONE_DISPATCH_ONLY`, `GITHUB_WORKFLOW_RUNS=0`, `DISPATCH_EXECUTED=NO`, `REMOTE_DISPATCH_TOOL=UNAVAILABLE`, `LIVE_BUDGET_RECHECK=OWNER_GUI_REQUIRED`, `R5B_DESTRUCTIVE=FORBIDDEN`, `PG-R01..10=0/10`, `CANONICAL_T02=0/86`, `PRODUCTION=NO_MUTATION`.
> **Parents:** [canonical README](./README.md), [Phase 1 frozen logical boundary](./logical-service-boundary-api-contract.md), [frozen infrastructure placement](./master-infrastructure-placement-contract.md), [R5A exact source and gate](./phase4b-02-e46-f3b-r5a-first-diagnostic-bootstrap-commit-and-first-run-decision-20261011.md).
> **Scope:** documentary owner authorization record, preflight facts and deterministic GUI operator handoff. This record does not authorize the assistant to create workflow triggers or modify settings; no executable change made to sandbox.

## 1. Owner's exact approved action

The owner explicitly authorized **exactly one** `workflow_dispatch` on:
- Repository `Reltroner/lms-trust-sandbox`, default branch `main`.
- Frozen HEAD `3f8f923bf444f18b7ed5eed8ab738345f9b1a728`.
- File `.github/workflows/e46-f3b-r5a-diagnostic.yml` SHA256 `1e318115f31d15fc5feb7d0af0cb18c704a62c1e8d94f030809dbb1b2e4e10a4`, Git blob `d2f616c72e7c225431b54b2fa51d0e5b7b4139b8`.
- One standard GitHub-hosted `ubuntu-24.04` job bounded by `timeout-minutes: 10`, synthetic-only PostgreSQL18 and Redis8 services, no host-published service ports, no external Actions `uses:`, `permissions: {}`.
- Owner budget **Actions $0 / Stop usage Yes unchanged**.
- Explicitly excludes R5-B, any Redis `FLUSHDB`, automatic retries, reruns, paid larger runners and all production changes.
- If a gate fails, STOP and request new scope-specific approval rather than changing source/settings or retrying.

**Consent classification:** `OWNER_APPROVED_BUT_UNUSED`. It must be marked **CONSUMED** only after one `workflow_dispatch` has actually been initiated; it is not transferable to R5-B.

## 2. Fresh read-only GitHub repo and run verification

Connected GitHub repository read-only inspection:
- Repository `Reltroner/lms-trust-sandbox` public with `default_branch=main`.
- Exactly one branch `main` at the approved commit; exactly one root commit with zero parents.
- Exact Git tree leaf file `.github/workflows/e46-f3b-r5a-diagnostic.yml` (no executable R5-B file).
- Fetched YAML still 7,199 bytes and Git blob SHA `d2f616c72e7c225431b54b2fa51d0e5b7b4139b8`, matching already reviewed SHA256.
- `workflow_dispatch` only; `runs-on: ubuntu-24.04`, 10m job, `permissions: {}`; no `push`/`pull_request`/`schedule` triggers, no `uses:`, `ports:`, production credentials.
- GitHub Actions REST `/actions/runs` returned `total_count=0`. No runner or database started.
- Connected Github action inventory has read/write code operations and rerun existing jobs but **NO dispatch_new_workflow / workflow_dispatch mutation**. Never use rerun commands, source edits or synthetic commits as a substitute. Assistant therefore **DID NOT DISPATCH**.

**Billing limit:** Previously owner-provided GitHub Billing screenshot established `Actions=0 USD budget`, `Stop usage=Yes`. The connector cannot read private current account Budgets, so **present value is not reverified at execution time**. Owner MUST perform a no-change GUI confirmation immediately before clicking `Run workflow`; if altered/missing or if public free runner is blocked, STOP. Never increase/disable budget.

## 3. Deterministic owner GUI dispatch — no commands, no extra cost allocation

1. Open https://github.com/settings/billing/budgets — **read-only**, locate **Actions** account budget. Require **$0 budget**, **Stop usage Yes**; do not press New budget or adjust spending.
2. Open https://github.com/Reltroner/lms-trust-sandbox/actions and select **E46-F3B-R5A Diagnostic Read Only**. Confirm URL belongs to sandbox, not LMS-BE.
3. Confirm no unexpectedly running/completed jobs; `main` still approved HEAD; workflow source/path unchanged. If drift STOP.
4. Click **Run workflow**, choose **main**, click the final green **Run workflow** once. Do not double-click, do not choose a PR branch, do not click Re-run.
5. Open the resulting run page, record URL/ID, `head_sha`, `event=workflow_dispatch`, attempt, conclusion, and only redacted job markers. Do not paste passwords or access tokens into documentation.
6. If job fails, is blocked by budget or image pull, is cancelled or has unexpected run-count/commit, STOP. Do not retry or modify workflow until evidence is analyzed and a new owner authorization is granted.

**Operator GUI action is authorized by the owner's one-time approval**, but has not been performed. There is no background job polling or automatic execution in the connected assistant toolchain.

## 4. Scope of runtime assertion after a run

Only after logs show real tools and services can acceptance mark `R5A_RUNTIME=PASS/FAIL/BLOCKED`: Bash, psql, pg_isready, GNU timeout, PG18 server_version_num range, PostgreSQL active + default transaction_read_only, Redis8 PING/INFO/DBSIZE, service container ID/network consistency and exact safe repo/event/ref. A startup failure, missing CLI, job-context mismatch or script bug is scoped diagnostic failure.

Even a successful R5A never changes `PG-R01..10=0/10`, `T02_HTTP=0/86`, `D02_OWNER_TRUST_RATIFICATION=HOLD`. R5-B destructive source remains withheld from sandbox and requires distinct first-code-commit/dispatch permission. Production remains forbidden.

**Next message expected after owner GUI dispatch:** the run URL and final status/logs, without secrets, to permit accurate run acceptance and archival. If owner chooses not to dispatch, report `EXECUTION_PENDING_OWNER_GUI`, not `RUNNING`.
