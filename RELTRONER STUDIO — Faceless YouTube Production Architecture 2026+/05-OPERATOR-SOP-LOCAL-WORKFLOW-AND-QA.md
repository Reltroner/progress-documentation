# 05 — Operator SOP, Local Production Workflow, and QA Gates

**Version:** 1.0-draft | **Status:** proposed SOP; commands require implementation and verification  
**Primary environment:** Windows, PowerShell, local filesystem, Claude coding agent, Remotion/FFmpeg, human review

## 1. Operator responsibilities

| Role | Decision authority | Must not do |
| --- | --- | --- |
| Founder / creative director | Topic, canon interpretation, voice character, final aesthetic, publication approval | Treat AI critique as automatic approval |
| Research assistant (ChatGPT, Gemini, NotebookLM) | Draft research, outlines, alternative narratives | Invent citations, present sources as canon |
| Coding agent (Claude Code) | Implement bounded code changes, run local scripts, report evidence | Rewrite canonical source, buy credits, publish unattended |
| Local renderer and QA scripts | Deterministically validate and render | Assert subjective audio quality or canonical truth |
| Distribution operator | Final manual upload and metadata verification | Overstate product features or disclose unapproved material |

A single person may perform multiple roles; the gates still remain separate. An AI agent must not self-certify the final release.

## 2. Baseline environment preflight

Before project initialization:

- Confirm Windows version, available disk, RAM, CPU characteristics, and storage free space.
- Confirm Node version and compatibility with the chosen Remotion release.
- Confirm git, npm, and FFmpeg availability using explicit version commands.
- Confirm Playwright/browser rendering dependencies and fonts.
- Record Claude access boundaries and expected local agent capability.
- Determine CapCut TTS export viability and audio usage rights.
- Check whether optional Flow credits are actually accessible; do not require them.
- Check repository path permissions and source read-only configuration.
- Ensure the working directory is isolated from deployed website and VPS configs.
- Store a reproducible dependency lockfile after testing.

Illustrative inspection commands (read-only):

~~~powershell
node --version
npm --version
git --version
ffmpeg -version
ffprobe -version
Get-PSDrive -PSProvider FileSystem
~~~

Commands may fail before their dependencies are installed; failure is an environment finding, not a cue to install unknown third-party binaries without review.

## 3. Project initialization and secure dependency policy

1. Create a dedicated local repository only after architecture acceptance.
2. Choose a known Remotion version and inspect its current license conditions.
3. Pin dependency versions and inspect package-lock changes.
4. Inspect installation/postinstall scripts for unexpected network or privileged behavior.
5. Do not give the agent secrets for paid model providers.
6. Disable provider-side API spending and paid credits wherever account controls exist.
7. Keep the canonical Reltroner source repository mounted as read-only reference.
8. Create an immutable snapshot or commit reference for a pilot episode's source files.
9. Do not auto-upload generated video assets to GitHub Actions, LFS, or an external cloud account.

Do not run opaque shell installers merely because a video reference recommends them. Capture all required package provenance and licenses.

## 4. End-to-end production standard operating procedure

### Gate 0 — Topic intake

Record: audience segment, human question, why this idea is relevant, source paths, speculative/historical status, desired format, and intended destination. Reject ideas that only explain internal architecture without an intelligible audience benefit.

### Gate 1 — Source research

Collect the applicable master principles and the precise topic-specific references. Read the relevant sections, note conflicts and null/unassigned values, and identify what is fact, canon, interpretation, or hypothesis. Store source SHA, URL, and verification date.

**Output:** source manifest and research note.

### Gate 2 — Script and story review

Draft hook → tension → mechanism → consequence → conclusion. Each paragraph must have an explicit purpose. Read it aloud or audition with the actual synthetic narrator. Confirm the narration can fit the planned duration without rushing.

**Output:** script, storyboard, canon/evidence review, founder script approval.

### Gate 2A — ENM narrative design and conversational voice rehearsal

Before locking the storyboard, produce a short **emotion / novelty / memorability** brief. Identify one human stake, one genuine source-grounded reveal, and one honest takeaway/visual or sonic anchor. Check the draft against [document 11's ENM-01–ENM-12](11-EMOTIONAL-NOVEL-MEMORABLE-STORYTELLING-STANDARD.md).

Review the proposed Indonesian synthetic narrator **by listening** for conversational pacing, meaningful pauses, and fair emotional interpretation. Do not fabricate a personal witness or exaggerate fear. The book *Talk Like TED* informs presentation craft; its stage-duration heuristics do not impose an 18-minute runtime on Shorts.

**Output:** ENM brief and editorial disposition: PASS / REVISE / DEFER, without implying any audience outcome.

### Gate 3 — Build the scene plan

Allocate stable scene IDs, target frame ranges, template, visual assets, subtitles, narration, and audio event cues. Validate that scene intervals cover the expected total duration, and that no unauthorized visual assets are referenced.

**Output:** episode and scene manifests.

### Gate 4 — Visual and voice preparation

Produce or select original still images, diagrams, SVGs, fonts, and permitted optional Flow footage. Record provenance. Render scene-by-scene synthetic narration with licensing confirmation. Listen for language quality. Do not continue to final export on missing or cut-off voice.

**Output:** approved visual and audio asset registries.

### Gate 5 — Motion and individual previews

Render low-resolution preview scenes first. Inspect 9:16 readability, hierarchy, safe zones, timing, and unexpected flicker. Use code-driven animations for text, graphs, and precise visual claims.

**Output:** preview artifacts and scene notes.

### Gate 6 — Sound design

Place ambience and SFX according to scene-relative cues. Mix buses, duck optional music under voice, check boundaries for clicks, remeasure after voice revisions, and conduct an actual listening review.

**Output:** timeline-valid audio cues, mixed episode audio, listening observations.

### Gate 7 — Integration and regression QA

Assemble full MP4. Validate resolution, duration, FPS, codec, sync, full playback, captions, source/rights ledger, and AI disclosure decision. Compare unchanged scene outputs and inspect cross-scene transitions.

**Output:** QA report and release candidate.

### Gate 8 — Human publication decision

The founder signs off on the actual final master, claims, audio, thumbnail, title, description, and disclosure. Block on unresolved rights, canon contradictions, inaccessible route, missing voice, or significant sync errors.

**Output:** release approval record.

### Gate 9 — Manual YouTube publication

Upload via YouTube Studio; do not assume an automated uploader is available. Verify metadata, visibility, audience and altered/synthetic-content fields when applicable, subtitles, links, and the resulting public playback.

**Output:** public video URL and publication record.

### Gate 10 — Post-release learning

Capture analytics when available, interpret results conservatively, extract editorial improvements, and decide whether a new template is useful. Never change canonical fiction based solely on engagement signals.

## 5. Example bounded revision prompt

~~~text
TASK: Revise only scene SC-004 of episode depcutland-001.

SCOPE: Visual animation only.
CHANGE: Reduce dolly speed and soften the reveal.
INVARIANTS:
- Do not modify narration, subtitles, scene duration, SFX cue timing, or source claims.
- Do not change other scene source files or canonical content.
- Do not invoke paid services or purchase extra credits.

EXECUTION:
1. Inspect manifest and related components.
2. Describe the smallest change set.
3. Implement only the scoped change.
4. Run focused validation and render SC-004 preview.
5. Reassemble the final video if approved.
6. Report changed file paths, hashes, duration and QA status.
7. Do not publish.
~~~

## 6. Proposed CLI responsibilities

The following names are **design targets**, not commands guaranteed to exist:

| Command | Purpose | Expected failure conditions |
| --- | --- | --- |
| video:validate | Schema and timeline check | Missing scene, gap, duplicate ID, invalid asset |
| video:preview | Low-resolution individual preview | Missing fonts/assets, renderer error |
| video:render-scene | Render selected scene artifact | Incompatible template, render failure |
| video:mix-audio | Mix approved narration and cues | Missing audio, invalid cue, license missing |
| video:assemble | Package scene outputs and soundtrack | Mismatch duration/frame rate |
| video:inspect | Analyze exported file technical properties | Wrong codec, duration, audio clipping |
| video:report | Produce QA and reproducibility evidence | Required artifacts absent |

Never construct success messages purely from subprocess invocation. Use exit codes and verified artifact existence; inspect output with ffprobe and listen/watch the result.

## 7. Proposed automated QA matrix

| Area | Test | Hard gate |
| --- | --- | --- |
| Manifest | Required fields, uniqueness and legal enum values | Yes |
| Timeline | Frame intervals, sum, overlaps, transition contract | Yes |
| Source | Source paths and revision identifiers resolve | Yes |
| Canon | Claim status and manually reviewed interpretation | Yes, with human sign-off |
| Visual | Width, height, FPS, no black/blank unintended frames | Yes |
| Subtitle | Fit, margin, font size, synchronization | Yes |
| Audio | File presence, duration, sync, clipping, true peak | Yes |
| Human audio | Pronunciation, sound balance, fatigue, emotional appropriateness | Yes |
| Rights | Asset-level licenses, attributions and permissions | Yes |
| Budget | No billable requests or additional subscriptions | Yes |
| Publication | Human approval and destination verification | Yes |

Automated visual comparisons should tolerate deliberate changes inside the selected scene while preserving unrelated scenes. Snapshot testing cannot by itself decide whether a fictional visual is philosophically or aesthetically correct.

## 8. Incident and rollback SOP

- **Tool or install failure:** stop; record exact version/stack trace; do not automatically change every dependency.
- **Visual regression:** restore last approved scene or template and re-run focused visual tests.
- **Voice mismatch:** preserve prior approved WAV/MP3 version; replace only after audition.
- **Canon contradiction:** block release; point to exact source line/claim; request founder decision.
- **Rights uncertainty:** quarantine asset and use a licensed alternative.
- **Audio clipping or desync:** re-mix and re-encode; retest whole episode.
- **Unexpected spending requirement:** halt provider use immediately.
- **Disk full:** remove transient caches after identifying safe candidates; retain masters, manifests, source records and licenses.
- **Failed publication:** preserve approved local master and release record; do not auto-retry in a way that duplicates uploads.

## 9. Minimum evidence packet

For every published video retain: source manifest; script version; scene manifest; approved voice assets; SFX/music license ledger; final MP4 hash; duration/resolution/audio inspection; human review checklist; thumbnail and metadata copy; AI-disclosure decision; publication URL and upload date.

## 10. MVP definition of done

- One full, correctly exported 9:16 pilot video.
- All narration synthetic, no founder recording.
- At least two independent audio buses beyond narration demonstrated if relevant.
- One completed scoped scene revision, with unaffected scene outputs verified.
- All licensing and canon claims reviewed.
- Final full-length human playback and listening approval.
- Reproducible build with no added spending.
- No implication that an unverified LMS, mentorship, or product feature is live.

The result is an accepted **workflow experiment**, not a guarantee of YouTube performance.

## 11. ENM-specific production and regression checks (2026-11-03 patch)

Include a human narrative review alongside automated tests:

| Gate | What must be checked | Hard-fail condition |
| --- | --- | --- |
| ENM-E | Human stakes and emotion are meaningful and fair | Invented trauma, coercive urgency, false first-person testimony |
| ENM-N | The reveal provides a defensible new perspective | Unsupported rankings, invented canonical rules or fabricated facts |
| ENM-M | One clear takeaway is reinforced by image/sound | Flashy but unintelligible conclusion, misleading compression |
| ENM-VOICE | Synthetic voice sounds natural for Indonesian context | Cut words, robotic cadence obstructing understanding, inappropriate emotional mimicry |
| ENM-AUDIO | SFX/ambience follow scene-relative meaningful events | Effects overpower dialogue or desynchronize after a scene edit |
| ENM-REVIEW | Real human listen/watch and editorial sign-off | Only AI-generated QA or fictional acceptance report |

If a rewrite changes meaning or approved narration, invalidate the script approval and downstream caption, voice, sound, and frame dependencies. A visual-only ENM revision must preserve approved claims, audio, and unaffected scene artifacts unless the operator explicitly expands scope.
