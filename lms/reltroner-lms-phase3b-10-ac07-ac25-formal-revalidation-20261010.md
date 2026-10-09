# Reltroner LMS — Phase 3B-10 Formal Revalidation of B3-AC07 and B3-AC25

> **Recorded:** 2026-10-10 (Asia/Jakarta); **method:** Read-only SHA-pinned re-audit of existing source + GitHub Actions and newly ratified owner decisions.  
> **Formal scope:** Phase 3B nonproduction **contracts, immutable CI snapshot and governance exception only**. **No fresh BE/FE code commit, no rerun represented as new, no Keycloak/JWT runtime, Redis store or production test.**  
> **Result:** B3-AC07 = **PASS_SCOPED (ADR ratified)**; B3-AC25 = **PASS_SCOPED_WITH_OWNER_WAIVER (manual contract / GitHub technical protection absent)**; B3-AC28 = **BLOCKED pending separate final Phase 3B acceptance/source integration authority**.

## 1. Normative decision sources and historic trace

1. [FZ-10 approved 28 criteria](./reltroner-lms-phase3a-04-fz10-phase3b-entry-exit-authorization-20261009.md), particularly AC07 (workload identity + delegated signed assertions, rotation/nonce/replay fixtures) and AC25 (all CI/fixture evidence, timestamp, SHA and reviewer).
2. [Phase 3B-07R source and CI evaluation](./reltroner-lms-phase3b-07r-remediation-and-revalidation-20261009.md) plus [historical 28-gate matrix](./reltroner-lms-phase3b-07r-acceptance-revalidation-20261009.json) (**immutably retained**: 24 scoped PASS, 1 trace, 2 partial, 1 blocked).
3. [ADR-LMS-TRUST-001](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md), ratified by explicit owner statement **for Phase 3B nonproduction design only**.
4. [BRANCH-GOV-001](./branch-gov-001-main-branch-contractual-protection-20261010.md), binding procedural `main` merge discipline, not GitHub technical protection.
5. [GOV-WVR-001](./gov-wvr-001-phase3b-branch-protection-owner-exception-20261010.md), new explicit **owner-approved Phase 3 branch protection enforcement waiver**, superseding the supplemental 3B-07/08 requirement to enable GitHub `main` protections before nonproduction Phase 3 exit. This is a scoped risk acceptance, not a fabricated `protected:true`.

## 2. Reconfirmed unchanged source and positive evidence

| Field | BE | FE |
|---|---|---|
| PR | [#11](https://github.com/Reltroner/LMS-BE/pull/11) — draft, open, unmerged | [#3](https://github.com/Reltroner/LMS-FE/pull/3) — draft, open, unmerged |
| Accepted `phase3-dev` SHA | `0fc17dabc1af845053ac525986f40fb260f73e4c` | `9795489d9b0e1a13d81675fac29e649900c4381d` |
| Frozen `main` SHA | `e30a61780994d85671cbf079e6b9ce899b3fe837` | `f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7` |
| GitHub Actions source run | [37960568787](https://github.com/Reltroner/LMS-BE/actions/runs/37960568787) — `success` on **exact BE SHA**, 7/7 Actions jobs, 255 PHP source contract/model assertions | [37960704557](https://github.com/Reltroner/LMS-FE/actions/runs/37960704557) — `success` on **exact FE SHA**, 2/2 Actions jobs, 9 Node catalog-contract tests |
| Observed run completion | 2026-10-09 16:38:50 UTC | 2026-10-09 16:41:20 UTC |
| GitGuardian | `completed/success` on source SHA | `completed/success` on source SHA |
| GitHub main protection / rulesets | `protected:false` / empty list | `protected:false` / empty list |

**Required check context audit:** BE Actions `Pure PHP frozen contract tests`, `Laravel service assistant`, `Laravel service learning`, `Laravel service mentorship`, `Laravel service knowledge`, `Laravel service gateway`, `Laravel service audit` plus `GitGuardian Security Checks` all `success`; FE Actions `catalog-contract` and `frontend-build` plus `GitGuardian Security Checks` `success`. FE `Cloudflare Pages` was additionally successful but **not** a production release authority. Formal independent GitHub PR review approvals: **none observed**, consistent with an owner-authored source PR; governance review is documented as owner-decision evidence and cross-repo AI/revalidation audit, not falsified GitHub approvals.

## 3. B3-AC07 — final scoped trust disposition

| Verification dimension | Scoped evidence | Conclusion |
|---|---|---|
| Workload + delegated principal schema | [source trust contract at exact BE SHA](https://github.com/Reltroner/LMS-BE/blob/0fc17dabc1af845053ac525986f40fb260f73e4c/contracts/identity/trust-contract.json), including `caller_service`, `recipient_service`, `operation_id`, subject, capability, `request_id`, freshness and `jti` | DESIGN SOURCE PRESENT |
| Ed25519 signed assertion negative suite | [BE signed-trust test](https://github.com/Reltroner/LMS-BE/blob/0fc17dabc1af845053ac525986f40fb260f73e4c/contracts/tests/validate-trust-crypto.php) verifies actual synthetic sodium signature and denial of replay, wrong audience, expiry, future nbf, missing capability, recipient mismatch, unknown key and signature tamper. Included in 255 PASS source assertions | TEST-ONLY PASS |
| Explicit configuration choice | Ratified ADR and [BE candidate profile](https://github.com/Reltroner/LMS-BE/blob/0fc17dabc1af845053ac525986f40fb260f73e4c/contracts/identity/crypto-profile-proposal.json) agree on EdDSA/Ed25519 JWS, TTL <=60s, skew 5s, rotation overlap 180s and per-service key binding; ratified ADR additionally formalizes atomic replay, Redis-outage deny and >=65s quarantine | **OWNER RATIFIED** |
| Historic `PENDING_SECURITY_ADR` markers | The frozen BE source test checks the *historical at-commit state*: the profile object still says `CANDIDATE_NOT_OWNER_RATIFIED_SECURITY_ADR`, and internal-workload `trust-contract.json` lists `PENDING_SECURITY_ADR` parameters. This is true **as of the earlier source commit**, not the later dated owner ratification. Normative current design parameter authority is the subsequently approved and versioned ADR. Do not silently edit immutable source SHA, claim the JSON was modified, or treat the marker as overriding a later owner decision. | **DOCUMENTED TEMPORAL SUPERSESSION**, runtime implementation must reconcile source markers before use |
| OIDC access-token algorithm allowlist | Separate `oidc.access_token.allowed_signing_algorithms` remains unresolved. Ed25519 internal delegation choice **does not** approve Keycloak's access-token signing algorithm, which must be established from effective Keycloak JWKS/runtime in Phase 4 | **SEPARATE PHASE 4 HARD GATE** |
| Production/runtime proof | No live dual-assertion middleware, real `kid` custody/rotation, Redis atomic replay outage or Keycloak regression executed | **NOT CERTIFIED / DEFERRED** |

**B3-AC07 formal scoped judgment: PASS_SCOPED** because all FZ-10 **Phase 3B design+synthetic test** requirements are met and the once-open security-selection decision has now been ratified. **Do not label it runtime security PASS**. Preserve signed fixture limitations, including no unpredictable real runtime `jti`/atomic Redis demonstration. **Source documentation status normalization is required before Phase 4 runtime implementation**; do not accidentally deploy the historic test profile.

## 4. B3-AC25 — final scoped evidence/governance disposition

**FZ-10 exact criterion:** “All scoped acceptance tests/fixtures green with CI run URL, timestamp, commits and reviewer evidence.” The two source heads are identical to their already-successful 07R CI test heads, and this re-audit re-read job conclusions and check-run names; no fresh run is represented or required because source did not change. The same documentation ledger, 28-gate machine matrix, 44 invariant crosswalk, 14 findings and human approval/AI review provenance remain auditable. **All mandatory tested source checks are green.**

**GitHub protection question (separate control):** Both `main` remain **`protected:false`**. The owner **explicitly rejects enabling** GitHub `Settings → Branches` for Phase 3 closure, and the newer [GOV-WVR-001](./gov-wvr-001-phase3b-branch-protection-owner-exception-20261010.md) formally accepts residual enforcement risk using [BRANCH-GOV-001](./branch-gov-001-main-branch-contractual-protection-20261010.md) as a **human process, not GitHub branch protection**. This is a change to a premerge governance hard-gate interpretation, **not evidence the missing technical control has been implemented**.

**B3-AC25 formal scoped judgment: PASS_SCOPED_WITH_OWNER_WAIVER** (`normalized_status=PASS_SCOPED`, `waiver_applied=true`, `github_branch_protection_enforced=false`, `residual_risk=OWNER_ACCEPTED_PHASE3`). This does not authorize BE/FE source merge; immediately-before-merge checks and a later separate signed owner instruction remain necessary.

## 5. Revised 28 gates / 44 invariants

| Formal scoped gate state (Phase 3B-10) | Count |
|---|---:|
| `PASS_SCOPED` (including AC25's explicit waiver subclass) | **26** |
| `PASS_TRACE_ONLY` | **1** |
| `PARTIAL_EVIDENCE` | **0** |
| `BLOCKED` (B3-AC28 final exit owner approval) | **1** |
| **Total** | **28** |

Changes from 3B-07R are only `B3-AC07 PARTIAL → PASS_SCOPED` and `B3-AC25 PARTIAL → PASS_SCOPED_WITH_OWNER_WAIVER`. `B3-AC28` is **not** changed; the owner's statement that Phase 3 **may** close without branch protection is an explicit waiver **not yet** an unambiguous **final Phase 3B source acceptance and merge order**. Therefore **Phase 3B is now eligible for final owner exit review without GitHub Settings, but not yet formally EXIT PASS**. No false `28/28` PASS claim.

**44 frozen invariants:** no owner-authorized architecture change; preserve exactly 20 infrastructure + 24 logical/API IDs as design traces, 24 annotated by 07R tests, **0 additionally production/runtime certified**. The amended Phase 3 governance evidence requirement is a human process decision, **not an amendment to physical/logical invariant semantics**.

## 6. Explicit remaining decision, and what is no longer a blocker

**No longer required for Phase 3B closure:** clicking `Settings → Branches`, activating branch protection/rulesets, or obtaining `protected:true`. Owner chose that restriction explicitly and accepted its residual risk. Do not ask the owner to do it again to close this phase.

**Still required:** owner final Phase 3B **nonproduction** scoped acceptance on immutable BE/FE SHA pair and `B3-AC28` final exit receipt; after that a **separate one-time authorization** to merge BE PR #11 and FE PR #3 to `main` if desired. Actual postmerge `push: main` green evidence cannot precede the merge. A **separate** Phase 4 nonproduction work order is mandatory before provisioning; not part of the proof for current source contract/runtime.

**Conclusion:** `3B07R 24+1+2+1 → OWNER-RATIFIED ADR + GOV-WVR-001 → 3B10 26 SCOPED (1 WITH WAIVER) + 1 TRACE + 1 BLOCKED → FINAL PHASE 3B EXIT REVIEW READY WITHOUT BRANCH SETTINGS → SOURCE PRs UNMERGED; PHASE4 NOT AUTHORIZED`.
