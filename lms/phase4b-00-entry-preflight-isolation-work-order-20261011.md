# Reltroner LMS — Phase 4B-00 Entry, Source Pinning & Workspace Isolation Work Order

> **Document:** LMS-P4B-00-ENTRY-20261011  
> **Status:** OWNER REQUESTED START / OPERATOR PREFLIGHT AUTHORIZED; ENGINEERING IMPLEMENTATION, PROVISIONING AND PRODUCTION CHANGES **NOT YET AUTHORIZED BY THIS WORK ORDER**.  
> **Observed date:** 2026-10-11 Asia/Jakarta (GitHub source verification in initiating conversation).  
> **Parent authority:** [README](./README.md) §7–9, [Phase 0C physical FROZEN](./master-infrastructure-placement-contract.md), [Phase 1 logical FROZEN](./logical-service-boundary-api-contract.md), [ADR-LMS-TRUST-001](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md), [Phase 4A closure E31](./phase4a-00-read-only-runtime-infrastructure-discovery-work-order-20261010.md#26-e31--phase-4a-00-owner-conditional-final-discovery-acceptance--closed-with-residuals-2026-10-10).  
> **Principle:** Source-only acceptance is not runtime certification. In every AI explanation: TUJUAN → FAKTA → GAP → RISIKO → SOLUSI → TOOLS/OWNER → OTORISASI → BUKTI.

## 1. What is the first executable task?

**Phase 4B-00 is an entry/preflight gate, not an invitation to run six newly provisioned services in production.** The owner's new instruction explicitly starts Phase4B and requests large, copy-paste-ready Windows PowerShell 5.1 / Gemini IDE / GUI execution at high productivity. This authorizes a *local read-only evidence batch* and versioned planning. It does **not** by itself approve changes to the incumbent VPS/HRM/Keycloak/PostgreSQL/Redis, DNS/Cloudflare, hosting purchase, FE dirty checkout, source main branches, or production. Future nonproduction changes need an exact, narrow implementation scope and evidence from this gate.

**Entry invariants:** no `git pull`, `fetch`, `reset`, `clean`, worktree creation, branch checkout, file edit, package install, migrations, deployment, SSH authentication attempt, SQL/Redis queries, token issuance, console GUI changes or secret extraction in this preflight. Read-only Git `ls-remote`, `rev-parse`, `status --porcelain`, `remote get-url`, `show HEAD:path`, `worktree list`, and executable version checks are allowed. The **only** filesystem write permitted by the operator batch is a local evidence/report file under the operator's Windows TEMP directory, not within either repository.

## 2. Observed GitHub baseline (recheck before any write)

| Repository | Pinned current main SHA at entry | Caveat |
|---|---|---|
| `Reltroner/LMS-BE` | `a2672d0085fe84b55520f8f52f41a8c7fc8568a0` | Six Laravel apps; all six `routes/api.php` business placeholders at 4A E30; health routes present |
| `Reltroner/LMS-FE` | `eb01a4d2c924299b929aebf0f4826b94cf341fc6` | Owner 4A E27 local FE `f2d40417...` had 3 dirty entries: **PRESERVE** |
| `Reltroner/progress-documentation` | `c9f3498965cd46c452006cc2d02ac0831db4ea26` | 4A-00 E31 formally CLOSED with 10 unresolved scoped gates; frozen contracts unchanged |

Frozen architecture counts remain **20 physical + 24 logical**; Phase3 nonproduction 28/28 accepted; 44/44 trace rows but **0 newly live-certified** at 4B start. No source main HEAD movement was seen in GitHub before this work order; **local and remote state are not automatically inferred**.

## 3. Deterministic Phase 4B-00 runbook (Windows PowerShell 5.1)

1. **Operator:** run the copy/paste ready single batch supplied in the initiating conversation on **Windows PowerShell 5.1**, not on VPS or in the Gemini terminal.
2. **Tools:** git and optional PHP/Node; public GitHub `ls-remote` network read-only. Repository candidates are verified by **origin owner/repository**, never trusted solely by folder name. Missing local clones should be marked **NOT_FOUND**, not auto-cloned.
3. **Evidence:** write report in Windows TEMP; record timestamp, Git version/PowerShell version, exact external `main` SHAs for BE/FE/docs, local working-tree SHA, dirty-entry counts, linked worktrees, tool availability, six API placeholder checks, local directory presence.
4. **Safety:** no display of local private file contents, `.env`, tokens, passwords, SSH keys or untracked filenames. If returning a report, redact personal path/account and URL query secrets.
5. **Decision:** do **not** prepare an FE worktree until operator report verifies whether existing uncommitted entries are protected. If Git network read fails, label `REMOTE_UNVERIFIED` and **STOP**—do not assume pins still current. If BE origin, HEAD or clean status differs, **STOP_BE_WRITE**.
6. **Exit:** `P4B00-PRE01` main pins verified; `PRE02` local repo identity; `PRE03` BE clean/pinned; `PRE04` FE workspace preserved; `PRE05` environment tools; `PRE06` six API routes observed; `PRE07` no production mutation and report captured. These are **entry proof**, not source implementation tests.

## 4. Future engineering packages — STOP until scoped authority

- **4B-01:** isolated BE nonproduction branch/worktree and reconciliation of G03 stale crypto status, with exact code allowlist and no private keys. Gemini IDE is **implementation agent only**; cannot alter frozen contract, production or GitHub main. Paired source PR + CI + owner SHA approval.
- **4B-02:** secure OIDC learner/admin capability and Ed25519 internal dual-assertion gate and negative fixtures; never use frontend `RoleGate` as backend authorization or conflate OIDC RS256 and internal Ed25519.
- **4B-03:** four owner-scoped PG DBs, Redis atomic replay/outbox and service ownership in isolated nonproduction; DB access denial is not permission bypass.
- **4B-04:** gateway 26 contract API routes, provider business handlers, honest positive/negative HTTP tests; five non-Gateway services stay private.
- **4B-05:** independently deployable admin, immutable assets, approved DNS/TLS and pinned Cloudflare releases; preserve production learner deployment.
- **4B-06:** quantitative 1-vCPU incumbent HRM/Keycloak budget; DR integrity and isolated restore; operational evidence, rollback and release acceptance.

These are **proposed partition labels**, not frozen new phases or authorization. Workload ordering may change after actual report and owner decision. Source implementation can later be staged in safely isolated repo PRs; no production release until independent human approval.

## 5. Rollback and stop policy

This initial command batch makes **no changes to source or production**, so no production rollback should be needed. The local TEMP evidence file may be retained or deleted by the operator later; do not automatically delete it. Source feature PR rollback must use reviewed revert/isolated branch disposal after verifying clean status, never destructive alteration of a dirty user checkout. Production rollback is **unproven** until explicitly designed and validated. **Zero errors / zero technical debt cannot be promised**; stop conditions, exact pinning, negative tests, fail-closed design, and audit receipts reduce risk.

**Present checkpoint:** `4A-00_CLOSED -> 4B-00_ENTRY_OPERATOR_PREFLIGHT_AUTHORIZED -> LOCAL_EVIDENCE_AWAITED -> 4B-01_SOURCE_IMPLEMENTATION_NOT_YET_APPROVED -> PRODUCTION_NOT_AUTHORIZED`.

## 6. E32 — Owner Windows PowerShell 5.1 preflight receipt (2026-10-11 00:14 Asia/Jakarta)

**Operator evidence:** Output pasted directly in the current owner conversation, local timestamp **2026-10-11T00:14:32.7639516+07:00**, corresponding to **2026-10-10T17:14:32.7669501Z**. The first run was blocked by an earlier script error: Windows PowerShell 5.1 `Tee-Object` lacks `-Encoding` and did not produce a valid report. The owner then reran the existing `$ReportBlock` via `Tee-Object -FilePath $Report` in the same PowerShell session, with existence/nonzero-size checks. **Final evidence is the corrected second execution only**; the first failed invocation is not counted as PASS.

| Gate | E32 observed output | Scoped disposition |
|---|---|---|
| PRE01 | git 2.41.0.windows.1; `git ls-remote` exit=0 and exact main pins BE `a2672d0085fe84b55520f8f52f41a8c7fc8568a0`, FE `eb01a4d2c924299b929aebf0f4826b94cf341fc6`, Docs `c9f3498965cd46c452006cc2d02ac0831db4ea26` at **operator collection time** | `PASS_REMOTE_PINS`; docs pin becomes **historical** upon merging this documentation PR; fresh docs SHA required next |
| PRE02 | BE/FE local origins verified in C:\Projects search; Docs local clone not found in searched directory | `PASS_BE_FE_FOUND`; docs local checkout **optional**, not auto-cloned |
| PRE03 | BE local `main`, `HEAD=a2672d...`, dirty count **0**, `status exit=0`, **2 worktrees** | `PASS_BE_BASELINE_SAFE`; other BE worktree path/branch/dirty state not yet inventoried |
| PRE04 | FE local `main`, `HEAD=f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7`, dirty count **3**, `status exit=0`, **2 worktrees** | `PASS_FE_OBSERVED_AND_UNTOUCHED`; **not clean, not pinned, do not reset or change this checkout** |
| PRE05 | PHP 8.4.4 CLI ZTS; Node v22.23.1; npm and Composer detected | `PASS_TOOLCHAIN_PRESENT`; version compatibility for exact application/test matrix still requires execution |
| PRE06 | `API_{gateway,learning,mentorship,knowledge,assistant,audit}_PLACEHOLDER=True`, total **6/6** | `PASS_EXPECTED_SOURCE_DISCOVERY`; **not** a business API implementation PASS |
| PRE07 | Script reports no SSH, deployment, Git reset/fetch/pull/clean/checkout, or source edits; report exists, nonzero size **5,318 bytes** | `PASS_SCRIPT_SCOPED_READ_ONLY`; shell output is not independent whole-system mutation forensics |

**Exact E32 terminal classification:** `P4B00_ENTRY_CLASSIFICATION=READY_FOR_REVIEW_OF_ISOLATED_4B01_WORK_ORDER`. **All PRE01–PRE07 PASS within their defined entry scope.** `PHASE4B_01_CODING_AUTHORIZATION=NOT_GRANTED_BY_THIS_REPORT` and `PRODUCTION_AUTHORIZATION=NOT_GRANTED`. No backend/FE source compilation or runtime tests were performed in E32.

### 6.1 What is allowed next?

**Proceed to `4B-01` scoped engineering environment design and a separate guard-driven BE worktree inventory.** Before creating any new worktree, the operator must inspect the existing **two BE worktrees and two FE worktrees** for path/branch collision, hidden dirty work, unsafe location, and stale branches without resetting anything. The existing FE main checkout with three dirty entries is off-limits.

The first proposed code implementation is a **bounded nonproduction trust-contract status reconciliation (G03)** in isolated BE worktree, **NOT** six-service full implementation. Exact allowlist/negative tests/review and owner authorization belong in the *subsequent* Phase4B-01 work order; this preflight result alone does not authorize editing BE source. A new isolated worktree must originate from freshly verified remote BE `main` SHA and a clean/pinned local source; avoid `git fetch` or updating original main without separately approved instructions.

**No-cost/no-runtime-change priority:** review/inventory → approve per-file source scope → isolated worktree → Gemini IDE agent only for coding → PHP static/fixture tests + GitHub CI → owner PR review. Existing HRM/Keycloak/PostgreSQL/Redis, VPS hosting and Pages/DNS remain untouched. No guarantee of zero errors, but each gate has explicit observable stop conditions.

**E32 checkpoint:** `PHASE4A_CLOSED -> PHASE4B-00_PRE01..07_PASS_SCOPED -> PR41_E32_ARCHIVE_PENDING_MERGE -> PHASE4B-01_WORKTREE_INVENTORY_NEXT -> 4B-01_CODING_NOT_AUTHORIZED -> PRODUCTION_NOT_AUTHORIZED`.
