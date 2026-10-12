# RC-W1-15 — Successful RC-W1-12R One-File Restoration; W1 Browser QA Ready

> **Evidence:** Owner-supplied Windows PowerShell output at `2026-10-12T22:30:24.4662754+07:00`. Actor: owner local operator; script: `RC-W1-12R-G2-QA-one-path-restore-PS51-fix-20261012.ps1`. Reviewer has NOT executed any Windows commands against the owner's workstation. Output is an executed operator receipt, not a prior expected marker.
> **State:** `G1=APPROVED`; `G2_SOURCE_REVIEW=PASS_SCOPED`; `G2_QA_INSTALL/TYPECHECK/CONTENT/LOCAL_BUILD=PASS`; **`RC_W1_12R_RESTORE=PASS_SCOPED`**; **`BROWSER_QA=AUTHORIZED_READY_NOT_EXECUTED`**; `G3–G8=NOT_AUTHORIZED`; `PHASE1=NOT_ACCEPTED`; `PHASE2=NOT_ACTIVE`.
> **References:** [RC-W1-14 earlier PowerShell-5.1 guard STOP and corrected script](./RC-W1-14-ps51-native-node-e-quoting-stop-and-one-path-restore-script-fix-20261012.md), [RC-W1-12 approved exact restoration](./RC-W1-12-owner-approved-generated-next-env-restore-and-local-browser-qa-20261012.md), [RC-W1-13 browser agent blocked on missing restore](./RC-W1-13-qa-agent-preflight-blocked-restore-not-executed-and-http-smoke-evidence-20261012.md), [RC-W1-10 tests/build](./RC-W1-10-g2-qa-build-pass-next-env-generated-file-integrity-stop-20261012.md).
> **Immutable project baseline:** `Reltroner/reltroner-studio`, SHA `18b295f96ccb521b228a1855e79448158c09db15`; local W1 branch `phase1/w1-creator-reader-ia-20261012`; local isolated worktree `C:\Projects\reltroner-studio-w1-ia`; original primary worktree `C:\Projects\reltroner-studio` HEAD `d6969ddfbc5e7d98d49b1523259785125159e722`. Public GitHub Studio `main` remains the reviewed SHA as of documentation publication.

## 1. Operator-reported successful executed postconditions

Owner ran corrected PowerShell-5.1 script after original `node -e` argument handling problem was isolated. It read and compared every line of `HEAD:next-env.d.ts` to the worktree-generated file, expecting exactly one dev → production types import substitution, before executing the precise preapproved one-path Git restoration. The console printed:

```text
=== RC-W1-12R APPROVED SINGLE-FILE RESTORE (PS5 QUOTING FIX) ===
2026-10-12T22:30:24.4662754+07:00
NEXT_ENV_GENERATED_DIFF=EXACT_ONE_LINE_PASS
RC_W1_12_PRE_RESTORE=PASS
=== EXACTLY ONE OWNER-APPROVED RESTORE ===
RC_W1_12_NEXT_ENV_RESTORE=PASS
G2_QA_SOURCE_STATUS=EXACT_THREE_TSX
G2_QA_PRIMARY_14=HASHES_UNCHANGED
G2_QA_BROWSER=AUTHORIZED_LOCALHOST_ONLY
NO_NPM_CI_NO_BUILD_NO_COMMIT_NO_PUSH_NO_PR_NO_PREVIEW_NO_DEPLOY
```

**Meaning / scope:** The script post-restoration check found **exactly three modified tracked TSX files** `app/page.tsx`, `components/ecosystem/EcosystemHero.tsx`, `components/ecosystem/UseCasePathways.tsx`. `next-env.d.ts` is now unmodified relative to HEAD, and the script compared in-memory SHA256 before/after of those three TSX, `package.json`/`package-lock.json`/`bun.lock`, and all 14 untracked owner Markdown files on primary; protected 14 all unchanged **during this script invocation**. It also verified stable Git refs and expected primary status. No new commit/push/PR/deploy occurred in the provided script. Note: this is not a new cross-session comparison against the original provisioning hash receipt; the check is in-session.

This successfully supersedes the RC-W1-13 `BLOCKED_RESTORE_EVIDENCE` state. The old `node -e` script STOP remains a truthful historical event, but the corrected one-file cleanup is now complete. No new source modification authorization was granted.

## 2. Already executed tests preserved without rerun

The separate authorized G2-QA operator receipt previously showed:
- exactly one `npm ci --ignore-scripts --no-audit --no-fund --no-save`: 263 packages installed, exit 0;
- `npm run typecheck` exit 0;
- `npm run content:validate`: 0 errors, 371 warnings across 419 files, exit 0;
- `npm run build` Next 16.2.6: 440/440 static pages, postbuild sitemap, exit 0 (159.1 seconds).
These remain **LOCAL G2-QA scoped pass** and do **not** prove browser UX/GA consent/physical responsive behavior. **No second install or production build may be run without separate authorization.**

## 3. Newly unlocked, already owner-approved localhost browser QA

If the existing production-mode server is not still listening on `127.0.0.1:3101`, the owner may run the already-built output strictly bound to loopback:

```powershell
Set-Location 'C:\Projects\reltroner-studio-w1-ia'
$env:NEXT_TELEMETRY_DISABLED = '1'
npm.cmd run start -- --hostname 127.0.0.1 --port 3101
```

Wait for `Ready`; do not start a second server if one is already active. This is localhost only, **not** deployment. The browser agent must first recheck exact branch/HEAD, only the three modified TSX and clean `next-env.d.ts`, and must not demand a persistent `$env:RC_W1_12_NEXT_ENV_RESTORE` variable (the marker was emitted on the owner console). Owner has now supplied the real receipt, so `BLOCKED_RESTORE_EVIDENCE` no longer applies unless state changes.

Browser agent tasks:
- Use actual Chrome browser/DevTools or real browser automation; viewport emulation 320×480, 375×812, 768×1024 and 1440×900; zoom 200%; Tab/Shift+Tab and computed focus; first-fold Creator/Reader equal prominence and secondary collaborator; image/css errors; horizontal overflow `scrollWidth/clientWidth`.
- Verify Creator `/blog/no-copypaste-worldbuilding`, Reader `/blog/asthortera-glossary` and lore warning `aria-describedby="reader-lore-note"`, collaborator `/blog/for-recruiters`, `#app-dock`, `#knowledge-bridge` and one deliberate unknown-route 404. Record baseline `/#knowledge` and `/#roadmap` mismatches as W2/W7 follow-up, not automatic W1 implementation changes.
- W4 Google Analytics preconsent issue remains unresolved. Block tracking/analytics network requests **before first browser navigation**, with Chrome DevTools request blocking or equivalent. If interception cannot be confirmed before first navigation, STOP and ask for human setup. No contact/newsletter submits, external/authenticated LMS/HRM, API inference, provider/network mutations or paid cloud calls.
- Restrict agent filesystem reads to the approved isolated worktree and relevant QA evidence only. Previous agent inspected unrelated personal paths; that behavior is out of scope, not warranted merely because broad tool permissions exist. Label HTML `curl`/HEAD checks as HTTP smoke, not Chrome viewport proof. Report unsupported browser capabilities as `NOT_EXECUTED`.
- After browser QA stop server with Ctrl+C and verify the same three modified TSX, restored next-env, Git refs and owner-protected files where actually measured. No source edits or cleanup. Collect one consolidated W1-IA01..12 matrix + screenshots/viewport evidence and residual issue register for independent review.

## 4. Gate / release discipline

`RC-W1-15_LOCAL_RESTORE=PASS_SCOPED`; `G2_QA_BROWSER=READY_AUTHORIZED` but `BROWSER_TEST_RESULT=NOT_EXECUTED`; `W1_ACCEPTANCE=PARTIAL`; `G3=NOT_AUTHORIZED`; `G4–G8=HOLD`; `WEB_PHASE1=NOT_ACCEPTED`; `PHASE2=NOT_ACTIVE`. W3 image 404, W4 analytics privacy, W5 AI entitlement, W6 sender DNS/Web3Forms, W7 E2E and all 27 WEB-AC remain mandatory.
