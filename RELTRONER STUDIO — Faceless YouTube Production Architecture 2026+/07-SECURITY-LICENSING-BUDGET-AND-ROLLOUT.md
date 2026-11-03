# 07 — Security, Licensing, Financial Constraints, Risk Register, and Rollout

**Version:** 1.0-draft | **Status:** controls and rollout proposal  
**Highest priority constraint:** no incremental subscription, API, cloud-rendering, or credit purchases

## 1. Budget boundary

The program does not authorize purchases or billable resource provisioning. The founder already has subscriptions/access described as Claude Pro, Gemini Pro, ChatGPT Plus, NotebookLM, and CapCut; entitlement, quotas, and usage rights must be checked in the account rather than inferred from product nicknames.

**Allowed within existing entitlements:** local development, existing AI-assisted research/coding, free or appropriately licensed software, compatible audio assets, available non-purchased generative credits, and manual YouTube publishing.

**Not authorized:** new subscriptions, pay-as-you-go AI provider calls, commercial voice plans, renting GPUs, paid stock video/music, new dedicated VPS, additional Flow credits, or GitHub features with unapproved usage charges.

“Rp0 incremental subscriptions” does not mean labor, local electricity, disk usage, internet connectivity, and existing subscription costs are literally zero.

## 2. Resource control

- Render locally, using CPU-friendly preview settings where possible.
- Use low-resolution proxies and only final-render approved scenes.
- Avoid re-encoding the same scene unnecessarily through content-addressed caches.
- Limit cache retention; store master and provenance separately.
- No new GitHub Actions rendering pipeline until usage and budgets are explicitly assessed and authorized.
- Do not silently enable Git LFS with billable storage/bandwidth.
- Prefer assets already owned or licensed by the studio over generated footage.
- Block paid API endpoints at the orchestration level.
- Keep Flow optional and enforce a per-video allowance from existing credits only.

## 3. Supply-chain and local execution risks

Third-party skills, CLIs, and MCP servers may execute scripts or expose access paths. Before installing:
1. Validate official repository owner and canonical release.
2. Read LICENSE, README, package scripts, and relevant dependency versions.
3. Inspect installer scripts for network destinations and unexpected writes.
4. Check whether application code and model weights have different licenses.
5. Pin and record versions.
6. Run with least filesystem/network privileges practicable.
7. Do not share personal tokens, cloud credentials, GitHub write tokens, or production secrets with untrusted tooling.
8. Confirm disk requirements and rollback/uninstall options.
9. Avoid global package upgrades that could disrupt other Reltroner projects.

## 4. Asset/license registry contract

Record one row per item:

| Field | Required |
| --- | --- |
| Unique asset ID and checksum | Yes |
| Source URL/creator/origin | Yes |
| Date acquired | Yes |
| Local storage path | Yes |
| License type and link/copy | Yes |
| Commercial/public YouTube permission assessment | Yes |
| Attribution requirement | Yes |
| Modification restrictions | Yes |
| Applicable output/episode | Yes |
| Human rights approval and date | Yes |

Do not use assets of uncertain provenance. Open source code licensing, model weight licensing, output rights, and redistribution rights are distinct issues. A free audio download is not itself a universal commercial license.

## 5. Synthetic-content and platform policy gate

For each final episode, determine:
- whether realistic altered/synthetic footage could be mistaken for authentic events, people, or places;
- whether audio simulates an identifiable real person;
- whether YouTube's current altered/synthetic disclosure field applies;
- whether narration or visuals could mislead viewers into believing Asthortera is real;
- whether attribution and rights notices need to appear in description;
- whether thumbnails are consistent with delivered footage and title.

Record the decision, rationale, reviewer, and policy reference. If uncertain, prefer transparent explanation and a manual policy check before publishing.

Official references:
- https://support.google.com/youtube/answer/14328491
- https://support.google.com/youtube/answer/1311392
- https://www.youtube.com/audiolibrary

## 6. Privacy and channel security

- No unnecessary personal information in video exports, metadata, screenshot overlays, project paths, or logs.
- Never publish the founder's desktop session with personal files or authentication tokens visible.
- Do not export GitHub secrets, YouTube cookies, or API keys.
- Keep YouTube login/upload as a manual authorized step initially.
- Use least-privilege repository access and review MCP permissions.
- Do not disclose private unreleased story files unintentionally in titles, thumbnails, captions, or captured app screens.
- Be mindful of model-provider prompt retention and third-party upload terms.

## 7. Risk register

| ID | Risk | Severity | Mitigation | Release impact |
| --- | --- | --- | --- | --- |
| R01 | New paid provider charge | Critical | No billing secrets; provider allowlist; manual cost gate | Block |
| R02 | Canon contradiction | High | Source manifest, status tags, founder review | Block |
| R03 | Copyright/licensing uncertainty | Critical | Per-asset license registry and replacement path | Block |
| R04 | Incorrect Indonesian TTS pronunciation | High | Listen to each line; audition alternatives | Block if material |
| R05 | Audio cue drift after revisions | High | Scene-relative frames and global revalidation | Block |
| R06 | Clip/caption obstruction by Shorts UI | Medium | Safe-zone overlay and phone preview | Block if essential content hidden |
| R07 | Windows render incompatibility | High | Early single-shot spike; fallback workflow | Phase gate |
| R08 | Excessive memory/storage usage | Medium | Proxies, controlled cache cleanup | Phase gate |
| R09 | Dependency skill exfiltration | Critical | Review scripts, isolate permissions, no secrets | Block |
| R10 | Low-value repetitive templating | High | Distinct editorial question, original analysis, human review | Block |
| R11 | Flow access/credits unavailable | Low | Still imagery and coded motion fallback | No block |
| R12 | Unsupported product/LMS claims | High | Verify deployed experience and status | Block |
| R13 | Agent self-approval or auto-publication | High | Required human approval state | Block |
| R14 | Analytics misinterpretation | Medium | Contextual comparison and sample caution | Do not change canon |

## 8. Rollout phases and exit gates

### Phase P0 — Research and architecture

Outputs: documented source authority; tool alternatives; budget rules; scene/audio contracts; risks; pilot storyboard.

**Exit:** founder approves a bounded technical spike, not the entire future architecture.

### Phase P1 — Windows environment spike

Outputs: pinned local toolchain, single Remotion test scene, local FFmpeg mux, no paid calls.

**Exit:** reproducible scene preview and export with recorded hardware limitations.

### Phase P2 — Audio and selective-revision spike

Outputs: one synthetic Indonesian narration, one ambience layer, two SFX cues, short scene revision, diff/manifest validation.

**Exit:** changed scene updates properly, unchanged content preserved as expected, full timeline verified.

### Phase P3 — Pilot episode

Outputs: 55-second 9:16 Depcutland video, source attribution ledger, safe-zone QA, full audio review, release-candidate file.

**Exit:** founder listens, watches, and approves. “Pilot complete” is not “channel growth achieved.”

### Phase P4 — Second-topic reuse test

Outputs: creator-facing episode using the same engine with different topic/visual grammar.

**Exit:** objectively reusable modules, measured human effort and revision overhead.

### Phase P5 — Publication and evaluation

Outputs: video metadata, manual upload, URL, release record, early analytics when meaningful, backlog decision.

**Exit:** decision to maintain, simplify, or expand the system based on actual evidence.

## 9. Stop conditions

Stop or defer tool usage if it requests unexpected payment, broad secret access, unreviewed executable code, external upload of confidential data, model licensing incompatible with distribution, or disproportionate storage/compute resources.

Stop publication if the approved final master is not the file actually uploaded, if a material canon claim is unresolved, if voice is unintelligible, or if permissions are unverified.

## 10. Decision register (initial)

| ADR | Proposed position | Status |
| --- | --- | --- |
| ADR-001 | One authoritative scene manifest | Proposed |
| ADR-002 | Remotion as preferred local renderer | Proposed; spike required |
| ADR-003 | FFmpeg as final assembly/mix processor | Proposed |
| ADR-004 | Voice/SFX/ambience/music buses separate | Proposed |
| ADR-005 | Voice generated without founder recordings | Constraint |
| ADR-006 | No additional paid resources | Binding project constraint from founder |
| ADR-007 | Flow optional, not production-critical | Proposed |
| ADR-008 | Human approval required before upload | Proposed control |
| ADR-009 | Canon repositories read-only during video work | Proposed control |
| ADR-010 | First pilot Depcutland, 9:16, 55 s | Candidate, not approved publication |

Changing an ADR requires documenting reason, trade-off, risk and founder approval. This document does not ratify architectural or canonical decisions by itself.

## 11. Retention and maintenance plan

Retain final masters, approved scripts, scene/audio manifests, essential source snapshots and licensing records. Expire transient render caches after verification. Recheck external pricing, permissions and YouTube rules before major production changes. Store incidents and corrective actions in the video project's own operational documentation.

## 12. Future-proofing principle

The 2026+ claim denotes an architecture capable of incremental improvement, not a promise that YouTube's recommendations or provider entitlement rules are static. Local deterministic assets and portable manifests reduce dependence on any one AI vendor.
