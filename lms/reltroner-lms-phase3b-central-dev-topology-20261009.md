# Reltroner LMS — Phase 3B Central Development PR Topology & 3B-02..06 Engineering Evidence

> **Status:** One **DRAFT central source PR per repository**; source main remains unmodified, Phase 3B-07 holistic freeze **PENDING**.  
> **Owner intent:** Avoid misordered PR merges, duplicate commits, review noise and technical debt by reviewing one Phase 3 cumulative end-to-end source snapshot before any app `main` merge.  
> **Date:** 2026-10-09, Asia/Jakarta.

## 1. Governing decision and exact GitHub topology

| Source repo | Frozen `main` SHA | Central unmerged cumulative branch SHA | ONLY open Phase 3 source PR |
|---|---|---|---|
| LMS-BE | `e30a61780994d85671cbf079e6b9ce899b3fe837` | `phase3-dev@f43c91de8150d2ad22de61154f9ec9391f1548df` | [DRAFT PR #11](https://github.com/Reltroner/LMS-BE/pull/11) → `main` |
| LMS-FE | `f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7` | `phase3-dev@3ee0ee0285388f0489016d1689d2ea2ae899dd97` | [DRAFT PR #3](https://github.com/Reltroner/LMS-FE/pull/3) → `main` |

**Strategy:** previous Phase 3B branches form verified strictly linear ancestry (BE 3B-01 → 02 → 03 → 05 → 06; FE 3B-04 → 05). Each central `phase3-dev` branch was created **directly at the cumulative tip** of its ancestry. Historical PRs were then **CLOSED AS SUPERSEDED, NOT MERGED INDIVIDUALLY**; all their commits and original branches are retained and included in central branches. No `rebase`, `reset`, force-push, or new merge commit was required. This is intentionally simpler than retargeting and merging nine obsolete BE PRs sequentially.

**Historical preservation:** backend [#2](https://github.com/Reltroner/LMS-BE/pull/2), #3, #4, #5, #6, #7, #8, #9, #10 closed unmerged; frontend [#1](https://github.com/Reltroner/LMS-FE/pull/1), #2 closed unmerged. The owner-accepted 3B-01 tested SHA and evidence remain preserved as ancestors of central PR #11. No lost source or early `main` mutation.

## 2. Actual evidence for 3B-02..3B-06 (not a product/runtime certificate)

| Work package | Central artifacts/evidence | CI/model result at stated SHA | Final phase disposition |
|---|---|---|---|
| 3B-01 | OpenAPI v1, 26 method+paths, 19 capability matrix, PHP `validate.php` | 22 PASS / 0 FAIL | Contract-only content owner ACCEPTED, integrated branch unmerged |
| 3B-02 | OIDC client flow, token validation and scoped internal delegation contract/fixtures | 22 PASS / 0 FAIL (synthetic policy checks) | **CANDIDATE**, real crypto parameters and live token checks deferred |
| 3B-03 | Four DB owner/grant contracts, nine versioned event schemas, outbox/inbox/booking failure fixtures | 30 PASS / 0 FAIL (contract models) | **CANDIDATE**, no real DB migration/race/transaction proofs |
| 3B-04 | 31 stable lesson IDs, deterministic manifest, Studio rights form, public-only build guards | 8/8 FE catalog test PASS | **CANDIDATE**, no production published-content certification |
| 3B-05 | BE six Laravel independent CI jobs + PHP contract job, FE catalog and Next/static output build | BE 7/7 jobs SUCCESS; FE 2/2 jobs SUCCESS | **CANDIDATE**, 3B-07 coverage/gate review still required |
| 3B-06 | Frozen golden API/permission/event snapshot and compatibility/negative model fixtures | 19 PASS / 0 FAIL | **CANDIDATE**, no live provider/consumer runtime verification |
| 3B-07 | Final SHA snapshot, 44-invariant trace, 28/28 acceptance evidence, human/AI review | **NOT STARTED** | **GLOBAL EXIT HOLD** |

**Pinned CI evidence:**

- [Backend Phase 3B cumulative six-service + contracts CI](https://github.com/Reltroner/LMS-BE/actions/runs/37950916475) on `f43c91de8150d2ad22de61154f9ec9391f1548df`: all seven jobs successful. Pure PHP checks: **22 API + 22 Identity + 30 Persistence + 19 Compatibility**, all zero failures; six separate Laravel tests green.
- [Frontend Phase 3B catalog + publication privacy build](https://github.com/Reltroner/LMS-FE/actions/runs/37951012017) on `3ee0ee0285388f0489016d1689d2ea2ae899dd97`: **catalog-contract 8/8 PASS**, **frontend-build PASS**. Previous CI failing on `63edbd171f7fe5e04d4c2223820234e5e8663db4` was inspected, and repaired in `phase3-dev`.

**Frontend bug remediation:** `scanPublicOutput` used the temporary scan output root to locate the checked-in unpublished denylist; this raised `ENOENT` in the catalog-contract test. Corrected to read policy from a separate audited contract root while scanning the passed output directory. CI rerun on `phase3-dev@3ee0ee0...` passed. No original frontend working tree edits.

## 3. Strict governance — block main merge until Phase 3 end-to-end review

1. Keep [BE PR #11](https://github.com/Reltroner/LMS-BE/pull/11) and [FE PR #3](https://github.com/Reltroner/LMS-FE/pull/3) **DRAFT / NOT MERGED**. These are the **only open app-source PRs** to `main` under Phase 3. Never use automatic merging.
2. Continue improvements directly in pinned reviewed `phase3-dev` branches, without extra temporary Phase 3 PRs unless a specific owner approval requires a different review strategy. Every commit, test and SHA must be logged.
3. Phase **3B-07** must explicitly validate each of the **28 FZ-10 acceptance criteria**, 44 FROZEN invariants, cross-service negative tests, schema drift, privacy publication guard, backend/frontend dependency and diff. CI passing is not enough by itself: missing crypto/DB/provider proofs need precise downstream deferral gates and no false final PASS.
4. Before any source `main` merge, produce one coherent **backend+frontend snapshot** with exact current commits and reproducible CI links, review by AI/human, resolve discovered issues, and obtain **a new explicit project-owner approval**.
5. Do not alter Phase 0C/1 FROZEN contracts, make production changes, run live Keycloak/VPS/Postgres/Cloudflare mutation, claim Phase 4 readiness or assert zero technical debt without comprehensive negative evidence.

## 4. Risks/uncertainties explicitly retained

- `3B-02`: algorithm/key exchange/rotation, signed delegation and replay control are specified in principle, but cryptography details are intentionally marked **PENDING SECURITY ADR**; mock model cannot prove signature verification.
- `3B-03`: PostgreSQL grants, booking occupancy and outbox/inbox are schema contracts, not real DB fixtures or validated recovery behavior. No 2PC/Redis-only correctness authorized.
- `3B-04`: 31 stable lesson IDs and public-only static export have green branch tests; Studio redistribution-rights attestation still requires real provenance approval before Knowledge ingest.
- `3B-05`: CI covers six Laravel skeleton services and FE build; original application integration/production remains out of scope. Security/negative mutation completeness must be independently reviewed in 3B-07.
- `3B-06`: negative tests are **models and golden schema comparisons**, not live service-to-service provider execution.

## 5. Next checkpoint and transfer to other AI

Proceed to **3B-07 — Holistic Phase 3 Acceptance & Evidence Freeze**; it must read both central DRAFT PRs and the exact 28 test gate register, not closed old subphase PRs as active work. Distinguish **candidate source integrated and CI green** from **all 28 final acceptance PASS**, and never recommend merging the source `main` before a new owner command.

- [Machine-readable central topology, historical PR status and CI SHA evidence](./reltroner-lms-phase3b-central-dev-topology-20261009.json).
- [FZ-10 original work order](./reltroner-lms-phase3a-04-fz10-phase3b-entry-exit-authorization-20261009.md).
- [FZ-11 frozen architecture](./reltroner-lms-phase3a-fz11-postmerge-activation-20261009.md).
- [Living engineering end-to-end ledger](./engineering-end-to-end-progress-ledger.md).

**Authoritative state:** `3A DESIGN FROZEN → 3B-00 ACCEPTED → 3B-01 CONTRACT ACCEPTED → 3B-02..06 SOURCE CANDIDATES CENTRALIZED / CI GREEN → 3B-07 REVIEW PENDING → SOURCE MAIN MERGE HOLD`.
