# RC-W1-09 — Owner-Approved G2-QA Amendment, Isolated npm Install and Local Tests

> **Gate:** `G1=APPROVED`, `G2=APPROVED`, **`G2-QA RC-W1-08=OWNER_APPROVED_NOT_EXECUTED`**, `W1=SOURCE_PASS_SCOPED_QA_PENDING`, `G3..G8=NOT_AUTHORIZED`.
> **Approval received:** 2026-10-12 Asia/Jakarta, exact user decision: “aku menyetujui G2-QA amendment RC-W1-08 untuk satu percobaan instalasi dependency yang dibatasi, dilanjutkan pengujian lokal hanya jika setiap pemeriksaan berhasil”.
> **Authoritative proposal:** [RC-W1-08](./RC-W1-08-proposed-g2-qa-isolated-npm-dependency-and-runtime-tests-20261012.md); [RC-W1-07R corrected preflight](./RC-W1-07R-successful-read-only-lockfile-toolchain-revalidation-20261012.md); [RC-W1-06 source review](./RC-W1-06-independent-source-review-g2-implementation-and-qa-blockers-20261012.md).
> **Immutable approved source base:** `Reltroner/reltroner-studio` `18b295f96ccb521b228a1855e79448158c09db15`. No approval to advance local `main` or edit author files.
> **Evidence status:** OWNER_CONVERSATION_DECISION; public GitHub source/lock separately read for script design. **No `npm ci`, build, localhost browser, Git source change, PR or production operation was executed by this documentation publication.**

## 1. Explicit authorization and boundaries

The owner has approved one carefully staged G2-QA execution on exactly the **already-existing** local `C:\Projects\reltroner-studio-w1-ia` feature worktree, branch `phase1/w1-creator-reader-ia-20261012`, at base `18b295f96ccb521b228a1855e79448158c09db15`:

1. Fresh read-only STOP-first verification (origin, remote main SHA, Git refs, both worktree topology, exact local branch/HEAD and **three** previously modified TSX paths).
2. Snapshot current SHA-256 hashes for all **14** originally untracked Markdown in primary checkout `C:\Projects\reltroner-studio`, plus three approved TSX files, lockfiles and refs, checking after each potentially writing stage. Do not access private file contents beyond local hash calculations, and do not publish hash values/contents if unnecessary.
3. Inspect Node `v22.23.1`, npm `10.9.8`, official public npm registry, `package-lock.json` `lockfileVersion=3`, package/lock root dependency specs and the unusual `learn-nextjs:"file:"` self-link. **No modification to this local link is authorized**.
4. **Exactly one** `npm.cmd ci --ignore-scripts --no-audit --no-fund --no-save` attempt in isolated worktree; public npm registry downloads and npm user cache writes are within this limited grant. `node_modules` must not exist when starting. On failure or changed protected files/source refs STOP without fallback, cleanup, retry or reinstall.
5. After `npm ci` exit 0 and full state verification, run `npm.cmd run typecheck`; if successful then `npm.cmd run content:validate`; if successful then **one** `npm.cmd run build` (Next.js plus `postbuild next-sitemap`), with generated files and source status audited before and after. Do not automatically repeat failing steps.
6. Only after successful toolchain/tests/build may the owner start the localhost Next UI and run bounded browser tests: true browser viewport 320×480, 375×812, 768×1024, 1440×900, 200% zoom, keyboard focus, Creator/Reader/collaborator CTA, route/anchors and negative cases. Device-toolbar emulation is not proof on a physical mobile device.
7. Return *actual* console outputs, exit codes, Git patch scope and browser evidence for independent review. **No W1 PASS / G3 approval is implied by script success alone.**

**Hard prohibited:** modifying three TSX files further without separate bounded issue/owner decision, `package.json`, `package-lock.json`, `bun.lock`, other source, any primary checkout files/14 author drafts, `git clean/reset/pull`, new branch/worktree, `npm install`, `npm cache clean`, `npm audit fix`, `bun install`, `npx`, developer tool upgrade, symlink/copy dependencies, npm lifecycle scripts, scripts with provider side effects, network AI inference, DNS/Resend/Web3Forms/Vercel payments, Git commit/push/PR, Preview, merge, deployment.

## 2. Operator script companion — downloadable to Downloads, not repository

The conversation supplies the file:

```text
RC-W1-08-G2-QA-approved-isolated-validation-20261012.ps1
SHA256: ba70e3f758ba97a28541dbd89d6938de9154ffbc67f6c37757fef244e07fca2b
```

The script is supplied as a downloadable **external** operator artifact; this GitHub document does not claim that a copy was committed into the Studio or documentation repo. On Windows: save to Downloads, inspect using Notepad, copy the entire text and paste into a non-admin PowerShell 5.1 session; no Execution Policy changes, no need to run `git pull`, no scripts written to Studio worktree. The script itself checks the allowlist, primary protected content, refs and exact source SHA; runs no installer unless every precondition passes.

Expected stage markers, conditional on actual execution:

```text
INVARIANTS_BEFORE_INSTALL=PASS
NPM_REGISTRY=OFFICIAL_PUBLIC
LOCKFILE_REGISTRY_AND_ROOT=PASS
NPM_CI_EXIT_CODE=0
INVARIANTS_AFTER_NPM_CI=PASS
TYPECHECK_EXIT_CODE=0
INVARIANTS_AFTER_TYPECHECK=PASS
CONTENT_VALIDATE_EXIT_CODE=0
INVARIANTS_AFTER_CONTENT_VALIDATE=PASS
BUILD_EXIT_CODE=0
INVARIANTS_AFTER_BUILD=PASS
G2_QA_LOCAL_TYPECHECK=PASS
G2_QA_CONTENT_VALIDATE=PASS
G2_QA_LOCAL_BUILD=PASS
G2_QA_BROWSER=READY_FOR_SEPARATE_LOCAL_TESTS
```

These are **target markers, not observed evidence**. If `STOP`, nonzero npm exit code, ref/primary/file hash mismatch, unexpected newly generated tracked files, inadequate disk, registry mismatch or request for private credentials: stop immediately. No automatic corrective commands are authorized. `--ignore-scripts` may prevent native modules from completing necessary setup; if so, stop and report.

Known network side effects: npm public registry package download and npm cache, plus local Next.js build may request Google Fonts. `npm run build` may invoke `next-sitemap` and write generated output in isolated worktree. The guard records and STOPs on unexpected tracked/untracked files; ignored `.next` build products may still be present. The script is designed for PowerShell 5.1 and reviewed statically, **not independently executed under Git for Windows in this conversation**.

## 3. Manual localhost browser QA is separate after build

If and only if all previous steps PASS, the owner may start local `npm run dev` in the isolated worktree (temporary ignored `.next` output permitted) and inspect `http://localhost:3000/`. Avoid contact sends, CAPTCHA solves, LMS/HRM login, external click navigation, external provider writes or API inference. Collect actual desktop DevTools measurements and keyboard results; external browser emulation is labeled as emulation. `Ctrl+C` stops dev server. Check Git status and 14 author hashes again after browser tests before any further source-stage request.

## 4. Gate disposition and completion requirement

`RC-W1-07R=PASS_SCOPED_READ_ONLY`; `RC-W1-08_OWNER_APPROVED`; **`RC-W1-09_EXECUTION=PENDING_OPERATOR_EVIDENCE`**. Prior `RC-W1-08 PENDING_OWNER` lines describe historic proposal state and are superseded by this ratification. G3 Source PR/Push, G4 Preview, G5 main merge, G6 production, G7/8 QA/release remain separate explicit approvals. W3 background.webp HTTP 404, W4 GA consent, W5 Workers AI free model entitlement and W6 Resend DNS/Web3Forms remain mandatory later workstreams. `WEB_PHASE1=NOT_ACCEPTED`, `PHASE2=NOT_ACTIVE`.
