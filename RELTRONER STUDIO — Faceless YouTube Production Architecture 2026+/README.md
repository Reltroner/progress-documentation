# RELTRONER STUDIO — Faceless YouTube Production Architecture 2026+

> **A proposed zero-additional-spending, code-driven, scene-addressable production system for original, fully faceless Reltroner Studio YouTube content.**

| Field | Value |
| --- | --- |
| Documentation baseline | 2026-11-03 |
| Document release | v1.0 — Architecture and Operating Proposal |
| Status | **DOCUMENTED / NOT YET IMPLEMENTED / NOT PRODUCTION ACCEPTED** |
| Primary production mode | Local Windows video rendering, independently addressable scenes |
| Editorial authority | Reltroner Studio's binding source-of-truth hierarchy |
| Narration | Synthetic voice; no recording or cloning of the founder's voice |
| Audio | Separate voiceover, ambience, sound effects, and optional music buses |
| Incremental spending policy | **Rp0 for new subscriptions, paid APIs, paid credits or hosted rendering** |
| Initial delivery experiment | One 55-second Depcutland Short, then one creator-facing reuse test |
| Release authority | Human/founder approval; no unattended publication |

## 1. Executive summary

Reltroner Studio holds original worldbuilding, creative-system, fictional-civilization, philosophical, and narrative source material in its own website and repositories. The proposed production architecture converts this material into visually coherent, narratively valuable YouTube episodes while preserving source authority, rights, and artistic judgment.

The critical workflow requirement is **sequence-level revision**: an operator should be able to request changes to a specific scene, for example “make the SC-004 camera slower but preserve narration and SFX,” without rebuilding all creative decisions or unnecessarily re-rendering unrelated scenes.

The architecture uses a source-verified editorial pipeline, **one authoritative scene manifest**, a local code-based renderer, independent synthetic speech and sound-design tracks, a review/QA stage, and a manual YouTube release gate. AI tools help draft, reason, code, and critique; they do not ratify canon, substitute for human listening, or authorize publication.

**This repository folder documents a target architecture, not an already installed or functioning video studio.** Any technical achievement must be independently verified and recorded.

## 2. Why this system exists

**Problem:** AI-generated videos, motion graphics, narration, and sound design become expensive, fragile, or hard to revise when created as a monolithic prompt-to-video export. A single timing or narration mistake may force disproportionate rework. Generic template outputs can also separate the channel from Reltroner Studio's authentic creative identity.

**Solution:** a local-first production environment with versioned episodes, independently addressable scenes, frame-based timing, approved assets, voiceover and audio cue registries, deterministic rendering and assembly, tracked dependencies, and scoped revision commands.

**Expected operational result (not yet demonstrated):** a reproducible faceless video workflow that can adjust a selected sequence, regenerate only the necessary artifacts, maintain sync, and provide inspection evidence before release.

**Potential strategic value:** translate the Creative Compound Machine and Asthortera into accessible viewer experiences, generate ethically earned discovery for reltroner.com, reuse original creative material, and reduce future production friction without new subscription spending. No views, subscriber growth, commercial conversion, or production efficiency improvement is claimed as measured.

## 3. Documentation index

Read the documents in this order. Each file stands alone but is designed to be followed together.

| Document | Coverage |
| --- | --- |
| [01 — Strategic Charter and Governance](01-STRATEGIC-CHARTER-AND-GOVERNANCE.md) | Studio positioning, original creative value, source hierarchy, canon and editorial authority, non-goals |
| [02 — Reference Audit and Tool Decisions](02-REFERENCE-AUDIT-AND-TOOL-DECISIONS.md) | Screenshot-by-screenshot identification, Claude Video 2.0, Remotion, Playwright, AI skills, VoiceStudio, Flow, licenses and choices |
| [03 — System Architecture and Data Flow](03-SYSTEM-ARCHITECTURE-AND-DATA-FLOW.md) | Data flow, repository structure, scene and asset identity, render orchestration, cache invalidation, status model |
| [04 — Scene and Audio Contracts](04-SCENE-AUDIO-SPECIFICATION-AND-REVISION-CONTRACT.md) | Example JSON manifests, integer-frame timing, four audio buses, synchronization, sound cue and targeted revision contracts |
| [05 — Operator SOP and QA](05-OPERATOR-SOP-LOCAL-WORKFLOW-AND-QA.md) | Stepwise production, Windows preflight, human review, automated QA, rollback, evidence records |
| [06 — YouTube Strategy and Measurement](06-YOUTUBE-CONTENT-STRATEGY-AND-MEASUREMENT.md) | Creator/readers pillars, audience-first hooks, Shorts and long-form positioning, distribution, policy, analytics |
| [07 — Security, Licensing and Rollout](07-SECURITY-LICENSING-BUDGET-AND-ROLLOUT.md) | Rp0 constraint, supply-chain review, rights registry, privacy, risks, phase gates, decision log |
| [08 — Depcutland Pilot Blueprint](08-PILOT-EPISODE-DEPCUTLAND.md) | 55-second 9:16 six-scene sample, Indonesian narration, audio directions, preview revisions and release checklist |
| [09 — Sources and Verification Register](09-SOURCES-STATUS-AND-DECISION-LOG.md) | Authoritative sources, official tool/policy references, verified versus proposed status, unresolved questions |
| [10 — Claude Code Implementation Handoff](10-CLAUDE-CODE-IMPLEMENTATION-HANDOFF.md) | Constrained engineer/agent brief, executable test targets, acceptance matrix, ready-to-adapt build instruction |

## 4. Non-negotiable constraints

1. **No incremental paid spending.** Existing subscriptions may be used within current entitlements; additional provider charges, credits, hardware rentals, paid stock or cloud rendering are not authorized.
2. **100% faceless.** No on-camera founder appearance, no personally recorded narration, no unauthorized voice impersonation.
3. **Studio identity comes first.** Reltroner is neither a generic AI-tools channel nor an undifferentiated lore encyclopedia; its two value engines must remain recognizable.
4. **Canon is read-only for video operations.** Source changes are governed elsewhere. Unpublished developments cannot be quietly represented as published lore.
5. **Audio is not an afterthought.** Voiceover, ambience, SFX and music have explicit timing, rights and mixing decisions.
6. **Local deterministic workflow by default.** Optional Google Flow footage must not be a hard dependency.
7. **Human review is mandatory.** The founder approves the message, pronunciation, sound design, artistic choices and final master before upload.
8. **YouTube policies and license rights apply.** Editorial originality, synthetic-media disclosure, asset-level rights, and accurate claims are mandatory release considerations.
9. **No automatic production acceptance.** A plan, screenshot, tool README or successful partial render is not the final release gate.

## 5. Simplified production flow

~~~text
RELTRONER SOURCES / ORIGINAL SITE (READ-ONLY)
        |
        v
RESEARCH -> CLAIM STATUS -> EDITORIAL SCRIPT
        |
        v
SIX-STAGE OR OTHER APPROVED STORY STRUCTURE
        |
        v
EPISODE + SCENE MANIFESTS (FRAME-BASED)
        |
        +--------------+---------------+
        |              |               |
        v              v               v
SCENE RENDER     SYNTHETIC VOICE    AUDIO / ASSET RIGHTS
        |              |               |
        +--------------+---------------+
                       |
                       v
          AMBIENCE + SFX + OPTIONAL MUSIC
                       |
                       v
            LOCAL ASSEMBLY + TECHNICAL QA
                       |
                       v
        HUMAN VISUAL / AUDIO / CANON APPROVAL
                       |
              +--------+---------+
              |                  |
              v                  v
       TARGETED REVISION   FINAL MASTER
              |                  |
              +--> REVALIDATE    v
                         MANUAL YOUTUBE PUBLISH
                                |
                                v
                       ANALYTICS + LEARNING
~~~

## 6. Proposed technical choices

| Function | Preferred approach | Notes |
| --- | --- | --- |
| AI coding operator | Claude Code with existing plan | Availability and usage caps must be verified |
| Editorial research | Existing ChatGPT/Gemini/NotebookLM | Evidence must be traced to sources |
| Primary timeline and video engine | Remotion | Proposed, subject to local tests and license eligibility |
| Encoding, muxing and final audio mix | FFmpeg | Local version must be verified |
| Browser visual testing | Playwright / optional Playwright MCP | Inspect scripts and permissions |
| Visual design reference | Impeccable, Apple Design and Claude Video 2.0 | Optional, not a second authoritative renderer |
| MVP synthetic narration | Existing CapCut TTS if permitted | Test voice rights, export and quality |
| Future local narration experiment | VoiceStudio | Conditional on models, disk, CPU and licensing |
| Sound and music resources | YouTube Audio Library, Audacity | Individual asset provenance required |
| Optional cinematic footage | Google Flow | Only existing eligible credits, no purchases |
| Release/analytics | YouTube Studio | Manual upload and human review initially |

These are **selected options for evaluation**, not confirmation of local installation or final commercial-license eligibility.

## 7. Pilot scope

**Working topic:** Why Must the Future Look Cyberpunk?  
**Source:** [Depcutland](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/factions/depcutland.md)  
**Format:** 9:16 / 1080 × 1920 / 30 fps / 55-second target

| Scene | Proposed duration | Role |
| --- | --- | --- |
| SC-001 | 0:00–0:05 | Hook |
| SC-002 | 0:05–0:14 | Contrast |
| SC-003 | 0:14–0:25 | Introduce Depcutland |
| SC-004 | 0:25–0:36 | Knowledge and institutional mechanism |
| SC-005 | 0:36–0:47 | Human question |
| SC-006 | 0:47–0:55 | Optional invitation |

Test one constrained change to SC-004, preserving voice, SFX relative-frame anchors and all other scenes. The pilot is a **candidate**; its script, final art, voice and release are not yet approved.

## 8. Rollout and evidence gates

| Gate | Required evidence | Present status |
| --- | --- | --- |
| Architecture documented | Linked specifications and decisions | Documentation created |
| Windows stack validated | Node, Remotion, FFmpeg, runtime metrics | Pending |
| Scene preview | Actual video and inspectable metadata | Pending |
| Audio and synthetic voice | Authorized voice asset, cues and listening review | Pending |
| Selective revision | Scoped SC-004 diff, cache and output check | Pending |
| Pilot full export | 1650-frame target validated against actual output | Pending |
| Founder release approval | Human approval record for the exact file | Pending |
| YouTube publication | Verified video URL and metadata | Pending |
| Audience impact | Actual channel metrics and commentary | Unknown / not evaluated |

Do not interpret the architecture-documentation gate as evidence that any later phase is complete.

## 9. Verified creative authority and external references

### Reltroner sources
- [Binding Master Source of Truth](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/principles/reltroner-studio-master-source-of-truth.md)
- [Subordinate Communication Framework](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/principles/reltroner-studio-communication-framework.md)
- [Full content repository](https://github.com/Reltroner/reltroner-studio-remodeling/tree/main/content)
- [The Abyss of Comfort](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/series/the-abyss-of-comfort.md)
- [Reltroner Studio](https://www.reltroner.com/)

### Production and publication references
- [Claude Video 2.0](https://github.com/ItsssssJack/claude-video-2)
- [Remotion](https://www.remotion.dev/)
- [FFmpeg](https://ffmpeg.org/)
- [Playwright MCP](https://github.com/microsoft/playwright-mcp)
- [VoiceStudio](https://github.com/debpalash/VoiceStudio)
- [Flow](https://flow.google.com/)
- [YouTube Audio Library](https://www.youtube.com/audiolibrary)
- [YouTube Studio](https://studio.youtube.com/)

Refer to document 09 for additional source, policy, and verification links. Third-party entitlements and rules are subject to change.

## 10. Change-control statement

This folder is an operational architecture record under the existing Reltroner creative constitution. It does not ratify new fiction canon, activate a commercial offer, change the website or LMS, establish new licensing rights, or authorize automatic publishing. Future implementation and approval results must be added as dated evidence instead of backdating a proposal into a completed deployment.

**Next legitimate action:** inspect the actual Windows environment and execute the limited local technical spike described in document 10, after explicit implementation approval.
