# RELTRONER STATISTICS — Permanent Single-Checkout and No-Worktree Policy

> **Owner directive:** RATIFIED / HARD REQUIREMENT, effective 2026-11-18 (Asia/Jakarta).
>
> **Applies to:** `Reltroner/reltroner-statistics`, all local IDE agents, scripts, QA/debugging, creative-quality and deployment changes, all future contributors and automation following this documentation.
>
> **One authorized local Statistics checkout:** `C:\Projects\reltroner-statistics`.
>
> **Canonical Git branch:** `main` in `https://github.com/Reltroner/reltroner-statistics` is the upstream source of truth, not an arbitrary local feature branch.
>
> **Supersession:** this policy overrides every earlier instruction, runbook, local-agent prompt or historical example recommending or allowing a *new local secondary Git worktree* for Reltroner Statistics. Such historical worktrees were previously used for PAGE-004 and DEPLOY-SHA-005; they are recorded as past engineering facts, **not** ongoing permission.

## 1. Non-negotiable prohibitions

1. **NEVER create, clone, or use a second local checkout/worktree of Reltroner Statistics**, including a new `git worktree add`, sibling folder, mirror repo or temporary separate clone under any Windows path. `C:\Projects\reltroner-statistics` is the **only** permitted Statistics local working directory.
2. **NEVER change the upstream repository's `main` branch as a side effect of cleanup.** Main is read from GitHub, and ref updates in the approved local checkout must be strictly fast-forward and version-verified.
3. **NEVER wipe, reset, stash, unstage, overwrite, or commit the owner's protected local files without separate, explicit owner authorization:**
   - `C:\Projects\reltroner-statistics\.vscode\settings.json`
   - `C:\Projects\reltroner-statistics\public\reltroner-statistics-logo.webp`
   This includes preserving their **staged index status** if staged. Preflight and postflight SHA-256 values must match.
4. **NEVER invoke** `git reset --hard`, `git clean -fdx`, `git push --force`, force-update `main`, unchecked branch switches, or unattended deletion on the only approved checkout.
5. **NEVER claim “local main = GitHub main” merely from `git fetch` or `origin/main`**. Verify local `refs/heads/main`, fetched `origin/main`, `ls-remote` and, if available, the GitHub branch API. Verify that the *checked-out* `HEAD` also equals main when a 1:1 checkout is requested.
6. **NEVER create a second local worktree as a safety workaround.** Safety must instead be achieved through read-only inventory, hash-verified external backup, clean Git staging, standard in-place feature branches, and explicit stop conditions. If in-place work cannot proceed without losing owner WIP, **STOP and report**.
7. **NEVER apply this directive to another repository by inference**. `https://reltroner.com/` is the **Reltroner Studio website**, which has its own upstream source repository and local checkout. Statistics has the separate public site `https://statistics.reltroner.com/`. This policy concerns only **Reltroner Statistics**; it does not rename or authorize writing Studio's directory or repository.

## 2. Authorized single-checkout workflow

The supported operating model is **one filesystem checkout, many Git branches and remote Pull Requests**:

```text
GitHub: Reltroner/reltroner-statistics (main: source of truth)
        |
        | fetch, inspect origin/main + ls-remote + GitHub API
        v
C:\Projects\reltroner-statistics       [ONLY local checkout]
        |-- main                    exact upstream SHA when synchronized
        |-- feature branches        ordinary git switch in the SAME directory
        |-- protected owner WIP     hash-preserved and never silently unstaged
        +-- QA/build/test           local, without second worktree
        |
        +--> push a feature branch and open PR (only with owner-approved scope)
        +--> GitHub Actions verifies and publishes authorized main merge
```

- Before touching a local branch, record `git branch --show-current`, `git rev-parse HEAD`, `git status --porcelain=v1 --untracked-files=all`, `git worktree list --porcelain`, the protected files' SHA-256, and fetched/advertised remote-main identity.
- Perform clean branch transitions only if Git proves preserved WIP cannot be overwritten. The two protected files may remain staged as **explicit documented exceptions to tree cleanliness**; strict 1:1 parity means the Git commit/tree referenced by `HEAD` and `main` matches upstream, **not** that these two intentional local additions are absent.
- Do not switch a branch or merge when the working tree contains unrelated changes. Keep them in place and stop for review; do not bypass with a temporary secondary worktree.
- During ordinary feature work, make **only** purpose-scoped changes. Commit changes on a feature branch in the single checkout. Do not commit the two protected files unless owner separately authorizes their inclusion.
- Before a new engineering task, enforce this policy regardless of a previous model's saved notes, old IDE prompt, stale task log or prior exception. A request to “preserve work using another worktree” is superseded; if the owner explicitly revises the policy, first update this document and register that decision.

## 3. One-time retirement of historical auxiliary worktrees

These are **historically observed and owner-designated cleanup targets**, not permitted working directories going forward:

| Exact Windows path | Classification | Retirement rule |
| --- | --- | --- |
| `C:\Projects\reltroner-statistics-rs-ai-page-004` | old PAGE-004 auxiliary worktree | verify registered to the authorized Statistics repository, clean tracked/untracked changes, then `git worktree remove` (use `--force` only if necessary for ignored generated files, after explicit targeted validation) |
| `C:\Projects\reltroner-statistics-rs-deploy-sha-005` | old SHA-005 auxiliary worktree | same |
| `C:\Projects\_reltroner-owner-backups` | old owner backup folder, **not a Git worktree** | copy/hash-verify the two protected originals to an external fallback first, ensure the folder contains no unexpected symlinks and remove only this exact named folder |

**Safety boundaries:** do not delete `C:\Projects\reltroner-statistics`; do not run `git worktree remove` on the owner checkout; do not delete other `C:\Projects\*` folders; do not assume a folder's name proves it is disposable. Refuse cleanup on an unexpected registered worktree, conflicting branch, repository mismatch, uncommitted user changes or SHA-256 mismatch. Retiring these directories **does not** delete remote PRs, branches or GitHub history. Retain a dated operational log outside the three deleted folders.

**Execution boundary:** updating this GitHub document cannot delete files on the owner's Windows computer. The cleanup is only complete when the owner executes a verified local PowerShell 5.1 script and observes `LOCAL_MAIN_1_TO_1_GITHUB: PASS`, `PROTECTED_STAGED_FILES_PRESERVED: PASS`, `ONLY_ONE_STATISTICS_WORKTREE: PASS`, and each exact-target deletion PASS. Never record such local execution as already done based solely on this policy commit.

## 4. Compliance acceptance

| Check | Required result |
| --- | --- |
| Local repository root | `C:\Projects\reltroner-statistics` |
| Origin URL | `Reltroner/reltroner-statistics` only |
| Local `main` SHA, `HEAD`, fetched `origin/main`, remote `ls-remote`, GitHub API `main` | identical 40-hex SHA |
| Working-tree exceptions | only owner-authorized preserved files; no hidden lost work |
| Protected file SHA-256 before/after | byte-identical |
| Protected index | staged status unchanged unless owner explicitly changes it |
| Worktree registry | exactly one Statistics working tree, the approved root |
| Deleted paths | only three exact historical targets, after all preconditions |
| GitHub main and published site | no push/redeploy triggered by local maintenance |
| Runtime functional and non-functional behavior | unchanged; no app source code or production infrastructure modified |

## 5. Authority and relationship to earlier records

This rule is a **durable owner policy** in the documentation repository and remains binding for agents following it until the owner explicitly changes it in a later documented decision. It cannot physically prevent arbitrary shell commands by an external program; enforce it with preflight checks and fail-closed tooling. Historical descriptions of sibling worktrees in [PAGE-004](./2026-11-18-rs-ai-page-004-universal-page-aware-intelligence-architecture.md), [DEPLOY-SHA-005](./2026-11-18-rs-deploy-sha-005-deployment-sha-parity-debugging.md), and earlier runbooks remain true **about those past sessions**. Their former worktree recommendations are **not current instructions**.

**Scope clarification:** the owner wrote “for `https://reltroner.com/`,” but the Statistics repository is the source for **`statistics.reltroner.com`**. The main Studio website `reltroner.com` belongs to a different source/control plane and is not synchronized by this Statistics-only policy.
