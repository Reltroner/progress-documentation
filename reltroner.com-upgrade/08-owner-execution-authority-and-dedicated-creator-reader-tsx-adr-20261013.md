# RC-WEB-ADR-008 — Owner Execution Authority and Dedicated Creator/Reader TSX Onboarding Pages

> **Status:** **OWNER RATIFIED 2026-10-13 Asia/Jakarta** in conversation after presenting a desktop screenshot of localhost W1. **This ADR supersedes only conflicting execution-gate defaults and the former W1 direct-article-CTA destination design**; the ratified 18 WEB invariants, all 27 WEB-AC, zero additional cash, protected 14 author drafts, LMS frozen boundaries and objective source/test acceptance remain normative.
> **App source base:** `Reltroner/reltroner-studio` main `18b295f96ccb521b228a1855e79448158c09db15`, W1 isolated local `C:\Projects\reltroner-studio-w1-ia` branch `phase1/w1-creator-reader-ia-20261012`, three previously modified TSX paths. Primary `C:\Projects\reltroner-studio`, local main `d6969ddfbc5e7d98d49b1523259785125159e722`, 14 untracked protected author Markdown.
> **Normative parents:** [ARCH-001](./00-ratified-frontend-architecture-contract-20261012.md), [AC-001](./03-phase1-acceptance-and-invariant-traceability.md), [GOV-001](./05-source-workspace-and-release-governance.md), [UX 11](../all-in-reltroner-master-source-of-truth/11-reltroner-com-landing-and-ux-journeys.md). They retain the detailed acceptance matrix and target DoD.
> **RC-W1-18:** Owner's attached Antigravity console report states targeted CDP viewport emulation at 320×480, 375×812 and 768×1024 with `deviceScaleFactor=1`, matched PNG intrinsic dimensions and `scrollWidth == clientWidth`, and successful ZIP packaging. **Evidence is agent/operator-reported**; the new ZIP itself was **not uploaded to ChatGPT in this turn**, so do not claim the assistant independently opened these new PNG bytes or verified their hashes. This outcome does not authorize falsely accepting redesigned routes before testing them.

## 1. Owner execution decision — no ritualistic permission bottleneck

Owner states, in substance: *As the human decision maker I can direct work regardless of order W0–W9; when I instruct the assistant to work, work, and let me inspect and assess it, despite my not being a deep software engineer.* The assistant/IDE agent must act on the **specific current instruction** rather than repeatedly stalling for purely ceremonial G0/G1/G2 re-approvals. Human owner can reprioritize, skip, combine, reopen or delegate any W0–W9 or G0–G8 activity, when technically possible, by an explicit direction. W8/W9 are **owner sequencing labels, not newly invented automatically completed workstreams**.

**Binding interpretation:**
1. A clear present-tense instruction to implement a specified safe, reversible, no-cost isolated source change is an owner work authorization for **that named outcome and necessary tightly bounded file scope**. The owner has now authorized correcting the two W1 CTAs and creating separate TSX landing pages; do not ask them to reapprove the same bounded patch before generating it.
2. Preflight, integrity assertions, negative tests, provenance and regression evidence remain **execution-quality checks**, not veto powers over the owner's choice of *sequence*. If checks fail, report actionable failure and STOP unsafe mutation; do not fabricate success.
3. **Production release, main merge with automatic deployment, DNS write, paid subscription, billing exposure, public email dispatch, destructive reset/cleanup and access to private services** remain materially distinct side effects. A direct owner instruction that clearly identifies such an action and scope may authorize it, but an unrelated order such as “implement a TSX page” does not. Explain concrete impact, verify state, and use bounded/recoverable execution. Do not infer a blanket future spend or irreversible-change license from the sequencing rule.
4. Do **not** impose additional arbitrary authorization layers just because an old progress ledger says G3 HOLD, when the *current owner instruction actually authorizes an equivalent scoped action*. Conversely, no retrospective fictitious CI, preview, release or WEB-AC PASS without evidence.
5. The owner judges the UX/product result as a human; the assistant remains responsible for professional engineering safety, regression clarity, accessibility, security, honest provider limitations and objective testing. Owner's limited software engineering specialization is **not grounds to dilute DoD**.

## 2. Product correction: Homepage CTAs must not open an existing Markdown article directly

At local `127.0.0.1:3101` screenshot two blue CTA buttons are highlighted:
- *Start with worldbuilding revision* → current `/blog/no-copypaste-worldbuilding`, a route rendering Markdown source.
- *Start with the Asthortera glossary* → current `/blog/asthortera-glossary`, another Markdown-derived article.

Owner specifies **both should first enter new purpose-built `.tsx` Next.js App Router onboarding pages**, not an existing Markdown page. This does not repeal WEB-I05: Markdown/Git remains the canonical source for actual authored articles, canon, and long-form reading; TSX is the UX/navigation **layer** that contextualizes those resources.

**New stable routes chosen for this small scope:**
```text
/  →  /start/creators   →  /blog/no-copypaste-worldbuilding (+ /blog/creative-lore-bible)
/  →  /start/readers    →  /blog/asthortera-glossary (explicit lore disclosure) /series
```

**Owner acceptance on onboarding pages:**
- Creator: independent page with substantive creative method orientation (question → constraints → revision), clear Creative Compound framing, multiple deliberate choices to real published articles; no fabricated “mentorship/course sold” claims.
- Reader: independent gentle fictional-Asthortera introduction first, no named canon spoilers in page-level orienting copy; explicit FICTION boundary and *opt-in* spoiler-aware glossary/series links. Do not assert that glossary or series is spoiler-free.
- Both pages: unique metadata, Next.js server component `page.tsx`, no added deps, accessible headings/links/focus, mobile 320/375, tablet 768, desktop 1440, keyboard and internal navigation. Secondary recruiter/collaborator path remains intact. Existing anchors, footer, LMS/HRM, global navbar and 14 author files unchanged.
- Hero CTA text should honestly describe navigation to the new pathway, not falsely imply an immediate article: proposed *Explore the Creator pathway* / *Explore the Reader pathway*. Avoid rewriting existing unrelated sections.

## 3. Exact **new owner-authorized** local W1 mutation scope

```text
MODIFY existing: components/ecosystem/EcosystemHero.tsx
CREATE new:     app/start/creators/page.tsx
CREATE new:     app/start/readers/page.tsx
```

The pre-existing W1 local changes `app/page.tsx` and `components/ecosystem/UseCasePathways.tsx` remain preserved and **unchanged during this incremental patch**; the pre-existing `EcosystemHero.tsx` modification is preserved except for exact CTA href/label/context copy. Expected resulting worktree: exactly **three modified tracked W1 TSX** plus **two new untracked page.tsx** until specifically staged; zero staged files; `next-env.d.ts` remains clean prior to testing. No `content/**`, `.env*`, packages, config, styling, LMS/HRM, provider or resource changes. No GitHub Studio branch/push/PR is needed to materialize the correct local patch. Do not create a divergent remote source branch from main that omits the three uncommitted local W1 source changes.

**Implementation artifact supplied to owner**: single self-contained `RC-W1-19-apply-dedicated-creator-reader-routes-20261013.cjs`, SHA-256 `0d6f1cf5f58d3689e25e53cf4d4841159aee2f97ea446f9087fab65117e2e31f`. Uses built-in Node and Git only, validates exact source status/HEAD and 14 protected drafts before writing, targets exactly the three above paths, outputs `RC_W1_19_PATCH=PASS` if postconditions hold. **Prepared and statically syntax-checked in the assistant container, NOT YET RUN on the owner's Windows PC.** Do not claim TSX production build/browser QA passed until tested on owner's candidate.

## 4. Test and acceptance update

Old `RC-W1-01` direct-article first-contact decision is historical, **superseded for these two primary buttons only**. Preserve original W1 historical acceptance and mark new result only upon runtime:
- `WEB-AC01`: first-time user understands purpose and two independent paths; needs *human* comprehension and mobile evidence.
- `WEB-AC02`: homepage → Creator TSX → explicit published creative practice resource works with keyboard and 320/375/768/1440.
- `WEB-AC03`: homepage → Reader TSX spoiler-aware orientation → informed optional glossary, fiction not presented as empirical truth.
- `WEB-AC04`: secondary engineering link remains visible; no new misleading offerings.
- `WEB-AC21/22/24`: real Next route/SEO/a11y acceptance plus content/typecheck/build at exact future candidate, not old build.

**New local code has no test receipt yet.** A successful prior W1 440-page build/Chrome QA proves the *old source state*, not the two new TSX routes. One bounded noninstall typecheck/content validation plus one new build can be considered after patch; Next may regenerate tracked `next-env.d.ts`, so exact generated-file diff must be inspected/restored narrowly before claiming source-integrity PASS. Browser agent must block GA network before first navigation (W4 unresolved). No need to repeat entire W0 discovery, npm ci, remote provider tests or irrelevant viewport recorder.

## 5. Owner verification and forward motion

Owner need only run the one prepared local Node script against the isolated worktree, inspect localhost `/start/creators` and `/start/readers` after a fresh build, and share the actual QA evidence/feedback. The assistant should continue work by interpreting that feedback, not demand that the owner personally map TSX routes or debug TypeScript. G3 proposal source allowlist must be updated to **five source paths** before any owner-directed PR; older exact-three-file packet RC-G3-00 is historical for pre-amendment W1. No automatic commit, push, PR, Preview or production release follows from this change order.

**Current:** `OWNER_RATIFIED_AUTHORITY=YES`; `OWNER_RATIFIED_TSX_ONBOARDING=YES`; `RC-W1-18=AGENT_REPORTED_PASS_PENDING_ZIP_REVIEW`; `RC-W1-19=PREPARED_LOCAL_PATCH_PENDING_OWNER_EXECUTION`; `W1_SOURCE_OLD_BUILD=PASS_SCOPED`; `NEW_TSX_ROUTE_RUNTIME=NOT_EXECUTED`; `G3=NOT_STARTED`; `WEBSITE_PHASE1=NOT_ACCEPTED`; `PHASE2=NOT_ACTIVE`.
