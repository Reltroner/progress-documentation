# RC-W1-11 — Verified One-Line Next.js Generated File Delta; Proposed One-Path G2-QA Restore Exception

> **2026-10-12 OWNER DECISION ADDENDUM:** The owner subsequently **APPROVED the exact one-path generated-file restoration and localhost browser QA**. See [RC-W1-12 owner ratification and execution envelope](./RC-W1-12-owner-approved-generated-next-env-restore-and-local-browser-qa-20261012.md). All `NOT AUTHORIZED` statements below concerning *only that specific future one-path restore* describe historical pre-approval status. **Operator restore and browser tests have not yet been observed.** G3–G8 remain HOLD.

> **Owner read-only evidence:** 2026-10-12T20:05:46.7875333+07:00, Windows PowerShell output `RC_W1_10_DIFF_PROBE=COMPLETE_READ_ONLY`.
> **Status:** `G1=APPROVED`; `G2=APPROVED`; `G2_QA_INSTALL=PASS`; `TYPECHECK=PASS`; `CONTENT_VALIDATION=PASS_WITH_WARNINGS`; `BUILD_EXIT_0=PASS`; **`POSTBUILD_INTEGRITY=HOLD_EXPECTED_GENERATED_DELTA`**; `BROWSER_QA=HOLD`; `G3..G8=NOT_AUTHORIZED`.
> **Provenance:** Owner read-only Git status, exact diff, HEAD baseline, working file and generated types existence. Reviewer independently fetched the frozen GitHub `next-env.d.ts` at `18b295f96ccb521b228a1855e79448158c09db15`, matching the owner baseline. No direct reviewer access to owner's local Windows checkout.
> **Predecessor:** [RC-W1-10](./RC-W1-10-g2-qa-build-pass-next-env-generated-file-integrity-stop-20261012.md), [RC-W1-09 approved G2-QA scope](./RC-W1-09-owner-g2-qa-approval-isolated-npm-ci-and-tests-20261012.md).
> **This documentation receipt grants NO additional source-edit/cleanup authority.**

## 1. Exact confirmed file delta

The owner reran a **read-only** four-path status/diff probe:
- `M app/page.tsx`
- `M components/ecosystem/EcosystemHero.tsx`
- `M components/ecosystem/UseCasePathways.tsx`
- `M next-env.d.ts`

The full diff of the fourth path is **one single generated TypeScript import**; header references and comments are unchanged:

```diff
--- a/next-env.d.ts
+++ b/next-env.d.ts
@@
-import "./.next/dev/types/routes.d.ts";
+import "./.next/types/routes.d.ts";
```

The owner's direct baseline (`git show HEAD:next-env.d.ts`) matches GitHub base file blob `c4b7818fbb2c2c34c24feb1b627ee824507c5600`. The worktree file has only the production mode generated import. `.next/types/routes.d.ts` exists, and `.next/dev/types/routes.d.ts` does not exist at time of probe. This matches the successful `next build` execution under Next.js 16.2.6.

**Classification:** `ROOT_CAUSE=CONFIRMED_NEXT_GENERATED_DEV_TO_PRODUCTION_TYPE_IMPORT`; **NOT** a fourth intentional W1 application feature, NOT a TypeScript error, NOT a failed Next build, NOT a source regression proved by evidence. The original G2 safety check **worked as designed** by flagging a tracked generated file outside the three-authorized-file allowlist.

## 2. Non-authorization and proposed exact remediation

The original RC-W1-08 approval explicitly forbade cleanup/restore outside the three TSX paths; do not silently treat this known benign-generated edit as newly authorized. The narrowest non-destructive correction for a future **explicitly approved** G2-QA exception is:
- Verify the same branch, HEAD, four-path status and exact one-line diff immediately before changes.
- **If and only if** the owner grants a one-path restoration exception, restore just `next-env.d.ts` from the currently approved local `HEAD` using `git restore --source=HEAD --worktree -- next-env.d.ts`. Do not stage it; no Git refs are to be changed.
- Recheck remaining status is exactly the three expected source TSX edits; confirm `next-env.d.ts` baseline blob and no other tracked changes. Avoid `git clean`, `git reset --hard`, `git rm --cached`, `.gitignore`/lock changes, deletes or installs.
- Keep prior tests and build recorded as PASS (their shell exit codes were 0; do not rerun merely to recover a generated declaration).
- Browser QA may then resume under the **existing** owner-approved RC-W1-08 local-host scope after correct integrity and direct operator confirmation. Prefer the **already-built local production server** (`npm.cmd run start`) if verified suitable; this tests the 440-page build and avoids relying on a fresh dev compilation and potential dev-mode regeneration. Starting localhost may still load third-party analytics scripts; do not click external providers or submit forms. Recheck status after stopping the server.
- This is a **proposed exception**, not a current permission to issue the restore command. If the file differs from the recorded one-line diff when checked again, STOP and ask for a new scope; do not overwrite unknown edits.

### Exact owner decision needed (NOT RECEIVED)

```text
Saya menyetujui pengecualian G2-QA RC-W1-11 untuk memulihkan
hanya next-env.d.ts di isolated worktree
C:\Projects\reltroner-studio-w1-ia dari HEAD yang sudah disetujui,
setelah verifikasi diff satu baris dan tepat empat modified paths.
Tiga TSX W1 dan 14 Markdown primary tidak boleh berubah.
Setelah tiga-file status kembali, lanjutkan QA browser localhost
sesuai RC-W1-08 tanpa npm ci, build, push, PR, preview, atau deploy.
```

## 3. Browser QA still needs independent evidence

No actual browser run was observed. Upon exact future approval and restored clean generated file, validate 320×480, 375×812, 768×1024, 1440×900 (browser emulation labeled correctly), zoom 200%, Tab focus, Creator/Reader CTAs and `aria-describedby`, current real published routes, `#app-dock`, `#knowledge-bridge`, no horizontal overflow, plus negative 404/draft route. Do not assume localhost `next start` means privacy/analytics are fixed; W4 P1 GA issue remains mandatory. `npm run start` may be used only within the approved local-only testing boundary; no public network access/paid service writes.

**Current gate:** `W1_SOURCE_PATCH=REVIEWED_PASS_SCOPED`; `G2_QA_LOCAL_TESTS=PASS_THROUGH_BUILD`; `POSTBUILD_INTEGRITY=KNOWN_BENIGN_GENERATED_DELTA_NEEDS_EXPLICIT_RESTORE`; `G2_QA_BROWSER=HOLD`; `G3=NOT_AUTHORIZED`; `PHASE1=NOT_ACCEPTED`; `PHASE2=NOT_ACTIVE`. All 27 WEB-AC and unrelated W3/W4/W5/W6/W7 risks remain unchanged.
