# Reltroner LMS — Phase 3B-00 Local Git & CI Discovery Preflight Acceptance

> **Date:** 2026-10-09 (Asia/Jakarta).  
> **Class:** Read-only engineering verification / AI-to-AI handoff.  
> **Decision:** **3B-00 GIT & CI INVENTORY PREFLIGHT ACCEPTED** based on user-provided PowerShell evidence and independently retrieved GitHub metadata.  
> **Explicit distinction:** No six-service PHPUnit tests, FE build, application CI pipeline, or production runtime checks were executed as part of this phase. **3B-01 file allowlist still requires owner approval before coding.**

## 1. Source and proof provenance

| Frozen or observed reference | Verified SHA |
|---|---|
| Effective FZ-11 design-freeze merge anchor (PR #6) | `b9390a06ebc5db5377059a99109d59fea092cccb` |
| `progress-documentation/main` at review | `6d7ae4399f8e1fc770ef7d41968af1d2b030053e` |
| `Reltroner/LMS-BE/main` | `e30a61780994d85671cbf079e6b9ce899b3fe837` |
| `Reltroner/LMS-FE/main` | `f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7` |
| Physical Phase 0C FROZEN file blob | `b899761c9e833f9fa567055801b9ba0834ed56eb` |
| Logical Phase 1 FROZEN file blob | `cf089b8df4b5ccb1761b504ffae662a0053bf03e` |

**Evidence grades:** GitHub status, tree and dependency snapshots retrieved read-only through connected GitHub; local machine facts explicitly supplied by project owner as raw Windows PowerShell terminal output. We have not controlled or independently rerun commands on the owner's Windows computer. The scripts observed no fetch/pull or source/production writes, apart from the separately approved prior `git worktree add --detach` creating the isolated local worktree.

## 2. Deterministic local Git results

| Check | LMS-BE local workspace | LMS-FE isolated workspace |
|---|---|---|
| Local path | `C:\Projects\lms-reltroner-backend` | `C:\Projects\lms-reltroner-studio-phase3b` |
| Branch/head | `main` / `e30a61780994d85671cbf079e6b9ce899b3fe837` | Detached HEAD / `f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7` |
| HEAD matches FZ-11 SHA | **PASS** | **PASS** |
| Cached `origin/main` equals frozen SHA | **PASS** | **PASS** |
| GitHub remote main independently matched | **PASS** | **PASS** |
| Target working tree clean | **PASS** | **PASS** |
| Lockfiles present | **6/6 Composer** | **1/1 npm** |

Original `C:\Projects\lms-reltroner-studio` is **not** a coding target: its pre-existing uncommitted changes were preserved before and after creating the isolated detached-head worktree. The original `00-course-orientation.mdx` had 641 additions/14 deletions, `sso-architecture-roadmap.md` had 3 additions/3 deletions, and `structure.txt` remained untracked. **No `git stash`, `reset`, `clean`, `restore` or cherry-pick was run.**

## 3. Local toolchain and remote CI inventory

| Evidence | Status |
|---|---|
| PHP 8.4.4 (compatible with `^8.3` constraint) | DETECTED, **not test-run PASS** |
| Composer 2.10.3 | DETECTED |
| Node 22.23.1 / npm 10.9.8 | DETECTED |
| Six independent Laravel 13.35.0 `composer.lock` manifests | FILES PRESENT / REMOTE READ |
| PHPUnit 12.5.38 in pinned backend locks | LOCKED VERSION CONFIRMED |
| 36 backend PHPUnit test source files | SOURCE INVENTORY ONLY |
| FE Next.js 16.2.6, npm lockfile v3 | LOCKED VERSION CONFIRMED |
| GitHub Actions `.github/workflows/` in current trees | NONE FOUND (both repos) |
| GitHub API workflow runs of main | NONE FOUND (both repos) |
| Commit checks | BE 0; FE one successful **Cloudflare Pages** check (not LMS CI) |
| Full backend PHPUnit six-service execution | **NOT EXECUTED** |
| FE lint/content/Next static build/privacy-negative execution | **NOT EXECUTED** |

Absence of workflows is a documented `3B-05` implementation gap, **not a blocking Git integrity failure**. Lockfile presence is not a full dependency integrity or reproducible `npm ci`/`composer install` certification.

## 4. Gate status (PB00-01..12)

| Gate | Scope | Result |
|---|---|---|
| `PB00-01` | FZ-11 owner design freeze effective in docs main | **PASS** |
| `PB00-02` | GitHub LMS-BE/FE remote main SHA frozen equality | **PASS** |
| `PB00-03` | Six standalone Laravel service directory inventory | **PASS** |
| `PB00-04` | Six committed Composer and one npm lockfile present | **PASS_PRESENCE_ONLY** |
| `PB00-05` | Baseline CI inventory and gaps documented | **PASS_DISCOVERY_ONLY** |
| `PB00-06` | Correct local clone paths and origin identification | **PASS** |
| `PB00-07` | Local HEAD/branch trust context | **PASS** |
| `PB00-08` | Cached origin/main SHA parity | **PASS_WITH_FRESH_REMOTE_CROSSCHECK** |
| `PB00-09` | Clean target workspaces and safe original FE preservation | **PASS** |
| `PB00-10` | Local committed lockfile presence | **PASS_PRESENCE_ONLY** |
| `PB00-11` | Local PHP/Composer/Node/npm available | **PASS_DETECTION_ONLY** |
| `PB00-12` | 3B-01 file allowlist owner acceptance | **TRANSFERRED_TO_3B01_ENTRY** |

**Gate distinction:** PB00-12 belongs to the **Phase 3B-01 implementation entry review**, not a failed local Git invariant. Therefore the **3B-00 preflight is ACCEPTED for its defined read-only Git/CI discovery scope**, while 3B-01 agent coding is **NOT STARTED and not yet file-allowlist approved**.

## 5. Exact proposed Phase 3B-01 file allowlist (not approved for writes yet)

**Repository:** `Reltroner/LMS-BE` only; **base SHA:** `e30a61780994d85671cbf079e6b9ce899b3fe837`. All paths below are **proposals for files/directories to be created**, not claims they already exist.

| Potential path | Permitted purpose |
|---|---|
| `contracts/README.md` | Contract ownership, version strategy, reproducible local validation instructions |
| `contracts/openapi/v1/**` | Versioned OpenAPI 3.1 spec for EXACTLY 26 frozen method+paths |
| `contracts/authz/**` | Route capability, OIDC client context and resource ownership matrix |
| `contracts/schemas/**` | Request/response/RFC7807/pagination/idempotency schemas |
| `contracts/examples/**` | Sanitized valid/error/security-negative examples |
| `contracts/tests/**` | Test-only lint/assertions against OpenAPI and 26-operation policy inventory |

**Forbidden during 3B-01:** any `services/**` application code/controller/routes/migrations, `.github/workflows/**` (reserved 3B-05), `.env` and secrets, live Keycloak config, LMS-FE source, Studio canon, infrastructure, DB/schema mutation, new public resource family, new event/capability namespace, composer/npm dependency upgrade without separately approved change control.

**Exact mandatory acceptance targets:** `B3-AC01` (26 frozen operations), `B3-AC02` (19 capabilities and guest-offerings policy explicitly settled; `admin.learning.*` reserved), `B3-AC03` (RFC7807/error/request ID/pagination/idempotency), `B3-AC04` (per-route owner/client/authz/status/error + mock compatibility).

**Open policy decision:** Public `GET /mentorship/offerings*` may require explicit safe guest-only projection. This is **not** silently approved. `GET /mentorship/availability` remains authenticated booking-oriented by accepted ADR. Do not give B3-AC02 PASS without resolving public offering policy and recording fixtures.

## 6. Recommended deterministic next sequence

1. Owner reviews/merges this 3B-00 documentation PR; pin actual merge SHA in the next checkpoint.
2. Owner/reviewer explicitly approves the 3B-01 file allowlist, test and rollback plan. No IDE source mutation before that approval.
3. Use the **clean LMS-BE `main`** as reviewed baseline; create a scoped 3B-01 feature branch only after approving branch name/base. Do not use detached FE worktree for 3B-01.
4. IDE AI agent generates contract artifacts **only inside approved paths**, following FZ-10/11. Git diff file allowlist, inspect 26 exact routes and 19 capabilities, run tests when implemented, then produce commit/PR evidence for human acceptance.
5. Keep later packages 3B-02..07, Phase 4 and production separately gated. No source/production mutations were performed during this Phase 3B-00 acceptance documentation.

**Checkpoint:** `PHASE 3A FROZEN → 3B-00 GIT+CI INVENTORY ACCEPTED → 3B-01 ALLOWLIST REVIEW / NO CODING YET → PRODUCTION NOT AUTHORIZED`.

## 7. Canonical AI handoff

Read the [FZ-11 postmerge record](./reltroner-lms-phase3a-fz11-postmerge-activation-20261009.md), [FZ-10 work order](./reltroner-lms-phase3a-04-fz10-phase3b-entry-exit-authorization-20261009.md), [FZ-02 invariant trace](./reltroner-lms-phase3a-04-fz02-cross-contract-invariant-traceability-20261009.md), the two FROZEN parent contracts, this preflight record and the living [engineering ledger](./engineering-end-to-end-progress-ledger.md). Source-only contract planning is not product runtime certification.
