# RC-G3-00 — Separate W1 Source Commit/PR Decision Packet (NOT AUTHORIZED)

> **Decision packet prepared, not a signed decision**. G2 owner approval for three TSX source edits + bounded local QA is not G3 consent to commit/push/open a PR. Scope unchanged. Prior gate: [RC-W1-16](./RC-W1-16-independent-browser-qa-acceptance-review-and-residuals-20261012.md), [RC-W1-17](./RC-W1-17-direct-png-evidence-review-viewport-capture-mismatch-and-invalid-webp-20261012.md), [RC-W1-18 targeted follow-up](./RC-W1-18-targeted-viewport-correlation-and-evidence-closure-work-order-20261012.md).
> **App:** `Reltroner/reltroner-studio`; reviewed and latest checked GitHub main `18b295f96ccb521b228a1855e79448158c09db15`; isolated local branch `phase1/w1-creator-reader-ia-20261012`. Original `C:\Projects\reltroner-studio` primary worktree HEAD `d6969ddfbc5e7d98d49b1523259785125159e722`, with **14 protected untracked Markdown documents**.

## What G3 would mean, if separately approved later

Only after owner accepts the evidence decision and exact scope, an operator may stage/commit these **three named existing paths** from the isolated worktree, push **the dedicated feature branch only**, and open a reviewable source PR targeting GitHub Studio `main`. Do NOT merge or request Vercel Preview implicitly. The candidate commit SHA does not yet exist. No app source writes via this documentation receipt.

```text
app/page.tsx
components/ecosystem/EcosystemHero.tsx
components/ecosystem/UseCasePathways.tsx
```

Preserve existing source behavior (AppDock/knowledge routes, existing app links and footer); genuine non-technical Creator/Reader first-contact entries; secondary engineering. `next-env.d.ts` must remain byte-identical to local HEAD; all other files must stay unchanged. Forbid `git add .`, `git add -A`, reset, clean, switching the primary working tree, dependency changes or new test files. No secrets.

## Hard preflight for a future G3 authorization

1. Owner explicitly decides **G3 permitted or deferred**, including whether `RC-W1-18` mobile evidence must be closed first.
2. Read-only `git status --porcelain=v1 --untracked-files=all`: **exact three TSX modifications**, none staged/untracked; status on primary remains exactly 14 untracked Markdown, no tracked changes.
3. Confirm main remote SHA has not drifted since reviewed `18b295f...`; if changed, STOP and re-review upstream changes / rebase strategy, no force push.
4. `git diff --check` must pass; conduct explicit three-file diff and semantics review, hashes captured. No blanket formatting.
5. Prior legitimate npm ci once/typecheck PASS/content validator 0 errors 371 warnings/build 440/440 PASS are **worktree snapshots** and must not be presented as CI on the not-yet-existing candidate commit.
6. Capture `RC-W1-18` correct correlated images or obtain explicit owner decision to carry its residual as unresolved. Complete short read-only checks for mobile navigation, footer and safe LMS/HRM `href` (no external clicks), and unpublished route negative fixture separately in W2/W4 if none approved. Distinguish nonblocking baseline `/#knowledge`, `/#roadmap` from patch regressions.
7. Check Vercel Git/Preview integration behavior and *whether opening a PR or pushing a branch will automatically create a Preview and consume usage*. G3 cannot silently initiate G4; if automatic deploy unavoidable, STOP and seek a combined scoped G3/G4 decision.

## Owner decision options (NOT YET RECEIVED)

**A. Defer G3:** first complete exactly the RC-W1-18 screenshot correlation and small read-only missing W1 regressions, then re-evaluate.

**B. Authorize G3 with named residuals:** specify acceptable carried-open items; allow only the exact three-file branch commit and PR under validated non-auto-preview conditions. Preview, merge and production all remain separate approvals.

**C. Request scoped W1 remediation:** provide exact defect/evidence and distinct amendment; current G2 approval does not allow editing any fourth path.

G4 preview QA and billing, G5 independent owner main merge, G6 production authorization, G7 smoke/rollback, G8 website DoD remain HOLD. Because the Studio `main` is linked to production Vercel, do **not** treat a main merge as merely a code-integration event.

## No claim of website readiness

Only W1 three-file first-contact slice is candidate reviewable. W2 shared search/public index/rails, W3 CDN freshness, W4 privacy and HTML safety, W5 actual public-sourced AI, W6 Resend/Web3Forms and W7 integrated DoD all remain mandatory, including all 27 WEB-AC. This packet **does not authorize** any app commit, push, PR, workflow or deploy.
