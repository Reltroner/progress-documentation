# RC-W1-12 — Owner-Approved G2-QA One-Path Generated File Restoration & Local Browser QA

> **Decision:** `G2-QA_RC-W1-11_EXACT_ONE_FILE_RESTORE=OWNER_APPROVED`; `BROWSER_LOCALHOST_QA=AUTHORIZED_CONDITIONALLY`; `RESTORE=NOT_YET_EXECUTION_VERIFIED`; `G3..G8=NOT_AUTHORIZED`.
> **Approval:** 2026-10-12 Asia/Jakarta; owner message: “aku menyetujui pengecualian G2-QA RC-W1-11 untuk memulihkan hanya `next-env.d.ts`, kemudian melanjutkan browser QA localhost sesuai scope G2-QA yang sudah disetujui”.
> **Authority:** [RC-W1-11 confirmed diff and exact proposal](./RC-W1-11-generated-next-env-one-line-diff-confirmed-and-one-file-exception-proposal-20261012.md), [RC-W1-09 original G2-QA approval](./RC-W1-09-owner-g2-qa-approval-isolated-npm-ci-and-tests-20261012.md), [RC-W1-10 test outcomes](./RC-W1-10-g2-qa-build-pass-next-env-generated-file-integrity-stop-20261012.md), [RC-W1-06 W1 source review](./RC-W1-06-independent-source-review-g2-implementation-and-qa-blockers-20261012.md).
> **Execution status:** This GitHub receipt is a decision/documentation commit, NOT a source checkout write. The owner has not yet provided the next PowerShell/browser results. No PR/push/preview/deploy.
> **Repository:** `Reltroner/reltroner-studio`; frozen base SHA `18b295f96ccb521b228a1855e79448158c09db15`; isolated `C:\Projects\reltroner-studio-w1-ia` branch `phase1/w1-creator-reader-ia-20261012`. Primary `C:\Projects\reltroner-studio` and 14 untracked author Markdown MUST remain protected.

## 1. Scope of explicit exception

**NOW PERMITTED, after STOP-first preflight:** Use `git restore --source=HEAD --worktree -- next-env.d.ts` targeted **only to** generated tracked `next-env.d.ts` in the isolated W1 worktree, **only if** all these checks still pass:
- exact branch/HEAD/worktree identity, expected origin and no surprise Git refs;
- four and only four unstaged modified tracked paths: `app/page.tsx`, `components/ecosystem/EcosystemHero.tsx`, `components/ecosystem/UseCasePathways.tsx`, `next-env.d.ts`; no staged or untracked source changes;
- complete actual `next-env.d.ts` content equals frozen `HEAD:next-env.d.ts` with **one exact generated import replacement** from `./.next/dev/types/routes.d.ts` to `./.next/types/routes.d.ts`; refuse if any extra change;
- snapshot SHA-256 hashes for the three intended TSX edits, all 14 protected owner Markdown files and package/lock files; ensure they remain untouched through the restoration;
- after one targeted `git restore`, source status must show only the original three TSX modified; `next-env.d.ts` must match frozen HEAD; unchanged Git refs and protected author files.

**No general `git restore` rights.** This approval does not allow a fourth new source feature. It is a generated-file cleanup exception **with an exact matched-content precondition**. If any check fails, STOP; never auto-clean, reset, remove or edit any file not precisely approved.

## 2. Validated QA already completed — do not rerun solely for this restoration

Owner previously reported:
- one `npm ci --ignore-scripts --no-audit --no-fund --no-save`: installed 263 packages, exit 0;
- TypeScript `tsc --noEmit`: exit 0;
- `content:validate`: exit 0, 0 errors, 371 warnings across 419 Markdown;
- `next build`: exit 0, 440/440 pages, 159.1s, `next-sitemap` postbuild;
- postbuild script strict source check STOPPED **only** because Next.js regenerated `next-env.d.ts` by changing its dev route-types import to production route-types import. Owner subsequently supplied an exact read-only one-line diff and confirmed `.next/types/routes.d.ts=True`.

These genuine results remain PASS/PASS_WITH_WARNINGS, not an argument for a second install or build. The earlier stopped script did not print `G2_QA_BROWSER=READY_FOR_SEPARATE_LOCAL_TESTS`; new specific restoration and browser evidence are required.

## 3. Browser QA after restoration and explicit local gating

**Conditional permission:** Only after the targeted restoration script reports `RC_W1_12_NEXT_ENV_RESTORE=PASS`, start the already built **local production server**, not a production deployment:

```powershell
Set-Location 'C:\Projects\reltroner-studio-w1-ia'
$env:NEXT_TELEMETRY_DISABLED = '1'
npm.cmd run start -- --hostname 127.0.0.1 --port 3101
```

This runs `next start` bound to loopback. A newly launched server may have network requests to public third parties embedded in client scripts (the unresolved W4 analytics gap); browser testing should block analytics/third-party URLs in Chrome DevTools **before** navigating if strict no-third-party request behavior is required. No external clicks/authenticated services/contact/email/CAPTCHA/AI/provider submission. Avoid `npm run dev`: it can regenerate the same tracked `next-env.d.ts`.

**Required browser matrix and honest evidence:**
- 320×480, 375×812, 768×1024, 1440×900 in browser DevTools responsive mode; label as **emulated viewport**, not physical device; test 200% zoom, horizontal overflow, header obstruction, first-fold CTA reachability, keyboard focus/Tab and focus visibility;
- Creator `/blog/no-copypaste-worldbuilding`, Reader `/blog/asthortera-glossary` with lore warning and `aria-describedby`, secondary collaborator `/blog/for-recruiters`; test localhost 200/404 handling and correct internal anchors `#app-dock`/`#knowledge-bridge`;
- Probe legacy `/#roadmap` and `/#knowledge` as **baseline navigation gaps**, not a basis to edit outside the three TSX work order;
- check negative unknown route; do not try to discover or publish unpublished draft content. Unavailable native physical-device, screen-reader and consent/cookie tests must be explicitly `NOT_EXECUTED` or scoped partial.
- Stop server with Ctrl+C and re-verify exact three-file Git status, generated file, primary protected paths and refs. If `next-env.d.ts` is regenerated by the local server unexpectedly, STOP for renewed inspection rather than rerunning restore blindly.

**QA data receipt:** record command, exit codes/HTTP response, viewport measurements, screenshot semantics, accessibility status, W1-IA01..12, remaining warnings, any network effects, full worktree status. `W1=PARTIAL` and `G3=NOT_AUTHORIZED` until this evidence is independently reviewed.

## 4. Explicit nonauthorization

No `npm ci` again, no `npm run build` again, no `npm run dev`, no package/lockfile/next.config modification, no generic cleanup, no `git reset`/`clean`/`pull`, no Git commit/push/PR, Vercel Preview, merge or deployment, no DNS/Resend/Web3Forms/AI/billing/provider activation, no primary owner author-file mutation. No new W2/W3/W4/W5/W6/W7 source work or waiver of 27 WEB-AC.

**Current state:** `RC-W1-11_OWNER_RESTORE_EXCEPTION=APPROVED`; `RESTORE_EXECUTION=PENDING`; `BROWSER_QA=AUTHORIZED_AFTER_RESTORE`; `G3..G8=HOLD`; `PHASE1=NOT_ACCEPTED`; `PHASE2=NOT_ACTIVE`.
