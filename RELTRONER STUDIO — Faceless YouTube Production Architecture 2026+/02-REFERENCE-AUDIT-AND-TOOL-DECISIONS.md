# 02 — Screenshot Reference Audit and Zero-Additional-Cost Tool Decisions

**Version:** 1.0-draft | **Date:** 2026-11-03 | **Status:** researched architecture, installation not implied

## 1. Reference inspection method

The reference screenshots describe a *code-driven* production practice. They are evidence of what was visible in a third-party demonstration, not evidence that the linked tools, models, or capabilities are installed on the founder's Windows machine. Implementation details such as exact rendering internals, proprietary interface code, and actual licenses cannot be inferred solely from a screenshot.

The principal inferred loop is:

**AI instruction → scene manifest → motion code → browser/renderer preview → frame capture → sound design → final encoding → human review → targeted revision.**

The essential user requirement is **change one sequence without unnecessarily rebuilding everything**, with sound design preserved as a first-class production concern.

## 2. Screenshot-to-capability mapping

| Reference | Visible or implied component | Meaning | Decision |
| --- | --- | --- | --- |
| 01 | Apple Design skill by Emil Kowalski | Fluid interface and motion design advice | Optional visual principles |
| 02 | Impeccable design guidance | Design critique, consistency, styling | Optional; audit dependency/license |
| 03 | Playwright MCP | Browser automation, page inspection, screenshots | Recommended for QA |
| 04 | Claude Video 2.0 install | AI-assisted motion graphics skill, presets | Prototype/reference |
| 05–07 | Review sheet and sound-cue workflow | Per-shot feedback, independent audio work | Build simplified local equivalents |
| 08–10 | Claude Artifacts and preset gallery | Design exploration and previews | Inspiration, not a required runtime |
| 11–12 | VoiceStudio and voice comparison | Synthetic narrator selection and playback | Optional local experiment |
| 13 | Claude context compaction | Agent context management | Workflow hygiene only |
| 14–15 | Faceless creator pipeline | Script, audio, illustration, motion, repeatable distribution | Adopt structure, reject mass-copying |
| 16–18 | Code-driven frame/audio/MP4 pipeline | Deterministic rendering and packaging | Core production design |

Screenshot grouping numbers refer to the supplied reference sequence; they are not independently verified footage from a repository's latest release.

## 3. Tool responsibility matrix

| Layer | Preferred tool | Existing / free basis | Boundary |
| --- | --- | --- | --- |
| Research and topic development | ChatGPT Plus, Gemini, NotebookLM | Already possessed | Do not copy unverified claims into canon |
| Coding operator | Claude Code, subject to Claude Pro entitlement and limits | Already possessed | No assumption of unlimited agent use |
| Versioned creative sources | GitHub, local git | Existing | Read-only during video production |
| Primary scene engine | Remotion | Free only under applicable license terms | Validate local Windows setup |
| Alternative reference implementation | Claude Video 2.0 | GitHub project | Do not assume seamless Windows support |
| Animation primitives | React, CSS/SVG, permissible animation libs | Local/open-source | Deterministic code preferred |
| Browser inspection | Playwright and optional Playwright MCP | Free software | Restrict browser access and scopes |
| Audio/video encoding | FFmpeg | Local free software | Confirm local binary and license distribution |
| Synthetic voice MVP | CapCut text-to-speech, subject to current free availability | Existing CapCut use | May be manual per scene |
| Synthetic voice experiment | VoiceStudio | Local project | Models may be large, CPU slow; rights differ |
| Auxiliary TTS experiment | edge-tts | Free package | Service terms and reliability require checks |
| SFX and music | YouTube Audio Library | Free under track-specific terms | Record attribution requirements |
| Audio editor | Audacity | Free and open source | Human listening remains mandatory |
| Optional generated B-roll | Google Flow | Existing plan credits if entitled | Not a production dependency |
| Final manual editor | CapCut | Existing tool | Do not make CapCut project the sole source of truth |
| Upload and measurement | YouTube Studio | Existing channel | No unsupported claims about reach |

## 4. Primary engine selection: Remotion

Remotion is the proposed **single authoritative renderer** because it exposes compositions, time-based parameters, React components, and a scriptable local export workflow. Under the applicable individual/small-organization license, it may meet the no-extra-spend requirement. Verify the actual current license *before* use; licensing and eligibility may change.

Remotion is **proposed, not installed or technically accepted**. A Windows CPU-only spike must demonstrate:

1. Preview a 9:16 short locally.
2. Render a selected composition or defined scene range.
3. Preserve typography and layout on mobile dimensions.
4. Export deterministic images and an encoded MP4.
5. Verify a changed scene does not alter unrelated scene assets.
6. Deliver acceptable quality and runtime on the actual machine.

Do not run Remotion and Claude Video 2.0 as two competing authoritative timelines. Treat Claude Video 2.0 as a style/preset inspiration or isolated spike until its contracts and dependencies are understood.

## 5. Claude Video 2.0 reference

Repository: https://github.com/ItsssssJack/claude-video-2

The demonstrated project uses preset-style motion graphics, design selection, and video-rendering tooling. The screenshot refers to HyperFrames, GSAP, browser rendering, optional provider-generated clips, FFmpeg, and an installation check. Specific release behavior and current dependency licensing require inspection. Do not copy the original creator's brand assets, templates, or examples wholesale without permissions.

**Recommended acceptance condition:** reproduce *one* simple, self-authored 10-second scene as an exploratory comparison; select the stack based on observed reproducibility and operational cost, not marketing promises.

## 6. Design and browser tooling

- [Impeccable](https://impeccable.style/): optional style and interface consistency guidance. Command counts are version-specific; avoid encoding a screenshot's older count as a permanent fact.
- [Playwright MCP](https://github.com/microsoft/playwright-mcp): agent-accessible browser inspection and accessibility-oriented automation; validate invocation under the chosen IDE.
- [Playwright](https://playwright.dev/): scripted screenshots and visual assertions can run separately from MCP.
- [Ray Fu Claude skills guide](https://www.raycfu.com/guides/claude-skills-i-use): research reference only. Do not install every skill; minimize surface area, tool conflicts, and context overhead.
- [Apple Design skill reference](https://www.emilkowal.ski/): design inspiration rather than a required video-rendering engine.

**Security:** treat third-party skills as executable code and instructions. Review package scripts, outbound requests, transitive dependencies, secrets requirements, cache size, and license conditions before running. Do not grant repository or payment account write permissions unnecessarily.

## 7. Synthetic narration options

### A. CapCut TTS — MVP

Advantages: available to the founder, low initial technical cost, useful for testing whether an episode actually needs narration. Disadvantages: possibly manual export, voice presets or availability can change, less deterministic automation. Confirm voice language, commercial use policy, and watermark/export conditions.

### B. VoiceStudio — optional local test

Repository: https://github.com/debpalash/VoiceStudio

Advantages: local experimentation, voice casting, possible repeatable outputs. Constraints: downloaded models and environments may require considerable disk space and compute; supported OS/model/license details must be read directly. CPU-only rendering may be slow. Record version and model provenance.

### C. edge-tts — conditional prototype

Repository: https://github.com/rany2/edge-tts

Useful for automated voice samples. Reliance on online service behavior is a risk. Confirm permitted usage before it becomes the production voice provider; free package availability is not itself proof of unrestricted commercial rights.

**Voice rule:** no personal vocal recording and no unauthorized impersonation of an identifiable person. Compare voices by pronunciation, intelligibility, pacing, and usage rights, not simply emotional attractiveness.

## 8. Google Flow applicability and spending gate

Product: https://flow.google.com/

Google Flow may provide optional environmental establishing footage if the founder's actual account includes permitted credits. “Gemini Pro” is an informal product description; it must not be treated as proof of a particular Google AI subscription entitlement. Country availability, account eligibility, monthly credit grants, credit prices, and feature availability can change.

**Mandatory preflight:** check effective account tier, credit balance, cost per generation, usage rights, watermark and AI-disclosure implications. **Never purchase extra credits** under this program.

Use Flow for non-authoritative cinema and atmosphere, *not* exact maps, canonical statistics, textual overlays, identifiable character consistency requirements, or source-of-truth rewriting. If Flow is unavailable, the pipeline continues with original Reltroner images, SVG, code-driven camera motion, and compositing.

## 9. Zero-incremental-spend is a constraint, not “zero real cost”

- No new subscriptions, billed APIs, paid footage, rented GPU, or paid cloud rendering.
- Existing Claude Pro, Gemini, ChatGPT Plus, NotebookLM, and CapCut may be used **only within already available access**.
- Local compute, time, electricity, connectivity, equipment wear, storage, and existing subscriptions still have real costs.
- Some free tiers cap usage or restrict commercial distribution.
- Never assume “free to download” means “free of copyright, attribution, or model terms.”

## 10. Explicit decisions versus open questions

**Recommended decisions (proposal only):** scene-manifest authority; local renderer; separate audio cues; source provenance; no automatic paid calls; human release gate.

**To verify in the technical spike:** Remotion license eligibility, local Node/FFmpeg availability, render performance, Windows filesystem behavior, CapCut TTS export workflow, usable rights for voice/SFX assets, Flow entitlement, and reliable audio cue synchronization.

**Blocked until verified:** any assertion that the system is installed, the voice engine is licensed for a specific use, Google Flow credits are available, or selective re-render works on the actual computer.

## 11. Primary third-party references

- https://www.remotion.dev/
- https://www.remotion.dev/license
- https://github.com/ItsssssJack/claude-video-2
- https://github.com/microsoft/playwright-mcp
- https://playwright.dev/
- https://impeccable.style/
- https://www.raycfu.com/guides/claude-skills-i-use
- https://github.com/debpalash/VoiceStudio
- https://github.com/rany2/edge-tts
- https://ffmpeg.org/
- https://www.audacityteam.org/
- https://www.youtube.com/audiolibrary
- https://flow.google.com/

**Reference freshness policy:** these URLs are external source pointers, not assertions of perpetual pricing, eligibility, license, or feature counts. Reverify at install and before each distribution decision.

## 12. Narrative technique reference — *Talk Like TED* (2026-11-03 patch)

Carmine Gallo's *Talk Like TED* is a **storytelling and presentation-design reference**, not a software tool, renderer, rights-granting service, canonical Reltroner source, or YouTube recommendation specification. The three interpreted delivery dimensions are **emotional**, **novel**, and **memorable**.

The relevance to the reference screenshots is the difference between merely animating boxes and **delivering a meaningful idea**: one source-backed human question, a distinct contrast/mechanism, and a memorable image or sound cue. The faceless adaptation depends on original scripts, synthetic voice casting, sound design, and deliberate scene pacing rather than pretending to have a live TED presenter.

Consult [11 — ENM Storytelling Standard](11-EMOTIONAL-NOVEL-MEMORABLE-STORYTELLING-STANDARD.md). External source: [Carmine Gallo's explanation](https://www.carminegallo.com/the-3-things-the-worlds-best-presentations-have-in-common-salesforce-com-blog/) and [publisher's book page](https://read.macmillan.com/lp/talk-like-ted-by-carmine-gallo/). No new subscriptions or integrations are required for the editorial method.

## Addendum — Reltroner/skills audit and selective adoption (2026-11-06)

[Reltroner/skills at commit ca45fc496a3436251f191354091d557da31c15b5](https://github.com/Reltroner/skills/tree/ca45fc496a3436251f191354091d557da31c15b5) contains **19 SKILL.md directories** and a Claude plugin marketplace declaration. The repository README describes demonstration/educational skill examples; the document skills have distinct source-available licensing conditions. This is not proof of installation on the founder's computer.

**Editorial/routing patterns:** internal-comms (format selection), doc-coauthoring (context → revision → reader test), discernment-nudge (internal fact/reasoning check), frontend-design (specific visual decisions), and skill-creator (clear triggers and tests). **Conditional production helpers:** webapp-testing, canvas-design, algorithmic-art, theme-factory (inspiration only). **Not for the default pipeline:** unrelated document/API/gif/academy/MCP skills; especially **exclude Anthropic brand-guidelines from Reltroner brand decisions**. Never assume Claude Pro includes metered Claude API usage.

This is an **advisory skill-selection layer** applied to existing Remotion/FFmpeg, voice, audio and communication contracts. The repo's third-party installer scripts or included fonts must not be executed/copied merely because they are present. See [12 — Skills Routing](12-SKILL-ROUTING-AND-COMMUNICATION-QUALITY-ARCHITECTURE.md) for all 19 classifications and [13 — Evaluation](13-SKILL-ROUTER-OPERATOR-CONTRACT-AND-EVALUATION.md) for concrete triggers/tests.

**New current communication version:** [Communication Framework v1.3, §§22–23](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/principles/reltroner-studio-communication-framework.md). The earlier ENM-oriented notes remain valid but are now accompanied by the anti-slop and format-routing layer.
