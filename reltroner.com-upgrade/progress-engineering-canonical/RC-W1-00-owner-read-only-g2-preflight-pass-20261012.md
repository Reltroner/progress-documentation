# RC-W1-00 — Owner G2 Read-Only Local Workspace Preflight Receipt (PASS_SCOPED)

> **Observed time:** 2026-10-12T18:12:27.8216400+07:00 from owner PowerShell 5.1 output.
> **Evidence class:** OWNER_EXECUTED_WINDOWS_POWERSHELL_OUTPUT, not independent remote access to the owner's PC.
> **Authorized stage:** G1 approved and W0 discovery closed with accepted residuals; **G2 source implementation NOT approved**. This receipt is evidence/archive only.
> **Parent:** [RC-W0-10 owner G1 signoff](./RC-W0-10-owner-g1-ratification-and-discovery-closure-20261012.md) and [RC-W1-01 proposed G2 work order](./RC-W1-01-proposed-g2-first-contact-creator-reader-ia-work-order-20261012.md).
> **Source:** `Reltroner/reltroner-studio`; last independently checked remote `main` SHA from GitHub connector remains `18b295f96ccb521b228a1855e79448158c09db15`; source and resource repos were NOT changed by this archive.
> **Decision:** `G2_PREFLIGHT=PASS_READ_ONLY`, `W1_WORKTREE=NOT_CREATED`, `G2_APPROVAL=PENDING_OWNER`, `W1_CODING=NOT_STARTED`.

## 1. Exact owner-observed operator evidence

Owner executed the full preflight described in RC-W1-01 in Windows PowerShell 5.1. Key output:

| Inspection | Observed | Reviewer disposition |
|---|---|---|
| Wall clock | `2026-10-12T18:12:27.8216400+07:00` | Timed owner-reported snapshot |
| Local primary checkout | `C:\Projects\reltroner-studio` | Exists; command completed |
| Origin URL | Script required exactly `https://github.com/Reltroner/reltroner-studio.git` and proceeded without STOP | MATCHED per operator script |
| Branch | `main` | EXPECTED |
| Local primary HEAD | `d6969ddfbc5e7d98d49b1523259785125159e722` | Historical local main; deliberately not advanced |
| Local tracked modifications | none shown by `git status --porcelain=v1 --untracked-files=all` | NONE_OBSERVED |
| Local untracked | exactly 14 lines in `content/music/` (12) and `content/places/` (2) | PRESERVED_OWNER_ASSETS; NOT TO STAGE/CLEAN |
| Protected existence | `Protected files found: 14` | PASS scoped presence only, not SHA/integrity of bytes |
| Worktree list | single `C:/Projects/reltroner-studio`, `HEAD d6969dd...`, `refs/heads/main` | No pre-existing second worktree |
| `git ls-remote origin refs/heads/main` | expected = actual `18b295f96ccb521b228a1855e79448158c09db15` | PASS exact remote-head match at test time |
| Proposed worktree | `C:\Projects\reltroner-studio-w1-ia` collision check passed | No existing directory at test time |
| Proposed branch | `phase1/w1-creator-reader-ia-20261012` local and remote branch collision checks passed | Branch not yet created |
| Final script marker | `G2_PREFLIGHT=PASS_READ_ONLY` | Valid completion marker; not implementation authorization |

**Important:** Local `main` being behind remote is expected, NOT a requirement to update it. No `git pull`, `git reset --hard`, `git clean`, or write to protected Markdown is allowed. The owner output does not prove content hashes of protected files; it proves the files exist, and the porcelain output shows no tracked changes and only the previously listed 14 untracked files.

## 2. Remaining distinct readiness checks before any future G2 implementation

**Still unknown:** Whether the exact remote commit object `18b295f...` already exists inside the local Git object database. `git ls-remote` reports remote ref; it does NOT download commit objects. A proposed isolated `git worktree add ... 18b295f...` would require the exact commit object locally. If absent, STOP and seek separate narrow authorization for non-destructive `git fetch`, without touching the primary branch/working tree. Do not use `git pull` in the primary checkout.

**Before any worktree writes:** owner must explicitly approve G2 based on the exact source SHA, worktree path, branch name, allowlist, and local tests in RC-W1-01; perform a fresh remote-ref and no-collision preflight if material time elapses. Keep Vercel GitHub branch/PR preview triggers out of G2 by default, unless separately authorized.

**Risk still open:** Studio W3 image 404, W4 pre-consent GA tracking, W5 AI entitlement, W6 Resend/DNS, W6/Web3Forms, native 320px reCAPTCHA clipping, broader W2/W7 accessibility/publication/cost tests. G1 owner decision did not waive any of the 27 WEB-AC.

## 3. Safe optional next single check (read-only), G2 implementation not yet authorized

Owner may execute the following **only to confirm local commit object availability**, without fetch, branch or workspace mutation:

```powershell
& {
  $ErrorActionPreference = 'Stop'
  $Repo = 'C:\Projects\reltroner-studio'
  $SHA = '18b295f96ccb521b228a1855e79448158c09db15'
  $Found = & git -C $Repo cat-file -t $SHA 2>$null
  if ($LASTEXITCODE -eq 0 -and ($Found | Out-String).Trim() -eq 'commit') {
    Write-Host 'G2_REMOTE_COMMIT_OBJECT=AVAILABLE_LOCALLY'
  } else {
    Write-Host 'G2_REMOTE_COMMIT_OBJECT=NOT_AVAILABLE_LOCALLY'
    Write-Host 'STOP: do not create a worktree or fetch without separate scope approval.'
  }
}
```

This command checks only existence/type of the Git commit object. It does **not** run a content integrity test, check the working tree or prove the proposed routes render. Report actual output only; never assume AVAILABLE.

## 4. Gate conclusion

- `G1=APPROVED`, `W0=DISCOVERY_CLOSED_WITH_ACCEPTED_RESIDUALS`.
- `RC-W1-00=PASS_SCOPED_OWNER_REPORTED`, **not** `G2=APPROVED`.
- `RC-W1-01=READY_FOR_OWNER_G2_REVIEW`, three-file TSX allowlist; only this work order's explicitly scoped candidate may be approved.
- `W1=PLANNED_NOT_EXECUTED`; `W2–W7=HOLD`.
- `G3–G8=NOT_AUTHORIZED`, `PHASE1=NOT_ACCEPTED`, `PHASE2=NOT_ACTIVE`.

**No source, Git branch/worktree, package, Vercel, provider, DNS, AI, email, billing, preview, merge or production action was authorized or performed by this receipt.**
