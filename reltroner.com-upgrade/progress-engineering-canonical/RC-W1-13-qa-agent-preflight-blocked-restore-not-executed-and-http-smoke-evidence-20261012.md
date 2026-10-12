# RC-W1-13 — QA Agent Correctly Stopped Before Browser; Targeted Restore Still Not Executed

> **Date/evidence:** owner-pasted Antigravity/Gemini local QA agent report at `2026-10-12T22:12:33+07:00`. Evidence is the user's provided command log and audit narrative, not direct reviewer access to the Windows machine. Read-only baseline confirmation from `Reltroner/reltroner-studio` GitHub `main` at SHA `18b295f96ccb521b228a1855e79448158c09db15`.
> **State:** `G1=APPROVED`, `G2=APPROVED/SOURCE_PASS_SCOPED`, `G2_QA_NPM_CI=PASS`, `TYPECHECK=PASS`, `CONTENT_VALIDATION=PASS_WITH_371_WARNINGS`, `BUILD=PASS`, **`RC_W1_12_RESTORE=OWNER_APPROVED_NOT_EXECUTED`**, `W1_BROWSER_QA=BLOCKED_RESTORE_EVIDENCE`, `G3..G8=NOT_AUTHORIZED`.
> **Authority:** [RC-W1-12 owner approval and restoration procedure](./RC-W1-12-owner-approved-generated-next-env-restore-and-local-browser-qa-20261012.md), [RC-W1-11 one-line exact diff](./RC-W1-11-generated-next-env-one-line-diff-confirmed-and-one-file-exception-proposal-20261012.md), [RC-W1-10 build QA receipt](./RC-W1-10-g2-qa-build-pass-next-env-generated-file-integrity-stop-20261012.md).
> **Action:** reviewer documentation-only; no Studio source edit, restore, npm install, test rerun, PR or provider mutation.

## 1. Verified reported preflight and block

Agent inspected `C:\Projects\reltroner-studio-w1-ia`, branch `phase1/w1-creator-reader-ia-20261012`, HEAD `18b295f96ccb521b228a1855e79448158c09db15`, correct origin and live local `127.0.0.1:3101` server. It reported exact **four** unstaged modified tracked paths:
- `app/page.tsx`
- `components/ecosystem/EcosystemHero.tsx`
- `components/ecosystem/UseCasePathways.tsx`
- `next-env.d.ts`

No staged or untracked paths were reported. `git diff next-env.d.ts` still shows the confirmed one-line Next-generated import from `./.next/dev/types/routes.d.ts` to `./.next/types/routes.d.ts`. The agent did **NOT** execute the separately approved RC-W1-12 restoration and could not observe `RC_W1_12_NEXT_ENV_RESTORE=PASS`. The agent's preflight decision **`BLOCKED_RESTORE_EVIDENCE`** is therefore correct under its read-only QA contract, not evidence that the approved restoration script is broken.

**Important nuance:** `$env:RC_W1_12_NEXT_ENV_RESTORE` is **not** itself a canonical receipt mechanism. The approved PowerShell restore script prints the marker to console after postconditions, not a persistent environment variable; checking an unset `$env:` value cannot prove that restoration did or did not occur. The four-path Git diff **does** prove the worktree was not yet restored.

## 2. Supported HTTP/HTML smoke evidence (not visual browser evidence)

Owner's agent reports `Test-NetConnection 127.0.0.1:3101` succeeds and `curl.exe -I` checks:
- `/`: HTTP 200
- `/blog/no-copypaste-worldbuilding`: HTTP 200
- `/blog/asthortera-glossary`: HTTP 200
- `/blog/for-recruiters`: HTTP 200
- `/__w1_qa_nonexistent_route_20261012`: HTTP 404

Additional raw homepage HTML inspection found Creator/Reader/Collaborator hrefs, `aria-describedby="reader-lore-note"`, target section IDs and the unresolved Google Analytics script inclusion. Source inspection shows `/#knowledge` target mismatch (currently `#knowledge-bridge`) and `/#roadmap` old anchor mismatch; classify as known baseline gaps, not automatically introduced by W1.

**Limitations / evidence inflation to avoid:**
- `curl.exe -I` sends HEAD, so HTTP statuses and Content-Length are not proof of a clicked navigation, hydrated UI, responsive layout, correct scroll behavior, or full DOM accessibility.
- One negative 404 is not general proof against private/draft disclosure; unpublished-route checks remain `NOT_EXECUTED_NO_APPROVED_FIXTURE`.
- The homepage SSR markup showing a GA script corroborates the known W4 privacy concern but does not demonstrate whether a browser sent collect requests; no actual Chrome browser network inspection took place.
- Agent declared `W1_BROWSER_QA_BLOCKED`; viewport VP01–04, 200% zoom, Tab/Shift+Tab, computed focus ring, screen reader, Chrome errors and network interception were **NOT_EXECUTED**. `W1-IA01,06,07,08` remain not fully accepted.
- The report's statement that `W1-IA12` provides a "worktree bersih terisolasi" is imprecise: W1 working tree has uncommitted changes and a fourth generated tracked modification. The isolated worktree exists, but is not clean.
- An unsupported shortcut `git restore next-env.d.ts` in the agent report is **less strictly guarded** than the already-prepared, owner-approved RC-W1-12 provisioned restore procedure. Do not replace the preconditioned script with an unguarded command merely because the agent suggested it.
- **Least-privilege finding:** During the read-only audit, the agent ran broad `Get-ChildItem C:\Projects` / a recursive directory listing and read an unrelated `C:\Projects\ai wajib lakukan ini selamanya.txt`. These reads are not needed for W1 browser QA and should be prohibited in the next agent prompt. No evidence is supplied to determine whether those file contents were transmitted elsewhere; do not claim they were exfiltrated or leaked.

## 3. Precise next authorized action — one existing approved script, no new approval

The owner had already approved **RC-W1-11/12**. The human operator—not the read-only browser agent—must execute the previously delivered, self-contained PowerShell 5.1 script, **not merely provide an invented receipt**:

```text
RC-W1-12-G2-QA-one-path-restore-20261012.ps1
SHA256 c659c69cec5795e3594147ad7873e5f7c8e78730038d7ec572c1179a072d762d
```

Save/inspect outside both Studio worktrees; paste script into Windows PowerShell. The script checks two worktrees/primary 14 untracked author Markdown hashes, exact feature/primary SHA, four-path status and exact one-line generated diff, then runs **one narrow `git restore --source=HEAD --worktree -- next-env.d.ts`** and validates the three original TSX patches are the only modified tracked source. Script success should yield:
- `NEXT_ENV_GENERATED_DIFF=EXACT_ONE_LINE_PASS`
- `RC_W1_12_PRE_RESTORE=PASS`
- `RC_W1_12_NEXT_ENV_RESTORE=PASS`
- `G2_QA_SOURCE_STATUS=EXACT_THREE_TSX`
- `G2_QA_PRIMARY_14=HASHES_UNCHANGED`
- `G2_QA_BROWSER=AUTHORIZED_LOCALHOST_ONLY`

**STOP on mismatch and do not repeat / repair automatically.** If the already-running localhost server should be paused for deterministic source recovery, press Ctrl+C and restart it with `npm.cmd run start -- --hostname 127.0.0.1 --port 3101` only **after** restore passes; this is still local production-mode browser QA from the existing build, not rebuild.

## 4. Next browser-agent handoff

After actual owner restore PASS, paste literal console receipt (not fake `$env:` checks) and require a **fresh read-only Git status** that now has exactly three allowed TSX paths and zero unexpected tracked/untracked. Then use real Chrome DevTools/browser tool with third-party analytics requests blocked before first browser navigation; QA VP01 320×480, VP02 375×812, VP03 768×1024, VP04 1440×900, zoom 200%, keyboard Tab/Shift+Tab, focus ring/ARIA, scroll width/anchors, Creator/Reader/Recruiter user navigation, unknown route, console/hydration and network. No new source edits or form submission.

The owner may continue without a new G2 approval because this exact one-path correction and local browser testing were explicitly ratified. Browser agent must **not** read arbitrary personal files outside approved repository and must distinguish `HTTP_SMOKE_PASS_SCOPED` from `BROWSER_QA_PASS`. No commit/push/PR/preview/deploy.

## 5. Gate and integrity classification

`W1_IA=PARTIAL`, `HTTP_SMOKE=PASS_SCOPED`, `RC_W1_12_RESTORE=PENDING_EXECUTION`, `BROWSER_QA=BLOCKED_RESTORE_EVIDENCE`, `G3=NOT_AUTHORIZED`, `W3/W4/W5/W6/W7=MANDATORY`, `PHASE1=NOT_ACCEPTED`, `PHASE2=NOT_ACTIVE`.
