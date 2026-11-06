# 04 — Scene Manifest, Voiceover, Sound Design, and Revision Contracts

**Version:** 1.0-draft | **Status:** proposed schema and operating contract, not an implemented API

## 1. Core principle: make audio first-class

Video quality and editorial correctness are not sufficient without intelligible narration and synchronized sound. The audio production contract is **independent from, but synchronized with, the visual scene contract**.

Four preferred buses:
1. **Voice:** principal synthetic narrator; highest intelligibility priority.
2. **Ambience:** environmental room tone, exterior air, distant machinery, cosmic environmental metaphors.
3. **SFX:** localized events, transitions, impacts, paper movement, UI interactions, whooshes.
4. **Music:** optional, subordinate to narration and rights policy.

A fifth optional master bus may apply overall limiting/normalization during final assembly. Keep a music-free mode available for reflective, documentary, and copyright-conservative material.

## 2. Minimal episode manifest (illustrative)

~~~json
{
  "schemaVersion": "1.0-proposed",
  "episodeId": "depcutland-001",
  "title": "Why Must the Future Look Cyberpunk?",
  "status": "DRAFT",
  "format": {
    "width": 1080,
    "height": 1920,
    "fps": 30,
    "durationFrames": 1650,
    "language": "id-ID"
  },
  "contentRoute": "/readers",
  "sourceManifest": "sources.json",
  "sceneIds": ["SC-001", "SC-002", "SC-003", "SC-004", "SC-005", "SC-006"],
  "masterAudio": {
    "voiceBus": "voice",
    "ambienceBus": "ambience",
    "sfxBus": "sfx",
    "musicBus": "music"
  },
  "rightsApproved": false,
  "editorialApproved": false
}
~~~

This JSON is a proposal, not proof of a file or shipped application. The canonical timebase is frames. Validate the exact total against the sum of scene durations and any transition overlap.

## 3. Minimal scene manifest (illustrative)

~~~json
{
  "sceneId": "SC-004",
  "episodeId": "depcutland-001",
  "startFrame": 750,
  "durationFrames": 330,
  "visual": {
    "template": "asthortera-cinematic",
    "assetId": "depcutland-archive-approved-v1",
    "camera": "slow-dolly",
    "safeZoneProfile": "youtube-shorts-v1"
  },
  "narration": {
    "voiceAssetId": "VO-SC-004-v1",
    "text": "Teknologi tidak selalu harus memamerkan bentuknya.",
    "language": "id-ID",
    "pronunciationReview": "PENDING"
  },
  "subtitleTrackId": "SUB-SC-004",
  "audioCues": ["SFX-ARCHIVE-REVEAL-001"],
  "sourceRefs": ["SRC-DEPCUTLAND-001"],
  "approval": "DRAFT"
}
~~~

The asset ID is hypothetical and must resolve through the approved manifest before rendering. No original cinematic image is asserted to exist here.

## 4. Audio cue manifest (illustrative)

~~~json
{
  "cueId": "SFX-ARCHIVE-REVEAL-001",
  "sceneId": "SC-004",
  "relativeFrame": 18,
  "bus": "sfx",
  "assetId": "sfx-soft-reveal-v1",
  "gainDb": -14,
  "fadeInFrames": 0,
  "fadeOutFrames": 12,
  "licenseRecord": "licenses/sfx-soft-reveal-v1.json"
}
~~~

**Correct placement formula:** globalFrame = scene.startFrame + cue.relativeFrame. When upstream scene durations change, recompute globalFrame; do not store only a stale global second offset.

## 5. Voice production protocol

1. Finalize a draft script and classify each significant claim.
2. Break narration into scene-level utterances with explicit pronunciation notes.
3. Select a synthetic voice with appropriate Indonesian pronunciation and rights.
4. Render each utterance to a separately versioned audio file.
5. Measure actual file length, sample rate, peaks, and silence.
6. Listen to every line for missing syllables, cutoff words, errors, and pacing.
7. Adjust the narration text or scene duration; never silently stretch audio to hide timing problems.
8. Approve each scene voice before mix.
9. If a voice is replaced globally, invalidate all affected voice and mix outputs.

Avoid cloning a living person's recognizable voice without consent. No founder voice recording is used.

## 6. Sound design procedure

For each scene, record:
- intended feeling and acoustic environment;
- spoken words and narration pauses;
- visual events requiring synchronized cues;
- permitted/approved SFX with rights evidence;
- cue timing by relative frame;
- desired prominence and fade length;
- silence, music, or ambient exceptions;
- listening notes and revision owner.

Prefer restrained, meaningful sound cues. A diagram transition does not require a loud effect for every shape. Do not allow background music to compete with narration.

## 7. Illustrative mix settings and safety checks

Suggested starting points, subject to listening review:

| Parameter | Initial guideline | Not a platform mandate |
| --- | --- | --- |
| Output audio format | AAC in MP4 | Confirm compatibility |
| Mixing sample rate | 48 kHz | Adapt to source requirements |
| Integrated loudness | Approximately -14 LUFS | Experiment; verify speech dynamics |
| True peak | Approximately -1 dBTP or below | Verify actual output |
| Voice priority | Clear above ambience/music | Human intelligibility check |
| Automatic ducking | When narration is active | Prevent audible pumping |
| Silence gaps | Explicitly reviewed | Silence can be intentional |

**Warning:** loudness targets do not certify good sound. A mechanically compliant mix may still contain harsh sibilance, poor Indonesian pronunciation, distracting repetitive SFX, or inappropriate emotional cues.

## 8. Per-scene revision commands

A revision request must identify:
- episode and stable scene ID;
- scope (visual, voice, SFX, ambience, music, caption, source claim);
- exact change requested;
- elements that must remain invariant;
- permission for changing timing (yes/no);
- expected preview and verification output.

Example:

> Revise only SC-004 in depcutland-001. Slow down the visual dolly; preserve approved narration, text, audio cue relative frames, scene duration, caption copy, color palette, and SC-001 through SC-003 and SC-005 through SC-006. Re-render SC-004, reassemble the episode, and report changed output hashes. Do not change any source material or invoke a paid API.

For voice-only edits, adjust and recheck alignment. For changed durations, recompute the full timeline and flag downstream consequences rather than violating the invariants.

## 9. Revision dependency matrix

| Change | Rerender visual scene? | Rerender voice? | Rebuild audio/video assembly? | Recheck global timeline? |
| --- | --- | --- | --- | --- |
| Camera movement only | Yes | No | Yes | Yes |
| Typography within one scene | Yes | No | Yes | Yes |
| Voice pronunciation only | Usually no | Yes | Yes | Yes |
| SFX timing only | No | No | Yes | Yes |
| Scene duration | Yes | Maybe | Yes | Yes |
| Global font/theme | Potentially all scenes | No | Yes | Yes |
| Master music mix | No | No | Yes | Yes |
| Canon correction in speech | Possibly | Yes | Yes | Yes |

These are default dependency expectations, not guaranteed implementation results.

## 10. Caption and vertical safe-zone policy

- Compose for 9:16 mobile viewing; establish a configurable safe-zone overlay.
- Do not place essential text beneath typical platform UI overlays.
- Use legible fonts, contrast, modest line lengths, and adequate screen dwell.
- Generate captions from the **approved actual narration**, not an earlier draft.
- Test on at least one phone-sized viewport before release.
- If new narration changes wording, invalidate dependent subtitles even when visual art remains unchanged.

Platform overlays can change; treat any fixed safe-zone dimensions as configuration subject to periodic review.

## 11. Audio evidence and rights registry

For every sound asset store: title/filename, provider URL, creator if applicable, download date, version, license text or reference, attribution requirement, permitted use, modifications, and output episodes. A usage assertion must be backed by an asset-specific record, not by a blanket claim that all sounds from a website are free.

Recommended origin: https://www.youtube.com/audiolibrary. Consult track-level licensing and attribution before release. Audacity (https://www.audacityteam.org/) and FFmpeg (https://ffmpeg.org/) are local processing tools; they do not grant copyright licenses for source recordings.

## 12. Quality gates

**Before scene approval:** correct canon/source claim, voice intelligibility, scene timing, usable visual hierarchy, subtitle alignment, cue timing, asset provenance.

**Before episode approval:** no audible pops across scene boundaries, no unplanned gaps or clipping, clear narration, acceptable loudness, full-length MP4 playback, proper dimensions, correct rights records, and reviewed AI content disclosures.

An agent's numerical QA report is insufficient alone. Final sound requires a real listening review.

## 13. Emotional, novel, memorable scene/audio extension (2026-11-03 patch)

Add **optional editorial annotations**, not breaking changes to the proposed technical manifest:

| Field | Meaning | Constraint |
| --- | --- | --- |
| `storyRole` | Hook, expectation inversion, mechanism, human consequence, takeaway | Must not misclassify canon |
| `emotionIntent` | Curiosity, wonder, recognition, unease, reflection, etc. | Must fit source and not manipulate |
| `noveltyFunction` | What a viewer genuinely learns or reframes | Must reference evidence |
| `memoryAnchor` | Specific visual/sonic reminder of the honest thesis | Not repetitive decoration |
| `voiceDeliveryNote` | Synthetic narrator pacing and affect | Must be auditioned |
| `audioIntent` | Why ambience, SFX or silence is chosen | Cue remains scene-relative |
| `storytellingApproval` | PENDING, REVISE, PASS | Human decision, not a model assertion |

If the implementation schema does not accept these fields, keep them in a separate editorial brief; never describe unimplemented metadata as operational.

### 13.1 Sound-design guardrails for emotional engagement

- Voice must remain natural and comprehensible; synthetic intensity is not a substitute for authentic insight.
- The meaningful reveal should be synchronized to an actual on-screen event; avoid arbitrary loud stingers.
- Silence is a valid memory anchor when it gives a thought room to land.
- A new soundtrack mood or voice treatment requires a bounded scope, rights check, listening review, and re-mix of affected dependencies.
- Emotional pacing is not a reason to violate scene invariants or falsify a canonical consequence.

### 13.2 ENM release gate

Verify the video's human stake, source-grounded contrast, one-sentence takeaway, meaningful anchor, voice intelligibility, and honest emotional framing. Mark missing evidence **REVISE** or **DEFER**, not PASS. Full specification: [document 11](11-EMOTIONAL-NOVEL-MEMORABLE-STORYTELLING-STANDARD.md).

## Addendum — Narrative/skill metadata is not a new scene engine (2026-11-06)

The new [skill routing architecture](12-SKILL-ROUTING-AND-COMMUNICATION-QUALITY-ARCHITECTURE.md) can annotate **editorial decisions** (task type, selected skill pattern, original source revision, human question, novelty evidence, cold-reader status). Do not add those fields to a strict scene JSON validator until the schema supports them and negative tests pass. A separate source packet is the default.

**Scene and sound remain authoritative in their own contracts:** stable IDs, integer frames, scene-relative cue anchors, approved synthetic speech, source rights, and relevant rerender dependency graphs. No skill may declare an audio mix “emotionally correct” without actual listening. No design skill automatically approves fonts, artwork, video assets, or fictional canon. No skill creates a second renderer.

**Revision example:** A request to make SC-004 less generic should route to Communication Framework §23 and source-backed scene direction; an SFX-only edit should route directly to this document and the existing local mix process, **not** load unrelated communication or art skills.

**Extra human checks:** COM-27 format fit, COM-28 source traceability, COM-29 specificity, COM-30 no invented authority, COM-31 no padding, COM-32 audience comprehension, COM-33 genuine cold-reader evidence/pending, COM-34 human release. Keep COM-21–COM-26 ENM/audio gates intact.

For task contracts and concrete failure cases see [13 — Skill Router Evaluation](13-SKILL-ROUTER-OPERATOR-CONTRACT-AND-EVALUATION.md). **Status:** proposed; no runtime or new TTS functionality is claimed.
