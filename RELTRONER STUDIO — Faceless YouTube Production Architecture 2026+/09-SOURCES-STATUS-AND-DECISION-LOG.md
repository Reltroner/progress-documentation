# 09 — Source Index, Verification Status, Open Decisions, and Audit Trail

**Version:** 1.0-draft | **Baseline date:** 2026-11-03  
**Purpose:** distinguish reference evidence, design proposals, future acceptance, and facts that may change.

## 1. Source verification vocabulary

- **Directly inspected (repository):** GitHub file or directory content was actually read during the preceding research/documentation workflow.
- **Official reference:** URL identifies provider documentation; its current terms must be checked before use.
- **Screenshot observation:** a capability visibly shown in the user's reference screenshots; not proof of an installed or supported runtime.
- **Proposed architecture:** recommended design requiring implementation.
- **Operationally accepted:** only after specific test evidence and explicit human acceptance (none declared here).
- **Externally published:** only when a verified URL and publication record exist (none declared here for the pilot).

## 2. Directly inspected Reltroner sources

| Reference | Role | Observed editorial meaning |
| --- | --- | --- |
| [Master source of truth](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/principles/reltroner-studio-master-source-of-truth.md) | Apex creative authority | Creative compounding + civilizational simulation, limits on identity and canon |
| [Communication framework](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/principles/reltroner-studio-communication-framework.md) | Subordinate operational guide | Relevance, value translation, evidence, optional invitations |
| [Content tree](https://github.com/Reltroner/reltroner-studio-remodeling/tree/main/content) | Source inventory | Broad collection of blogs, principles, factions, characters, series and more |
| [Depcutland profile](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/factions/depcutland.md) | Pilot topic | Archival/neoclassical/epistemic civilization; canon-status distinctions matter |
| [The Abyss of Comfort](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/series/the-abyss-of-comfort.md) | Narrative examples | Active story and planned forward arcs are distinguished |
| [No Copy-Paste Worldbuilding](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/blog/no-copypaste-worldbuilding.md) | Authorship ethos | AI output must be refined rather than blindly accepted |
| [YouTubers Have Channels, I Have a Civilization](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/principles/youtubers-have-civilization.md) | Historical creative perspective | Platform reach is not the same as owned worldbuilding |

The content tree was observed to have approximately 486 entries under content/ during research; this is a point-in-time inventory, **not** a fixed episode count or guarantee of published canonical readiness. Some files are indexes or drafts.

## 3. External tool references

| Tool/source | URL | Verification action before production |
| --- | --- | --- |
| Remotion | https://www.remotion.dev/ | Confirm current capabilities and system requirements |
| Remotion licensing | https://www.remotion.dev/license | Confirm founder eligibility and distribution terms |
| Claude Video 2.0 | https://github.com/ItsssssJack/claude-video-2 | Inspect repo, package scripts, licenses, compatibility |
| Playwright MCP | https://github.com/microsoft/playwright-mcp | Validate supported host/client and permission scope |
| Playwright | https://playwright.dev/ | Confirm browser install and screenshot usage |
| Impeccable | https://impeccable.style/ | Audit version and installation source |
| Ray Fu skill guide | https://www.raycfu.com/guides/claude-skills-i-use | Curate only relevant skills; no mass installation |
| VoiceStudio | https://github.com/debpalash/VoiceStudio | Confirm Windows, model languages, weights and rights |
| edge-tts | https://github.com/rany2/edge-tts | Confirm service permissions and reliability |
| FFmpeg | https://ffmpeg.org/ | Verify downloaded binary/version/license |
| Audacity | https://www.audacityteam.org/ | Verify local version and export support |
| YouTube Audio Library | https://www.youtube.com/audiolibrary | Record each audio track's attribution/license |
| Google Flow | https://flow.google.com/ | Verify account tier, location, credits, generation terms |
| Reltroner website | https://www.reltroner.com/ | Validate route availability at upload |
| YouTube Studio | https://studio.youtube.com/ | Review analytics, upload, disclosure settings |

Do not treat any unverified numerical credit allowance, model price, feature count, or included package entitlement as permanent. Recheck in the founder's account.

## 4. YouTube policy and analytics references

- Recommendations and viewer experience: https://support.google.com/youtube/answer/141805
- Shorts-related signals and analytics: https://support.google.com/youtube/answer/11914225
- Audience retention and key moments: https://support.google.com/youtube/answer/9314415
- Monetization and originality/inauthentic content: https://support.google.com/youtube/answer/1311392
- Altered/synthetic content disclosure: https://support.google.com/youtube/answer/14328491
- Copyright information: https://support.google.com/youtube/answer/2797466

These links are starting points. They are not a substitute for checking the currently applicable policy or any copyright owner's specific terms at publication.

## 5. Decisions made only at proposal level

| ID | Choice | Rationale | Confidence / status |
| --- | --- | --- | --- |
| D01 | Local, scene-based rendering | Revision precision and no metered render costs | Proposed |
| D02 | Remotion as preferred primary engine | Code-driven React composition and repeatability | Proposed; untested locally |
| D03 | FFmpeg final assembly | Deterministic accessible media processing | Proposed |
| D04 | Audio-first independent tracks | Cue preservation and genuine sound design | Proposed |
| D05 | Human approval for canon and publishing | Source integrity and authorship | Required by operating plan |
| D06 | CapCut TTS for earliest MVP | Existing access, minimal setup | Conditional on account and rights |
| D07 | VoiceStudio for later evaluation | Voice casting/local experimentation | Optional, untested |
| D08 | Flow optional only | Existing credits may add cinema, cannot be dependency | Proposed |
| D09 | Pilot Depcutland | Concrete canonical topic and distinctive visual contrast | Candidate |
| D10 | Two pilots over initial experiment | Tests cross-pillar reuse instead of upload volume | Candidate |

## 6. Explicitly unresolved items

- Local Remotion installation, actual renderer speed and version.
- Current licensed Remotion use under founder's circumstances.
- Current entitlement of Claude Pro coding agent workflows.
- Whether the founder's Google account enables Flow and the remaining credits.
- Indonesian TTS voice availability, rights, pronunciation, and quality.
- Approved fonts, imagery, soundtrack, ambience and SFX asset inventory.
- Exact safe zones for current YouTube Shorts UI at release time.
- Actual private channel analytics and audience composition.
- Whether user-approved tools permit reliable voice export in the chosen format.
- Pilot script approval, render pass, audio listening, and publication decision.

**No item above should be relabeled “done” without the evidence packet described in the operator SOP.**

## 7. Evidence capture template

~~~yaml
evidence_id: "EV-YYYYMMDD-001"
phase: "P1"
requirement: "Render 9:16 scene locally"
tested_at: null
machine: null
tool_versions: {}
command: null
expected: "1080x1920 MP4 and audible audio"
actual: null
artifact_hash: null
pass: null
reviewer: null
limitations: []
~~~

Do not populate result fields before the test occurs.

## 8. Documentation change policy

- Preserve the distinction between **proposed**, **tested**, **accepted**, and **published**.
- Link any significant architectural change to a dated decision and rationale.
- Update tool and policy assumptions when providers change.
- Keep canonical fictional data in the authoritative content repositories; this documentation is a media-operations derivative.
- Add specific acceptance logs in future revisions instead of rewriting the original research as if later evidence always existed.
- Never claim commercial outcomes or production readiness from a planning document alone.

## 9. Current attestation

As of the baseline documentation date, this folder records an architecture and experiment plan. It does **not** represent an installed Reltroner Video Studio, a passing renderer pipeline, an approved synthetic voice, a production-ready audio mix, a published pilot, or measured growth of the existing YouTube channel.

## 10. Storytelling reference and scope clarification — 2026-11-03

**Book:** Carmine Gallo, *Talk Like TED: The 9 Public-Speaking Secrets of the World's Top Minds* (2014).

**Author-confirmed organizing components:** emotional, novel, memorable. The operational adaptation for faceless Reltroner Studio media is developed in [11 — ENM Storytelling Standard](11-EMOTIONAL-NOVEL-MEMORABLE-STORYTELLING-STANDARD.md).

**Source references:**
- https://www.carminegallo.com/books/talk-like-ted/
- https://www.carminegallo.com/the-3-things-the-worlds-best-presentations-have-in-common-salesforce-com-blog/
- https://read.macmillan.com/lp/talk-like-ted-by-carmine-gallo/

**Evidence status:** publicly described presentation method, not directly measured YouTube results or a guaranteed neuroscience law. It does not supersede the studio's constitutional sources.

**New proposal decision D11:** augment editorial scripts and review with ENM classification, original visual/audio memory anchors, and anti-manipulation checks. **Status:** documented, untested in an actual video.

**No claim:** no increase in views, retention, subscribers, conversions or voice quality is established by the documentation patch.

## 11. 2026-11-06 skills audit and Communication Framework v1.3 integration

**Directly inspected repository:** [Reltroner/skills, main at ca45fc496a3436251f191354091d557da31c15b5](https://github.com/Reltroner/skills/tree/ca45fc496a3436251f191354091d557da31c15b5) (commit date 2026-10-28). Tree audit: **19 directories containing a top-level SKILL.md**. Marketplace metadata organizes sample skills into several groups; repository documentation describes them as educational/demonstration materials and warns that behavior in different Claude products can differ.

**Directly inspected Communication Framework:** [reltroner-studio-communication-framework.md](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/principles/reltroner-studio-communication-framework.md), **v1.3**, lastUpdated **2026-11-06**, source blob SHA **9a54fad8bcd02d9aa3e2f11d6d6ee712d2e5502c** at the time of this audit. New section **§23** covers source-routed AI communication, anti-slop, cold-reader review, and **COM-27–COM-34**; §22 preserves ENM. Earlier references to v1.2 are historical baselines and should not be interpreted as the current version.

**Source pattern examples inspected:** internal-comms, doc-coauthoring, frontend-design, discernment-nudge, skill-creator, webapp-testing, algorithmic-art, canvas-design, theme-factory, brand-guidelines, web-artifacts-builder, mcp-builder, and others by repository metadata. The Anthropic brand-guidelines source defines Anthropic colors and fonts and is **excluded** as Reltroner creative authority.

**D12 (proposed):** Task-specific skill routing, not all-skills installation.  
**D13 (proposed):** Skills as lower-trust procedural input to the approved source and communication framework.  
**D14 (proposed):** Integrate §23 anti-slop + §22 ENM + existing video/audio gates.  
**D15 (proposed):** Evaluate against SK-01–SK-20 before claiming skill routing reliability.  
**D16 (preserved):** Rp0 incremental spending; no extra API/cloud charges, no automatic publishing.

**Verification limit:** This is a repository-content audit and documentation design, not installation, skill execution, cold-reader testing, a rendered video, live channel analytics, or production acceptance.

Companions: [12 — Skills Architecture](12-SKILL-ROUTING-AND-COMMUNICATION-QUALITY-ARCHITECTURE.md) and [13 — Operator Tests](13-SKILL-ROUTER-OPERATOR-CONTRACT-AND-EVALUATION.md).
