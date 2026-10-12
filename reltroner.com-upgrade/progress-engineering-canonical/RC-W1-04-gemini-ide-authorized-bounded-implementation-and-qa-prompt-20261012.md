# RC-W1-04 — Owner-Authorized G2 Gemini IDE Coding and Local QA Prompt

> **2026-10-12 OFFLINE RECOVERY ADDENDUM:** Human-owner G2 provisioning RECEIPT IS NOW AVAILABLE and reports `G2_ISOLATED_WORKTREE=READY` / `G2_PROTECTED_14=HASHES_UNCHANGED`; the initial Gemini attempt stopped with no file edits because that receipt was not supplied to the agent and its GitHub connector returned 404. See [RC-W1-05](./RC-W1-05-provisioning-success-gemini-gate-stop-offline-recovery-20261012.md). The owner may supply the separately delivered self-contained `RC-W1-05-Gemini-offline-handoff-20261012.md` by attachment or inline paste. In an offline-only IDE session, do **not** repeatedly attempt inaccessible GitHub URLs; review the handoff and isolated local source instead. No fresh provisioning required. No `node_modules` was found, so do not install dependencies and record runtime tests BLOCKED_DEPENDENCIES. Historical first-run prerequisites below are satisfied once this receipt is in the IDE context.

> **Status:** G2 OWNER APPROVED; GEMINI CODING MAY BEGIN **ONLY AFTER** RC-W1-03 operator PowerShell reports `G2_ISOLATED_WORKTREE=READY` with exact SHA and hashes unchanged.
> **Source:** `Reltroner/reltroner-studio`, approved commit `18b295f96ccb521b228a1855e79448158c09db15`, branch `phase1/w1-creator-reader-ia-20261012`, worktree `C:\Projects\reltroner-studio-w1-ia`. If GitHub main has moved since exact owner approval, STOP and ask architect to re-review rather than silently rebase.
> **Authoritative:** [RC-W1-03 G2 owner ratification](./RC-W1-03-owner-g2-ratification-and-isolated-execution-20261012.md), [RC-W1-01 scoped work order](./RC-W1-01-proposed-g2-first-contact-creator-reader-ia-work-order-20261012.md), [27 acceptance crosswalk](../03-phase1-acceptance-and-invariant-traceability.md), [workspace/release governance](../05-source-workspace-and-release-governance.md).
> **This document does NOT authorize source PR, push, Vercel Preview, production merge/deploy, DNS/provider changes or dependency installation.**

## Exact IDE prompt — copy/paste only after G2 worktree READY

~~~text
ROLE: Gemini IDE Senior Frontend Implementer + QA Analyst.
WORK ORDER: RC-W1-01 / RC-W1-03 / RC-W1-04.
CONTEXT: Owner APPROVED G2 only, NOT G3–G8. Current phase Reltroner.com Phase 1 W1.
LANGUAGE: Indonesian report. Operating system Windows; PowerShell 5.1.
ACTIVITY: Implement one bounded IA slice, test locally, return evidence; STOP.

FIRST READ THE ENTIRE RATIFIED WORK ORDER and acceptance:
https://github.com/Reltroner/progress-documentation/blob/main/reltroner.com-upgrade/progress-engineering-canonical/RC-W1-03-owner-g2-ratification-and-isolated-execution-20261012.md
https://github.com/Reltroner/progress-documentation/blob/main/reltroner.com-upgrade/progress-engineering-canonical/RC-W1-01-proposed-g2-first-contact-creator-reader-ia-work-order-20261012.md
https://github.com/Reltroner/progress-documentation/blob/main/reltroner.com-upgrade/03-phase1-acceptance-and-invariant-traceability.md

CRITICAL START CONDITION:
The human operator must have pasted successful RC-W1-03 provisioning with:
  G2_ISOLATED_WORKTREE=READY
  G2_BASE_SHA=18b295f96ccb521b228a1855e79448158c09db15
  G2_PROTECTED_14=HASHES_UNCHANGED
If absent, STOP without writing anything.

ALLOWED WORKSPACE:
C:\Projects\reltroner-studio-w1-ia
NEVER work in C:\Projects\reltroner-studio, even for partial edits or config changes.

PRECONDITIONS YOU MUST VERIFY (READ ONLY):
- git remote get-url origin = https://github.com/Reltroner/reltroner-studio.git
- git branch --show-current = phase1/w1-creator-reader-ia-20261012
- git rev-parse HEAD = 18b295f96ccb521b228a1855e79448158c09db15
- git status --porcelain=v1 --untracked-files=all initially empty in this worktree.
- git worktree list --porcelain contains primary and isolated worktree, exactly.
- Do not try to fetch, checkout, branch, stage, commit, push or rebase.
- If any mismatch STOP immediately and report.

HARD CHANGE ALLOWLIST — EXISTING TSX FILES ONLY:
1. app/page.tsx
2. components/ecosystem/EcosystemHero.tsx
3. components/ecosystem/UseCasePathways.tsx
Read-only inspect other files when needed, but DO NOT modify other paths, content, generated-public assets, metadata or config. No new components/files unless explicitly reapproved.
No global CSS, app/layout, private content, .env, analytics, contact form, AI, CDN, DNS, Resend, Web3Forms or LMS/HRM changes.
No dependency install, npm ci, npm install, npm update, npx, lockfile write, code generators, git clean/reset, broad formatting or automatic commit. Never access secrets, private user files or any of the 14 untracked Markdown in primary.

FEATURE GOAL:
- Homepage must clearly and immediately offer TWO primary entries:
  For Creators: honest creative/worldbuilding system that compounds, published practical evidence.
  For Readers: clear fictional Asthortera worldbuilding onramp, spoiler-aware and welcoming to new readers.
- Make them equally prominent at the first-contact hero (not submerged in a subsequent content card); maintain existing h1, meaningful copy, semantic links, accessible names, visible focus and responsive spacing.
- Existing secondary collaborator/engineering/recruiter path remains discoverable and clearly different from fictional worldbuilding.
- Preserve current ecosystem, #app-dock / #knowledge-bridge anchors, app dock, LMS/HRM links, external link behavior, live-versus-planned availability and basic visual identity.
- Avoid unsupported marketing claims: mentorship/live courses or payments are NOT complete unless validated; no 'guaranteed spoiler-free' claim, no fictional lore presented as nonfiction.
- Keep all new implementation TS/TSX TypeScript-first. Reuse existing components, no unnecessary abstraction/framework.

INITIAL READ-ONLY ROUTE VERIFICATION:
- Candidate Creator: content/blog/no-copypaste-worldbuilding.md -> /blog/no-copypaste-worldbuilding
  Alternative if stronger: content/blog/creative-lore-bible.md.
- Candidate Reader: content/blog/asthortera-glossary.md -> /blog/asthortera-glossary.
- Secondary collaborator: content/blog/for-recruiters.md -> /blog/for-recruiters.
- Inspect actual frontmatter published flag and visible content for introductory suitability and spoiler level.
- Distinguish source published:true vs actual browser HTTP readiness. Do not invent successful browser tests.
- If the Reader candidate reveals major spoilers or is not an onramp, STOP. Propose exact amendment instead of editing content/ or fabricating pages.

ENGINEERING FLOW:
A. Read current three files and all existing anchors/hrefs.
B. Before editing, present a compact implementation plan and exact candidate destinations.
C. Edit only three allowed files. Prefer small, declarative link/copy/data improvements and robust responsive Tailwind.
D. Immediately inspect git diff --name-only, git diff --check, git diff --stat and actual patch.
E. If ANY tracked/untracked source outside allowlist changes, STOP; DO NOT auto-delete, undo, clean or stage. Report exact paths.
F. Run available local validation only when installed dependencies already exist inside isolated worktree. Do not install packages or link primary node_modules.
G. Do not trigger Next production build repeatedly. npm run build invokes postbuild next-sitemap, which may generate public/sitemap/robots artifacts. One near-final build is within G2 local test envelope only when dependencies already installed; inspect source state before and after; if nonallowlisted tracked files change, STOP and report without cleanup.
H. Browser QA through an already installed browser tool if it can launch localhost safely. npm run dev is allowed only inside isolated worktree with already installed node_modules; its generated .next cache is in isolated worktree. Never submit real contact/newsletter, solve CAPTCHA, access authenticated LMS/HRM, or call paid services.
I. No push, PR creation, deployment or merge.

VALIDATION MATRIX (each PASS_SCOPED/PARTIAL/FAIL/BLOCKED/NOT_EXECUTED):
W1-IA01 hero two real, equal Creator/Reader CTA.
W1-IA02 Creator target published, useful, honest.
W1-IA03 Reader target spoiler-aware and introductory, not raw advanced canon.
W1-IA04 secondary collaborator/engineering route accessible.
W1-IA05 regression: existing AppDock, external LMS/HRM links, anchors and nav.
W1-IA06 keyboard focus, accessible labels, Escape/drawer as relevant.
W1-IA07 responsive native 320x480, 375x812, 768x1024, 1440x900; no offscreen CTA/overflow.
W1-IA08 exactly 3 allowlisted changed paths; no new dependency or source file.
W1-IA09 if tools available: npm run typecheck; npm run content:validate; one npm run build (watch postbuild effects).
W1-IA10 wrong/draft route negative checks without publishing or modifying content.
W1-IA11 no provider/AI/analytics/contact change; Rp0 incremental spending.
W1-IA12 diff, tested snapshot, known limitations, rollback base and next G3 gate.

IF node_modules absent: output BLOCKED_DEPENDENCIES for npm/dev/build. Static source/diff tests still continue.
IF browser automation cannot open actual native 320/375: output NOT_EXECUTED_NATIVE, do not label iframe or desktop emulation as full PASS.
IF test would write outside allowed source paths: do not use it unless G2 local generated outputs are explicitly safe and can be isolated; never auto-clean.

FINAL REPORT IN ONE RESPONSE, NO FILE WRITES TO PRIMARY OR PUBLIC GITHUB:
- Timestamp, actor/tool, repo origin, base HEAD, worktree identity.
- Preflight status, scope and original 14 primary draft protection evidence.
- Before/after navigation contract and chosen URLs with source publication evidence.
- Exact changed file list/diff summary; lines changed.
- Table W1-IA01–12, executed commands with exit codes and authentic browser sizes.
- Build/QA limitations, new vs pre-existing issues, side effects/ignored cache.
- Recheck isolated git status, unchanged primary expected; no secret values.
- G3 recommendation: READY_FOR_REVIEW or BLOCKED, NEVER self-authorize PR/push.
- Do not commit, push, PR, deploy, change DNS/provider or request purchases.
STOP at the completed report and wait for independent reviewer.
~~~

## Engineering acceptance interpretation

Passing a compiler, TypeScript and Next.js build is not by itself WEB-AC01–04 acceptance. No issue outside W1 scope is implicitly waived. **G3 remains gated by source diff/QA review** and Vercel preview may be triggered by GitHub push, so no source remote activity in this step.

Known defects W3 background.webp 404, W4 GA tracking before visible consent, W5 Workers AI free model entitlement, W6 Resend Failed DNS/Web3Forms onboarding, W6 mobile reCAPTCHA clipping, W7 native mobile accessibility remain mandatory.
