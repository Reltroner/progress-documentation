# RC-W1-01 — Proposed G2 Work Order: Creator/Reader First-Contact IA Slice

> **Status: `G1=OWNER_APPROVED`, `G2=AWAITING_DISTINCT_OWNER_APPROVAL`, `W1=PLANNED_NOT_EXECUTED`.**
> **Created:** 2026-10-12 Asia/Jakarta. This file is **not implementation authorization**. Derived from [G1 ratification](./RC-W0-10-owner-g1-ratification-and-discovery-closure-20261012.md) and [RC-W0-09 proposed entry](./RC-W0-09-final-discovery-disposition-and-proposed-w1-entry-20261012.md).
> **Contract:** [ratified architecture WEB-I01–18](../00-ratified-frontend-architecture-contract-20261012.md), [WEB-AC01–27 traceability](../03-phase1-acceptance-and-invariant-traceability.md), [zero-incremental-cost boundary](../04-zero-incremental-spend-and-provider-boundaries.md), [source/release G0–G8 governance](../05-source-workspace-and-release-governance.md).
> **Source SHA observed from GitHub main:** `18b295f96ccb521b228a1855e79448158c09db15`; resource repo `6c6fb38f8ff3376c0789c15bcfe4d0cafc4d057e`. Before G2 use `git ls-remote` / GitHub read, and **STOP if any new source main SHA is not separately reviewed and approved**.
> **Financial limit:** Rp0 incremental cash; no paid activation, dependency install, new runtime API or unapproved Vercel preview/prod deployment.
> **Primary checkout preservation:** `C:\Projects\reltroner-studio` had owner-reported local `main` SHA `d6969ddfbc5e7d98d49b1523259785125159e722` with **14 protected untracked Markdown files**; never change or clean these files; fresh snapshot before any G2 execution.

## 1. Purpose / user behavior / deliberate limits

**W1-01 user story:** A first-time visitor landing on `/` immediately distinguishes two primary, equally discoverable routes:
1. **For Creators** — practical *creative systems that compound* / worldbuilding framework, with link to actual existing publicly published creative-method evidence rather than fictional promises of paid course or completed mentorship.
2. **For Readers** — nontechnical, **spoiler-aware introduction** to Asthortera / The Abyss of Comfort before exploring detailed lore; label fiction explicitly and avoid linking unaware newcomers straight into the 200k-character master Season 17–37 architecture.

Keep **third secondary collaborator/engineering lens** discoverable and distinguish it from fictional/canon content. Preserve existing ecosystem/LMS/HRM navigation and live-vs-coming-soon honesty. W1 is first-contact IA/copy/navigation only, **not** W2 shared-search/rails, W3 CDN assets, W4 GA privacy, W5 AI, W6 provider integration or W7 production acceptance.

### Site truth / verified candidates for destinations

The following files exist at the checked Studio source SHA and have `published: true` frontmatter. This proves a source-level publication flag, not live HTTP 200, absence of spoilers, or satisfaction of all owner product claims:

| Proposed purpose | Existing source | Candidate public route | Notes |
|---|---|---|---|
| Creator approachable first evidence | `content/blog/no-copypaste-worldbuilding.md` | `/blog/no-copypaste-worldbuilding` | Explains authorial refinement; not itself a complete marketed course |
| Creator framework alternative | `content/blog/creative-lore-bible.md` | `/blog/creative-lore-bible` | Specific creative lore guidelines; distinguish fiction/canon and meta-method |
| Creator full blueprint secondary reference | `content/principles/reltroner-studio-master-source-of-truth.md` | `/principles/reltroner-studio-master-source-of-truth` | Very large apex constitution, unsuitable as only gentle first-time entry |
| Reader lore orientation candidate | `content/blog/asthortera-glossary.md` | `/blog/asthortera-glossary` | Terms and concepts; **spoiler-light classification NOT yet verified** |
| Reader deeper story (NOT default entry) | `content/series/the-abyss-of-comfort.md` | `/series/the-abyss-of-comfort` | Massive multi-season narrative architecture, risk of high-level spoilers |
| Collaborator/recruiter evidence | `content/blog/for-recruiters.md` | `/blog/for-recruiters` | Already linked in `UseCasePathways.tsx` |

**Final G2 UI route decision:** Creator candidate `/blog/no-copypaste-worldbuilding` or alternative creative-lore-bible; Reader candidate `/blog/asthortera-glossary` only after source spoiler sensitivity review and live/preview route verification. If spoiler-safe reader entry does not exist, **STOP and propose a separate narrowly scoped content/route amendment**, not improvising a newly published lore page within this three-file G2 scope.

## 2. Source inspection and precise allowlist

At Studio `18b295f`:
- `app/page.tsx`: existing TSX page composes `EcosystemHero`, `AppDock`, `EcosystemPillars`, `UseCasePathways`, `FeaturedKnowledgeBridge`, `EcosystemRoadmapPreview`; existing footer "Ready to explore?" stays functional.
- `components/ecosystem/EcosystemHero.tsx`: currently title Reltroner Studio and generic `Explore Ecosystem`, `Browse Knowledge Base`, `Open LMS`; lacks directly named Creator and Reader CTA.
- `components/ecosystem/UseCasePathways.tsx`: currently learners/builders/HR-admins/lore readers/partners-recruiters. Reuse its small data-driven cards rather than introducing duplicate navigation mechanisms or renaming unrelated services.
- `package.json`: available scripts `typecheck` (TypeScript `tsc --noEmit`), `content:validate`, `build` (Next.js + postbuild `next-sitemap`); `build:clean` invokes a destructive cache clean and **MUST NOT** be used.

**Exact PROPOSED change allowlist (existing TSX files only):**
```text
app/page.tsx
components/ecosystem/EcosystemHero.tsx
components/ecosystem/UseCasePathways.tsx
```

**No other edits**, including tests, without separately amended G2 scope. Do not add dependencies. If source-level testing needs new test files, present the exact additional files and rationale and STOP pending scoped approval; browser observation/source tests may be executed without new tracked files after G2 if authorized.

**Explicit never-touch list in this slice:** `content/**`, `public/images/**`, `lib/**`, `app/layout.tsx`, `components/GoogleAnalytics.jsx`, `components/RouteAnalytics.jsx`, `app/contact/**`, `components/sections/ContactForm.jsx`, `package*.json`, `next.config.mjs`, `tsconfig.json`, `.vercelignore`, `.github/**`, `.env*`, `node_modules`, existing docs, LMS/HRM/VPS, `reltroner-studio-resource`. No root or global CSS modifications; scope expansion requires new owner approval.

## 3. Proposed UI contract and minimal behavior

- Hero `h1` remains semantic; explain in plain language that Studio builds **creative systems that compound**, demonstrated through Asthortera **fictional civilizational simulation**.
- Prominent distinct CTA labels such as `For Creators` and `For Readers`. Each must have direct real destination and independent keyboard-focus/accessible-name semantics. Do not present three equal CTAs where external LMS displaces the two ratified primary routes.
- Third lens `For Collaborators / Engineering` remains discoverable as **secondary** and points to published `/blog/for-recruiters`; never imply the website is an agency, promises free prototypes, or sells mentorship already live.
- Keep existing `#app-dock` and `#knowledge-bridge` anchor destinations where other links rely on them; avoid fragment links to non-existent ids. Preserve `AppDock`, `Open LMS`, `Open HRM`, disabled/upcoming states and external `target=_blank rel=noreferrer` behavior; no SSO/security changes.
- Use minimal typed static data and Tailwind classes consistent with existing design, preserving dark theme and 320px layout, without UI framework installation. Prefer reusing existing section components over introducing a "mega hero" or new architecture layer.
- Avoid claiming a glossary is absolutely spoiler-free without page review. Reader route must use appropriately accurate `introductory`/`spoiler-aware` wording, and no automatically generated fictional/nonfiction classification beyond existing source and ratified W2 taxonomy plan.
- Respect mobile header/keyboard and existing skip-navigation flow; no CAPTCHA, newsletter or third-party request behavior changes.

## 4. Safe G2 read-only operator preflight — CAN RUN NOW, NO WRITES

**Actor:** owner in **Windows PowerShell 5.1**, not Gemini IDE agent. This script only inspects primary local workspace and remote Git refs. No `git fetch`, `pull`, `checkout`, `worktree add`, `reset`, `clean`, `npm` or file writes.

```powershell
& {
    $ErrorActionPreference = 'Stop'
    $Repo = 'C:\Projects\reltroner-studio'
    $CandidateWorktree = 'C:\Projects\reltroner-studio-w1-ia'
    $Branch = 'phase1/w1-creator-reader-ia-20261012'
    $ExpectedOrigin = 'https://github.com/Reltroner/reltroner-studio.git'
    $ReviewedRemoteHead = '18b295f96ccb521b228a1855e79448158c09db15'

    Write-Host '=== RC-W1-01 / G2 READ-ONLY PRE-FLIGHT ===' -ForegroundColor Cyan
    Get-Date -Format o

    if (-not (Test-Path -LiteralPath $Repo -PathType Container)) {
        throw 'STOP: Studio primary repository does not exist.'
    }

    $ActualOrigin = (git -C $Repo remote get-url origin).Trim()
    if ($LASTEXITCODE -ne 0 -or $ActualOrigin -ne $ExpectedOrigin) {
        throw "STOP: origin mismatch: $ActualOrigin"
    }

    $BranchPrimary = (git -C $Repo branch --show-current).Trim()
    $HeadPrimary = (git -C $Repo rev-parse HEAD).Trim()
    if ($LASTEXITCODE -ne 0 -or $BranchPrimary -ne 'main') {
        throw "STOP: unexpected primary branch: $BranchPrimary"
    }

    Write-Host "Primary branch: $BranchPrimary"
    Write-Host "Primary HEAD: $HeadPrimary"

    Write-Host '--- Protected authoring files inventory ---'
    $Protected = @(
        'content/music/astrostelia-the-astronomers-horizon.md',
        'content/music/astrostelia-the-waltz-of-falling-stars.md',
        'content/music/cenrestier-the-eternal-citadel.md',
        'content/music/cenrestier-where-the-fortresses-stand.md',
        'content/music/depcutland-the-grand-library.md',
        'content/music/reltronland-the-pursuit.md',
        'content/music/stelpadland-across-the-quiet-lake.md',
        'content/music/stelpadland-adventure-awaits.md',
        'content/music/stelpadland-keep-moving-forward.md',
        'content/music/stelpadland-snowfall-in-stelpadland.md',
        'content/music/stelpadland-the-open-trail.md',
        'content/music/stelpadland-the-wild-and-the-warm.md',
        'content/places/reltronland-map-scale-architecture.md',
        'content/places/skytropolis.md'
    )
    $Missing = @($Protected | Where-Object {
        -not (Test-Path -LiteralPath (Join-Path $Repo $_) -PathType Leaf)
    })
    Write-Host "Originally reported protected paths: $($Protected.Count)"
    Write-Host "Missing since W0 snapshot: $($Missing.Count)"
    if ($Missing.Count -gt 0) {
        $Missing | ForEach-Object { Write-Host "MISSING: $_" }
        throw 'STOP: protected local files changed; preserve state for review.'
    }

    Write-Host '--- All changes, tracked and untracked ---'
    git -C $Repo status --porcelain=v1 --untracked-files=all
    if ($LASTEXITCODE -ne 0) { throw 'STOP: failed to inspect primary Git status.' }
    Write-Host '--- All worktrees ---'
    git -C $Repo worktree list --porcelain
    if ($LASTEXITCODE -ne 0) { throw 'STOP: failed to inspect worktrees.' }

    Write-Host '--- Remote main, read-only, NO FETCH ---'
    $RemoteLine = @(git -C $Repo ls-remote origin refs/heads/main)
    if ($LASTEXITCODE -ne 0 -or $RemoteLine.Count -ne 1) {
        throw 'STOP: cannot uniquely resolve GitHub main.'
    }
    $ActualRemoteHead = ($RemoteLine[0] -split '\s+')[0]
    Write-Host "Reviewed GitHub main: $ReviewedRemoteHead"
    Write-Host "Live GitHub main:     $ActualRemoteHead"
    if ($ActualRemoteHead -ne $ReviewedRemoteHead) {
        throw 'STOP: GitHub main has moved; re-review G2 scope and exact source SHA.'
    }

    Write-Host '--- Isolated destination and branch collision checks ---'
    if (Test-Path -LiteralPath $CandidateWorktree) {
        throw "STOP: destination already exists: $CandidateWorktree"
    }
    $LocalBranchExists = @(git -C $Repo branch --list $Branch)
    if ($LASTEXITCODE -ne 0 -or $LocalBranchExists.Count -ne 0) {
        throw "STOP: branch already exists locally: $Branch"
    }
    $RemoteBranchExists = @(git -C $Repo ls-remote --heads origin $Branch)
    if ($LASTEXITCODE -ne 0 -or $RemoteBranchExists.Count -ne 0) {
        throw "STOP: branch already exists remotely: $Branch"
    }

    Write-Host 'PREFLIGHT_RESULT=PASS_READ_ONLY'
    Write-Host 'No branch/worktree created; no source modified.'
    Write-Host 'G2_NOT_AUTHORIZED_UNTIL_SEPARATE_OWNER_APPROVAL'
}
```

**Important:** This preflight verifies existence of protected files and read-only Git state, but owner must review unexpected **additional** untracked/tracked changes. The command itself cannot prove all other user files safe for writing; that is why no primary worktree mutation is allowed. In particular, the old local `main` is behind remote; no `git pull` on primary. `PREFLIGHT_RESULT=PASS_READ_ONLY` does **not** grant G2.

If `git ls-remote` cannot access the remote, STOP rather than substituting local `origin/main` stale ref.

## 5. Future G2 execution envelope (ONLY AFTER new explicit owner authorization)

**Proposed identity:**
- Repo: `Reltroner/reltroner-studio`.
- Exact base: `18b295f96ccb521b228a1855e79448158c09db15` **only if** live main still matches immediately before execution. Otherwise re-propose with the new reviewed SHA.
- Proposed branch: `phase1/w1-creator-reader-ia-20261012` (only if unique at execution).
- Proposed worktree: `C:\Projects\reltroner-studio-w1-ia` (must not already exist, separate from primary).
- Expected maximum source scope: the three exact TSX files in §2.
- Expected owner permission after distinct G2: create isolated worktree + branch at the exact **locally verified object** matching approved remote main; implement only allowlisted files; run tests solely in isolated worktree. No `fetch`, dependency install, push, preview, merge or deployment without explicit subauthorization. If the remote object is not available in the local Git object database, STOP and ask before performing network object retrieval; no historical SHA guessed. If a later authorized fetch is necessary, it must be a narrowly scoped, separately approved non-destructive transfer; do not casually `pull` primary.
- IDE coding agent (Gemini model available in owner's IDE) may implement **only after owner confirms G2 approval and exact worktree identity**. Agent should never operate in the primary checkout.

**Review checkpoints:** G2 owner decision → isolated worktree creation permitted → agent implementation only bounded source → local tests/run report → independent ChatGPT review → separate G3 PR/push permission and G4 Vercel preview → G5 main merge → G6 production release → G7 postdeploy evidence → G8 website Phase 1. Never interpret one step as authority for all others.

**No source push by default** because Vercel project is GitHub-integrated; a PR/branch push may trigger a Preview deployment consuming Hobby quota; a merge to main may automatically deploy production. Therefore stop for provider policy and owner approvals before network Git writes, even if the code tests pass.

## 6. Proposed Gemini IDE bounded implementation prompt (DO NOT RUN BEFORE G2)

```text
ROLE: Gemini IDE ENGINEER, STRICTLY SCOPED WORK ORDER RC-W1-01.
AUTHORIZATION: DO NOT START unless owner has shown explicit G2 approval
for exact SHA, branch, worktree path and three-file allowlist.

INPUT CONTRACT:
- Studio repository origin https://github.com/Reltroner/reltroner-studio.git
- Base SHA = 18b295f96ccb521b228a1855e79448158c09db15
  (STOP if live approved base differs).
- Worktree ONLY C:\Projects\reltroner-studio-w1-ia,
  branch phase1/w1-creator-reader-ia-20261012.
- NEVER work in C:\Projects\reltroner-studio primary.
- Edit ONLY:
  app/page.tsx
  components/ecosystem/EcosystemHero.tsx
  components/ecosystem/UseCasePathways.tsx
- Preserve 14 protected untracked Markdown files on primary.
- No secrets, network API, dependency install, provider changes, DNS, deploy,
  push, PR, merge, broad refactor or source content publication.

TASK:
1. Read the three files and the RC-W1-01 published contract.
2. Implement clear first-contact Creator and Reader primary entry CTAs with
   real preverified published destinations, secondary collaborator/recruiter
   discovery and retained LMS/HRM/app dock paths.
3. Keep TSX, semantics, focus states, responsive 320/375px and dark styling.
4. Distinguish real creative framework evidence and fictional universe lore.
   DO NOT promise paid course, mentorship, SLA or spoiler-free content without proof.
5. Do not change GA, contact, CSS globals, publishing filters or any other file.
   If needed, STOP and request a new owner-authorized file-scope amendment.
6. Before making any source edit, verify that git HEAD and worktree/branch
   match the owner-approved G2 envelope.
7. Run only explicitly approved local tests from this isolated worktree.
   Provide exact commands, exit codes, diff file list, screenshots at 320px
   and desktop and an unambiguous blocked/gap list.
8. Report all issues; no auto-fix outside allowlist and no automatic commit/push.
STOP immediately for source drift, broken route, unknown publication or spoiler
risk, changed primary drafts, unexpected build scripts, new cost or secret risk.
```

## 7. Test protocol and acceptance for later authorized candidate

**Test execution is NOT yet performed.** Proposed tests are permitted only if separately included in G2 owner authorization, on the isolated exact-SHA worktree.

| ID | Positive/negative acceptance | Verification |
|---|---|---|
| W1-IA01 | Hero offers two prominent and distinct Creator/Reader CTAs with accessible labels and accurate destinations | DOM/source + browser screenshots |
| W1-IA02 | Creator path reaches existing `published:true` framework or method proof; avoids fictional business promises | Source frontmatter + click/route |
| W1-IA03 | Reader orientation has honest fiction boundary and no surprise master-architecture spoilers; if unclear, BLOCKED | Content/readability review + click/route |
| W1-IA04 | Secondary engineering/collaborator path remains reachable, not labelled fictional | Browser route + source |
| W1-IA05 | Existing Ecosystem, `#app-dock`, `#knowledge-bridge`, LMS/HRM, footer and mobile nav are not broken | Smoke interaction desktop & 320/375 |
| W1-IA06 | Keyboard Tab/Shift+Tab, focus visibility, link names and 200% zoom do not hide required actions | Browser interactive checks |
| W1-IA07 | No horizontal overflow, no hidden CTA due to mobile fixed header at 320×480 and 375×812 | Viewport metrics/screenshot, inspect clipping |
| W1-IA08 | Changed files exactly allowlist, no new dependencies, no owner draft paths touched, no accidental secrets | `git status`, `git diff --name-only`, `git diff --check`, author QA |
| W1-IA09 | TS typecheck, content validate, production build and sitemap only if approved in worktree | `npm run typecheck`, `npm run content:validate`, **one** `npm run build` after near-final candidate |
| W1-IA10 | Negative tests: wrong/nonexistent route, draft URL, unrelated global nav regression, invalid anchor and class/wrapping failure | Source/route tests within allowed surfaces |
| W1-IA11 | No email, analytics consent fix claim, AI inference, DNS mutation, preview cost or unwanted Vercel build | Diff and process evidence |
| W1-IA12 | Source/reviewer evidence at exact SHA and PR/candidate rollback concept | Bounded review receipt before G3 |

**Important testing trade-off:** Next/Vercel historically generated 440 pages in about 5 minutes; avoid repeated full builds. The last production build's 440/440 is a **historical baseline**, not test evidence of this future W1 candidate. Do not run `npm run build:clean` or `npm run clean`; cleaning `.next` on any checkout can destroy user generated data and is not required for W1.

## 8. Negative STOP gates and downstream debt

- Any of the 18 WEB invariants weakened; any of the 27 acceptance criteria silently waived.
- Any edit outside 3 approved TSX files, any content draft publication/taxonomy shortcut, dependency change or SSR behavior creep.
- Unable to find spoiler-aware published Reader path without user-visible risk disclosure.
- Primary checkout touched, 14 original protected files absent/overwritten, source branch/HEAD drift or worktree path collision.
- Any unexpected network/paid dependency, auto-upgrade, Vercel-preview deploy triggered unintentionally, privacy breach, key/token in output, or route 404 introduced.
- Do not suppress existing live P1 issues: GA pre-consent tracking (W4), Resend domain DNS Failed (W6), image 404 (W3), pending Workers AI entitlement (W5), mobile reCAPTCHA clipping (W6/W7).
- Typecheck/build/lint failure not reasonably attributable to scope must be classified and presented, never "fixed" by altering global config outside allowlist.

Rollback plan before G3: preserve base SHA, work only in isolated candidate; revert candidate via explicit approved branch/worktree procedures if necessary. Never `git reset --hard` or `git clean -fd` in primary.

## 9. Distinct owner G2 decision (NOT YET GIVEN)

This work order is **READY_FOR_OWNER_REVIEW**, not approved. Only after reviewing live main SHA and safe local preflight may the owner approve bounded code work. Suggested exact authorization statement:

```text
Saya menyetujui G2 RC-W1-01 hanya untuk
Reltroner/reltroner-studio SHA 18b295f96ccb521b228a1855e79448158c09db15,
branch phase1/w1-creator-reader-ia-20261012,
worktree C:\Projects\reltroner-studio-w1-ia,
tiga file app/page.tsx, components/ecosystem/EcosystemHero.tsx,
components/ecosystem/UseCasePathways.tsx,
dan pengujian lokal pada worktree terisolasi sesuai RC-W1-01,
dengan syarat read-only preflight PASS dan SHA tidak drift.
Saya TIDAK mengizinkan perubahan primary, DNS/provider,
dependency install, push/PR/preview, merge atau production deploy.
```

**Until the owner actually gives a distinct G2 decision: `W1=PLANNED_NOT_EXECUTED`, no source writes, no worktree creation and no Gemini code execution.**
