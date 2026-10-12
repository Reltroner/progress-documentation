# RC-W1-20 — Owner Local Five-Path TSX Patch PASS; New-Routes Build & Browser Validation Next

> **Owner evidence:** user-provided Windows PowerShell output from `node "$env:USERPROFILE\Downloads\RC-W1-19-apply-dedicated-creator-reader-routes-20261013.cjs"`. This is a real **owner-reported source execution receipt**, not independently run by reviewer on Windows.
> **Current:** `RC_W1_19_PREFLIGHT=PASS`, `RC_W1_19_PATCH=PASS`, `SOURCE_SCOPE=EXACT_THREE_MODIFIED_PLUS_TWO_UNTRACKED_TSX`, `PRIMARY_14=HASHES_UNCHANGED_DURING_SCRIPT`; `RC_W1_20_TYPECHECK/CONTENT/BUILD=NOT_EXECUTED`, `NEW_TSX_BROWSER=NOT_EXECUTED`, `G3_SOURCE_PR=NOT_STARTED`, `PHASE1=NOT_ACCEPTED`.
> **Authority:** [owner ratified TSX CTA correction and cross-workstream execution governance](../08-owner-execution-authority-and-dedicated-creator-reader-tsx-adr-20261013.md), [18 WEB invariants](../00-ratified-frontend-architecture-contract-20261012.md), [27 WEB acceptance criteria](../03-phase1-acceptance-and-invariant-traceability.md). No code was committed by this documentation change.
> **App baseline:** Studio `main` verified at `18b295f96ccb521b228a1855e79448158c09db15`; isolated operator branch `phase1/w1-creator-reader-ia-20261012` at same HEAD, local W1 worktree `C:\Projects\reltroner-studio-w1-ia`. Primary `C:\Projects\reltroner-studio` has 14 protected untracked Markdown. Existing Next.js build from prior W1 source **is stale for the two new pages**.

## 1. Evidence from owner console (observed, not expected)

```text
=== RC-W1-19 OWNER-ORDERED TWO DEDICATED TSX ROUTES ===
RC_W1_19_PREFLIGHT=PASS
RC_W1_19_PATCH=PASS
RC_W1_19_NEW_ROUTES=/start/creators,/start/readers
RC_W1_19_MODIFIED_EXISTING=components/ecosystem/EcosystemHero.tsx
RC_W1_19_PRIMARY_14=HASHES_UNCHANGED
RC_W1_19_GIT_STATUS=THREE_MODIFIED_TSX_PLUS_TWO_UNTRACKED_TSX
RC_W1_19_TESTS=NOT_EXECUTED
NO_INSTALL_NO_BUILD_NO_COMMIT_NO_PUSH_NO_PREVIEW_NO_DEPLOY
```

Exactly **five source paths** form the current local W1 candidate:
- Modified tracked `app/page.tsx`, `components/ecosystem/EcosystemHero.tsx`, `components/ecosystem/UseCasePathways.tsx`.
- Newly created **untracked** `app/start/creators/page.tsx` and `app/start/readers/page.tsx`.

The W1 Hero CTAs now target two dedicated public TSX onboarding routes rather than opening existing Markdown articles directly. Creator may then choose published creative-practice articles; Reader gets a fiction-boundary introduction before optionally entering lore-bearing glossary/series. Existing Markdown remains canonical authored content, not a UI first-contact landing page. No *new runtime PASS* can be inferred from earlier 440-page build or old browser captures.

## 2. Next operator work order — minimal local validation, previously ratified scope

**Artifact:** `RC-W1-20-isolated-five-file-local-validation-20261013.ps1`, SHA-256 **`51eff97e5dc177e45cc8e5de3a3d74cbbdd41445c40858bd8022128020965399`**, 181 lines. Created externally to Studio. **Statically reviewed, not executed in Windows PowerShell 5.1**. Operator should inspect before paste; no claim of native Windows integration validation.

Before running: stop any existing `next start` on local port 3101 with Ctrl+C. The script refuses to build while the port remains occupied. It verifies expected local branch/HEAD/origin, initial exact five-path status (three M + two ??), primary protected 14 Markdown, installed existing node_modules, expected links/Reader ARIA and hashes/refs. It runs once each in isolated worktree:
1. `npm.cmd run typecheck`;
2. `npm.cmd run content:validate`;
3. `npm.cmd run build` (Next + next-sitemap via postbuild).

**No `npm ci` or package changes.** The previous build validates the old code; one fresh build is necessary for newly added App Router routes. Warnings from content:validate are recorded as warnings, not hidden. If any command fails, STOP without rerun or cleanup. After successful build, exact five-file status, byte hashes of protected files/source and ref stability are checked.

**Generated Next file:** Next can regenerate tracked `next-env.d.ts` with a dev → prod route-types import. If and only if this is the **entire** one-line diff (`1 added/1 removed`), script restores *that exact generated file only*, within the owner's already ratified nonproduction implementation and generated-file recovery envelope. If diff or status deviates, STOP; no general restore/reset/clean.

Expected success markers (not yet seen):

```text
RC_W1_20_PREFLIGHT=PASS
RC_W1_20_SOURCE_FIVE_PATHS=VERIFIED
RC_W1_20_TYPECHECK_EXIT_CODE=0
RC_W1_20_CONTENT_EXIT_CODE=0
RC_W1_20_BUILD_EXIT_CODE=0
RC_W1_20_NEXT_ENV_RESTORE=PASS|NOT_NEEDED
RC_W1_20_LOCAL_VALIDATION=PASS
RC_W1_20_FIVE_FILE_INTEGRITY=PASS
RC_W1_20_PRIMARY_14=UNCHANGED
RC_W1_20_BROWSER=READY_LOCALHOST_3101
```

Do not count expected markers as actual results until operator pastes console.

## 3. Follow-on targeted browser acceptance

After source/build output PASS: start one production-mode localhost server `npm.cmd run start -- --hostname 127.0.0.1 --port 3101`; configure/verify block of Google Analytics/Tag Manager tracking **before** browsing (W4 remains open). Verify homepage primary CTA actual click navigates respectively `/start/creators` and `/start/readers`; both return 200 with authored TSX orientation, unique metadata, correct breadcrumb/home navigation and accessible keyboard focus. Creator secondary links to published `/blog/no-copypaste-worldbuilding`/`creative-lore-bible` succeed. Reader does not reveal named canon plot spoilers before opt-in; Reader warning `aria-describedby` exists and optional glossary navigates only after deliberate click. Test 320×480, 375×812, 768×1024, 1440×900 (true viewport API), 200% zoom, Tab/Shift+Tab, zero overflow, collaborator link/LMS/HRM href unchanged. Inspect console/hydration/404, no external clicks, no form submits. Report actual evidence; no need to replay entire earlier W1 article QA.

**W1-18 separate evidence:** the user previously attached text report with correlated CDP viewport metrics and an exported ZIP name, but new ZIP binary wasn't delivered in that turn; classify as `AGENT_REPORTED_PASS_SCOPED`, pending independent bytes review. It covered prior W1 UI and does not validate these new TSX pages.

## 4. G3 and overall status

Previous [RC-G3-00](./RC-G3-00-separate-w1-source-pr-decision-packet-pending-owner-20261012.md) exact three-file scope is superseded by *five* existing/new W1 paths. Owner can direct Git commit/PR explicitly under ADR-008, but source patch PASS is not an automatic instruction to commit/push, invoke Vercel Preview, merge or deploy. Vercel auto-preview risk must be checked before pushing a PR. Prior owner G1/G2 statuses and all website invariants remain binding.

Current `W1_NEW_TSX_SOURCE=LOCAL_PATCH_PASS`, `W1_NEW_TSX_RUNTIME=UNTESTED`, `G3=NOT_STARTED`, `W2..W7=OPEN`, `WEBSITE_PHASE1=NOT_ACCEPTED`, `GLOBAL_PHASE1=NOT_EXITED`, `PHASE2=NOT_ACTIVE`.
