# Reltroner LMS — Phase 3B-07R Deterministic Remediation & Revalidation

> **Date:** 2026-10-09 (Asia/Jakarta). **Disposition:** Phase 3B-07R SOURCE REMEDIATION + CI REVALIDATION EXECUTED, **FINAL PHASE 3B EXIT = HOLD**.
> **Source governance:** exactly one BE source [DRAFT PR #11](https://github.com/Reltroner/LMS-BE/pull/11) and one FE [DRAFT PR #3](https://github.com/Reltroner/LMS-FE/pull/3). **Neither merged to `main`.** No direct production mutation, no Keycloak or DB provisioning.

## 1. Immutable source and CI snapshot

| Source / proof | Audited SHA | Result |
|---|---|---|
| FZ-11 accepted Phase 3A architecture | `b9390a06ebc5db5377059a99109d59fea092cccb` | unchanged FROZEN baseline |
| BE `main` original | `e30a61780994d85671cbf079e6b9ce899b3fe837` | unchanged |
| FE `main` original | `f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7` | unchanged |
| [BE central DRAFT PR #11](https://github.com/Reltroner/LMS-BE/pull/11) `phase3-dev` | `0fc17dabc1af845053ac525986f40fb260f73e4c` | source remediations only, main still frozen |
| [FE central DRAFT PR #3](https://github.com/Reltroner/LMS-FE/pull/3) `phase3-dev` | `9795489d9b0e1a13d81675fac29e649900c4381d` | source remediations only, main still frozen |
| [BE CI](https://github.com/Reltroner/LMS-BE/actions/runs/37960568787) | BE exact candidate SHA | **SUCCESS**, 7/7 jobs, 6 Laravel service suites and **255** separate PHP source contract/model assertions |
| [FE CI](https://github.com/Reltroner/LMS-FE/actions/runs/37960704557) | FE exact candidate SHA | **SUCCESS**, frontend build + catalog contract, **9/9 Node tests** |
| BE/FE GitGuardian checks | exact candidate SHAs | **SUCCESS**; no claim of exhaustive secrets review |

**BE PHP breakdown:** 22 OpenAPI + 22 identity policy + 42 persistence (failure-state, grant/migration, mutant detection) + 23 compatibility/provenance + 136 mock operation/DTO/ownership negative cases + 10 sodium Ed25519 signed synthetic assertion tests = **255 PASS, 0 FAIL**. Do **not** equate this number to the separate 28 frozen FZ-10 acceptance gates.

## 2. Deterministic fixes completed in existing `phase3-dev` branches

1. **R-01 CI merge safety:** BE and FE now include `push: main` and PR-to-`main` workflow triggers. Removed redundant `phase3-dev` push trigger (avoids duplicated CI jobs while the PR event still tests candidate SHAs). After an authorized merge, the *actual merge SHA* must receive a new green main run; it is not yet observed.
2. **R-04/05 durable boundary model:** replaced persistence cases E01–E08 hardcoded `id → expected` answers with input-driven deterministic failure simulation and fault mutants. Test now checks owner DB grant policy, migration additive/breaking cases, outbox recovery, booked-slot conflict, idempotency and Audit reconciliation expectations. Actual database grants and transactions are explicitly future runtime gates.
3. **R-06/12 provenance:** both BE Knowledge source release and FE Studio attestation now reject **valid-format but incorrect synthetic source commits or SHA256 digests** unless they match an independent expected reference. This is a stronger nonproduction model; it is **NOT** actual signed Studio redistribution rights verification.
4. **R-07 public privacy:** FE scan expanded to CSS, SVG, source maps, filenames/route paths and unknown asset types. Only whitespace-only `.gitkeep` files under four reviewed asset directories are exempt; malicious placeholder content fails. CI encountered that fail-closed boundary and passed after a bounded exact fix. Full production binary-source provenance remains a separate release requirement.
5. **R-08 mock protocol:** separate no-network PHP mock executes all 26 operations against owner/client/capability, denial of anonymous, wrong admin context, cross-owner, unsigned delegation, private Knowledge results, and request/response DTO compatibility mutants. **Not real HTTP Laravel service behavior**.
6. **R-09 negative mutation evidence:** removed bearer/401/owner/DTO schema, forged source digest, malformed failure state, unpublished assets are rejected. GitGuardian succeeded on candidate SHAs. These are sampled source-level mutants, not full coverage or a proof of absence of vulnerabilities.
7. **R-03 signed trust proposal:** added a test-only EdDSA/Ed25519 assertion verification profile with actual synthetic sodium signing, expiry, audience, recipient, capability, key identity and replay negative cases. Its signing algorithm, key distribution, rotation and nonce-store strategy are **CANDIDATE / NOT RATIFIED BY OWNER**, so no production trust authority was introduced.

## 3. FZ-10 28 mandatory criteria — after actual CI revalidation

| Acceptance | Result | Specific evidence / remaining gap |
|---|---|---|
| `B3-AC01` | **PASS_SCOPED** | 26 exact OpenAPI 3.1 method+paths, 22 PHP tests; **Boundary:** Live business handlers not exercised |
| `B3-AC02` | **PASS_SCOPED** | 19 capability values, admin.learning.* reserved, offerings default denial; **Boundary:** Real JWT capability enforcement untested |
| `B3-AC03` | **PASS_SCOPED** | Per-operation Problem Details/request_id/401/403, cursor and booking Idempotency-Key; **Boundary:** External OpenAPI standards validator and provider DTO execution absent |
| `B3-AC04` | **PASS_SCOPED** | 136 independent mock API/owner/client/status and negative tests including all 26 operations; successful BE CI; **Boundary:** Actual Laravel business handlers deferred to Phase 4+ |
| `B3-AC05` | **PASS_SCOPED** | Issuer/aud/two clients/PKCE S256 policy plus identity mock tests; **Boundary:** No real Keycloak clients or token validation |
| `B3-AC06` | **PASS_SCOPED** | Synthetic invalid JWT, audience, issuer, client and missing cap decisions; **Boundary:** Synthetic signature_verified boolean not actual cryptographic JWT |
| `B3-AC07` | **PARTIAL_EVIDENCE** | 10 real sodium Ed25519 synthetic signatures/replay/aud/expiry tests PASS; bounded crypto-profile-proposal.json exists; **Boundary:** Owner has not ratified signing algorithm, key distribution/rotation, replay storage and deployment ADR |
| `B3-AC08` | **PASS_SCOPED** | Diff does not modify HRM or Keycloak, internal unbound principal disallowed; **Boundary:** No runtime HRM/Keycloak nonmutation probe; FZ10 excludes live services |
| `B3-AC09` | **PASS_SCOPED** | Four owner DB candidates with executable grant-model check and 3 migration compatibility fixtures; **Boundary:** No actual PostgreSQL GRANT or applied DDL in Phase 3 |
| `B3-AC10` | **PASS_SCOPED** | Nine exact version 1 event schemas; PII minimizing envelope checks; **Boundary:** No actual publisher/consumer yet, deferred Phase 5+ |
| `B3-AC11` | **PASS_SCOPED** | 42 persistence model checks include input-driven crash/outbox/inbox/failover and 8 negative mutants; prior fixture-ID answer tautology removed; **Boundary:** No live Redis/Postgres faults until authorized runtime phases |
| `B3-AC12` | **PASS_SCOPED** | Booking idempotency/occupied slot and Keycloak-Audit intent failure transitions executed as deterministic models; **Boundary:** Real booking contention/Audit reconciliation deferred Phase 6/7 |
| `B3-AC13` | **PASS_SCOPED** | 31 Git registry stable IDs; missing source/rename fail-closed test; **Boundary:** Source mapping external to MDX, FZ10 accepts versioned registry |
| `B3-AC14` | **PASS_SCOPED** | Deterministic canonical JSON manifest, per-course revision verified in FE CI; **Boundary:** Live release and full historical revision migrations not performed |
| `B3-AC15` | **PASS_SCOPED** | 9/9 frontend catalog tests + Next build PASS; CSS, SVG, source maps, filename routes, unknown assets and approved placeholders tested; **Boundary:** Binary assets and production Cloudflare deployment privacy need later release checks |
| `B3-AC16` | **PASS_SCOPED** | FE Studio attestation now requires an independent pinned source commit/digest; wrong well-formed hashes and absent source rejected; **Boundary:** Live Studio publication-rights signatures/Knowledge enforcement Phase 8 |
| `B3-AC17` | **PASS_SCOPED** | All six independent Laravel PHPUnit + locked Composer CI jobs SUCCESS; **Boundary:** Only service skeleton, not live domain provider business correctness |
| `B3-AC18` | **PASS_SCOPED** | FE npm ci, typecheck, lint, content/resource/orphan, Next build and privacy export PASS; **Boundary:** No live Cloudflare/publication proof; CI output only |
| `B3-AC19` | **PASS_SCOPED** | Mutation tests reject wrong owner, removed bearer, missing 401, breaking DTO, state-model flags, draft assets and format-compatible forged digest; **Boundary:** Mutation coverage is intentionally finite and source-only |
| `B3-AC20` | **PASS_SCOPED** | Source workflows use no production deploy/DB/Keycloak steps; GitGuardian checks green for both pinned commits and negative harness failures fail CI; **Boundary:** No production endpoint smoke and no guarantee of every possible secret exposure |
| `B3-AC21` | **PASS_SCOPED** | Golden 26/19/9, 136 mock HTTP operation checks and request/response schema mutation compatibility model PASS; **Boundary:** Actual domain providers and wire HTTP conformance Phase 4+ |
| `B3-AC22` | **PASS_SCOPED** | 26 operation anonymous, wrong client, missing cap, cross-owner and private search denial models included in BE CI; **Boundary:** Real middleware and private Knowledge search ACL runtime Phase 4/8 |
| `B3-AC23` | **PASS_SCOPED** | Synthetic duplicate receipt/stale event and failed index release decision functions PASS; **Boundary:** No real broker or index transaction; FZ10 calls for isolated deterministic simulation |
| `B3-AC24` | **PASS_SCOPED** | BE Knowledge release model rejects well-formed wrong commit and wrong SHA256 digest against separately pinned synthetic trust manifest; **Boundary:** Real signed source rights/Knowledge release Phase 8 |
| `B3-AC25` | **PARTIAL_EVIDENCE** | Fresh BE 7/7 and FE 2/2 CI green on pinned candidate heads with timestamps and test output; **Boundary:** Owner final Phase3 sign-off missing, branch protection absent, crypto trust profile ADR pending; phase3B exit remains HOLD |
| `B3-AC26` | **PASS_TRACE_ONLY** | FZ02 maps 20 physical and 24 logical invariants to future evidence; audited 44 IDs; **Boundary:** Traceability is not runtime certification; many phase4-11 proofs pending |
| `B3-AC27` | **PASS_SCOPED** | 26 ops, 19 caps, nine events, four DB, service boundaries and diff vs frozen main checked; **Boundary:** Source diff audit only, not proof of no behavioral defect |
| `B3-AC28` | **BLOCKED** | Phase 3B-07R re-audit documents nonproduction candidate plus two green CI runs; no final exit signature; **Boundary:** Explicit owner final source merge approval, effective branch rules and distinct Phase4 work order not present |

**Totals:** **24 PASS_SCOPED + 1 PASS_TRACE_ONLY + 2 PARTIAL_EVIDENCE + 1 BLOCKED**. The 28 items are *all classified*, not all accepted. PASS_SCOPED only certifies narrow nonproduction contracts or CI.

**Outstanding mandatory decisions:** `B3-AC07` (cryptographic profile owner ratification), `B3-AC25` (final evidence/owner approval and enforceable branch governance), `B3-AC28` (final 3B exit signature + separate Phase 4 work order). These keep **FINAL PHASE 3B EXIT HOLD**.

## 4. Crosswalk of 44 frozen invariants

All **20 infrastructure + 24 logical/API** invariant IDs from FZ-02 remain present, normatively unchanged, mapped to Phase 3B tests and explicit later hard gates. **24/44 rows received new source/CI annotations** while all **44/44 retain design traceability** and **0/44 are newly claimed verified on production/runtime**. The full row-by-row invariant audit is in [machine crosswalk](./reltroner-lms-phase3b-07r-invariant-44-crosswalk-20261009.json).

Architectural counts remain **six microservices**, **26 external API operations**, **19 capability names**, **nine semantic events**, **four owned PostgreSQL databases**, source-controlled initial content. The frozen original contracts are not modified by 3B-07R.

## 5. Reconciled 14 findings and still open gates

| ID | Original concern | Revalidation status |
|---|---|---|
| `R-01` | CI does not run on push to main after final merge | **REMEDIATED_CI_SOURCE_POSTMERGE_CHECK_PENDING** — Both workflows now run on pull_request main and push main; phase3-dev push duplication removed. No main merge performed. |
| `R-02` | No main branch protection | **BLOCKED_GITHUB_BRANCH_RULES** — Main protected=false for BE/FE. GitHub connected actions offer branch/ruleset READ only; changing settings requires separately authorized action/API capability. |
| `R-03` | Trust assertion cryptography unratified | **PARTIAL_OWNER_SECURITY_ADR_PENDING** — Cryptographic EdDSA RFC8037 synthetic verifier checks actual sodium signatures and nonce/replay, but proposed key distribution, rotation, replay-store fail-closed policy not owner ratified. |
| `R-04` | Crash/failover persistence tests are ID-to-answer assertions | **REMEDIATED_NONPROD_MODEL** — Replaced E01..E08 answer lookup with input-driven failure state transitions and negative fault mutants; BE 42 persistence model assertions PASS. |
| `R-05` | Grant and migration compatibility test gaps | **REMEDIATED_SCOPED_MODEL_RUNTIME_DEFERRED** — Four DB owner/grant model plus three additive/breaking migration cases tested; actual PostgreSQL grants and schema apply explicitly Phase4+. |
| `R-06` | Source rights attestation hash validation too weak | **REMEDIATED_SCOPED_SYNTHETIC_TRUST** — BE/FE now deny plausible wrong commit/digest against separately pinned synthetic expected values; real Studio rights signer/Knowledge release remains Phase8. |
| `R-07` | FE privacy scanner extension coverage incomplete | **REMEDIATED_FE_CI_GREEN** — FE scanner now rejects draft routes across CSS/SVG/maps/filenames, unknown extensions, and only allows whitespace placeholders in known asset dirs; 9 Node tests + build PASS. |
| `R-08` | Consumer/provider compatibility fixtures are static golden strings | **REMEDIATED_MOCK_PROTOCOL** — BE source mock 136 assertions across all 26 method/path operations, client/cap/owner/ACL negative cases and request/response DTO mutation compatibility; live HTTP provider deferred. |
| `R-09` | CI mutation proof and non-production claims incomplete | **REMEDIATED_SCOPED_MUTANTS** — Negative mutations for removed bearer, incorrect 401, wrong owner, breaking DTO, outbox booking flags, draft assets and valid-shape forged digest; GitGuardian green BE+FE; not exhaustive security guarantee. |
| `R-10` | Real Keycloak issuer, PKCE and signed workload delegation untested | **DEFERRED_RUNTIME_PHASE4** — Real Keycloak clients and cryptographic audience/issuer runtime remain Phase4 nonproduction separate work order. |
| `R-11` | Durable state and booking race unverified | **DEFERRED_RUNTIME_PHASE4_PLUS** — PG grants, booking race, outbox durability, Audit reconciliation require authorized live DB test harness; Phase3 only synthetic. |
| `R-12` | Studio/Knowledge and private search authoritative provenance not live | **DEFERRED_RUNTIME_PHASE8** — Signed Studio canon redistribution rights and Knowledge index private ACL runtime Phase8. |
| `R-13` | Service provider endpoints not integrated or deployed | **DEFERRED_RUNTIME_PHASE4_PLUS** — Real Laravel business controller/provider and 26 method route support not implemented during Phase3 contract stage. |
| `R-14` | 28/28 final acceptance and owner source-merge signature missing | **BLOCKED_FINAL_OWNER_EXIT** — 28 gate matrix is 24 scoped PASS +1 trace-only +2 partial +1 blocked; owner final merge signoff and Phase4 separate work order not received. |

**Important review distinction:** the workflow trigger is fixed in source, but branch protection **still reports false** and cannot be modified via the available connected GitHub operations (only read). The owner must separately authorize or use an administration-capable workflow to apply required PR/check/no-force-push rules. Do not state premerge branch governance is finished until effective settings are verified.

**Explicit Phase 4–12 deferrals:** actual Keycloak/OIDC clients and runtime tokens; PostgreSQL transactions/slot races/Redis outage/Audit durability; real Studio rights signer and Knowledge ACL/release; Laravel business provider HTTP behavior; production Cloudflare publication, asset provenance and VPS infrastructure. These do not become false Phase 3 runtime PASS.

## 6. Governance and next deterministic acceptance

- Both central application PRs remain **DRAFT, OPEN, UNMERGED**. No extra Phase 3 source PRs, force-pushes, historical branch rewrites or app `main` changes.
- This 3B-07R report captures new SHA-pinned CI and acceptance evidence. It is not a guarantee of zero bugs or zero technical debt.
- **Decision needed before final 3B sign-off:** ratify or revise the non-production cryptographic trust ADR; establish effective `main` branch protection; resolve or explicitly owner-disposition B3-AC25 and accept final scoped Phase 3B exit. Only then should the owner issue a **new separate explicit source merge instruction**.
- After the future approved merge: verify actual main-merge SHAs, GitHub Actions **push `main`** green for both BE and FE, main tree integrity, then separately authorize Phase 4 nonproduction work order. No production authority is inferred from any Phase 3 approval.

## 7. Machine-readable handoff

- [28 FZ-10 gate revalidation and source CI pins](./reltroner-lms-phase3b-07r-acceptance-revalidation-20261009.json)
- [44 FROZEN invariant delta crosswalk](./reltroner-lms-phase3b-07r-invariant-44-crosswalk-20261009.json)
- [14 risk resolution/remainder decisions](./reltroner-lms-phase3b-07r-risk-revalidation-20261009.json)
- [Earlier Phase 3B-07 audit baseline](./reltroner-lms-phase3b-07-holistic-end-to-end-audit-20261009.md)

**Checkpoint:** `3A DESIGN FROZEN → 3B-00 PASS → 3B-01 ACCEPTED → 3B-02..06 CONTRACT CI GREEN → 3B-07R REMEDIATION EXECUTED + BOTH NEW CI GREEN → 24 PASS_SCOPED/1 TRACE/2 PARTIAL/1 BLOCKED → FINAL PHASE3B EXIT HOLD → SOURCE MAIN MERGE HOLD`.
