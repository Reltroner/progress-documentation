# GOV-WVR-001 — Phase 3B Branch-Protection Technical Enforcement Exception

> **Status: OWNER-APPROVED GOVERNANCE EXCEPTION FOR PHASE 3 ONLY**  
> **Recorded:** 2026-10-10 (Asia/Jakarta; no unverified exact time).  
> **Authority:** Explicit owner instruction to **close Phase 3 without configuring GitHub Settings branch protection**, following owner-adopted [BRANCH-GOV-001](./branch-gov-001-main-branch-contractual-protection-20261010.md).  
> **Affected:** Reltroner/LMS-BE `main` and Reltroner/LMS-FE `main`; B3-AC25 / R-02 governance control, the original FZ-10 exit administration assumption.  
> **Applicability:** **Phase 3B source contract/CI and future *source* integration after separate authorization only**. No Phase 4, production, identity, database or cloud provisioning rights.

## 1. Owner decision — exact substance / non-consent boundaries

The owner first chose a markdown-only `main` governance contract instead of changing GitHub Settings. On **2026-10-10**, the owner explicitly renewed and expanded the decision:

> "tetapi aku tetap menolak {Settings → Branches → Add branch protection rule, dengan target `main`. Wajibkan PR, status checks, conversation resolution, serta larangan force-push dan penghapusan branch.} untuk closing phase 3 dan phase 3 bisa di nyatakan selesai tanpa melakukan {Settings → Branches → Add branch protection rule, dengan target `main`. Wajibkan PR, status checks, conversation resolution, serta larangan force-push dan penghapusan branch.}"

**Precise decision:** The project owner waives **machine-enforced GitHub branch protection/rulesets configuration as a prerequisite to Phase 3 engineering exit**, and substitutes the previously owner-adopted manual procedure in BRANCH-GOV-001. This decision changes the **Phase 3-specific evidence requirement**, not the reality of GitHub permissions. It does **not** waive successful CI, scoped security checks, owner final exit sign-off, or **separate exact-SHA authorization for application merges**. It does not reapprove source SHA changes.

**Change hierarchy:** The 2026-10-09 FZ-10 frozen `B3-AC25` acceptance text ("all scoped acceptance tests/fixtures green with CI run URL, timestamp, commits and reviewer evidence") is **not edited or deleted**. Its CI and evidence obligation remains active. This newer owner-authorized, versioned `GOV-WVR-001` creates a specifically scoped exception to a supplementary requirement added by the Phase 3B-07 audit: effective GitHub `main` branch protection as a premerge hard gate. No other frozen 20 physical / 24 logical invariants are modified.

## 2. Observed technical facts, not waived or misreported

| Proof | Backend | Frontend |
|---|---|---|
| GitHub branch API | `main protected:false` | `main protected:false` |
| Rulesets listing | `[]` | `[]` |
| Source candidate | `phase3-dev` at `0fc17dabc1af845053ac525986f40fb260f73e4c` | `phase3-dev` at `9795489d9b0e1a13d81675fac29e649900c4381d` |
| Main unchanged at waiver review | `e30a61780994d85671cbf079e6b9ce899b3fe837` | `f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7` |
| PR state | [PR #11](https://github.com/Reltroner/LMS-BE/pull/11) DRAFT/OPEN/UNMERGED | [PR #3](https://github.com/Reltroner/LMS-FE/pull/3) DRAFT/OPEN/UNMERGED |
| CI (exact SHA) | [run 37960568787](https://github.com/Reltroner/LMS-BE/actions/runs/37960568787) SUCCESS, 7/7 Actions, 255 synthetic contract/model assertions; GitGuardian SUCCESS | [run 37960704557](https://github.com/Reltroner/LMS-FE/actions/runs/37960704557) SUCCESS, 2/2 Actions, 9 catalog tests; GitGuardian SUCCESS |

The exception expressly **accepts residual risk**: GitHub does not independently prevent accidental/malicious direct push, force push, unreviewed merge or branch deletion. A human or other automation may disregard project policy, and manual review could miss a time-of-check/time-of-use race. Therefore never state `main protected:true`, `GITHUB_BRANCH_PROTECTION_PASS`, or `no bypass possible`.

## 3. Binding compensating controls — operational, not machine-enforced

Before a future authorized application `main` merge:

1. Keep **one cumulative PR per app repository**, no new Phase 3 source PR and no direct push to `main`. Review the paired BE/FE immutable snapshot jointly.
2. Re-fetch BE/FE `main` full SHAs and PR `phase3-dev` heads **immediately before** the operation; if SHA drift, stop and re-evaluate both 28 acceptance and 44 invariant mapping.
3. Reverify **all seven** BE GitHub Actions checks, **both** FE Actions checks and both GitGuardian checks `completed/success` against the intended candidate. PR test SHA alone is not postmerge evidence.
4. Preserve signed-in-owner human approval record, AI/human review comments, all review threads and blocker resolutions, frozen-contract inventory and read-only premerge evidence index.
5. Require **separate** explicit owner final **nonproduction Phase 3B** acceptance and distinct **one-time BE PR #11 / FE PR #3 main merge authority**; this waiver is neither.
6. Execute future merge only with exact expected PR head SHA and correct branch base. Stop if either repo head/base, required checks or owner scope diverges; no force push, no source-history rewrite or deletion.
7. After authorized merges, inspect **actual BE/FE `main` merge SHAs** and new `push: main` CI jobs. Require success on each actual merged commit before declaring **source integration** complete. A synthetic PR merge SHA is not sufficient.
8. Remain explicitly fail-closed for failed/missing CI and any unexplained security defect. This owner governance exception can excuse a missing technical branch rule, **not failing security or code checks**.

The compensating controls lower risk but cannot equal technical enforcement. The owner can rescind the exception later, but no configuration of GitHub Settings is now a **Phase 3 closure dependency**.

## 4. Gate interpretation

- **B3-AC25:** **PASS_SCOPED_WITH_OWNER_WAIVER**; satisfies the FZ-10 nonproduction evidence requirement via actual green pinned tests + reviewer evidence + formal exception, while the *technical branch-protection subcontrol remains NOT IMPLEMENTED and consciously waived* for this phase. Normalize to `PASS_SCOPED` only for counting Phase 3B's scoped 28-gate matrix, and separately expose `waiver_applied=true`, `technical_control_enforced=false`, `residual_risk=ACCEPTED_BY_OWNER_FOR_PHASE3`.
- **R-02:** **OWNER_ACCEPTED_EXCEPTION / NOT_REMEDIATED_TECHNICALLY**. Do not change actual `protected` observation.
- **B3-AC07:** handled independently by the owner's ratified Ed25519 trust ADR and [Phase 3B-10 scoped revalidation](./reltroner-lms-phase3b-10-ac07-ac25-formal-revalidation-20261010.md).
- **B3-AC28:** owner has authorized **phase-closing eligibility without Settings** but has **not** explicitly authorized BE/FE source `main` merge or Phase 4 work. Until a distinct final 3B acceptance receipt exists, the final exit gate is **BLOCKED / pending owner final acceptance**. A phase may become formally CLOSED under this exception without GitHub settings, but the exception itself does not fabricate that closing event.

## 5. Sunset, handoff, and revision triggers

**Expire for purposes of any unapproved Phase 4/production release:** technical branch protection cannot be claimed fulfilled for later deployment gates. Any later security audit can reopen its suitability; the owner may reinstate GitHub rules separately. If BE/FE governance is later automated, record an independent observed technical activation (not a historical rewrite).

**Authoritative evidence order:** FZ-10 frozen contract → 3B-07R historical audit → ratified [ADR-LMS-TRUST-001](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md) → [BRANCH-GOV-001](./branch-gov-001-main-branch-contractual-protection-20261010.md) → this specific **owner waiver** → dated gate revalidation → future owner final phase exit / source-merge receipt.

**Outcome:** `TECHNICAL GITHUB PROTECTION = FALSE; OWNER EXCEPTION = TRUE; MANUAL CONTROLS = REQUIRED; B3-AC25 = PASS_SCOPED_WITH_OWNER_WAIVER; SOURCE MAIN MERGE = HOLD; PHASE4 = NOT AUTHORIZED`.
