# RC-W1-08 — **PROPOSED** G2-QA Amendment: Isolated npm Dependency Installation and W1 Runtime/Browser Testing

> **OWNER APPROVAL REQUIRED; NOT YET AUTHORIZED.**
> Prepared 2026-10-12 Asia/Jakarta after [RC-W1-07R PASS_SCOPED read-only toolchain review](./RC-W1-07R-successful-read-only-lockfile-toolchain-revalidation-20261012.md).
> **Existing authority:** [RC-W1-03 G2 owner ratification](./RC-W1-03-owner-g2-ratification-and-isolated-execution-20261012.md), [RC-W1-06 independent source review](./RC-W1-06-independent-source-review-g2-implementation-and-qa-blockers-20261012.md); initial G2 **explicitly prohibited** dependency installation.
> **Proposal purpose:** complete reliable W1 local runtime acceptance **without** prematurely allowing Git push/PR, Vercel Preview, merge or production deploy.
> **Source baseline exact SHA:** `18b295f96ccb521b228a1855e79448158c09db15`, source repo `Reltroner/reltroner-studio`; branch `phase1/w1-creator-reader-ia-20261012`, isolated `C:\Projects\reltroner-studio-w1-ia`.
> **No mutation reported in this document.** No dependency install, build, source changes, provider calls or GitHub Studio actions were executed when drafting this proposed work order.

## 1. Evidence now available

- Owner `RC_W1_07R=COMPLETE_READ_ONLY` at `2026-10-12T19:28:58.7843168+07:00`: original three tracked TSX diffs, exact branch and SHA, no `node_modules`, C: `48.79 GB` free.
- Node `v22.23.1`, npm `10.9.8`, Bun absent. Both `package-lock.json` (npm lockVersion 3) and `bun.lock` exist; choose **one installer only: npm**.
- Root `package.json` and npm lock `packages[""]` both named `learn-nextjs`. **Zero root dependency-spec mismatches**. This is not a full lock tree/ABI compatibility proof.
- Nonstandard `"learn-nextjs":"file:"` appears in root dependency declarations and `lock.packages["node_modules/learn-nextjs"]={link:true,resolved:""}`; treat as **self-link caution**, not a proven failure and not a reason to edit root package.
- `app/fonts.ts` sources Inter/Sora/JetBrains Mono via `next/font/google`; `npm run build` uses `next build` and automatically invokes `postbuild=next-sitemap`. A production build can fetch free Google font assets, and postbuild can generate `public` sitemap/robots files. No claim of truly offline build. Never permit font-download fake mocks or replacing assets without separate approval.

## 2. Precisely scoped optional owner grant

If owner approves `G2-QA-RC-W1-08`, it grants ONLY:

1. A fresh read-only STOP-first preflight: origin, exact branch/base SHA, three-only changed tracked files, no untracked extra paths; protected primary local checkout not written and historical 14 owner Markdown unchanged (re-read hashes if baseline receipt accessible). Confirm `node_modules` still absent. Check public registry URL without printing npm auth, avoid leaking `.npmrc`/tokens. Confirm Node/npm as already observed. Reconfirm storage and package/lock root match.
2. **One** npm v10 lockfile-driven dependency installation attempt **inside the isolated worktree only**, with `--ignore-scripts --no-audit --no-fund --no-save` and no package manager swap or package/lockfile edits. Default npm cache may write to the normal user npm cache; npm registry network to public package tarballs is within this proposed approval only. Optional native packages may use remote tarballs, yet no cloud deployments/services, payment, or provider mutations are allowed. `--ignore-scripts` prevents dependency lifecycle scripts; do not remove this flag to fix failed native tools without separate approval.
3. Post-install **immediate comparison** to a before-snapshot: only existing three tracked TSX files may remain modified; `package.json`, `package-lock.json`, `bun.lock`, other source paths and Git refs must be unchanged. `node_modules` is ignored/generated under isolated worktree, not part of the source file allowlist. Any unexpected tracked/untracked path => STOP, report, **no auto-reset/clean/remove**.
4. If npm returns nonzero (including due to `file:` self-link), STOP, preserve exact error and status. **No fallback** to `npm install`, `npm cache clean`, `--force`, `--legacy-peer-deps`, Bun, lockfile rewrite, reinstall, symlink/copy from primary, or `--ignore-scripts=false`. Do not silently retry.
5. If local dependencies install correctly, execute once **`npm run typecheck`**, then **`npm run content:validate`**. Record exit code and any errors; classify existing unrelated errors without mass-refactor. Next a **single near-final `npm run build`** from the isolated worktree, only after confirming enough disk, route/publication assumptions and expected generated files; record exact build/postbuild exit code, duration, whether network fonts were fetched and whether sitemap/robots generated. `NEXT_TELEMETRY_DISABLED=1` may be set for local commands; do not change tracked env files.
6. Compare Git status and diff before/after every potentially writing command. If postbuild writes tracked `public/robots.txt`, `public/sitemap*.xml` or other nonallowlisted paths, STOP without cleanup and request explicit owner direction.
7. Only if dependencies/Next localhost start safely, run one bounded **local** browser QA at 320×480, 375×812, 768×1024, 1440×900, 200% zoom, keyboard Tab/Shift+Tab, CTA focus/ARIA descriptions, cross-links, anchor targets, and typical 404/draft negative cases. Do not submit contact/newsletter, access any authenticated LMS/HRM, solve production CAPTCHA, call AI, invoke paid cloud services or click external links unintentionally. Browser DevTools viewport emulation must be labeled as emulation, not physical-device proof.
8. Collect W1-IA01..12 table with actor/commands/exit codes, actual browser screenshot dimensions, immutable base and local diff status. Stop and return evidence for independent review. **No Git commit, Git push, PR, Preview or deploy.**

### Potential installation command after owner approval only (DO NOT RUN YET)

```powershell
# AFTER explicit owner amendment and fresh STOP-first preflight.
# Must run from approved isolated worktree, not primary.
npm ci --ignore-scripts --no-audit --no-fund --no-save
```

This is one bounded attempt, not a promise it succeeds. An `npm ci` invocation may remove/replace `node_modules` if already present; therefore require that directory to be absent at fresh preflight. It may write npm's external default cache; that is a known permitted side effect only within the newly approved amendment. Do not use default npm configuration output dumps that may contain credentials. Npm may contact public npm registry and system proxy; STOP if registry/network identity deviates from expected, do not send credentials.

### No allowance for broad destructive or provider commands

Do not run `git clean`, `reset --hard`, `pull` primary, `build:clean`, `npm run clean`, `npm install`, `npm update`, `bun install`, `npx`, dependencies via symlink, `npm audit fix`, dependency vulnerability auto remediation, external test deploys or uncontrolled browser crawls.

## 3. Mandatory STOP gates

- Any live source SHA drift / unexpected branch/worktree/modified source before running, or unexpected package manager lock/root mismatch.
- Any network access requiring payment, credentials, unknown private registry, or extra package-manager installation.
- `npm ci` fails: STOP, don't mutate package/lock automatically or reinstall; report exact error, no cleanup.
- Installation triggers unknown lifecycle or writes tracked nonallowlisted files.
- Build triggers provider/auth/emails, starts background services, creates tracked files outside allowlist, downloads unexpected data, or exceeds reasonable CPU/network/disk footprint.
- Browser QA cannot accurately measure required viewports or screen reader/focus: mark `NOT_EXECUTED` or `PARTIAL`, not PASS.
- Known W3 background image 404, W4 Google Analytics pre-consent risk, W5 model entitlement, W6 Resend missing DNS/Web3Forms remain deferred **mandatory** workstream blockers; do not solve them in this W1-only QA.

## 4. Proposed owner decision text — current status PENDING

```text
Saya menyetujui amendment G2-QA RC-W1-08 untuk
C:\Projects\reltroner-studio-w1-ia saja:
satu percobaan npm ci berbasis package-lock.json dengan
--ignore-scripts --no-audit --no-fund --no-save,
tanpa mengubah package.json/lockfile maupun primary,
kemudian typecheck, content:validate, satu build,
dan QA browser lokal jika semua preflight dan STOP gate lulus.
Jika npm ci gagal atau ada perubahan di luar scope, STOP tanpa cleanup.
Saya tidak menyetujui Git commit/push, PR, Vercel Preview,
merge, production, provider/DNS/API, atau instalasi tool lainnya.
```

Until owner explicitly approves, **`G2_QA_AMENDMENT=PENDING_OWNER`**, `W1_RUNTIME_QA=BLOCKED_DEPENDENCIES`, `G3..G8=HOLD`, `WEB_PHASE1=NOT_ACCEPTED`, `PHASE2=NOT_ACTIVE`.
