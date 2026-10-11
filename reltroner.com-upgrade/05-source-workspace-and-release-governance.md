# RC-WEB-GOV-001 — Workspace Isolation, TypeScript Engineering and Release Governance

> Status: OWNER RATIFIED PROCESS; GitHub ruleset enforcement NOT VERIFIED.
> Target source: https://github.com/Reltroner/reltroner-studio .
> Documentation-only ratification does not authorize application PR merge or production deployment.
> Derived from LMS procedural discipline; no claim it inherits LMS application rulesets or frozen six-service scope.

## 1. Protected local authoring state

Owner reports primary checkout C:\Projects\reltroner-studio on main up to date with 14 untracked Markdown files: 12 content/music entries and 2 content/places entries (paths enumerated in [W0 §4.1](./02-w0-00-read-only-discovery-work-order-20261012.md)). These are **protected authoring work**, not repository dirt to be 'fixed'. Their presence may change; fresh operator read-only inventory is required at each code-entry gate. GitHub does NOT show untracked local files.

Forbidden on primary checkout without distinct owner approval: git clean -fd, reset --hard, broad git add ., git add -A, force checkout, checkout branch conflict, destructive worktree pruning, deletion of user's files, bulk format of content directory. Never overwrite primary content/music or content/places in initial website PRs.

## 2. Approved collaboration pattern for *future*, not W0

- W0 performs read-only checks only; **no worktree creation yet**.
- After W0 owner acceptance, create a new isolated Windows worktree in a separate directory at an **exact rechecked remote main SHA** on a named feature branch (example: phase1/web-ux-ia-20261012, but name must be checked unique).
- Worktree must be created/used by the local operator after a copy-paste-safe specific work order; GitHub connector should not mutate the primary local filesystem.
- Scope each PR to an allowlist of files. Staging must enumerate explicit filenames, no wildcard staging that absorbs the 14 untracked documents.
- Source tree and application preview tests must run from isolated worktree. Owner content creation remains uninterrupted in primary checkout.
- All new React components/services/types use .ts/.tsx. Existing .js/.jsx are migrated only at inspected, testable boundaries; TS checks alone do not prove app correctness.
- Maintain source/pipeline provenance: base SHA, candidate SHA, exact paths, dependency changes, CI, preview ID, rollback and user approval.

## 3. Roles and permissions

| Actor | Responsible for | Not permitted by this governance alone |
|---|---|---|
| Human owner | Ratify feature scope, judge budget/risk, grant code & production approvals, private provider GUI/config actions | Claim untested vendor/runtime success |
| ChatGPT architect/reviewer | Read source, draft work order/ADR, classify blockers and tests, review PR evidence | Act as implicit source merge/deploy approval |
| IDE AI agent | Implement bounded TS/TSX code in approved isolated branch after W0 | Broad repo rewrite, primary checkout cleanup, secret collection, auto-merge/main |
| CI / Vercel Preview | Supply build/test/deploy evidence | Replace owner sign-off or production/domain privacy review |
| Provider GUI operator | Redacted quota/config evidence, separately approved settings | Post API secrets or billing details into public GitHub |

## 4. Gate progression

G0 owner website requirements ratified → G1 W0 discovery accepted (source/provider/frontend unknowns classified) → G2 exact nonproduction branch & file-scope authorization → G3 source PR with test evidence and human review → G4 preview QA + no-spend provider proof → G5 independent owner main merge authorization → G6 controlled production release authorization → G7 postdeploy smoke/cost/privacy proof + rollback receipt → G8 website Phase 1 acceptance → global Phase 1 exit plus separate Phase 2 activation.

A doc commit can satisfy ratification archival evidence ONLY. No business owner approval is inferred for G2–G8 from this commit. Multiple staged PRs should retain independent rollback. If explicit production integration would automatically deploy on main, **owner must be told that before authorizing main merge**, and deployment/promotion strategy must be reviewed accordingly.

## 5. Negative gates and rollback

STOP if expected base SHA drift, unexpected dirty source files, source code changes outside allowlist, form/provider secrets in diff, unverified quota/auto-upgrade risk, published-only leak, failing critical tests, incompatible CDN release behavior, critical accessibility failure, inability to reproduce build, or lack of preview/prod rollback. Never 'just purge everything', force-push, push new prod source or toggle Cloudflare while investigating another subsystem.

Rollback means restoring a known-good accepted SHA or configuration **by an approved reviewed procedure**; document if automated deployment/revert has side effects. No guarantee of zero outage without evidence.

## 6. Deterministic issue/PR and review template

~~~text
WORK ORDER ID:
PURPOSE:
SOURCE REPOSITORY / EXPECTED BASE SHA:
BRANCH / ISOLATED WORKTREE:
ALLOWED PATHS / FORBIDDEN PATHS:
REQUIREMENTS / WEB-I / AC IDS:
DEPENDENCIES / INFRA / COST:
TEST COMMANDS / NEGATIVE FIXTURES:
EXPECTED OUTPUTS:
KNOWN FAILURE AND STOP CONDITION:
PREVIEW DEPLOYMENT:
SECURITY/PRIVACY NOTES:
ROLLBACK PLAN:
OWNER APPROVAL TO IMPLEMENT:
SOURCE CANDIDATE SHA:
CI/REVIEW RECEIPT:
OWNER APPROVAL TO MERGE:
OWNER APPROVAL TO DEPLOY:
POSTDEPLOY RECEIPT:
~~~

Owner sign-off is explicit text linked to an exact PR/SHA/scope; a generic 'approved architecture' is not auto-approval to change DNS/provider billing or production. Store sanitized release evidence in the website ledger, not an unrelated LMS execution receipt.

