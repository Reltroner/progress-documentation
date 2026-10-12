# RC-W1-14 — PowerShell 5.1 Native Node `-e` Quoting Precondition STOP; Safe One-Path Restore Fix

> **Owner evidence:** Windows PowerShell output `2026-10-12T22:22:25.6974848+07:00`, isolated W1 worktree `C:\Projects\reltroner-studio-w1-ia`. This is *owner-reported local execution*, not direct reviewer access to Windows.
> **Current gate:** `G1=APPROVED`, `G2=APPROVED/SOURCE_PASS_SCOPED`, `G2_QA_INSTALL/TYPECHECK/CONTENT/BUILD=PASS`, `RC_W1_11/12_ONE_PATH_RESTORE=OWNER_APPROVED`, `RESTORE_EXECUTION=STOP_BEFORE_MUTATION`, `BROWSER_QA=HOLD`, `G3..G8=NOT_AUTHORIZED`.
> **Authority:** [RC-W1-12 exact owner-approved one-file restoration](./RC-W1-12-owner-approved-generated-next-env-restore-and-local-browser-qa-20261012.md), [RC-W1-11 independently classified one-line Next.js types import](./RC-W1-11-generated-next-env-one-line-diff-confirmed-and-one-file-exception-proposal-20261012.md), [RC-W1-13 agent preflight HOLD](./RC-W1-13-qa-agent-preflight-blocked-restore-not-executed-and-http-smoke-evidence-20261012.md).
> **Source baseline:** `Reltroner/reltroner-studio` HEAD `18b295f96ccb521b228a1855e79448158c09db15`, historically verified on GitHub; primary historical HEAD `d6969ddfbc5e7d98d49b1523259785125159e722`.
> **Security/permissions:** No new owner authorization is needed to correct a read-only precondition defect in already-ratified one-file restoration; **no enlargement** of the mutation scope. Do not allow npm install, build rerun, reset/clean, PR/preview/deployment, provider/AI actions or primary author-file modifications.

## 1. Exact observed failure (before any write)

The owner ran the original `RC-W1-12-G2-QA-one-path-restore-20261012.ps1` block. It reached the JavaScript content precondition:

```powershell
& node -e $VerifyJavaScript $Repo
if ($LASTEXITCODE -ne 0) { throw 'STOP: generated file content precondition failed' }
```

Node printed:

```text
=== RC-W1-12 APPROVED SINGLE-FILE RESTORE ===
2026-10-12T22:22:25.6974848+07:00
STOP: next-env.d.ts has changes beyond the approved one-line generated import
STOP: generated file content precondition failed
```

The script did **not** print `NEXT_ENV_GENERATED_DIFF=EXACT_ONE_LINE_PASS`, `RC_W1_12_PRE_RESTORE=PASS`, or `RC_W1_12_NEXT_ENV_RESTORE=PASS`. The sole `git restore --source=HEAD --worktree -- next-env.d.ts` command occurs **later**, after the failed guard. Therefore this console execution stopped **before restoration**; it is not a failed Git restore. Existing source state should remain the original three approved TSX patches plus the one generated `next-env.d.ts` delta, subject to fresh preflight.

**Likely script-level root cause (not directly verified under Windows PS5.1):** Windows PowerShell 5.1's legacy native executable argument handling can strip or alter embedded double quotes in a multiline `node -e $VerifyJavaScript` argument. The JavaScript guard compares full strings that themselves include `"\..."`; if those double quotes are lost in the forwarded JS source, the `split(from)` check fails even when the file's diff is exactly the previously verified one-line import change. Alternative causes (actual source bytes/line endings changed) remain possible; the patched preflight will refuse unexpected differences. Do not claim conclusive quoting diagnosis without a direct native-argument trace.

## 2. Corrected external operator artifact — RC-W1-12R

**Script filename:** `RC-W1-12R-G2-QA-one-path-restore-PS51-fix-20261012.ps1`.

**SHA-256:** `1183d81e424e012e1f06ce69b6b179c43d47e9ff1dd604d7e943e49e738e3cc5`.

**Lines:** 169. External to both Git repositories; statically reviewed in this conversation, **not independently executed in Windows PowerShell 5.1**.

It is derived from owner-approved RC-W1-12 and replaces **only the fragile `node -e` content comparison** with:
- `git show HEAD:next-env.d.ts` baseline lines collected by the PowerShell-native command helper;
- current local `next-env.d.ts` lines via .NET `[System.IO.File]::ReadAllLines(..., [System.Text.Encoding]::UTF8)`;
- equal line-count gate plus **case-sensitive, line-for-line comparison** of all file lines, expecting exactly one baseline line `import "./.next/dev/types/routes.d.ts";` and current line `import "./.next/types/routes.d.ts";`;
- `git diff --numstat -- next-env.d.ts` still required to be exactly `1\t1\tnext-env.d.ts` to catch unapproved substantive differences. The line comparison treats LF and CRLF as equivalent; this is deliberate because Git's line text output and .NET ReadAllLines strip newline delimiters.
- only after these checks PASS, the **one same previously approved, exact-path** `git restore --source=HEAD --worktree -- next-env.d.ts` is reached.

**Other unchanged guards:** exact branch, worktree and primary SHA, origin and 2-worktree topology, exact four pre-restore status paths, exact 14 untracked owner files and 3 source TSX file hashes, package/lock hashes and stable Git refs, exact three post-restore modified paths and no generated-file diff. Unexpected status => STOP. No reinstall, build, cleanup or retry from STOP.

**Success markers expected (not yet observed):**

```text
NEXT_ENV_GENERATED_DIFF=EXACT_ONE_LINE_PASS
RC_W1_12_PRE_RESTORE=PASS
RC_W1_12_NEXT_ENV_RESTORE=PASS
G2_QA_SOURCE_STATUS=EXACT_THREE_TSX
G2_QA_PRIMARY_14=HASHES_UNCHANGED
G2_QA_BROWSER=AUTHORIZED_LOCALHOST_ONLY
```

Owner procedure: save external script in Downloads, inspect with Notepad, copy full contents into a non-admin PowerShell 5.1 shell and run **once**. Do **not** rerun the original `node -e` script, or use unguarded `git restore`. If the updated checks fail, STOP without assuming the cause.

## 3. Remaining QA

Prior actual `npm ci` exit 0, `tsc` exit 0, content validator 0 errors/371 warnings, and Next production build 440/440 pages exit 0 remain valid. Do not repeat. After the owner supplies the actual RC-W1-12R restore PASS and fresh status, resume localhost browser QA as already approved, 320/375/768/1440 viewport, 200% zoom, focus/ARIA, Creator/Reader/Collaborator routes and negative HTTP. Browser agent must limit file reads to approved worktree and evidence; never inspect unrelated private files. Third-party analytics blocker must be in effect before first navigation, and no forms/authenticated services should be submitted.

**Current state:** `ROOT_CAUSE_SCRIPT_NATIVE_ARGUMENT_QUOTING=SUSPECTED`; `RC_W1_12R_FIX=READY_NOT_EXECUTED`; `NEXT_ENV_RESTORE=NOT_VERIFIED`; `W1_BROWSER=HOLD`; `G3..G8=NOT_AUTHORIZED`; `WEB_PHASE1=NOT_ACCEPTED`; `PHASE2=NOT_ACTIVE`.
