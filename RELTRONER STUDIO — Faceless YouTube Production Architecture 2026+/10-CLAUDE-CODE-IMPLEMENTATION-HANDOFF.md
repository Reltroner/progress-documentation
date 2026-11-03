# 10 — Claude Code Implementation Handoff and Engineering Acceptance Tests

**Version:** 1.0-draft  
**Role:** Ready-to-adapt implementation brief, not evidence that a CLI or repository exists  
**Scope:** A bounded zero-additional-spending Windows production spike

## 1. Why this handoff exists

The previous documents define policy and desired behavior. This handoff translates them into a bounded implementation brief for an AI coding agent, minimizing unnecessary files, unverified assumptions, scope expansion, and paid-tool dependencies.

Use only after the founder selects the pilot phase and checks source authority and software licensing. Engineering execution should remain compatible with any higher-priority repository/owner policy, including restrictions on where AI agents may write.

## 2. Implementation objective

Build a **locally operated and reproducible scene-based faceless video MVP** at a separate workspace, tentatively C:/Projects/reltroner-video-studio, with one 9:16 Depcutland pilot.

The system must:
- read approved Reltroner content snapshots without altering them;
- validate schema-driven episode and scene definitions;
- render each scene independently from code;
- associate synthetic Indonesian voice and relative-frame audio cues;
- export an episode via local tools;
- support one targeted scene revision with verifiable regression boundaries;
- preserve audio rights and source provenance;
- require a human approval before any upload;
- never make a paid API call or create a new recurring service charge.

**Out of scope:** automated YouTube upload, a large design gallery, a multi-user SaaS app, paid AI rendering, continuous agent monitoring, background jobs requiring a hosted platform, and unrelated Reltroner site/LMS modifications.

## 3. Exact input data the agent should request/read from the workspace

- Current authoritative source file revisions, including the master creative constitution and Depcutland topic reference.
- The architectural documents in this folder.
- Installed runtime versions (Node, npm, git, FFmpeg, available browser).
- Available disk and realistic rendering hardware constraints.
- A small set of approved visual assets and their rights.
- Approved synthetic narration sample(s), model/provider permission evidence.
- Approved SFX/ambience with associated license and attribution records.

If an input is missing, mark it pending and create a deterministic test fixture rather than asserting it exists.

## 4. Non-negotiable operational guardrails

1. Read relevant files before editing anything.
2. Produce a minimal implementation plan with affected paths.
3. Do not change any canonical content repository, website app, infrastructure, DNS, Keycloak, LMS, or paid account settings.
4. Do not install packages globally without authorization.
5. Do not download opaque scripts or use unreviewed executables.
6. Use one authoritative timebase: integer frames.
7. Use stable episode/scene IDs and explicit asset references.
8. Make all rendering locally reproducible with pinned tool versions.
9. Use no new paid products, APIs or Flow credit purchases.
10. Do not invent successful command outputs or approval events.
11. Validate changes with tests and report observed evidence.
12. Never publish or upload without explicit human release authorization.

## 5. Incremental implementation tasks

### Task A — Repository shell

Create only the folders and config needed for a single test scene. Include README, package lock, .gitignore, baseline test harness and clear build steps. Avoid adding a web server/database unless technically necessary for local preview.

### Task B — Manifest validator

Validate:
- unique and ordered scene IDs;
- non-negative integer frames, positive durations;
- actual full-timeline coverage;
- valid source and asset IDs;
- expected audio cue placement;
- required license and evidence fields;
- explicit video language, aspect ratio and output settings.

Return non-zero exit status with path-specific errors. Add fixtures for duplicate scenes, gaps, out-of-range cues and unresolved sources.

### Task C — Static/animated 9:16 scene renderer

Render one scene using Remotion (subject to verified license), from a bundled original or placeholder asset whose permissions are clear. Confirm output dimensions, FPS, render duration and readability. Use explicit typography, safe-zone overlay and reusable composition interface.

### Task D — Voice and audio bus assembly

Load existing approved local narration; do not call a paid TTS API. Add one ambience and two illustrative SFX anchored relative to a scene. Use FFmpeg to mix and package the audio. Verify actual output with ffprobe and a listening test.

### Task E — Multi-scene and selective revision

Expand to the pilot's six ordered scenes with the durations in 08-PILOT-EPISODE-DEPCUTLAND.md. Record content fingerprints. Revise SC-004's visual motion only. Validate that other scene source/output remains unchanged where expected; rebuild final assembly and inspect transitions.

### Task F — Local review and report

Expose simple scene selection and preview via an appropriate local tool or filesystem outputs. An elaborate production UI is not required. Generate a text/JSON report listing changed files, rendered scenes, duration, key QA checks, and remaining human reviews.

## 6. Required acceptance tests

| ID | Input | Expected |
| --- | --- | --- |
| T-001 | Valid six-scene 55-second manifest | Validation succeeds and total frames = 1650 |
| T-002 | Duplicate SC-004 ID | Validation fails |
| T-003 | Scene with negative duration | Validation fails |
| T-004 | Timeline with unintentional gap | Validation fails |
| T-005 | Unknown image/audio asset ID | Validation fails |
| T-006 | Audio cue past scene end | Validation fails |
| T-007 | Audio track missing a license record | Validation or release gate fails |
| T-008 | 1080×1920 30 fps scene preview | Expected file and metadata exist |
| T-009 | Change only SC-004 camera params | Only relevant cache invalidated |
| T-010 | Revise SC-004 with invariant duration | Final episode stays at 1650 frames |
| T-011 | Narration longer than allotted | Warning/block; no silent truncation |
| T-012 | SFX relative frame after upstream scene shift | Absolute timing recomputed |
| T-013 | Simulated paid API requirement | Operation rejected without invocation |
| T-014 | Missing founder approval | Upload/release remains blocked |
| T-015 | Missing FFmpeg binary | Clear diagnostic; no fake success |
| T-016 | Finished export | Entire file actually plays with audible mix |
| T-017 | Change source SHA | Affected provenance validation reruns |
| T-018 | Invalid caption bounds | Visual QA warning/failure |
| T-019 | Intentional silence | Human review explicitly records intent |
| T-020 | Incomplete synthetic-media disclosure decision | Release gate blocked when required |

Automated tests should make no assumption that human listening, canon approval, or commercial rights can be established algorithmically.

## 7. Suggested CLI interface — proposed, not implemented

~~~powershell
npm run video:validate -- --episode depcutland-001
npm run video:preview -- --scene SC-004
npm run video:render-scene -- --scene SC-004
npm run video:mix-audio -- --episode depcutland-001
npm run video:assemble -- --episode depcutland-001
npm run video:inspect -- --episode depcutland-001
npm test
~~~

Avoid creating misleading no-op scripts that return exit code 0 while silently skipping work.

## 8. Ready-to-paste agent instruction

~~~text
PROJECT: RELTRONER VIDEO STUDIO — P1 LOCAL TECHNICAL SPIKE

Read the documentation in:
Reltroner/progress-documentation/
RELTRONER STUDIO — Faceless YouTube Production Architecture 2026+/

Treat its claims as a proposed architecture, not an installed system.
First inspect the local environment and relevant source-of-truth files.

GOAL:
Implement only the smallest Windows-local code-driven video pipeline
needed to render and inspect one 9:16 scene with an independent audio cue.
The intended primary engine is Remotion plus FFmpeg, subject to current
license and environment verification.

NON-NEGOTIABLES:
- Incremental new spending: Rp0.
- Do not invoke metered provider APIs or buy credits.
- Do not change canonical Reltroner, website, LMS, VPS, or unrelated files.
- Do not record or clone the founder's voice.
- Keep the source repository read-only and cite source commit revisions.
- Use integer-frame scene timing and deterministic asset manifests.
- Keep synthetic voice, ambience, and SFX as identifiable layers.
- Do not publish or declare human acceptance on your own.

EXECUTION:
1. Inventory toolchain versions, free disk, and any missing prerequisites.
2. Identify exact files to create and relevant licenses.
3. Build the minimal project and validator with negative tests.
4. Render an original 9:16 test scene using permitted assets.
5. Assemble at least one licensed audio cue and a placeholder approved
   synthetic narration file, if available.
6. Verify output with ffprobe, visual preview, and actual artifact paths.
7. Report all changed files, commands, failures, and residual blockers.
8. Stop after the agreed technical spike; do not implement additional
   interface features, models, backend services, or deployment pipelines.

DEFINITION OF DONE:
A reproducible local scene preview, schema validation tests, real
audio/video inspection, no billable external calls, and an honest report
of which human review gates are pending.

If a prerequisite or rights record is missing, mark the result blocked
and show a minimal fallback instead of claiming production readiness.
~~~

## 9. Required final implementation report

Include:
- achieved scope and actual branch/commit if versioned;
- environment and tool versions;
- changed paths;
- test command results and any skipped checks;
- output path, dimensions, FPS, duration, and hashes;
- measured audio checks plus outstanding listening review;
- source and licensing status;
- spending/credit activity statement supported by observed actions;
- known blockers and a minimal next step.

## 10. Conditions for broader work

Do not proceed from a single scene spike to a full production environment until the founder has inspected the evidence. Extend one tested capability at a time: validator → scene renderer → audio mix → targeted revision → pilot → manual publication.

This keeps the project's technical ambition subordinate to its actual creative purpose, available resources, and operating authority.
