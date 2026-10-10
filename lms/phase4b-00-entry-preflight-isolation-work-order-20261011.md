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
