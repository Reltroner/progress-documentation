# Reltroner LMS — Phase 3B-08 Security Ratification & Merge Governance Execution Packet

> **Subsequent owner decision — 2026-10-10 (Phase 3B-09):** ADR-LMS-TRUST-001 **OWNER-RATIFIED for Phase 3B NONPRODUCTION DESIGN ONLY**. The owner chose a **markdown-only manual governance contract** instead of enabling GitHub branch protection now: [BRANCH-GOV-001](./branch-gov-001-main-branch-contractual-protection-20261010.md). This Phase 3B-08 text below remains a **historical proposed GUI/admin implementation plan**, **not the current selected execution path**. Actual BE/FE `main` still `protected:false`; the manual contract is NOT technical enforcement; B3-AC25 remains partial, B3-AC28 blocked, and neither source PR may merge. The ratification also does not rewrite 3B-07R's historic gate matrix.

> **Checkpoint:** 2026-10-10 Asia/Jakarta; **disposition:** GOVERNANCE DOCUMENTATION PREPARED; **SOURCE MERGE HOLD**, **PHASE 4 NOT AUTHORIZED**, **PRODUCTION UNTOUCHED**.  
> **Authority:** FZ-10 + FZ-11 + Phase 3B-07R audit. This document proposes enforceable decisions; it is **not** a fictitious owner signature or GitHub settings write.

## 1. Fresh observed preflight (not inferred from CI alone)

| Repository | PR candidate | `main` baseline | Exact GitHub Actions evidence | State |
|---|---|---|---|---|
| [LMS-BE](https://github.com/Reltroner/LMS-BE/pull/11) | `phase3-dev` `0fc17dabc1af845053ac525986f40fb260f73e4c` | `e30a61780994d85671cbf079e6b9ce899b3fe837` | [37960568787](https://github.com/Reltroner/LMS-BE/actions/runs/37960568787), 7/7 SUCCESS, 255 source contract/model assertions | Draft/open/unmerged |
| [LMS-FE](https://github.com/Reltroner/LMS-FE/pull/3) | `phase3-dev` `9795489d9b0e1a13d81675fac29e649900c4381d` | `f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7` | [37960704557](https://github.com/Reltroner/LMS-FE/actions/runs/37960704557), 2/2 SUCCESS, 9 catalog tests | Draft/open/unmerged |

GitHub REST `GET /repos/{owner}/{repo}/branches/main` reported **`protected:false` on both**; `GET /repos/{owner}/{repo}/rulesets` reported **`[]` on both**. The connected GitHub operations expose administration READ only for these resources; **no write settings action** is present. Do **not** claim protection enabled. All BE/FE source SHA evidence pre-dates this documentation work and was not mutated by it.

## 2. Exact main-branch protection work order (GUI / admin-capable surface only)

On **each** repo open **Settings → Branches → Add branch protection rule**, target **exact branch name `main`**. Or use **Settings → Rules → Rulesets** if available on the account; choose **Active** and limit target to the `main` branch only. Do **not** create overlapping conflicting rulesets and legacy protections. Require a pull request before merging; block force pushes and deletions; require conversation resolution. Enable required successful status checks and preferably up-to-date branch check if the PR workflow can satisfy it. No direct push-to-main exception for regular development.

**Exact observed GitHub check-run names to require (select existing GitHub Actions app context; do not invent workflow/display names):**

| BE required checks | FE required checks |
|---|---|
| `Pure PHP frozen contract tests` | `catalog-contract` |
| `Laravel service assistant` | `frontend-build` |
| `Laravel service learning` | `GitGuardian Security Checks` |
| `Laravel service mentorship` | |
| `Laravel service knowledge` | |
| `Laravel service gateway` | |
| `Laravel service audit` | |
| `GitGuardian Security Checks` | |

**Solo owner safeguard:** the existing PRs are authored by the same connected owner, and GitHub does not permit self-approval as a qualifying PR review. Do **not** configure `>=1 required approving reviews` with no independent eligible reviewer, which creates an unresolvable gate. It is acceptable to require PR path + checks + conversation resolution **with zero required external approvals** while retaining an explicit owner SHA-pinned approval/merge receipt and AI/human review outside GitHub's review-count gate. If an independent reviewer is recruited, add review requirement with a separately documented owner change. Do not misrepresent self-authored comments as GitHub formal review.

**Scope correctness:** `Cloudflare Pages` appeared as an FE check at the snapshot; it is not proposed as a required source merge gate because production deployment remains unapproved. Keep Cloudflare deployment/secrets/branch preview policy separately gated. BE requires all seven contract/service checks plus GitGuardian; FE requires both source checks plus GitGuardian. First verify GitGuardian remains installed/available as a required check on `main`/PR contexts; missing contexts can block all future merges and must be reconciled, **never bypassed silently**.

**Verification after owner GUI save (independent evidence):**

1. Re-read `GET https://api.github.com/repos/Reltroner/LMS-BE/branches/main` and the equivalent FE endpoint; capture exact `protected:true`, current SHA, UTC timestamp, rule overview URL or screenshot. Re-read `/rulesets`; absence of a ruleset alone is not proof of missing protection if legacy branch rule is used.
2. Re-read `GET /repos/Reltroner/{LMS-BE|LMS-FE}/branches/main/protection` **only** with a permitted admin-capable session to verify actual contexts/review policy and required PR path. Without admin access, mark details `NOT_VERIFIABLE`, not PASS.
3. Demonstrate that the draft source PR cannot currently merge and that required checks are attached to the exact proposed PR head/merge context; preserve evidence of protected `main`, no bypass and no force-push/delete. Do not deliberately attempt to violate production/repo settings.
4. Re-read both PR head SHAs and their CI results **after** settings apply; any source SHA drift triggers a new combined 28/44 revalidation. Keep the source PRs draft until the owner signs Phase 3 exit.

**Important:** `main` branches remain intentionally unchanged in this work order. GitHub settings changes are administrative governance mutations, not source-main merges; the user must perform them in the GitHub GUI or supply a separately authorized admin write capability.

## 3. Ratification order and decision provenance

The security ADR recommendation is [ADR-LMS-TRUST-001](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md). Accept explicitly the **individual** profile dimensions: EdDSA/Ed25519 JWS, service-pinned public keys and rotation, 60s maximum assertion life, 5s skew, 180s routine rotation overlap, atomic Redis one-time `jti` with fail-closed recovery quarantine, and runtime proof deferrals. If any dimension is revised, update the ADR before ratification. This does **not** authorize applying keys to VPS or changing Keycloak realm.

The last owner approval for BE PR #11 and FE PR #3 applied to **older candidates** and expressly did **not** authorize `main` merge. It cannot silently be extended to the 07R SHAs. The exact current user request to complete governance is permission to **prepare and execute available governance tasks**, but is **not by itself an explicit selection of a named cryptographic parameter set or permission to merge**.

**Decision receipts required** (record the owner's actual statement verbatim; do not fabricate or backdate): (a) **security-ADR ratification** for the named SHA and profile, (b) proof that BE+FE `main` branch rules are now effective, (c) **Phase 3B scoped acceptance** of the combined BE+FE immutable SHA snapshot and the 28-gate/44-invariant interpretation, and (d) **separate explicit, one-time, two-PR `main` merge instruction**. Phase 4 is a distinct subsequent work order after post-merge proof.

## 4. Precise frozen acceptance accounting

Prior actual Phase 3B-07R result remains **24 PASS_SCOPED + 1 PASS_TRACE_ONLY + 2 PARTIAL_EVIDENCE + 1 BLOCKED**. All 44 FZ-02 invariants remain design-traced; 24 rows have fresh CI annotation; **zero** received production/runtime certification.

| Gate | Current before owner/admin actions | Closure evidence | Cannot be inferred from |
|---|---|---|---|
| `B3-AC07` Internal trust | **PARTIAL_EVIDENCE** | Owner-ratified ADR-LMS-TRUST-001 exact parameter record and scoped tests at candidate SHA; runtime separately gated | Ed25519 synthetic fixture PASS by itself |
| `B3-AC25` Evidence/merge governance | **PARTIAL_EVIDENCE** | Effective BE/FE branch rules, required check contexts green, source SHA re-pin/owner evidence signature | Green CI while `main protected:false` |
| `B3-AC28` Final Phase 3B exit | **BLOCKED** | Owner explicitly signs Phase 3B **nonproduction scope** exit for these immutable SHAs, plus distinct source-merge permission; Phase 4 only later | This prepared document or Docs PR merge |
| `B3-AC26` 44 invariants | **PASS_TRACE_ONLY** | 44 stable IDs with explicit future runtime proof obligations | Source checks imply real deployment |

No unilateral promotion to **28/28 PASS** is valid before the exact remaining evidence is observed and recorded. Ratification resolves a design-policy deficit; it cannot erase future infrastructure, provider HTTP, Keycloak, PostgreSQL, Redis-fault, Knowledge provenance or HRM nonregression gates.

## 5. Final change-control and postmerge sequence

**Do not merge either source PR now.** After steps 2–4 are demonstrably true and owner issues an explicit new merge command: mark both PRs ready, refresh and compare final `phase3-dev` SHAs against the ratified snapshot, verify required checks and strict branch policy, merge each PR exactly once with method pre-approved by owner. Stop on divergent SHA, failure, stale context, security ambiguity or reviewer gate. Never merge one repo and assume the paired repo was integrated; coordinate release and rollback.

**After the *actual* authorized BE/FE main merges:** pin **both actual main merge SHAs** (not prior PR head or GitHub synthetic test-merge SHA), observe newly triggered `push: main` checks complete green for both, verify 26/19/9/4 inventories and source-tree integrity, record any rollback decisions, then issue an explicit **Phase 4 nonproduction** work order. No claim of live end-to-end runtime or production permission until later phases.

## 6. Owner's actionable sign-off format (unsubmitted)

```text
SECURITY ADR DECISION:
I [APPROVE / REVISE] ADR-LMS-TRUST-001 for NONPRODUCTION DESIGN ONLY.
Parameters: EdDSA Ed25519 JWS; <=60s TTL; 5s skew; 180s routine rotation;
per-service pinned public keys; fail-closed atomic replay + quarantine.
BE SHA: 0fc17dabc1af845053ac525986f40fb260f73e4c.

BRANCH GOVERNANCE:
BE main protected: [observed true/false + evidence]
FE main protected: [observed true/false + evidence]
Required check contexts: [verified lists] | PR path and force-push/deletion guards: [verified].

FINAL PHASE 3B EXIT (SEPARATE):
I [ACCEPT / HOLD] the NONPRODUCTION Phase 3B snapshot
BE=0fc17dabc1af845053ac525986f40fb260f73e4c
FE=9795489d9b0e1a13d81675fac29e649900c4381d
with 28 acceptance gates' explicit evidence and 44 frozen invariant trace,
without runtime/production certification.

SOURCE MERGE AUTHORITY (SEPARATE):
I [AUTHORIZE / DO NOT AUTHORIZE] merging LMS-BE PR #11 and LMS-FE PR #3
after their exact SHA and required-check revalidation. No production rollout.
```

Do not fill an unchecked field with `true`, insert an invented owner signature, or construe the sign-off example as having been submitted.
