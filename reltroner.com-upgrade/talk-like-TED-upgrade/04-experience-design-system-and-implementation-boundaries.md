# 04 — Experience Design System, Interaction, Accessibility and Implementation Boundaries

> Status: OWNER-APPROVED EXPERIENCE DIRECTION / CANDIDATE VISUAL EXECUTION  
> Rule: improve meaningful interaction and cognitive clarity, **not** technical spectacle.

## 1. Unifying visual metaphor — The Causal Thread

One conceptual relation threads through the website: **idea → constraint → interaction → consequence → changed state → next possibility**. Visually, understated connections, transitions or related annotations may imply this sequence. The metaphor is a **design tool**, not a required decorative line on every component.

Visual goals:
- Premium Reltroner Studio navy/blue identity, dark-blue editorial science-fantasy tone, professional readability and restrained luminous emphasis.
- Images convey person, setting, emotional question or physical mechanism; surrounding copy communicates truthful status and actions.
- A single subject and readable hierarchy beat a collage of 12 unrelated abstractions.
- Preserve approved first-party CDN artwork, crop intent, subject visibility, source bytes and alt/context metadata.
- Do not embed all textual explanations, watermarks or numerous canon badges into art pixels. Place honest disclosure adjacent or in accessible metadata.

## 2. Motion grammar: meaningful state changes only

| Interaction | Allowed use | Must not do |
| --- | --- | --- |
| Reveal | Show that a decision causes a new condition | Hide the essential answer behind hover or animation |
| Connection highlight | Identify the precise dependency in a causal sequence | Create decorative motion without information |
| Before/after comparison | Make a changed world state visually inspectable | Present a fabricated historical or canon event as fact |
| Depth/lens switch | Current Lore / Backstory / Wiki or person/community/civilization | Change underlying example inconsistently |
| Optional feedback | Summarize model, own artifact and new question | Pretend an automated pedagogical score is validated |

Motion must respect **prefers-reduced-motion** and not be needed to understand the causal relation. Accessible semantic text, keyboard focus, visible states and nonanimated fallback are required. Avoid autoplay, scroll hijacking, excessive parallax and WebGL merely for branding.

## 3. Existing component reuse map

| Component / source | Proposed role | Guardrail |
| --- | --- | --- |
| app/page.tsx | Orient two audience routes and route to optional depth | Do not turn homepage into an LMS or lore encyclopedia |
| HomepageCdnArt | Existing editorial image carrier | Preserve asset URLs and integrity |
| CreativeLoop | Existing causal demonstration | Reuse; no forced duplicate wizard |
| app/creators/page.tsx, CreatorGoals | Recognizable creator situation/goal | Preserve personal choice and not storing a profile unless accurately verified |
| CreatorNotebook | Creator-owned input, output and portable Markdown | No new server save, account or silent AI transfer |
| app/readers/page.tsx, ReadingPreview | Person-first dilemma and narrative lens | Maintain one logically consistent noncanonical case |
| ReaderConnections, ReaderScales | Cross-institution effects and micro/meso/macro | Trace causality; avoid overstating fictional universality |
| app/explore/page.tsx, ExploreClient | Curiosity routing into existing taxonomy | Preserve existing four intents and archive collection coverage |
| app/about/page.tsx, SelectedWorkShowcase | Founder process and inspectable outputs | No unverified testimonials or commercial results |
| app/contact/page.tsx, ContactExperience | Low-friction inquiry and honest acknowledgement | No change to provider/security transport without separate contract review |
| Existing Navbar / MobileNavbar / Reltroner Navigator | Shared navigation and contextual help | Honor latest owner-approved mobile/desktop behavior, not an obsolete October mock |

Names are a **24 October source observation** and require reconfirmation at implementation HEAD. Reuse may take the form of a copy or section-order improvement without any new React components.

## 4. Information hierarchy and responsiveness

- At first viewport: one relevant H1, concise support sentence and clear **Creator / Reader** decision if homepage. Preserve secondary browsing routes in navigation.
- Maintain comfortable line length, semantic headings, accessible breadcrumbs and distinguishable CTA labels.
- On small screens, stack content in reading order **not** arbitrary CSS grid order; ensure focus and assistive reading order match visual intent.
- Preserve latest binding owner navigation instructions concerning mobile Navigator / hamburger / Reading Path; do **not** resurrect older rails or obsolete /start routes by blindly copying historic docs.
- Never hide access to Explore, About, Contact or published article navigation in pursuit of “three things only”.
- Tool output and user notes must remain legible without JavaScript motion or pointer hover.

## 5. Performance and asset responsibility

No new dependency, paid image service, remote animation player or image-generation vendor is justified merely by this upgrade. Existing assets may already carry the intended mood. Prefer CSS layout and component reuse.

Audit Core Web Vitals, critical image behavior, large background image cost, lazy/priority loading, CLS and semantic alt text with real preview measurements. Respect current CDN sync/revalidation contracts, including resource bytes changing without filename changes. Never “fix” broken imagery by silently substituting unrelated stock art.

## 6. Accessibility, privacy and trust

- Maintain keyboard routes for navigation, disclosure, modal/lens switching, worksheet and contact.
- Focus indicators, readable contrast, appropriate tap targets, visible form errors and screen-reader labelling remain required.
- Use reduced motion or no-animation as a fully functional mode.
- Avoid unrequested analytics or event tracking; if usability measurement is later added, enforce consent, minimal data and actual privacy disclosure.
- AI is optional where correctly supported; deterministic navigation and existing non-AI functionality must still work under quota/provider failure.
- Newsletter requires independent explicit consent and unsubscribe rules; contact submission is not newsletter sign-up.
- Preserve form abuse mitigation, server-only keys, no secrets in frontend, and exact provider delivery semantics.

## 7. Definition of “improve the interface”

A refinement is valuable if at least one is observed without introducing regressions: visitors orient faster; can explain mechanism more accurately; complete their creative artifact; follow a meaningful reader question; locate an appropriate published source; or complete a legitimate inquiry. Visual flair without improved experience is insufficient.
