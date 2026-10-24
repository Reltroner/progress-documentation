# 07 — Source Authority, Claim Traceability and Owner Decision Ledger

> Source review date: 2026-10-24 Asia/Jakarta  
> This is a **dated** traceability map, not a permanent claim about current deployments or provider status.

## 1. Hierarchy of authority

| Source | Authority and topic | Status in this package |
| --- | --- | --- |
| [Studio Master Source of Truth v2.3](https://github.com/Reltroner/reltroner-studio/blob/main/content/principles/reltroner-studio-master-source-of-truth.md) | Binding studio identity, IP/narrative, creative method, evidence and §55 strategy | **Binding** |
| [Communication Framework v1.0](https://github.com/Reltroner/reltroner-studio/blob/main/content/principles/reltroner-studio-communication-framework.md) | Audience value translation, L1–L5, ethical outreach, UX copy | **Proposed, subordinate** |
| [WOS README](../../worldbuilding-operating-system/README.md) | Course candidate inventory and revised usage-first mission | **Curriculum candidate v0.3** |
| [WOS reference model](../../worldbuilding-operating-system/07-worldbuilding-os-reference-model.md) | Six-stage model, state changes and transfer caution | **Instructional candidate** |
| [WOS 14 usage & transfer map](../../worldbuilding-operating-system/14-usage-mental-model-and-transfer-map.md) | 89 lesson mapping and W/M/N/X evidence separation | **Instructional candidate** |
| [WOS 12 communication contract](../../worldbuilding-operating-system/12-creator-communication-and-lesson-copy-contract.md) | Beginner-facing lesson copy and anti-jargon practices | **Proposed** |
| [Ratified website contract](../00-ratified-frontend-architecture-contract-20261012.md) | Technical frontend scope/invariants, security/cost/provider boundaries | **Binding within website domain** |
| [Website journeys](../../all-in-reltroner-master-source-of-truth/11-reltroner-com-landing-and-ux-journeys.md) | Ratified audience-first first-contact UX | **Ratified, subject to later explicit ADR** |
| [Engineering progress ledger](../01-engineering-progress-ledger.md) | Dated source/QA evidence and known gaps | **Historical unless refreshed** |
| [Source repository](https://github.com/Reltroner/reltroner-studio) | Current application content and behavior, when inspected | **Repository fact only at checked SHA** |

Relevant Studio Master anchors: §§1–2 (identity, two value engines, technology restraint), §5 (USP), §§19,24–29 (Earth-to-Asthortera and human relevance), §§46–47 (Creative Compound Machine), §§49–50 (narrative/canon), §§52–54 (claims and translation), §55 (phase and scope). Relevant Communication Framework anchors: §§1–4,9–13,15–18.

## 2. Observed source structure (24 October review)

| Route | Source | Relevant observed imports/features |
| --- | --- | --- |
| / | app/page.tsx | HomepageCdnArt; CreativeLoop; ReadingPreview; NewsletterSection |
| /creators | app/creators/page.tsx | EditorialCdnArt; CreatorGoals; CreatorNotebook; lighthouse worked example |
| /readers | app/readers/page.tsx | EditorialCdnArt; ReadingPreview; ReaderConnections; ReaderScales |
| /explore | app/explore/page.tsx | ExploreAboutCdnImage; ExploreCuriositySection from ExploreClient |
| /about | app/about/page.tsx | ExploreAboutCdnImage; SelectedWorkShowcase; Imagine/Build/Grow |
| /contact | app/contact/page.tsx | ContactExperience |

The inspected Next.js application and components are a **source baseline**, not proof that every live widget's network behavior or cross-browser rendering passed. Inspect HEAD again before editing.

## 3. Decision log

| Date | Decision / observation | Classification | Engineering consequence |
| --- | --- | --- | --- |
| 2026-10-12 | Studio Master §55 specifies bounded product foundation and independent LMS/website gates | RATIFIED STRATEGY | No uncontrolled expansion or automatic phase transition |
| 2026-10-12/13 | Website design, W1 journey and later owner-specific ADRs documented | HISTORICAL / SOME RATIFIED | Reconcile later decision and current code; no indiscriminate replay |
| 2026-10-22 | Studio communication/value translation framework written | SUBORDINATE PROPOSAL | Human-first, evidence-bound communication pattern |
| 2026-10-24 | WOS v0.3 usage/mental model/transfer revision documented | CURRICULUM PROPOSAL | Creator page can teach useful reasoning without claiming cross-domain proof |
| 2026-10-24 | User requested integration of three Talk Like TED characteristics with WOS and six public routes | USER REQUIREMENT | Evaluate Emotional–Novel–Memorable, two pathways and six-page IA |
| 2026-10-24 | Assistant proposed A+B staged experience, causal thread, six-page refinement, P0/P1/P2 and validation | DESIGN PROPOSAL | Preserve minimal, reusable implementation |
| 2026-10-24 | User explicitly accepted all proposals and requested content in this folder | **OWNER-APPROVED DESIGN + DOCUMENTATION WRITE** | Create full handoff; **not** automatic release of changes to reltroner-studio |

## 4. What was approved, exactly

- Adopt Emotional, Novel, Memorable **as high-level communication design anchors**.
- Do not claim a scientific universal “three things memory limit.”
- Use the two value engines and progressive disclosure to prevent lore and jargon overload.
- Preserve and refine existing live-ish component architecture rather than restart design.
- Homepage = orientation and meaningful proof; Creators = creator-owned practice plus optional reasoning reflection; Readers = choice and scale; Explore = curiosity/connection/depth; About = authentic process; Contact = low pressure/integrity.
- Introduce **The Causal Thread** as an optional design language with restrained motion.
- Prefer low-resource A (message hierarchy) then B (component experience); validate C-like ambitious features before considering them.
- Keep data/canon/status trust, current effective frontend architecture and LMS separation.

## 5. Differentiation: proposal versus verified claim

**Proposal:** “A structured consequence experience should help a visitor remember the studio.”  
**Would require proof:** a recorded usability or recall task under a documented version.

**Proposal:** “Worldbuilding may scaffold reusable mental models.”  
**Would require proof:** W/M/N/X-specific independently observed learning evidence; there is no current claim of universal skills transfer.

**Proposal:** “Existing site can gain clarity without a new backend.”  
**Would require proof:** source diff, working routes, actual performance and QA in affected environments.

**Existing document:** 8 WOS modules and 89 lesson titles are planned.  
**Invalid leap:** therefore 89 production lessons are released on lms.reltroner.com.

## 6. Historical contradiction handling

Do not let earlier 12–13 October /start/creators and /start/readers experiments, deprecated mobile Reading Path rules or old provider/deployment statuses automatically override the later observed six-route app. Current ratified ADRs still govern their stated scope; live source and tests govern implementation behavior. Where newer owner decisions and older documents conflict, create an explicit traceable resolution rather than silently rewriting history.

## 7. Change log

- **2026-10-24 — v1.0:** Initial integrated design package following owner's explicit approval. Documentation-only; all acceptance statuses remain untested until implementation evidence is provided.

## 8. Owner handoff rule

A future patch must reference this folder and its exact version, current source SHA, relevant ratified owner decisions, and discrete acceptance tests. The presence of this documentation is not itself a release instruction or an authorization to override protected infrastructure.
