# 14 — Asthortera Ball TV: Season Contract and P7 Reusable Landscape Adapter

**Date:** 2026-11-07  
**Type:** Cross-repository production integration specification  
**Status:** Owner-directed TV adaptation decisions documented; P7 adapter **proposed / not implemented or visually accepted**  
**Scope:** The *Asthortera Ball* Countryball TV program only; genuine 3D, longer landscape episodes, reusable production  
**Non-goals:** No canon release, no TV season ratification, no story rewrite, no automatic YouTube publication, no new paid dependencies

## 1. Purpose and single-source ownership

This file is the **technical bridge** between the already authored Asthortera creative rules and the engineering in [claude-animated-shorts-engineering](https://github.com/Reltroner/claude-animated-shorts-engineering). It **does not replace** earlier documents 01–13, rewrite national lore, or create a second TV season bible.

| Decision / data | Single authoritative owner | What this document does |
| --- | --- | --- |
| Studio and canon precedence, publication boundary, narrative mode doctrine | [Reltroner Studio master constitution §§0, 23, 48–50](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/principles/reltroner-studio-master-source-of-truth.md) | Applies authority; never ratifies canon itself |
| TV program identity, season/arc/episode order, current opening | [Asthortera Ball franchise bible](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/series/asthortera-ball.md) | Consumes locked narrative references |
| Nation colors/emblems/accessories, speech/acting profiles, active P6-based 3D appearance | [Asthortera Countryball Character Reference Guide](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/characters/asthortera-countryball-characters.md) | Compiles named profiles into rig props |
| Relationship of TV to the novel/inter-series timeline | [Asthortera novel series roadmap](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/series/series-roadmap.md) | Keeps separate chronologies and IDs |
| Viewer-language, source disclosure, anti-slop and editorial copy | [Communication Framework v1.3](https://github.com/Reltroner/reltroner-studio-remodeling/blob/main/content/principles/reltroner-studio-communication-framework.md) | Applies editorial QA |
| Scene, audio, provenance, selective revision and release process | [Documents 03–07](README.md) in this folder | Extends, not forks, existing contracts |
| Running implementation, dependencies and technical evidence | [claude-animated-shorts-engineering `main`](https://github.com/Reltroner/claude-animated-shorts-engineering/tree/main) | Specifies **additive P7 work** |

**Precedence:** master constitution > relevant ratified canon and current franchise/character contracts > production architecture > individual manifest and agent output. Documentation being public on GitHub does not automatically mean every proposed fictional event is published canon.

## 2. Decisions to preserve, without resetting earlier work

1. **Keep WB-NPC-001 P6 as the genuine 3D base:** three-dimensional sphere/body, curved facial geometry with **mouth**, **exactly two detached volumetric hands**, plus lighting, shadows, motion and Remotion frame synchronization. **Do not rebuild a mouthless/handless model** to conform to an obsolete 2D visual restriction. No long arms, legs, feet or realistic humanoid anatomy.
2. **Named countryballs require national identity adapters:** country-specific palette, emblem placement, approved accessories, characteristic expression/motion and behavioral constraints. The generic white P6 sphere **is not** a finished Pasgerflitball, Reltronlandball or Depcutlandball.
3. **Series remains an ensemble:** Pasgerflitball is a strongly reusable **viewer gateway**, not a compulsory lead. The active S1E1 remains **"The Pencilfania Problem"** with its recorded cast. *The Wrong Kind of Wake-Up* and older outline material are **development candidates**, not silent substitutes or published episodes.
4. **Only country/civilizational personifications and related institutions** enter this initial TV production contract. Phantomkind and Cosmeilian species-centered characters/manifestation rigs are **deferred**, not retconned or deleted from Asthortera.
5. **The Abyss of Comfort season numbering remains separate.** Shared places, meanings and continuity are possible only after an explicit canon/chronology check.
6. **The P3/P5 legacy path is preserved** alongside P6. No forced migration that deletes `Pen`, `Pool`, `Actor`, earlier portrait compositions, archived frames, audio templates or tests.
7. A TV performance decision **does not itself approve a story, nation-specific artwork, season release or uploaded video**.

## 3. Separate three kinds of identity

- **Canon identity:** world/country/institution/personality with provenance and an explicit canon status.
- **Performance identity:** `countryball-3d-p6` rig topology and rendering behavior, including the expressive mouth and two detached hands.
- **Production identity:** stable `programId/seasonId/episodeId/shotId`, source revisions, renders, tests and human approval.

These are *different keys*. A character can reappear in many episodes without copying the source rig or changing its canon definition. A color/emblem change in a named-character adapter must invalidate relevant rendered shots but must not mutate source lore.

## 4. TV story hierarchy (upstream of the existing scene manifest)

```text
ASTHORTERA SHARED UNIVERSE / CANON AUTHORITIES
  └── PROGRAM: asthortera-ball  (not The Abyss of Comfort seasons)
      └── SEASON: narrative state transition, theme and causality
          └── STORY ARC: bounded connected investigation/conflict
              └── EPISODE: standalone meaningful change within the arc
                  └── SCENE: stable story unit, source and dialogue IDs
                      └── SHOT: camera/cast/environment/time asset unit
                          └── REMOTION FRAMES + AUDIO CUES + CAPTIONS
```

The **scene manifest remains the authoritative intermediate production representation** from documents 03–04. A season compiler must *emit* compatible episode/scene/shot/audio records from the narrative input, **not** introduce an unrelated second scene engine.

Season = consequential state cycle, not an arbitrary video-count or length requirement. Every episode should have a causal payoff; broader unresolved questions may persist. Canon state does not reset on season boundaries.

Narrative reading modes (master §49) transfer to video as **Current Lore** (characters/dialogue), **Backstory** (only causally necessary history) and **Wiki** (system explanation). Switch only when the audience needs context; return to Current Lore.

## 5. Minimal additive P7 repository layout — proposed, not installed

```text
src/production/
  contracts/             # program, season, episode, scene, shot, format
  canon/                 # source revisions + statuses, read-only adapters
  registry/              # nation profiles, P6 rig, world, camera, audio IDs
  timeline/              # integer-frame validation + compiler
  validation/            # cross-reference and continuity gates
episodes/landscape/asthortera-ball/
  season-01/             # story bible + manifests, all development-only
assets/registry.json     # allowlist/provenance of reusable assets
studio/src/production/
  LandscapeEpisode.tsx   # composition wrapper using existing 3D runtime
  SceneRenderer.tsx      # scene/shot renderer, no scene logic duplication
  CaptionLayer.tsx       # optional accessible captions
studio/scripts/production/
  validate-season.mjs
  compile-episode.mjs
  render-shot.mjs
  assemble-episode.mjs
  verify-output.mjs
tests/production/        # contract, identity, source and regression tests
.local/production/       # ignored renders, caches, voices, QA evidence
```

**Existing dependencies remain authoritative:** Three.js for 3D scenes/characters, Remotion for frame-based composition, captions, audio orchestration and render; the existing Python `templates/audio/*` foundation plus FFmpeg for local audio/muxing. The P6 rig is the live 3D base. Blender is **optional and later**, only for reusable models where a GLB import is demonstrably more efficient. No Blender runtime or additional dependency is required for P7A/P7B.

**Initial target profiles:** landscape `1920x1080 @ 30fps`, review `960x540 @ 30fps`, legacy portrait `1080x1920 @ 30fps`. These are proposed configuration profiles, **not** proof a landscape render already exists. Preserve frame-derived deterministic motion; do not use wall-clock effects.

## 6. Referenceable input contract (illustrative, not a shipped parser)

```json
{
  "schemaVersion": "tv-program-1",
  "programId": "asthortera-ball",
  "seasonId": "AB-TV-S01",
  "episodeId": "AB-TV-S01E01",
  "storyStatus": "development-material",
  "workingTitle": "The Pencilfania Problem",
  "format": "landscape-1080p",
  "fps": 30,
  "sourceRefs": [
    {
      "repository": "Reltroner/reltroner-studio-remodeling",
      "path": "content/series/asthortera-ball.md",
      "revision": "PIN_AT_BUILD",
      "status": "development-material"
    }
  ],
  "characterProfiles": [
    "henchowayball",
    "pencilfaniaball",
    "reltronlandball"
  ],
  "sceneIds": ["SC-001"],
  "narrativeModes": ["current-lore"],
  "approval": {
    "nationArt": "pending",
    "technical": "pending",
    "creative": "pending",
    "canonFreeze": false,
    "publication": "blocked"
  }
}
```

This intentionally short schema **does not invent full script timing or visuals**. Scene details, immutable frame counts, dialogue, audio cues, visual treatments and shot references belong in existing scene/episode contracts. `PIN_AT_BUILD` must be replaced by a verified source revision before production candidate status. A finished program adapter must validate that all listed IDs resolve and block missing nation profiles.

## 7. Reuse and selective rendering

- A **nation adapter** maps the existing P6 rig to a named Countryball identity; it must not fork the rig for every country. Store immutable approved per-character profiles with explicitly versioned color/emblem/accessory properties.
- A **world adapter** reuses procedural scenes (starting with P6 `ArchiveWorld3D` if visually appropriate) without copying the whole P6 episode story.
- **Shot fingerprints** must include character profile + rig version, world/materials/lighting, camera, episode/shot input, source revisions, renderer/configuration and referenced audio/caption decisions. Changing a shared dependency invalidates all affected shots.
- **Incremental sequence render** should cache only verified outputs; preserve unmodified scenes. Use distinct *draft / review / final* profiles and measure runtime/quality before increasing duration.
- Audio/captions/voice use scene-local utterance and cue IDs, global offsets computed from integer frames; never silently time-stretch narration or replace an owner's voice. Preserve separate music/ambience/SFX/dialogue buses; apply document 04 and licensing gates.
- QA and reports should be **machine-readable plus founder-reviewable**; only human review can approve camera feel, character look, writing, sound and publication. A technically successful MP4 is not published canon.

## 7.1 P7A implementation checkpoint — 2026-11-07

P7A source has been **squash-merged into GitHub `main`** via [PR #1](https://github.com/Reltroner/claude-animated-shorts-engineering/pull/1), merge commit `332c599cead10027a2524aa9048122f6ae7536c2`. The committed implementation contains: typed program/season/episode contracts, strict offline validation, a small countryball-only development fixture for active S1E1 *The Pencilfania Problem*, a read-only validation CLI, and automated contract tests. Source refs are commit-pinned once at program scope and referenced by key. The P6 genuine 3D rig remains a **reference**; no new nation mesh, renderer, synthetic dialogue, render cache or completed landscape episode has been created by this checkpoint.

**Evidence status:** GitHub source integration is confirmed; the owner's local P3–P6 `main` was verified clean and commit-identical before PR #1 merged. After the merge, local `main` must fast-forward to the current GitHub `main`. The Windows npm commands **have not yet been verified**: `npm run p7a:validate`, `npm run p7a:test`, `npm run typecheck`, `npm test`, and `npm run build`. GitGuardian's success is a security scan, not these tests. No P7 landscape video, creative acceptance, canon freeze or publication is implied. **Owner workflow policy:** one existing local working checkout on `main`; do not create local feature worktrees/branches. Any later P7 feature PR targets `main` directly.

## 7.2 P7B source implementation checkpoint — 2026-11-07

The engineering repository [`main`](https://github.com/Reltroner/claude-animated-shorts-engineering/tree/main) now contains the **P7B implementation source** for four provisional canon-referenced national profiles (Pasgerflitball, Reltronlandball, Depcutlandball, Pencilfaniaball), an additive adapter using **P6's existing mouth, genuine sphere and exactly two detached 3D hands**, procedural solid national emblems, Depcutland's fedora, and two Remotion landscape gallery-proof compositions (1920×1080 and 960×540; 120 frames at 30 FPS). A new local-only renderer supports stills, silent motion previews, a silent full-resolution proof and FFprobe validation. The source is documented in [`docs/P7B-NATIONAL-3D-LANDSCAPE-PROOF.md`](https://github.com/Reltroner/claude-animated-shorts-engineering/blob/main/docs/P7B-NATIONAL-3D-LANDSCAPE-PROOF.md).

**Acceptance remains pending:** these GitHub commits are source integration, **not** evidence that `npm run p7b:test`, `npm run typecheck`, `npm test`, `npm run build`, landscape stills, or an MP4 passed in the owner's Windows environment. The nation color render hexes and procedural emblem shapes/placement are development choices pending visual approval; the active S1E1 and its missing Henchoway visual profile are **not** silently changed. No additional local Git branch/worktree, new dependencies, canon freeze or publication is part of this phase.

## 8. P7 implementation gates and stop rules

| Gate | Deliverable | Acceptance |
| --- | --- | --- |
| P7A | Typed contracts/registries/season validation; additive structure | Existing P3–P6 tests and templates untouched; S1E1 identity/status guard |
| P7B | Nation-profile adapters + 16:9 proof using P6 real 3D rig | Mouth, exactly two detached hands, nation identities, 3D lighting, stable shadow, frame determinism; human visual inspection |
| P7C | Data-driven episode compiler, dialogue/caption/audio scene contract | Episode from manifest without writing new renderer; exact frame/cue synchronization |
| P7D | Incremental shot previews/renders/asset provenance | Targeted rerender proven; no cache reuse after dependency change; no `.local` tracking |
| P7E | Longer landscape episode pilot | Real FFprobe, voice/caption rights, staged QA, performance evidence and founder approval |
| P7F | Optional asset factory (Blender → approved GLB) | Only if a concrete reusable-asset need and license review justify it |

**Stop:** Do not remove working P3–P6 code, rewrite source canon through a video build, import unlicensed third-party animations, clone another creator's artwork/dialogue, add paid APIs/cloud render, merge unapproved season outlines, commit original `.local` media, or claim technical/creative/canon PASS without evidence.

## 9. Evidence and release semantics

The separate [engineering repository](https://github.com/Reltroner/claude-animated-shorts-engineering/tree/feat/white-ball-npc-v2) contains P3–P6 source and project logs describing completed **technical** prototype work. Its reported test/render outcomes are **not evidence of an implemented P7 season system** or creator approval of a nation-specific TV asset.

Status progression: **concept → development material → production candidate → canon freeze → published canon**, with technical QA and creative approval recorded independently. Preserve full draft freedom until the canonical publication boundary.

The original [55-second Depcutland Short blueprint](08-PILOT-EPISODE-DEPCUTLAND.md) is an **independent candidate pilot**, not Season 1 of Asthortera Ball; the original architecture documents are historical design context and remain valid except where this explicitly scoped supplement introduces a more specific TV adapter.

## 10. Source and maintenance rules

- **Canon owner:** Studio master; franchise and character specifics are delegated to their existing documents.
- **TV narrative owner:** Asthortera Ball franchise bible; season proposals and S1E1 corrections go there, not in this technical document.
- **Visual owner:** Countryball guide; change in mouth/hand topology requires explicit owner approval and regression review.
- **Production owner:** Existing engineering repository; code and runtime evidence must be verified there.
- **Communications owner:** Framework v1.3; use source-bound phrasing rather than marketing predictions.
- **No duplicate full story bibles:** references and small adapters only. Update source revision locks and a one-line change record if authorities change.
