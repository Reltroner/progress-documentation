# RC-WEB-ADR-009 — Owner Ratified Homepage Pathways and Professional Portfolio Evidence

> **Owner instruction:** 2026-10-13, screenshots: selected Use-Case Pathways Creator card, Skill-Wanderer “Recent Client Projects” as an **inspiration pattern**, and yellow-highlighted lower homepage gap immediately above “Ready to explore?”. **Status:** decision ACCEPTED; safe isolated local patch **PREPARED**, **NOT YET EXECUTED** on user's Windows PC.
> **Parent DoD (unchanged):** [Architecture/WEB-I01..18](./00-ratified-frontend-architecture-contract-20261012.md), [27 WEB-AC](./03-phase1-acceptance-and-invariant-traceability.md), [Zero spend](./04-zero-incremental-spend-and-provider-boundaries.md), [workspace/governance and owner execution override](./05-source-workspace-and-release-governance.md), [RC-WEB-ADR-008 Creator/Reader TSX](./08-owner-execution-authority-and-dedicated-creator-reader-tsx-adr-20261013.md).
> **Source:** Studio `main` reviewed SHA `18b295f96ccb521b228a1855e79448158c09db15`; owner isolated local `phase1/w1-creator-reader-ia-20261012`. Existing W1-19 owner receipt: exactly three modified existing TSX and two created untracked TSX onboarding pages; W1-20 six? **W1-20 has NOT been evidenced as run**; its original five-path validator becomes stale after this refinement.

## 1. Owner ratified specific UX behavior

- Homepage `Use-Case Pathways` card **For creators** must navigate to **`/start/creators`**; not to `/blog/no-copypaste-worldbuilding`. This is a *second homepage location* and is not automatically fixed merely because the Hero primary CTA was already updated.
- In the same card set, **For readers** should consistently navigate to the previously owner-ratified `/start/readers`, not directly to a lore-heavy Markdown glossary.
- Reference: https://skill-wanderer.com/ section “Recent Client Projects” for **professional evidence hierarchy**, image-first projects grid, readable card descriptions and whitespace. Copy no client logos, value propositions, paid-service/fee assertions, legal text, wording or brand styling. Reltroner's identity remains dark navy/blue, Creative Compound worldbuilding + engineering + learning.
- Insert the new section **immediately AFTER `EcosystemRoadmapPreview` and BEFORE the existing “Ready to explore?” final homepage CTA**: this is the visually yellow-marked empty space, not a random position in the knowledge archive.

## 2. Portfolio cards, source truth and asset provenance

**Heading:** `Selected Work & Practice`; secondary eyebrow `Work made visible`. Do **not** call it “Recent Client Projects” or claim these were contracted client commissions without documentary evidence. Two cards with photo/image top and text below, responsive: two columns on md/desktop, single column on narrow mobile, dark blue contrasting typography, semantic `<article>`, alt text, focus-visible link and an explicit broken-image fallback.

| Card | Verified Git repository path | Positioning (no invented client claim) |
|---|---|---|
| Direktori Listing | `landing-page-resource/images/direktori-listing.webp` | Selected product-interface visual |
| Kelas Digital | `landing-page-resource/images/rei-kelas-digi.webp` | Learning/practice visual |

Resource Git tree independently checked at commit **`50b259bf8db5b8c04baf0c0cb9b1cf11a32e9c70`**, and both blobs exist: Direktori Listing blob `04ae261ff50c9eef818a219893740c07f86b0e33` size 185,696 bytes; Kelas Digi blob `f34787aefbf133c72f2f456a9ed6898f144a3748` size 261,302 bytes. These prove repository source existence only. **Neither CDN delivery nor rendered image pixel/content quality has been tested.**

New component uses immutable Git SHA-pinned URLs on existing jsDelivr host:
```text
https://cdn.jsdelivr.net/gh/Reltroner/reltroner-studio-resource@50b259bf8db5b8c04baf0c0cb9b1cf11a32e9c70/landing-page-resource/images/direktori-listing.webp
https://cdn.jsdelivr.net/gh/Reltroner/reltroner-studio-resource@50b259bf8db5b8c04baf0c0cb9b1cf11a32e9c70/landing-page-resource/images/rei-kelas-digi.webp
```
This is the **W1 proof-section static pin**, not W3's still-incomplete *automatic same-filename update* pipeline; later W3 cannot claim done based on this manual pinned commit. UI includes a safe fallback label if image load fails; QA must report broken CDN as defect, not hide it as full success.

## 3. Exact mutation scope of RC-W1-21

Initial expected status at local Windows worktree before script: three tracked modified and two untracked TSX as confirmed by owner RC-W1-19. Targeted patch (no changes to Hero or onboarding pages):
```text
MODIFY app/page.tsx
MODIFY components/ecosystem/UseCasePathways.tsx
CREATE components/ecosystem/SelectedWorkShowcase.tsx
```
After patch, W1 exact source status: **three modified tracked TSX + three untracked TSX** (two existing onboarding pages plus newly created portfolio component). No `content/**`, `.env`, package/lock/config, image asset binary or primary author draft edits. No extra provider usage, external login, DNS, npm, Git commit/push/PR/preview/deploy from the patch.

Operator implementation artifact `RC-W1-21-apply-professional-landing-20261013.cjs`, SHA256 `30fc18ce717e71e82c7ae0303ac6ed00c7f1056a8805006baa4c1f53cb36b627`, created outside Git repo, `node --check` PASS in assistant container; **NOT YET RUN in owner's Windows environment**. Includes fail-closed exact worktree branch/HEAD/status, remote and primary 14 authored Markdown before/after hash snapshots and Git refs verification. It replaces exactly the Creator/Reader `PATHWAYS` objects, inserts one import and component call, and writes one new TSX file only. Unknown structure/status => STOP, not a blanket overwrite.

## 4. Six-file one-shot QA

The **old RC-W1-20 five-file validation script is obsolete once RC-W1-21 modifies source**. Replacement is `RC-W1-22-isolated-six-file-local-validation-20261013.ps1`, SHA256 `d93b950888b8b5577748aa24d152f27bc9f1ff4612b5a1401bfa3c65c5c0720d`, based on RC-W1-20 but expanded to 3 tracked modified + 3 untracked including `SelectedWorkShowcase`. It has the same exact hashed protected-file and refs guards, no install, one each local typecheck/content validation/production build, and only permits Next-generated `next-env.d.ts` one-line restore if exactly previously confirmed. It has been statically inspected, **not run on user's Windows**.

After validation PASS, a single localhost production server/browser QA must confirm:
1. direct click on highlighted Creator card → `/start/creators` (HTTP 200 TSX), Reader card → `/start/readers` (HTTP 200 TSX);
2. portfolio appears **after roadmap and before Ready CTA** with two actual loaded images; network HTTP successful CDN response with valid MIME, no fabricated project/customer claims, alt/fallback semantics;
3. 320×480, 375×812, 768×1024, 1440×900, 200% zoom, horizontal overflow, keyboard focus and layout;
4. incumbent Hero CTA links and published article follow-up unchanged, collaborator/recruiters access intact;
5. W4 preconsent Google Analytics issue remains unresolved; block trackers **before first navigation**; no contact/newsletter submission, LMS/HRM login or public production changes.
6. exact six-file status, `next-env` clean, primary 14 drafts unchanged during actions.

**Stop statuses:** unknown preflight, npm exit ≠0, incorrect screenshot source or CDN 404, unexpected files, generated-file diff beyond one line → STOP, share actual logs, no automatic retry or broad cleanup.

## 5. Release/DoD

Owner permits work sequencing without ceremonial W0–W9 blocking; this is **actual permission for the bounded W1 refinement**, not proof of successful Windows execution. Existing local W1-19 patch PASS remains. Portfolio section and link are not yet runtime verified. W2–W7 and all 27 WEB-AC, real W3 automated image freshness, W4 consent, W5 genuine AI, W6 email/contact and W7 integrated release remain mandated. No PR/production deployment from this work order alone. After RC-W1-21/22 PASS new potential W1 source candidate **six files**; any stale “five-file” G3 packet is historical only.
