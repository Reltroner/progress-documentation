# 12 — Source-Routed Skill Architecture and Communication Quality Layer

**Document status:** Proposed operational architecture — not an installed skill runtime  
**Version:** 1.0-draft | **Audit date:** 2026-11-06  
**External skill source:** [Reltroner/skills, pinned at ca45fc496a3436251f191354091d557da31c15b5](https://github.com/Reltroner/skills/tree/ca45fc496a3436251f191354091d557da31c15b5)  
**Communication authority:** [Reltroner Studio Communication Framework, current v1.3 (§22–§23)](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/principles/reltroner-studio-communication-framework.md)  
**Creative authority:** Existing binding Reltroner Studio Master Source of Truth; no change in constitutional precedence  
**Spending:** No additional paid tooling, provider API, new subscription, rented infrastructure, or purchased credits  
**Channel identity:** 100% faceless; founder voice is not recorded or imitated

## 1. Problem and design goal

The current video architecture supplies a source-to-scene rendering pipeline, independent audio tracks, human review, and an emotional / novel / memorable (ENM) editorial layer. The new requirement is to make AI assistance **task-aware, selective, source-bound, resistant to generic AI output, and testable**.

A large collection of Claude skills is not itself a production system. Automatically loading every example skill would cause overlap, inappropriate format selection, foreign brand styling, additional context cost, and potential executable dependency risk. The proposed solution is a **capability-routing layer**, not a second renderer, a new model subscription, or an unbounded multi-agent swarm.

**Core rule:** Choose the smallest relevant skill *pattern* for the actual production task; always bind it to Reltroner-approved context, evidence classes, and the current communication contract. Skill advice never replaces source authority or quality evidence.

## 2. Repository audit and source status

The referenced repository's main branch was inspected on **2026-11-06** and resolved to commit **ca45fc496a3436251f191354091d557da31c15b5**. The tree contained **19 top-level skill directories with SKILL.md**. The README describes the collection as Anthropic-oriented examples for Claude, some open-source and some source-available; it explicitly frames examples as educational/demonstration implementations and calls for testing before critical use. The marketplace metadata groups subsets into example skills, document skills, Claude API, academy guidance, and discernment guidance.

This document borrows **procedural patterns only**. It does not install those packages, fork them into Reltroner's brand rules, claim they are universally supported in ChatGPT/Gemini/Claude, or authorize execution of packaged scripts.

Immutable snapshot: https://github.com/Reltroner/skills/tree/ca45fc496a3436251f191354091d557da31c15b5  
Live index: https://github.com/Reltroner/skills/tree/main  
Marketplace declaration: https://github.com/Reltroner/skills/blob/main/.claude-plugin/marketplace.json  
Licensing notices: https://github.com/Reltroner/skills/blob/main/THIRD_PARTY_NOTICES.md

### 2.1 All 19 skills classified for the YouTube workflow

| Source skill | Routing disposition | Practical use for Reltroner Video Studio | Restriction |
| --- | --- | --- | --- |
| internal-comms | **Selected pattern** | Choose correct communication format for release notes, FAQs, channel updates, incident notices, and community responses | Not a universal corporate voice or video-script template |
| doc-coauthoring | **Selected pattern** | Source gathering → iterative script/storyboard refinement → independent cold-reader test | Do not pretend a separate reader test ran if it did not |
| frontend-design | **Selected pattern** | Subject-specific visual grammar, legible mobile typography, deliberate motion and interface writing | Do not import generic stylistic bans as canonical brand rules |
| discernment-nudge | **Selected pattern, internally** | Check essential facts, reasoning and missing context before approval | Do not append ritual questions to every viewer-facing video |
| skill-creator | **Selected pattern for authoring/evals** | Define precise triggers, input/output contract, negative tests, and failures for local video tasks | Not proof of passing a benchmark or an installed runtime |
| webapp-testing | **Conditional engineering skill** | Local Playwright screenshot tests, preview browser QA, console diagnostics | Only relevant if an actual local browser preview exists |
| algorithmic-art | **Conditional visual prototype** | Original seeded p5.js artwork for abstract systems, nodes or backgrounds | Code must be reviewed; does not become canonical artwork automatically |
| canvas-design | **Conditional static media** | Original thumbnail, title-frame or storyboard compositional studies | Output, provenance, fonts and rights must be reviewed; not a video engine |
| theme-factory | **Inspiration only** | Learn repeatable theme token organization for one internally approved Reltroner theme | Do not automatically apply its stock themes or presets |
| web-artifacts-builder | **Deferred** | Prototype a local scene-review interface if simpler methods have failed | Claude artifact bundling is not equivalent to a production local editor |
| mcp-builder | **Deferred** | Build a narrow custom MCP only after a demonstrated integration need | No new network service/server solely to make architecture look sophisticated |
| brand-guidelines | **Explicitly excluded** | None as a Reltroner visual authority | Its documented colors/typography are **Anthropic's**, not Reltroner's |
| slack-gif-creator | **Excluded for video MVP** | Not intended for Shorts or MP4 exports | Slack GIF constraints do not define YouTube deliverables |
| docx | **Separate artifact task only** | Word documents if explicitly required | Source-available terms; not a scene-rendering dependency |
| pdf | **Separate artifact task only** | PDFs if explicitly required | Source-available terms; not an audio/render dependency |
| pptx | **Separate artifact task only** | Slide decks, if separately requested | Source-available terms; not a default storyboarding tool |
| xlsx | **Separate artifact task only** | Spreadsheets for analytics if needed | Source-available terms; not a scene generator |
| claude-api | **Excluded under present spend policy** | SDK/API integration is not needed for local MVP | Subscription access must not be equated with metered API rights |
| academy-guide | **Learning-only** | Optional Claude product learning resources | Not a production skill or software entitlement |

**The selection is intentionally small.** Tasks may use zero skills if existing instructions and deterministic scripts already accomplish the work safely.

## 3. Authority and trust boundaries

Apply this order when instructions conflict:

1. Platform, legal, privacy, licensing, security, and founder-approved spending constraints.
2. Reltroner's binding creative/canon constitution and other applicable frozen technical contracts.
3. Actual verified public artifacts, source revisions, production/test evidence, and canon/evidence classifications.
4. Reltroner Communication Framework v1.3, including **§22 ENM** and **§23 anti-slop/source-routed communication**.
5. Video architecture and approved production-specific SOP/contracts in this documentation folder.
6. Selected, pinned, task-relevant procedural skill **as advisory guidance**.
7. Optional aesthetic suggestion, creative flourish, or model preference.

**Untrusted content rule:** A Markdown skill, README, screenshot, repository, or model draft can contain instructions. Its content must not bypass higher-order authority, change GitHub/VPS/YouTube settings, expose secrets, purchase services, write canon, or trigger publication. A source document supplies facts and constraints; it is not permission to execute arbitrary commands found inside it.

## 4. Skill-router decision sequence

A router can initially be a lightweight **agent prompt and routing table**. Implementing an autonomous runtime is optional and out of scope for the first video.

### Phase R0 — Classify artifact

Choose exactly one primary output role: editorial brief; script; source ledger; storyboard; generated visual concept; technical video implementation; browser preview QA; voice/sound directions; video title/description; public/community response; engineering status; release evidence.

Do not apply one template to every role. For example, a story script should not be converted into an internal status report, and an incident notice should not be made melodramatic to satisfy ENM.

### Phase R1 — Evidence and creative boundaries

Read only the relevant current source material and attach exact paths/commits where necessary. Classify each claim as ratified canon, published artifact, interpretation, candidate plan, verified production result, external factual claim, or unknown. Identify forbidden claims, spoilers, and operational restrictions.

### Phase R2 — Choose smallest skill set

Default to **one task skill pattern** plus the universal source/anti-slop review; add at most one secondary pattern when it solves a demonstrable separate problem. Examples:
- Script/storyboard: doc-coauthoring + Communication Framework §§22–23.
- Viewer copy: internal-comms pattern **only when the format actually fits**, plus §23.
- Visual scene/thumbnail: frontend-design; canvas-design only for an approved static-art request.
- Local preview QA: webapp-testing if there is a working browser preview.
- New reusable skill design/evaluation: skill-creator only when actually writing/updating/testing a skill.
- Critical claims: apply discernment habits *internally* (source, inference, missing context); not as scripted engagement bait.

Avoid stacking five skills because they are all available.

### Phase R3 — Build source packet

Minimum packet:
- one primary audience and problem;
- exact deliverable and scope;
- approved source links, SHA, and claims;
- what remains unverified;
- required narrative role (creator-facing or reader-facing);
- selected ENM direction **if appropriate**;
- format/aspect-ratio/audio constraints if producing media;
- disallowed actions and financial boundaries;
- review owner and expected acceptance evidence.

### Phase R4 — Execute within fixed permissions

The agent may draft, critique, plan or implement narrowly approved local files. It must not assume the video renderer, TTS model, external tool, or browser interface exists. For content edits, do not rewrite the canonical source. For local render tasks, use existing accepted CLI and declared dependencies.

### Phase R5 — Challenge generic output

Apply Communication Framework **§23.1 anti-slop**: replace interchangeable praise, generic phrases, inflated “revolutionary” claims, invented social proof, empty multi-part slogans, fake intimacy, overlong intros, and irrelevant CTAs with specific, source-backed mechanisms or remove them.

Apply ENM **only when useful**: emotion earned from an identifiable stake; novelty from sourced consequence; memorable takeaway that survives caveats. “Emotional + novel + memorable” is not a mandate to make every scene sensational.

### Phase R6 — Cold-reader and technical reviews

Conduct a *real* cold-reader test if available; otherwise mark **NOT EXECUTED** and perform a clearly labeled single-reviewer checklist. For video, test audio and visuals with actual rendered artifacts when they exist. No automatic scores can certify authentic emotion, human comprehension, voice quality, rights, or canon correctness.

### Phase R7 — Explicit release state

Gate: **PASS / REVISE / DEFER / NOT APPLICABLE** with evidence, reviewer, and remaining unknowns. A model-generated “looks great” is not a release record. Only founder-approved outputs may advance toward manual publishing.

## 5. Source-routed communication and video handoff

Each output type has a distinct minimum structure and selected procedural pattern.

| Deliverable | Audience and purpose | Preferred skill pattern | Must retain | Common failure |
| --- | --- | --- | --- | --- |
| YouTube Short script | First-time viewer; one question | doc-coauthoring + ENM | source claims, human stake, one novelty, one takeaway | encyclopedia dump or forced TED drama |
| Storyboard | Video operator; shot sequence | frontend-design, optional canvas-design | scene/frame IDs, 9:16 readability, source/status | stunning visuals detached from script |
| Explainer graphics | Viewer; demonstrate a mechanism | frontend-design, optional algorithmic-art | actual causal states, legibility, licenses | decorative particles hiding missing argument |
| Voice/sound brief | Synthetic narrator and audio operator | production audio contract + §22 | text, cue IDs, relative frames, rights | emotive SFX covering speech |
| YouTube title/description | New viewer and platform | §23 source-and-format routing | clear promise, truthful status, live relevant link | clickbait, invented rank, commercial offer |
| Community response | Genuine discussion | internal-comms/general communication pattern | thread premise, one useful answer, optional question | generic “join our community” |
| Production report | Founder/operator | internal-comms status pattern | actual files/tests/limits/next decision | “production ready” with no render |
| Local preview QA | Engineer | webapp-testing pattern | screenshots/logs, viewport and frame evidence | assuming script ran or ignoring mobile UI |
| Skill/agent task contract | Coding operator | skill-creator pattern | triggers, scope, expected failures, negative tests | unbounded auto-agent and fake evaluation |
| PDF/slides/xlsx deliverable | Explicit external artifact request | respective specialized artifact skill | exact scope and applicable license | importing a document skill into video runtime |

## 6. Anti-slop editorial gates from Communication Framework v1.3

The framework introduces **COM-27–COM-34** in addition to preexisting COM-01–COM-26:

| Gate | Video-production interpretation | Minimum evidence |
| --- | --- | --- |
| COM-27 — Format routing | A Short, long essay, source notice and release report use different formats | Artifact/audience/intent recorded |
| COM-28 — Source traceability | Material public/fictional claims are sourced or explicitly qualified | Source manifest; review notes |
| COM-29 — Specificity | One necessary Reltroner-specific mechanism survives | Claim-to-example trace |
| COM-30 — No invented authority | No fabricated metrics, released canon, traction, client or shipped product | Evidence-status audit |
| COM-31 — No decorative padding | Voice and motion do not add empty praise, forced beats or filler | Script and scene audit |
| COM-32 — Audience fit | Viewer understands the idea without internal jargon | Plain-language comprehension prompt |
| COM-33 — Cold-reader test | An outsider can state what is known, uncertain and next | Actual independent review or marked pending |
| COM-34 — Human accountability | Founder reviews consequential claims and final media | Signed approval, artifact hash |

COM-21–COM-26 remain applicable to emotional integrity, novelty, memorable accuracy, synthetic voice identity, sound design, and human ENM review. The full quality bar is **source-first + ENM when useful + anti-slop + technical/audio QA + human release approval**.

A text that merely feels “AI-generated” is not automatically bad, and a human-written paragraph is not automatically good. Critique observable unsupported claims, template repetition, and reader utility—not speculative authorship detection.

## 7. Integration with the existing video system

Do **not** create a second timeline, renderer, source of truth, or AI API backend. Keep the established flow:

**Read-only content → Source packet → Selected skill pattern → Draft → Evidence/ENM/anti-slop review → Approved scene manifest → Remotion/FFmpeg + synthetic audio → Preview QA → Final human release.**

A minimal proposed routing record can exist alongside the episode manifest (not inserted into the validator until its schema supports it):

~~~json
{
  "routingSchema": "skills-1.0-proposed",
  "episodeId": "depcutland-001",
  "taskId": "TASK-SCRIPT-001",
  "artifactType": "youtube-short-script",
  "audience": "first-time-asthortera-viewer",
  "primarySkillPattern": "doc-coauthoring",
  "secondarySkillPattern": null,
  "skillSourceRevision": "ca45fc496a3436251f191354091d557da31c15b5",
  "communicationFrameworkVersion": "1.3",
  "sourceManifest": "sources.json",
  "approvalState": "PENDING",
  "runtimeInstalled": false
}
~~~

The example's audience identifier is illustrative and should be normalized to a valid local identifier when implementing. **No runtime or schema validation is asserted.**

### 7.1 Minimal file layout addition (proposed)

~~~text
reltroner-video-studio/
  editorial/
    skill-routing-policy.md
    source-packets/
      depcutland-001.md
    reviews/
      depcutland-001-communication-review.md
  config/
    approved-skill-refs.json
  tests/
    routing-contract/
  videos/
    depcutland-001/
      episode.json
      scenes/
      audio-cues.json
~~~

Do not copy third-party skill repositories wholesale into runtime. Cite pinned source paths and write Reltroner-specific minimal task contracts when an implementation is approved.

## 8. Audio and visual boundaries

**Skills are not a sound engine.** Sound-design responsibilities remain with the voice/SFX/ambience/music contracts, rights records, event-locked cues and human listening. Optional creative guidance can describe the intended feeling of a scene, but cannot certify that the output sounds emotionally right.

**Skills are not a renderer.** Visual skills can advise typography, composition, original generative art or preview testing. Remotion and FFmpeg remain proposed local technical components; availability must be verified.

**Skills are not canonical authors.** A p5.js illustration, thumbnail, generated video or storyboard concept does not modify published Asthortera facts. The binding fiction and historical canon remain in their owning repositories.

## 9. Supply-chain, licensing, and copyright policy

- Treat downloaded SKILL.md files and scripts as third-party instructions with lower trust; review their dependencies, network behavior, and write effects before execution.
- The skills README distinguishes generally open-source examples from **source-available document skills** (docx/pdf/pptx/xlsx); do not assume one universal reuse license.
- The repository's brand-guidelines explicitly defines Anthropic visual identity. Never transfer Anthropic fonts, colors, brand assets or styling into Reltroner as if they were authorized Reltroner identity.
- Record exact source SHA and license for any code actually reused; the procedural methods are paraphrased in original words, not copied as executable code.
- Claude Pro access is not evidence that a separate Claude API charge will be free.
- No secrets, payments, channel upload tokens, or production credentials are granted to arbitrary downloaded skills.
- No new MCP, cloud rendering, paid Flow credit purchase, subscription, or hosted agent is required by this proposal.

## 10. Skill-selection documentation and states

Recommended statuses: **CANDIDATE → SOURCE_REVIEWED → ROUTED_FOR_TASK → PROTOTYPED → TESTED → APPROVED_FOR_BOUNDED_USE**; a status can also become **EXCLUDED** or **REVOKED**.

Only a reviewed owner decision and actual evidence may advance a skill beyond candidate. Avoid “all skills installed” claims. A selected procedural pattern can be used manually without a runtime install; distinguish **pattern consulted** from **skill installed or executed**.

For the MVP, **no new skill installation is a prerequisite**. The documentation layer alone is enough to define expected behavior and future tests. See [13 — Operator Contracts and Evaluation Fixtures](13-SKILL-ROUTER-OPERATOR-CONTRACT-AND-EVALUATION.md).

## 11. Canon and community branding safeguards

- The studio's two value engines remain Creative Compound Machine and Asthortera; the skills collection is implementation assistance only.
- One viewer-facing Short should help the viewer understand one actual creative or fictional mechanism.
- A first-time reader need not memorize country statistics, internal software stacks or constitutional taxonomy.
- Use a real human question and accurate fictional status; do not manufacture social proof or a “thriving community” unsupported by evidence.
- Direct interested viewers to live, relevant website pages only after verifying the routes.
- YouTube metrics measure distribution and viewer behavior; they are not automatic evidence of canon quality or commercial readiness.

## 12. Decisions and next evidence

**Proposed ADR-SK-01:** Selective, task-routed skill patterns; no universal auto-loader.  
**Proposed ADR-SK-02:** Source/communication authority precedes imported procedural skills.  
**Proposed ADR-SK-03:** Skills remain advisory; approved local deterministic renderer remains authoritative for output.  
**Proposed ADR-SK-04:** Anti-slop and ENM checks share a release review, without forcing formulaic writing.  
**Proposed ADR-SK-05:** No third-party vendor brand guidelines; no metered APIs or paid dependencies.  
**Proposed ADR-SK-06:** Mark review/test/installation evidence separately.

**Current attestation:** The repository was inspected and this is a documentation-level design. No new skill has been installed, no automated routing has run, no script has passed evaluation, and no YouTube production result is claimed.

## 13. Source links

- [Reltroner/skills source snapshot](https://github.com/Reltroner/skills/tree/ca45fc496a3436251f191354091d557da31c15b5)
- [internal-comms](https://github.com/Reltroner/skills/blob/main/skills/internal-comms/SKILL.md)
- [doc-coauthoring](https://github.com/Reltroner/skills/blob/main/skills/doc-coauthoring/SKILL.md)
- [frontend-design](https://github.com/Reltroner/skills/blob/main/skills/frontend-design/SKILL.md)
- [discernment-nudge](https://github.com/Reltroner/skills/blob/main/skills/discernment-nudge/SKILL.md)
- [skill-creator](https://github.com/Reltroner/skills/blob/main/skills/skill-creator/SKILL.md)
- [webapp-testing](https://github.com/Reltroner/skills/blob/main/skills/webapp-testing/SKILL.md)
- [algorithmic-art](https://github.com/Reltroner/skills/blob/main/skills/algorithmic-art/SKILL.md)
- [canvas-design](https://github.com/Reltroner/skills/blob/main/skills/canvas-design/SKILL.md)
- [theme-factory](https://github.com/Reltroner/skills/blob/main/skills/theme-factory/SKILL.md)
- [brand-guidelines — excluded](https://github.com/Reltroner/skills/blob/main/skills/brand-guidelines/SKILL.md)
- [Communication Framework §23](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/principles/reltroner-studio-communication-framework.md)
