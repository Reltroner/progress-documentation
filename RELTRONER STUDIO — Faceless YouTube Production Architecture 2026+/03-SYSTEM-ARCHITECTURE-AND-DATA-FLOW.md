# 03 — Target System Architecture, Repositories, and Data Flow

**Version:** 1.0-draft | **State:** proposed | **Design constraints:** Windows-first, local-first, scene-addressable, no additional spending

## 1. System context

The proposed system is **Reltroner Video Studio**, a separate local production workspace. Its purpose is to transform authored source material into video episodes while preserving source provenance and creative control.

### Sources and consumers

- **Inputs:** published Reltroner Markdown, source metadata, original site imagery, editorial topic briefs, compatible licensed audio, optional AI footage.
- **Operators:** human creative director, AI coding assistant, local deterministic scripts.
- **Outputs:** approved scripts, scene manifests, previews, voice assets, SFX cue sheets, final master MP4, captions, thumbnail assets, release records.
- **External delivery:** YouTube Studio and relevant reltroner.com destinations.
- **Feedback:** YouTube Analytics and voluntary audience response; not automatic canon changes.

## 2. Logical data flow

~~~text
RELTRONER CANON AND CONTENT (read-only)
  | source path + revision + status + cited claims
  v
RESEARCH AND EDITORIAL BRIEF
  | topic + audience + hook + evidence + limitations
  v
APPROVED SCRIPT
  | sentences + timings + pronunciation notes
  v
EPISODE AND SCENE MANIFESTS
  | scene IDs + visuals + timing + narration + SFX cues
  +-------------------+--------------------+
  |                   |                    |
  v                   v                    v
SCENE RENDER      VOICE RENDER       LICENSED ASSETS
  |                   |                    |
  +-------------------+--------------------+
                      v
              AUDIO / VIDEO ASSEMBLY
                      |
                      v
                 PREVIEW AND QA
                      |
          +-----------+-----------+
          |                       |
          v                       v
    TARGETED REVISION         HUMAN APPROVAL
          |                       |
          +----> revalidate       v
                         FINAL MASTER + CAPTIONS
                                  |
                                  v
                         YOUTUBE STUDIO UPLOAD
                                  |
                                  v
                         ANALYTICS / EDITORIAL REVIEW
~~~

The scene manifest is the authoritative intermediate representation; neither a CapCut editing session nor an AI conversation history is sufficient as the sole reconstruction record.

## 3. Proposed local repository

The following structure is a proposed implementation target, **not an existing verified local repository**.

~~~text
C:/Projects/reltroner-video-studio/
  README.md
  CLAUDE.md
  package.json
  package-lock.json
  config/
    brand.json
    render.json
    audio.json
  content-sources/
    source-manifest.json
  templates/
    asthortera-cinematic/
    civilization-explainer/
    creative-systems/
  src/
    components/
      Typography.tsx
      SceneTransition.tsx
      SafeZone.tsx
    compositions/
      EpisodeComposition.tsx
  assets/
    approved/
    licenses/
  audio-library/
    ambience/
    sfx/
    music/
    licenses/
  videos/
    depcutland-001/
      episode.json
      sources.json
      script.md
      scenes/
      voice/
      audio-cues.json
      storyboard/
      previews/
      outputs/
      release-record.md
  scripts/
    validate.mjs
    render-scene.mjs
    mix-audio.mjs
    assemble.mjs
    inspect-output.mjs
  tests/
  docs/
~~~

**Repository boundary:** do not write generated video caches, runtime dependencies, or large rendered files into the canonical Reltroner content repository. Keep originals and approved assets under a separate provenance-controlled storage strategy. Use .gitignore for generated/cache directories, or separately governed large-file storage if later needed; do not silently create billable LFS or Actions usage.

## 4. Required primary data objects

### SourceReference
- repository, relative path, immutable git blob/commit SHA;
- source title, relevant section, canon/evidence status;
- verification timestamp and last-approved interpretation;
- referenced claims and restrictions.

### Episode
- immutable episode ID, working title, audience route, production format;
- fps, height/width, total frames, language, editorial status;
- selected source references;
- ordered scene IDs and final release metadata.

### Scene
- stable scene ID, frame range, template, asset IDs, visual direction;
- voice and captions, relative audio cues, approval state;
- output cache fingerprint and dependencies;
- **no implicit authority to edit other scenes**.

### AudioCue
- stable cue ID, scene anchor, relative frame, asset reference;
- gain, fades, bus/layer assignment, licensing provenance;
- duration and resync policy.

### RenderArtifact
- scene or episode ID, render config, tool versions, output path/hash;
- source fingerprint, QA evidence, approval timestamp.

### ReleaseRecord
- final video hash, episode/commit references, title/description/version;
- rights/attribution, AI disclosure decision, human approval;
- upload timestamp and channel URL after publication.

## 5. Identity, reproducibility, and immutable records

Use stable IDs such as DEP-001, SC-004, VO-SC-004-v2, and SFX-DOOR-001. Do not reuse scene IDs for unrelated footage. Asset references must resolve through an explicit asset manifest.

Each successful output should be traceable to:
1. Exact source revision.
2. Episode manifest version.
3. Scene implementation revision.
4. Rendering dependencies and version.
5. Voice file hashes and TTS provenance.
6. Licensed audio asset hashes and attribution requirements.
7. Render settings and completed QA.

Prefer content hashes for cache invalidation and equality checks. Do not rely solely on file modification times.

## 6. Time model

Use **integer frames** as the authoritative internal timebase. For a 30 fps, 55-second video, total frames = 1650. Each scene occupies a half-open interval [startFrame, endFrame), with non-overlapping ordered coverage unless deliberate editorial transitions are explicitly modeled.

Support both 1080 × 1920 (9:16) and 1920 × 1080 (16:9), but do not design two layout systems before the MVP works. Final encoder specifications are validated on output, not inferred from config alone.

The total duration is derived from the manifest. Voice durations must be measured from actual rendered audio. A requested narration speed change can change timing and may require a downstream timeline rebuild.

## 7. Selective re-render contract

A scene-only change must:
- identify the affected scene and precise dependency footprint;
- invalidate only affected visual/audio output cache entries;
- preserve approved unaffected scene files bit-for-bit where feasible;
- rebuild the final mux/concat output when assembling the episode;
- rerun full-length timeline/audio checks, especially around boundaries;
- detect changes to narration length, transitions, master bus effects, and cross-scene ambience.

Selective rendering is an **optimization goal**, not a promise that every edit affects only one output byte. A global typography, tempo, narrator voice, font, or color change may legitimately require broad invalidation.

## 8. Render and orchestration layer

Proposed local commands (to be implemented; **not currently functional CLI commands**):

~~~powershell
npm run video:validate -- --episode depcutland-001
npm run video:preview -- --scene SC-004
npm run video:render-scene -- --scene SC-004
npm run video:mix-audio -- --episode depcutland-001
npm run video:assemble -- --episode depcutland-001
npm run video:inspect -- --episode depcutland-001
~~~

Every command should support clear exit codes, helpful errors, fixed output directories, and no paid network calls. Production rendering should ideally work offline after dependencies and approved assets are installed, except for optional external TTS/Flow generation.

## 9. State and approval flow

Episode: PROPOSED → RESEARCHED → SCRIPT_READY → SCRIPT_APPROVED → ASSETS_READY → SCENE_PREVIEW → QA_PENDING → RELEASE_APPROVED → EXPORTED → PUBLISHED.

Scene: DRAFT → RENDERED → NEEDS_REVISION or APPROVED. A revised scene returns to QA_PENDING. Publishing is never automatic.

**Only human release authorization may move the episode to RELEASE_APPROVED.** An AI agent may propose state changes, but must not forge approval evidence.

## 10. Observability and incident recovery

Keep per-step structured logs with task ID, scene ID, start/end time, executable version, exit status, and resulting artifact hashes. Avoid logging authentication tokens or private account data. Failed renders should preserve the last approved output. Retain source, script, manifest, and rights evidence independently of temporary caches.

Incident scenarios:
- corrupted preview → delete only affected cache and rerender;
- missing voice → keep episode blocked at ASSETS_READY;
- missing audio license → replace or remove the asset;
- incorrect lore → block publication, correct the script, update source record;
- local disk pressure → prune *unapproved temporary render* caches only;
- provider outage or expired credits → switch to local still-image animation.

## 11. Implementation acceptance contract

The architecture is provisionally accepted only for **design discussion**. Technical readiness requires a working Windows demo, repeatable CLI exit status, one approved MP4, scene-level revision evidence, audio/rights verification, and no new spending.

## 12. ENM narrative metadata and authority (2026-11-03 patch)

Introduce a **storytelling brief** between research/source classification and script approval. It records: viewer's human question, emotional tension and shift, audience's expected assumption, one source-supported novelty/reframing, an honest one-sentence thesis, optional visual/sonic memory anchor, and required canon references. The brief is an editorial annotation, not new fiction canon and not a substitute for the source manifest.

**Data flow amendment:** `source references → evidence classification → ENM brief → founder-approved script → scene manifest → audio/visual render → ENM review + technical/canon/rights QA → final human approval`.

Optional proposed attributes may reside in `episode.storytelling` and `scene.storyRole` only after schema implementation and tests. Until then, use a standalone versioned Markdown/JSON brief. A specific scene's emotional treatment must be editable without altering unrelated approved scene content. Changes to voice text/duration or soundtrack dependencies still require audio and timeline revalidation.

ENM review is a human editorial gate. An agent cannot infer emotional impact or memorability from a successful render, a loudness metric, or a synthetic scoring value. See [11 — ENM Storytelling Standard](11-EMOTIONAL-NOVEL-MEMORABLE-STORYTELLING-STANDARD.md).

## Addendum — Source-bound skill routing as a preproduction adapter (2026-11-06)

**Updated logical flow:** read-only canon and website references → source/evidence classification → artifact/audience routing → **minimum relevant skill pattern** → ENM + Communication Framework §23 anti-slop review → founder-approved script/scene manifest → local visual/audio rendering → deterministic QA + real listening + human approval.

The router is initially a **static documented decision**, not a new autonomous backend, hosted service or renderer. Inputs: task type, audience, proof, approved sources/SHA, budget, allowable write paths and review owner. Outputs: selected pattern, exclusions, source packet, permitted deliverable, known unknowns and approval state.

Suggested optional artifacts for an *approved future implementation*: editorial/skill-routing-policy.md, editorial/source-packets/, editorial/reviews/, config/approved-skill-refs.json, tests/routing-contract/. They must not be presented as existing paths without runtime verification.

Keep source/canon repository read-only, preserve integer-frame scene identity and independent audio buses, and prevent downloaded SKILL.md from silently overriding the master constitution or invoking paid operations. Source pin: [Reltroner/skills ca45fc4](https://github.com/Reltroner/skills/tree/ca45fc496a3436251f191354091d557da31c15b5). Authoritative communication rules: [v1.3 §§22–23](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/principles/reltroner-studio-communication-framework.md).

For router contract and negative tests see [12](12-SKILL-ROUTING-AND-COMMUNICATION-QUALITY-ARCHITECTURE.md) and [13](13-SKILL-ROUTER-OPERATOR-CONTRACT-AND-EVALUATION.md).
