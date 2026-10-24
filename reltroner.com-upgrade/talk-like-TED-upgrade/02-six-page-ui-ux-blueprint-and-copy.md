# 02 — Six-Page UI/UX Blueprint, Journey Continuity and Candidate Copy

> Status: OWNER-APPROVED PAGE RESPONSIBILITIES / CANDIDATE COPY REQUIRES IMPLEMENTATION REVIEW  
> Review baseline: the main branch of Reltroner/reltroner-studio inspected on 24 October 2026. The codebase may change; verify current HEAD and actual rendered site before editing.  
> Core rule: **Reuse working experiences rather than rebuild them for appearance.**

## 1. Route responsibility matrix

| Route | First visitor question | Emotional → Novel → Memorable | Primary action | Keep |
| --- | --- | --- | --- | --- |
| / | “What is this studio, and where do I begin?” | Curiosity → connected idea → two meaningful paths | For creators / For readers | Two audience routes, creator/reader previews, truthful optional newsletter |
| /creators | “Can this help my own world?” | Creative friction → inherited causal loop → usable artifact | Try experiment / notebook | Six-stage method, goal selector, private worksheet |
| /readers | “Why should I care about Asthortera?” | Character choice → macro consequences → human reflection | Experience spoiler-light story | ReadingPreview, ReaderConnections, ReaderScales |
| /explore | “Which door matches my curiosity?” | Question → relationship → relevant archive | Open suitable published object | Existing intents, collections, search and safe metadata |
| /about | “Who made this, and why?” | Motive → discovered method → ongoing credible practice | Examine work / source / contact | Founder story, 3 capability domains, 6 principles, selected work |
| /contact | “What can I ask and expect?” | Welcoming question → appropriate channel → clear receipt | Send legitimate inquiry | Existing form, inquiry routing, privacy/security and provider behaviors |

## 2. Homepage — the first meaningful impression

**Problem:** First contact must explain one studio without overwhelming the visitor with lore, methodology or portfolio inventory.

**Preserve:** current value-led hero, both primary routes, existing CreativeLoop/ReadingPreview sections, reusable HomepageCdnArt imagery, trustworthy depth/portfolio links and newsletter disclosures.

**Proposed hierarchy** (not a strict count of sections):
1. Hero: one understandable question plus creator/reader calls to action.
2. One concise proof: a single idea yields a decision, consequence and new question. Prefer a compact existing interaction.
3. Choose pathway: creator experiment or reader dilemma, each with one clear preview.
4. Optional supporting proof, archive/portfolio and thoughtful follow-up, progressively disclosed.

**Candidate hero:** “What if one idea could change an entire world?”  
**Candidate support:** “Explore how choices become consequences, how consequences create new possibilities, and how fictional worlds reveal familiar human questions.”  
**CTA candidates:** “I create worlds” → /creators; “I explore worlds” → /readers. **Do not change a ratified route destination without checking later ADRs and current effective navigation policy.**  
**Potential takeaway:** “An ending can become the beginning of something else.”

Existing headline “What if one idea could grow into an entire world?” already serves this purpose; replacing it is **optional, not itself a success condition**. Remove only demonstrably redundant explanatory copies.

## 3. Creators — from inspiration to a reusable mental model

**Source assets/components:** app/creators/page.tsx currently imports **CreatorGoals**, **CreatorNotebook**, and **EditorialCdnArt**; creator demonstrations are already present. Existing homepage also uses **CreativeLoop**.

**Problem:** The page demonstrates how ideas connect, but can more explicitly help the visitor name **what reasoning pattern they just practiced**.

**Proposed journey:** Recognize “lots of ideas, no next step” → show the familiar lighthouse before/after → try six-stage loop → produce own local artifact → display optional reflection “Which earlier change created your next question?” → optionally explore relevant released WOS content.

**Candidate reflection block:**  
- “You just explored **constraint → interaction → consequence**.”  
- “What changed in your world because of an earlier choice?”  
- “Which new question exists only because of that change?”  
- Optional: “Where else *might* this pattern help, and which assumptions would need checking?”

**Preserve:** no account requirement, local/private expectation only as verified by actual deployed implementation, Markdown export, user-initiated third-party AI use, no automatic submission and creator ownership. If evidence shows differences, correct claims before publishing. Do not make transfer exercise mandatory or use WOS as an upsell trap.

**Potential takeaway:** “My previous creative output can generate my next creative input.”

## 4. Readers — one choice, three scales

**Source:** app/readers/page.tsx imports **ReadingPreview**, **ReaderConnections**, **ReaderScales**, and EditorialCdnArt.

**Problem:** The user should first care about a person's dilemma, not memorize classification terms or national lore.

**Proposed integrated experience:** **One Choice, Three Scales**:
- **Micro / a person:** a researcher must decide whether to warn others of a risk.
- **Meso / an institution:** institutions must decide what to trust and how to respond.
- **Macro / multiple civilizations:** decisions may alter cooperation, accountability or social expectations.

Tie existing **Current Lore / Backstory / World Guide** explanatory modes to the **same single fictional example**, so changing lens adds relevant causality rather than reading three disconnected widgets. Label hypothetical/non-canon case visibly but unobtrusively.

**Candidate hero:** existing “What if a better world still had difficult choices?” remains strong.  
**Potential takeaway:** “A civilization can solve extraordinary problems without making human choices simple.”

The canonical archive is distinct from the hypothetical preview. Do not silently insert the researcher's story as officially published Asthortera lore.

## 5. Explore — curiosity navigation, not an encyclopedic wall

**Source:** app/explore/page.tsx plus ExploreClient. Currently organizes visitor intents and connections to knowledge collections.

**Problem:** A route can be discoverable without forcing a new visitor to browse many parallel classification lists.

**Proposed three-tier discovery grammar** (not three exclusive categories):
- **Discover:** “What interests me?” Preserve *existing* four curiosity-intent choices and published collections.
- **Connect:** “What does this choice affect?” Offer a few editorially verified related items with descriptive causal text.
- **Deepen:** “What should I read next?” Link to actual released article/wiki/series, with epistemic/canon status.

**Illustrative editorial relation:** institutional decision → cultural consequence → a person's dilemma. Never infer a factual causal relation from coincident tags or an AI guess. Static editorial links are preferable to launching a graph backend.

**Keep:** search, discoverability, publication flags, keyboard access, no artificial filtering that silently hides relevant content.

## 6. About — founder narrative as lived method

**Source:** app/about/page.tsx already contains **Imagine / Build / Grow**, six principles and SelectedWorkShowcase.

**Proposed narrative grouping**:
1. **The Desire:** why create worlds and investigate human existence?
2. **The Discovery:** how curiosity developed into systemic creative design and connected disciplines.
3. **The Continuing Practice:** what is actually made, reviewed, corrected or still planned?

Show the founder's documented work as **process and evidence**, not inflated commercial credentials, institutional endorsement or guaranteed impact. Keep three capability domains and six principles accessible as full detail instead of collapsing or deleting them.

**Potential takeaway:** “This studio practices the way of thinking its worlds are built with.”

## 7. Contact — one honest conversation

**Source:** app/contact/page.tsx delegates to ContactExperience; existing provider/security contracts remain mandatory.

**Recommended microcopy** (adapt to actual support scope): “Your idea does not need to be finished to ask a question.” / “One clear question is enough to begin a conversation.”

Preserve the existing inquiry categories and simple form. **Do not add** a three-step wizard merely to echo the framework. Explain likely asynchronous follow-up without promising response times. Distinguish form submitted, provider accepted and human follow-up; never imply instant mentorship or newsletter consent.

## 8. Cross-page continuity

- All pages share a coherent visual language and the same **cause → consequence → next question** intellectual signature, not repetitive identical marketing blocks.
- Keep two primary routes in global discovery, with Explore/About/Contact as supporting tasks.
- A visitor returning from an interactive example should have a truthful next destination; avoid losing context behind unrelated promo cards.
- Prefer deep links to **currently published** WOS lessons and story resources. Route links must be inspected and verified at implementation time.
- Retain reader freedom to read fiction without creator training; retain creator freedom to use the system without Asthortera lore.

## 9. Required QA before replacement copy

Review every suggested headline for voice, meaning in Indonesian/English, evidence status, readability, mobile wrapping, semantic heading hierarchy, search metadata, real CTA destination and non-regression. Proposed copy is **not** automatically production-approved byte-for-byte.
