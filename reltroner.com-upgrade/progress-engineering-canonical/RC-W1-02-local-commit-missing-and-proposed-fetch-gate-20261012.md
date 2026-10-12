# RC-W1-02 — Missing Local Commit Object, Narrow Git Fetch Plan, G2 Decision Pending

> **Recorded on 2026-10-12 Asia/Jakarta.** User supplied PowerShell console result after the 18:12:27 WIB preflight; the new probe did not output its own independent wall-clock timestamp.
> **Stage:** `G1_APPROVED`; `RC-W1-00_PREFLIGHT=PASS_SCOPED`; `G2_COMMIT_OBJECT=NOT_AVAILABLE_LOCALLY`; **`G2=NOT_AUTHORIZED`**.
> Evidence: OWNER_POWERSHELL_OUTPUT; reviewer separately checked GitHub Studio `main` on this date at `18b295f96ccb521b228a1855e79448158c09db15`. Owner's local PC cannot be accessed by the GitHub connector.
> Parent: [G1 ratification](./RC-W0-10-owner-g1-ratification-and-discovery-closure-20261012.md), [W1-00 protection/preflight](./RC-W1-00-owner-read-only-g2-preflight-pass-20261012.md), [W1-01 proposed scoped G2 work order](./RC-W1-01-proposed-g2-first-contact-creator-reader-ia-work-order-20261012.md), [workspace and release governance](../05-source-workspace-and-release-governance.md).

## 1. Observed output and exact diagnosis

Owner ran:

```powershell
$Repo = 'C:\Projects\reltroner-studio'
$SHA = '18b295f96ccb521b228a1855e79448158c09db15'
$Object = @(git -C $Repo rev-parse --verify --quiet "$SHA^{commit}")
```

Result:

```text
G2_REMOTE_COMMIT_OBJECT=NOT_AVAILABLE_LOCALLY
No fetch or worktree creation authorized.
```

**Implication:** GitHub main SHA exists as a remote advertised ref, but the Git *local object database* cannot resolve the exact commit object. This is consistent with the owner primary checkout being 11 commits behind remote. `git ls-remote` does not download objects. **No remote repository corruption, source loss or local reset is established by this output.** The prior read-only preflight remains PASS_SCOPED for the state it actually inspected, but **worktree creation at the reviewed exact SHA is currently blocked by missing object data**.

Status matrix:
- Remote GitHub `main`: SHA `18b295f96ccb521b228a1855e79448158c09db15`, observed at receipt time.
- Protected Windows primary `main`: `d6969ddfbc5e7d98d49b1523259785125159e722` in prior owner preflight.
- Protected untracked Markdown: 14 present in prior preflight; not rehashed by this object lookup.
- Proposed W1 branch: `phase1/w1-creator-reader-ia-20261012` — not created.
- Proposed isolated worktree: `C:\Projects\reltroner-studio-w1-ia` — not created.
- G2 source/coding permissions: **NOT GRANTED**.
- Source/app/provider/production changes: **NONE reported**.

## 2. Engineering decision: narrowly authorized fetch only, never pull/reset

Before the owner explicitly authorizes even this narrow write, **do not run the fetch command**.

After distinct written owner approval for `RC-W1-02` *object acquisition* (or explicit G2 approval containing this exact subpermission), perform these bounded checks and object transfer in **Windows PowerShell 5.1** from the owner's primary Git repository:
1. Check origin, primary `main` HEAD, exact 14 untracked and zero tracked modifications, active worktrees, no proposed branch/destination collisions, and remote `main` SHA; **STOP for any difference**. It is allowed to observe `git ls-remote`.
2. Confirm Git version recognizes `--no-write-fetch-head`, `--refmap=` and `--no-tags`; otherwise STOP (no flag stripping or fallback). Git official docs: https://git-scm.com/docs/git-fetch
3. If object remains absent, the proposed *narrow ref-less* Git fetch is:

```powershell
git -C 'C:\Projects\reltroner-studio' -c maintenance.auto=false -c gc.auto=0 fetch --no-tags --no-write-fetch-head --refmap= --no-recurse-submodules origin refs/heads/main
```

**Meaning:** only ask remote for `refs/heads/main`; an *empty* `--refmap=` disables automatic remote tracking ref mapping for this command; `--no-write-fetch-head` avoids writing `FETCH_HEAD`; `--no-tags` avoids tag auto-follow; automatic maintenance disabled. **It still writes the Git object database**, consumes network/download/storage, and cannot promise zero internal metadata changes. It is an operation on the primary repository's **shared Git data**, not on its tracked/untracked working-tree files. Using an explicit command-line refspec without `:<dst>` avoids an intended branch update. If command fails or unexpected refs/worktree change, STOP; do not automatically retry with `git pull`, `reset`, `clean`, `--force`, or `--unshallow`.
4. Verify the fetched exact object with `git rev-parse --verify --quiet "$SHA^{commit}"`, which must print the approved SHA, then re-run the original owner preflight and check all 14 path existence/content hashes against prefetch snapshot. Do not create worktree as part of a *fetch-only* approval.
5. If source main moves between read-only check and transfer, fetched object may be the **new main** instead. Compare fetched object to approved SHA and live remote ref after fetch; **STOP** and do not create worktree if drift detected. If object still unavailable, STOP for a new reviewed fetch plan.

Official Git documentation describes the fetch flags: https://git-scm.com/docs/git-fetch . The exact command/flag behavior should be tested against the installed Git version; no execution is claimed here.

## 3. Source isolation and efficient future authorization path

The owner can explicitly authorize in **one** narrowly defined future G2 decision: (a) read-only re-preflight, (b) the above fetch when exact object is absent, (c) verify exact SHA and protected files, (d) create only the proposed isolated worktree and unique branch, (e) allow IDE source modifications to only the **three TSX files** and approved local tests — **if and only if** every preceding check passes. This reduces round trips without collapsing risk gates. This is a **proposal only** until the owner states approval.

**W1 file allowlist (unchanged):**
- `app/page.tsx`
- `components/ecosystem/EcosystemHero.tsx`
- `components/ecosystem/UseCasePathways.tsx`

**Hard no even with bounded G2:** `git pull` in primary; `git reset --hard`; `git clean`; modify/add/stage 14 primary untracked Markdown; edit outside allowlist; dependency installs without further authorization; Git push, PR creation, Vercel preview, merge/main deploy, provider/DNS settings, billing/AI calls, production release. Worktree creation and IDE edits must NOT be inferred from permission for fetch alone.

Separate G3/G4/G5/G6 gates remain binding: GitHub push/PR may trigger Vercel Preview; main merge may trigger Production build. W3 image 404, W4 GA pre-consent risk, W5 AI entitlement, W6 sender DNS Failed and 27 WEB-AC production acceptance remain mandatory.

## 4. Owner authorization boundary (pending)

**Option A — approve fetch only:** explicitly approve `RC-W1-02` narrow object transfer and its read-only verification; no branch/worktree/source writes permitted.

**Option B — approve combined G2 scoped slice:** explicitly approve `RC-W1-01` implementation including the narrowly specified fetch subpermission, isolated worktree creation and 3-file source/test envelope; no dependency installs, Git push/PR/preview, merge, production or provider changes.

**Current status:** `G1=APPROVED`; `RC-W1-00=PASS_SCOPED`; `LOCAL_BASE_OBJECT=MISSING`; `G2=NOT_AUTHORIZED`; `W1_NOT_STARTED`; `W2–W7=HOLD`; `PHASE1=NOT_ACCEPTED`; `PHASE2=NOT_ACTIVE`.
