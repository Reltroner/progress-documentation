# RC-W1-03 — Explicit Owner G2 Ratification & Scoped Isolated W1 Execution

> **Decision:** `G1=APPROVED`; **`G2=APPROVED_BY_OWNER`**; `W1=AUTHORIZED_NOT_YET_EXECUTED`; `G3..G8=NOT_AUTHORIZED`.
> **Decision date:** 2026-10-12 Asia/Jakarta (owner conversation message). This is a documentation-only GitHub receipt, not a claim that the owner's PC was modified.
> **Authority:** [RC-W0-10 G1 closure](./RC-W0-10-owner-g1-ratification-and-discovery-closure-20261012.md), [RC-W1-01 exact three-file work order](./RC-W1-01-proposed-g2-first-contact-creator-reader-ia-work-order-20261012.md), [RC-W1-02 narrow Git object-fetch plan](./RC-W1-02-local-commit-missing-and-proposed-fetch-gate-20261012.md), [source/release governance](../05-source-workspace-and-release-governance.md), [WEB AC01–27](../03-phase1-acceptance-and-invariant-traceability.md).
> **GitHub Studio main independently reverified on decision date:** `18b295f96ccb521b228a1855e79448158c09db15`. Resource main `6c6fb38f8ff3376c0789c15bcfe4d0cafc4d057e`.
> **User-approved boundary, translated from explicit user wording:** "aku menyetujui G2 gabungan RC-W1-01 + RC-W1-02 dengan batas yang dijelaskan di atas." This approves exactly the *combined* scoped package outlined directly before the user response; it does NOT approve G3 or provider changes.

## 1. Decision and technical target

The owner's explicit decision authorizes one deterministic sequence on their own Windows PC:
1. Reverify primary Git origin, branch `main`, local historical HEAD `d6969ddfbc5e7d98d49b1523259785125159e722`, exact 14 original untracked Markdown entries, no tracked changes, current worktree topology, branch/path collisions, and live remote `main` exact expected SHA.
2. Snapshot SHA-256 hashes of all 14 protected untracked files and all Git refs in memory.
3. If exact commit object is missing, fetch **only** `origin refs/heads/main` using `--no-tags --no-write-fetch-head --refmap= --no-recurse-submodules` with auto-maintenance disabled. This writes Git objects and may write temporary metadata, but must not intentionally update local `main`, remote-tracking refs, tracked files or protected drafts. Any unexpected change is STOP, not automatic cleanup.
4. Verify approved exact commit object `18b295f...`, no Git ref drift, live remote still same, and 14 protected content hashes unchanged.
5. Create **exactly one** new isolated worktree `C:\Projects\reltroner-studio-w1-ia` and local feature branch `phase1/w1-creator-reader-ia-20261012` at approved SHA, without push or PR. Verify new worktree initially clean and primary state unchanged.
6. Let Gemini IDE work only in the new isolated worktree and modify only `app/page.tsx`, `components/ecosystem/EcosystemHero.tsx`, `components/ecosystem/UseCasePathways.tsx`; conduct G2-scoped local tests with no installs or provider calls. Collect output and stop for independent reviewer classification before G3.

### Exact allowlist
```text
app/page.tsx
components/ecosystem/EcosystemHero.tsx
components/ecosystem/UseCasePathways.tsx
```

### Approved first-contact IA intent

Two accessible, equally prominent primary entry paths **For Creators** (actual creative/worldbuilding method evidence) and **For Readers** (spoiler-aware fictional Asthortera introduction). Preserve secondary collaborators/engineering pathway, existing AppDock, LMS/HRM/external links and honest live/planned states. Candidate source-verified `published: true` paths at inspected SHA include Creator `/blog/no-copypaste-worldbuilding` and Reader `/blog/asthortera-glossary`, but Reader **spoiler sensitivity must be inspected before claiming safe first-time entry**. If no suitable safe Reader route exists, STOP and request a scope amendment; do not create content under this three-file approval.

## 2. Non-authorizations that remain binding

- **NO** changes to tracked files in the protected primary checkout, `git pull`, `reset --hard`, `clean`, broad `git add`, or deleting/re-writing any of the 14 music/places Markdown files.
- **NO** installation/upgrades (`npm install`, `npm ci`, `npx`) or copying/junction/symlinking `node_modules` across worktrees without new approval. A new worktree does not inherit ignored/untracked `node_modules`.
- **NO** push, PR, GitHub source commit/merge, Vercel Preview/Production, deploy hooks, DNS/Cloudflare/Resend/Web3Forms, Keycloak/LMS/ERP, AI inference, provider keys or payment changes.
- **NO** editing `content/**`, `public/**`, analytics, contact form, global CSS/config, image CDN resolver, scripts, or other code outside the three existing TSX files. Generated `.next` build/test cache is permitted **only within isolated worktree** when G2-local tests are valid; if local build unexpectedly alters tracked non-allowlisted files, STOP and report rather than silently fix/commit/delete.
- **No blanket risk-free guarantee:** fetch writes Git object storage; worktree writes Git shared metadata; local tests consume CPU/disk and may write generated files. Guarded evidence and exact STOP conditions mitigate rather than eliminate risk.
- Main merge likely triggers automatic Vercel production deployment. G5/G6 must address control of that behavior before merges; G2 does not.

## 3. Operator script contract, observability and STOP conditions

The associated owner-facing copy/paste-ready **PowerShell 5.1 provisioning batch** was authored in this approval session as `RC-W1-03-G2-provisioning-20261012.ps1`, delivered as a downloadable companion and/or inline command in the conversation. Its source of truth is the **exact approved procedure in this section and RC-W1-02**, not permission to invent fallback flags. The script is designed to **stop** on mismatched origin/branch/SHA, changed primary or protected draft hash, new tracked/untracked entries, branch or path collision, ref changes during fetch, failed exact commit fetch, new worktree not clean, or unexpected topology. It creates no log on the owner's disk; owner should paste/redact console output back for a subsequent provisioning receipt. Execution is NOT claimed until the owner supplies real output.

**Important limitations:** This document archives the intended algorithm; the companion .ps1 must be separately inspected before running and is not an independent test of Windows-specific Git. The actual workstation may have a Git version/configuration/hook/credential constraint that requires STOP and review. Git command options used conform to [Git fetch official docs](https://git-scm.com/docs/git-fetch) and [Git worktree official docs](https://git-scm.com/docs/git-worktree).

## 4. Gemini IDE bounded coding and QA contract (only after script READY)

Human operator **must open** `C:\Projects\reltroner-studio-w1-ia` in the IDE. The coding agent must verify `git branch --show-current` matches `phase1/w1-creator-reader-ia-20261012`, `git rev-parse HEAD` matches `18b295f...`, and initial Git tracked status is clean. Never point the coding agent at `C:\Projects\reltroner-studio`.

- Read RC-W1-01 in full. Implement only the 3 TSX paths; preserve original semantics and current links; make two primary accessible entries and a secondary collaborator path.
- Route truth: verify `published:true` and descriptions/sensitivity locally without modifying content. Do not claim glossary spoiler-free just because it is published. If needed, STOP for amended G2 content scope.
- QA checkpoints: `git diff --check`; `git diff --name-only`; inspect exact diff; `npm run typecheck` and `npm run content:validate` only when dependencies/tooling already installed **in the new worktree**; one later `npm run build` if available/explicitly in G2 testing, monitoring its `postbuild` sitemap generation for writes outside allowlist. Do **not** run `npm run check-slugs` because its script writes a local report and calls the public site; do not run `npm run clean` or `build:clean`.
- Browser QA against localhost is allowed only if `npm run dev` can start from the new isolated worktree **with preinstalled dependencies** and no auto-installs, proxying to public paid providers, authentication, e-mail or contact submission. If dependencies absent, mark `BLOCKED_DEPENDENCIES`, do not install anything.
- Native 320x480, 375x812, tablet and desktop verification; keyboard/Focus/Escape, broken route, CTA accessibility, anchor and navigation regression, spoiler-aware boundary, and before/after diff. Tool limitations must be reported as NOT_EXECUTED rather than false PASS.
- **End:** provide execution receipt and stop. No git commit, push, PR, preview or merge. All 27 WEB-AC remain mandatory in later workstreams.

## 5. Gate matrix after explicit G2 approval

| Gate | State |
|---|---|
| G1 W0 discovery | **APPROVED, CLOSED WITH RESIDUALS** |
| G2 nonproduction exact-scope engineering | **OWNER APPROVED**, execution not yet observed |
| G2 local object fetch | **AUTHORIZED CONDITIONALLY**, only approved flags, exact base SHA and preflight |
| G2 isolated worktree/branch | **AUTHORIZED CONDITIONALLY**, only named target and branch |
| G2 bounded Gemini TSX implementation/local tests | **AUTHORIZED CONDITIONALLY**, after worktree READY |
| G3 source PR/push | **NOT AUTHORIZED** |
| G4 Vercel Preview | **NOT AUTHORIZED** |
| G5 main merge | **NOT AUTHORIZED** |
| G6 production release | **NOT AUTHORIZED** |
| G7–G8 final smoke/acceptance | **NOT AUTHORIZED** |
| W3 image, W4 GA consent, W5 model, W6 sender DNS, W7 final website DoD | **MANDATORY downstream blockers** |
| Phase 1 website/global & Phase 2 | **NOT ACCEPTED / NOT ACTIVE** |

**Next evidence:** owner executes the approved one-shot PowerShell provisioning in Windows PowerShell 5.1; the reviewer classifies output. Do not claim the worktree exists or Git fetch succeeded until that output is returned.
