# Reltroner LMS — Phase 3B-02 through 3B-06 Staged Engineering Checkpoint

> **Scope:** Five FZ-10 work packages, six draft source PRs; all source merges into `main` **HOLD** pending Phase 3B-07 holistic snapshot.  
> **Data date:** 2026-10-09, Asia/Jakarta.  
> **Do not promote:** contract models to runtime/crypto/PostgreSQL correctness or candidate branch CI to a production deployment.

## 1. Owner approval and source provenance

Project owner accepts the 3B-01 source contract **without merging** and instructed staged engineering through 3B-06. The 3A design freeze is immutable at `b9390a06ebc5db5377059a99109d59fea092cccb`; BE frozen `main@e30a61780994d85671cbf079e6b9ce899b3fe837`, FE frozen `main@f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7`. Documentation PR #10 remains an OPEN merge-hold record. Source [BE PR #2](https://github.com/Reltroner/LMS-BE/pull/2) remains explicitly accepted **but UNMERGED**. The subsequent PRs below are all DRAFT/non-main and do not modify frozen main.

## 2. Exact cumulative stacked source PRs

| Work package | Repository and PR | Candidate source SHA prefix | Evidence classification |
|---|---|---|---|
| `3B-02` | LMS-BE [PR #7](https://github.com/Reltroner/LMS-BE/pull/7) | `38922061080c` | DESIGN_MODEL_CANDIDATE; real crypto algorithm/replay verification hard gate open |
| `3B-03` | LMS-BE [PR #8](https://github.com/Reltroner/LMS-BE/pull/8) | `2de1e5a9ca3b` | SCHEMA_MODEL_CANDIDATE; no live DB grants/transactions/migrations |
| `3B-04` | LMS-FE [PR #1](https://github.com/Reltroner/LMS-FE/pull/1) | `6d09117aff99` | SOURCE_CANDIDATE; actual stricter published course/path/resource guards in stacked FE 3B05 |
| `3B-05` | LMS-BE [PR #9](https://github.com/Reltroner/LMS-BE/pull/9) | `472046b6f124` | CI_ACTUALLY_GREEN_AT_3B05_SHA |
| `3B-05` | LMS-FE [PR #2](https://github.com/Reltroner/LMS-FE/pull/2) | `63edbd171f7f` | LATEST_CI_PENDING_ON_CURRENT_SHA; PREVIOUS_TITLE_METADATA_LEAK_CAUGHT_AND_BLOCKED |
| `3B-06` | LMS-BE [PR #10](https://github.com/Reltroner/LMS-BE/pull/10) | `f43c91de8150` | STATIC_MODEL_AND_7_BACKEND_CI_JOBS_GREEN; REAL_PROVIDER_COMPATIBILITY_PENDING |

**Stack graph:** BE `main` → accepted/unmerged 3B-01 PR #2 → 3B-02 PR #7 → 3B-03 PR #8 → 3B-05 PR #9 → 3B-06 PR #10; FE `main` → 3B-04 PR #1 → 3B-05 PR #2. Do not merge any of these into source `main` independently. No 3B-07 source branch exists yet.

## 3. Evidence — what is actually proven

**Backend CI:** GitHub Actions at [BE 3B-05 commit](https://github.com/Reltroner/LMS-BE/actions/runs/37946240319) and [BE 3B-06 cumulative commit](https://github.com/Reltroner/LMS-BE/actions/runs/37946756843) completed with **seven green jobs**: one native PHP contract lint/model validation and six independent Laravel service PHPUnit suites (gateway, learning, mentorship, knowledge, assistant, audit). This proves CI on the pinned non-main tree, not deployed providers or cryptographic signatures.

**Frontend CI:** [initial FE 3B-05 run](https://github.com/Reltroner/LMS-FE/actions/runs/37946323108) green, but the **stronger** public scanner then flagged draft metadata in public JS ([failure log](https://github.com/Reltroner/LMS-FE/actions/runs/37946793852)). Investigation traced matching strings to the draft-course **resource registry** bundled into the browser. FE remediation additionally uses allowlisted *published* course/path/resource client imports and published-only Contentlayer staging. CI of **final remediated SHA must be independently verified**; do not claim this latest code PASS from earlier runs.

**Work package maturity:** `B3-AC05..08` design/synthetic OIDC trust matrix only, cryptographic parameters unratified; `B3-AC09..12` owner schemas/outbox and simulation only, no actual PG migration or rollback; `B3-AC13..16` stable IDs+manifest and output privacy check under latest CI validation; `B3-AC17` backend six-service green; `B3-AC18` frontend final CI pending; `B3-AC19/20` partial negative/non-production CI; `B3-AC21..24` model negatives and golden snapshots green on backend CI, not live provider/consumer HTTP; `B3-AC25..28` belongs to 3B-07, not started.

## 4. Security and publication fail-closed

All published API operations remain authenticated as a conservative baseline, guest offerings not opened; Keycloak/HRM production untouched. The catalog's **31** Git source lessons stay untouched, the original FE local dirty workspace is preserved, only 3 backend lessons are currently marked published in the manifest. Frontend route, index, course, path and resources require explicit public publication allowlists; CI must block any leaked draft route, IDs, title/summary or unpublished course/path metadata before release. Story canon/rights remain owned by Studio; source rights attestation for Knowledge not assumed.

## 5. Stop conditions and next gate

- All source `main` merges **FORBIDDEN** until Phase 3B-07 holistic 28/28 acceptance evidence, AI/human review of pinned backend+frontend cumulative diff, 44 frozen-invariant compliance and new explicit owner source-merge sign-off.
- Any failed FE privacy scan means **FAIL** for current release candidate; investigate and fix at source, never just mute the scanner.
- Real workload signing/JWKS key rotation, nonce persistence, real DB grants/booking race/outbox failure, Knowledge rights, provider HTTP compatibility remain separately gated; synthetic fixture PASS cannot substitute.
- Keycloak/VPS/PostgreSQL/Redis/DNS/Cloudflare live changes and production deployment are **NOT AUTHORIZED**.

**Engineering checkpoint:** `3A FROZEN → 3B01 ACCEPTED UNMERGED → 3B02/03/04/05/06 SOURCE CANDIDATES → BE CI GREEN / FE LATEST PRIVACY CI CHECKING → 3B07 NOT STARTED → SOURCE MAIN MERGE HOLD`.
