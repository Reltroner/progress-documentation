# RC-W1-07R — Successful G2 Read-Only Lockfile and Toolchain Revalidation

> **Owner observation timestamp:** `2026-10-12T19:28:58.7843168+07:00`.
> **Evidence class:** OWNER_WINDOWS_POWERSHELL_READ_ONLY_OUTPUT; GitHub Studio baseline `main` separately confirmed as `18b295f96ccb521b228a1855e79448158c09db15`. No direct reviewer access to local Windows.
> **Status:** `RC_W1_07R=COMPLETE_READ_ONLY / PASS_SCOPED`; `G2=OWNER_APPROVED`; `W1_SOURCE_PATCH=OWNER_REPORTED/REVIEWED`; `RUNTIME_QA=BLOCKED_DEPENDENCIES`; `G2_QA_DEPENDENCY_INSTALL=NOT_AUTHORIZED`; `G3=HOLD`.
> **Previous failure superseded by this successful continuation:** [RC-W1-07](./RC-W1-07-qa-toolchain-discovery-json-parser-failure-and-read-only-fix-20261012.md); [source review](./RC-W1-06-independent-source-review-g2-implementation-and-qa-blockers-20261012.md).
> **No secret, token, developer identity, subscriber record, environment details or npm authentication config recorded.**

## 1. Owner-observed exact outcome

The owner ran the full corrected Windows PowerShell block `RC-W1-07R` using Node.js `JSON.parse` to read `package-lock.json` and `package.json`, avoiding the earlier PowerShell empty-object-key parser exception.

| Check | Observed result | Interpretation |
|---|---|---|
| Worktree | `C:\Projects\reltroner-studio-w1-ia` | Target isolated path (owner terminal) |
| Branch | `phase1/w1-creator-reader-ia-20261012` | MATCH |
| HEAD | `18b295f96ccb521b228a1855e79448158c09db15` | MATCH G2 approved source |
| Git status | `M app/page.tsx`, `M components/ecosystem/EcosystemHero.tsx`, `M components/ecosystem/UseCasePathways.tsx` | Exactly three previously authorized tracked modifications; no others shown |
| npm lockfile | `lockfileVersion = 3` | Expected npm lock format |
| package root name | `learn-nextjs` | Matches lock root name |
| package root local dependency | `learn-nextjs = file:` | Matched in both package and lock |
| lock self-entry | `node_modules/learn-nextjs` present, `link=true`, `resolved=` empty | Self-referential local package relationship represented by npm lock; no install semantics proven |
| root dependency spec mismatches | `0` | package/lock root declarations agree; NOT proof of entire dependency tree validity |
| C: FreeGB | `48.79` | Free-space snapshot, not reserved allocation |
| Script final marker | `RC_W1_07R=COMPLETE_READ_ONLY` and `NO_INSTALL_NO_BUILD_NO_PUSH_NO_DEPLOY` | Full corrected read-only script completed |

From the prior RC-W1-07 (not reexecuted here): Node `v22.23.1`, npm `10.9.8`, Bun NOT installed, `bun.lock` + `package-lock.json` tracked, `node_modules=False`. No package install was performed in either read-only probe.

## 2. Technical interpretation and QA readiness

- **PASS_SCOPED** means toolchain identity, root lockfile consistency, available disk and source isolation are observed sufficiently to **propose** G2 QA dependency amendment.
- **Not** an npm installation pass, compiled TSX pass, successful Next build, live route response or mobile browser QA pass.
- `learn-nextjs: "file:"` with `link:true` and empty resolved field has **not** been shown to fail, but should be treated as a possible local-link/installation caveat. Do not remove it, rewrite package/lock, switch package manager or run fallback installation without separate scope approval.
- Since Bun is not installed while npm is available and the npm root lock is coherent, the **least additional tooling** route is npm-first, using the tracked `package-lock.json`; don't automatically install Bun or choose both lockfiles.
- Exact production build includes Next.js Google fonts from `app/fonts.ts` (`next/font/google`) and an npm `postbuild` `next-sitemap` step; a future authorized build might require third-party font network access and emit sitemap/robots output. These have **NOT** been executed and require explicit observation and changed-path review.
- Git Studio primary original 14 untracked author files remain protected; last SHA-256 integrity receipt was provisioning, not rehashed in this read-only toolchain script.

## 3. Pending separate owner decision

Proposed future scope: [RC-W1-08 — Narrowly gated G2-QA dependency and runtime test amendment](./RC-W1-08-proposed-g2-qa-isolated-npm-dependency-and-runtime-tests-20261012.md). **It is only a proposal until the owner explicitly approves.**

No action is presently authorized to run `npm ci`, `npm install`, `bun install`, `npx`, copy/symlink dependency directories, clean ignored caches, change package/lock files, run build, commit, push, PR, preview, merge or deploy. The original G2 allows local tests only where dependencies already exist and requires missing dependencies to be reported as BLOCKED.

**Gate record:** `G1 APPROVED`; `G2 SOURCE PATCH PASS_SCOPED`; `RC-W1-07R PASS_SCOPED_READ_ONLY`; `G2-QA_INSTALL PENDING_OWNER`; `W1_IA PARTIAL`; `G3–G8 NOT_AUTHORIZED`; `WEB_PHASE1 NOT_ACCEPTED`; `PHASE2 NOT_ACTIVE`.
