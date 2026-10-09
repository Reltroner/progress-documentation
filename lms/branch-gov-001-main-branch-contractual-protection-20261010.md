# BRANCH-GOV-001 — LMS-BE / LMS-FE `main` Contractual Protection and Manual Merge Governance

> **Decision date:** 2026-10-10 (Asia/Jakarta); exact clock time not asserted.  
> **Owner decision:** **ADOPT CONTRACT-ONLY / MANUAL GOVERNANCE**, replacing the *planned immediate GitHub Settings action* with this versioned markdown contract.  
> **Scope:** `Reltroner/LMS-BE` and `Reltroner/LMS-FE`, target branch exactly `main`; Phase 3B source integration and all future changes until superseded.  
> **Enforcement status:** **DOCUMENTED POLICY ONLY — NOT GITHUB-ENFORCED**. As of this decision both `main` branch endpoints returned `protected:false`; no active ruleset was observed.  
> **Precedence:** Frozen Phase 0C infrastructure contract; frozen Phase 1 logical/API contract; approved FZ-10 Phase 3B 28 acceptance and FZ-11 design freeze; actual owner-signature instructions; this operational governance overlay. This file does **not** rewrite a frozen invariant or retroactively waive an acceptance gate.
>
> **Explicit limitation:** This document cannot technically prevent a direct push, force push, unreviewed merge, branch deletion, or an administrator bypass. It binds the project's operating procedure **by owner decision**, not GitHub's permission engine. A CI-green PR and a governance document together do **not** prove effective GitHub branch protection.

## 1. Owner instruction and disposition

The owner explicitly accepted **ADR-LMS-TRUST-001**, including EdDSA/Ed25519, JWS Compact, maximum 60-second TTL, 5-second clock skew, 180-second rotation overlap, service-pinned public-key distribution, atomic one-use Redis `jti` replay control and fail-closed >=65-second recovery quarantine, **only as Phase 3B nonproduction design**.

The same owner chose **not to configure** `Settings → Branches → Add branch protection rule` now, opting to record branch governance through a new `.md` contract under `progress-documentation/lms`. **This is an explicit procedural-control choice, not a factual statement that GitHub branch settings changed.**

Decision scope:
- **Approved:** document and follow the manual governance policy in this file; archive the ADR ratification and source-pinned evidence.
- **Not approved:** immediate technical branch protection configuration, any BE/FE source merge, source branch rewrite or reset, production deployment, Phase 4 activation, or bypass of FZ-10/FZ-11 gates.
- **Risk retained:** if an account or agent ignores these manual rules, GitHub currently cannot be relied upon to block the forbidden action. `R-02` remains an **accepted operating-mode choice with unmitigated technical-enforcement gap**, not a closed vulnerability or `protected:true`.

## 2. Repository topology and approved baseline snapshot

| Dimension | LMS-BE | LMS-FE |
|---|---|---|
| Repository | [Reltroner/LMS-BE](https://github.com/Reltroner/LMS-BE) | [Reltroner/LMS-FE](https://github.com/Reltroner/LMS-FE) |
| One central application PR | [#11](https://github.com/Reltroner/LMS-BE/pull/11) — DRAFT, OPEN, UNMERGED | [#3](https://github.com/Reltroner/LMS-FE/pull/3) — DRAFT, OPEN, UNMERGED |
| Approved work branch | `phase3-dev` | `phase3-dev` |
| CI-evidenced source head | `0fc17dabc1af845053ac525986f40fb260f73e4c` | `9795489d9b0e1a13d81675fac29e649900c4381d` |
| Unchanged `main` at policy decision | `e30a61780994d85671cbf079e6b9ce899b3fe837` | `f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7` |
| Source CI result | [37960568787](https://github.com/Reltroner/LMS-BE/actions/runs/37960568787) — 7/7 GitHub Actions; 255 synthetic contract/model assertions | [37960704557](https://github.com/Reltroner/LMS-FE/actions/runs/37960704557) — 2/2 GitHub Actions; 9 catalog tests |
| GitHub `main` protection reported | `false` | `false` |

The SHA pairs are **frozen review inputs, not automatic authorization to merge**. Recheck exact head, main base, CI run IDs, PR status, mergeability, cross-repo compatible snapshot, and source diff at each later premerge review. Any source head drift invalidates the current source-pinned gate and requires revalidation of impacted 28 criteria / 44 invariant crosswalk.

## 3. Binding project rules while operating without GitHub Rulesets

**POL-01 — PR-only discipline.** All intended changes to BE/FE `main` must be proposed through reviewed PRs. No direct push to `main`, whether by human, IDE agent, CLI, connector, workflow, or integration. No self-authorized emergency exception. If an emergency change is required, the owner must publish an explicit versioned exception with exact scope, rollback and review evidence **before** the action.

**POL-02 — No history destruction.** No force push, non-fast-forward ref update, `reset --hard` followed by forced update, rewriting a signed reviewed candidate SHA, or deleting protected-intent branches. A future branch retention/cleanup plan must be separately approved.

**POL-03 — Immutable evidence.** Before merge, record full 40-character BE/FE candidate heads and `main` bases; the exact CI run URLs and conclusions; branch provenance; 26 method/path operations, 19 capabilities, nine events, four owned DBs, six service topology, and 44 frozen-invariant traceability. No claim that these static checks prove later live API/Keycloak/PostgreSQL/Redis behavior.

**POL-04 — All mandatory CI green for exact candidate.** Require the following checks to be complete/success on the correct SHA (or, when GitHub runs on PR synthetic merge refs, capture both the source head and the tested merge ref/base relationship). Any skipped, pending, stale, unavailable or failed mandatory check **stops** merge:

| LMS-BE | LMS-FE |
|---|---|
| `Pure PHP frozen contract tests` | `catalog-contract` |
| `Laravel service assistant` | `frontend-build` |
| `Laravel service learning` | `GitGuardian Security Checks` |
| `Laravel service mentorship` | |
| `Laravel service knowledge` | |
| `Laravel service gateway` | |
| `Laravel service audit` | |
| `GitGuardian Security Checks` | |

`Cloudflare Pages` success is not treated as permission to deploy or as a source release requirement. Independently check the trusted GitHub Actions and GitGuardian app origins and latest conclusions, not only copied screenshots or self-reported logs.

**POL-05 — Review closure.** Manually inspect all unresolved review conversations, file diffs, security findings, schema/capability drift, and dependencies. Every blocking question must have an evidence-backed disposition. As these PRs are owner-authored, an owner's PR comment is **not** a GitHub qualifying independent review approval. No fictional external review.

**POL-06 — Two-stage owner sign-off.** (a) The owner must issue explicit acceptance of the full **Phase 3B nonproduction** evidence on exact BE/FE SHAs, 28 acceptance criteria and 44 invariant traceability, with documented treatment of risks; (b) **only after that**, owner issues a separate, exact-PR **one-time source `main` merge authorization**. Ratifying ADR-LMS-TRUST-001 or merging this documentation does **not** satisfy either instruction.

**POL-07 — Dual-repo coordination.** Do not merge the BE PR in isolation merely because its jobs pass if the paired FE acceptance is stale or incompatible. Check both immediately before the first authorized merge. If either fails between two merges, stop, preserve evidence, and request new owner instructions; do not silently repair via direct main push.

**POL-08 — Final merge execution and evidence.** After an authorized future merge, record actual **BE/FE main merge SHA**, verify new `push: main` GitHub Actions checks succeed on **those** SHAs (not the PR test-run or synthetic merge ref), ensure inventory and contract-tree integrity, and update the ledger. An all-green source CI does **not** authorize a VPS, DNS, Keycloak, PostgreSQL, Redis, Cloudflare or production change.

**POL-09 — Operational stop policy.** If any SHA changed unexpectedly, check contexts differ, permissions are unclear, findings lack disposition, or the owner has not separately approved final merge, **STOP**. Never treat this contract as machine-executed enforcement.

**POL-10 — Future technical-control option.** Actual GitHub protection/rulesets can be installed later by a new owner change instruction. Until verified by GitHub reads, always report `GITHUB_ENFORCEMENT = NOT_CONFIGURED`. This contract alone never qualifies as a successful technical control implementation.

## 4. Human / AI execution responsibilities

| Actor | Can do under this contract | Cannot do without independent authorization |
|---|---|---|
| Project owner | Ratify architecture/ADR, accept risk and test evidence, issue exact-SHA approvals and exceptions | Retroactively turn an unprotected branch into `protected:true` by declaration |
| ChatGPT / review AI | Read repositories, compare frozen contracts, prepare evidence, review gates, draft approved documentation changes | Assume owner signature, self-merge BE/FE PRs, equate manual policy to enforced settings |
| IDE AI agent | Implement explicitly scoped code on approved non-`main` branch when a dedicated work order exists | Direct `main` push/merge, mutate identity/runtime infrastructure |
| GitHub Actions | Supply reproducible test evidence for exact head/merged `main` SHAs | Replace an actual protected-branch mechanism or a human owner release decision |

Suggested manual operator control: before any merge, record two independent read-only snapshots separated in time (initial review and immediately-before-merge); compare SHAs and CI; capture owner decision verbatim in the archive; use exact expected-SHA merge precondition to reduce time-of-check/time-of-use mistakes. This **reduces** risk but cannot eliminate manual bypass.

## 5. Governance acceptance and outstanding debt

| Item | Factual disposition |
|---|---|
| `ADR-LMS-TRUST-001` | **OWNER RATIFIED — NONPRODUCTION DESIGN ONLY**; parameters and cryptographic runtime proof remain distinct |
| `R-03` | Owner security-selection decision closed; production trust key/replay implementation still deferred |
| `R-02` | **NOT TECHNICALLY REMEDIATED**; owner selected documented manual controls instead of GitHub Settings |
| `B3-AC07` | ADR ratification evidence exists; source-level reconciliation against the ratified ADR may still be needed before formal acceptance upgrade; not a runtime PASS |
| `B3-AC25` | **PARTIAL_EVIDENCE** — SHA-pinned candidate CI and procedural governance documented, but technical enforcement absent; do not label branch-protection gate PASS |
| `B3-AC28` | **BLOCKED** — final owner nonproduction exit and separate BE/FE merge authorization not supplied |
| Historical `3B-07R` count | **24 PASS_SCOPED + 1 PASS_TRACE_ONLY + 2 PARTIAL_EVIDENCE + 1 BLOCKED**, historical audit unchanged |
| 44 invariant runtime certification | **0** additional live runtime claims |
| Actual source `main` merges | **NONE** |
| Phase 4 / production | **NOT AUTHORIZED** |

**Gate-change policy:** owner may propose replacing the FZ-10 branch-protection hard gate with a manual compensating-control exception **only via a separately identified versioned governance change/waiver against that precise gate**; simply saving this file is not enough to assert that the original technical evidence exists. Such an exception must explicitly classify the higher residual risk and whether final Phase 3B source merging is permitted. In the absence of that separate final approval, `main` merge stays HOLD.

## 6. Cross-reference and archival handoff

- [Ratified ADR-LMS-TRUST-001](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md)
- [Prior Phase 3B-08 governance planning packet (historical baseline)](./reltroner-lms-phase3b-08-security-and-final-merge-governance-20261010.md)
- [FZ-10 original entry/exit acceptance authority](./reltroner-lms-phase3a-04-fz10-phase3b-entry-exit-authorization-20261009.md)
- [Phase 3B-07R fixed-source evidence index](./reltroner-lms-phase3b-07r-remediation-and-revalidation-20261009.md)
- [End-to-End Engineering Progress Ledger](./engineering-end-to-end-progress-ledger.md)

**Effective governance status after document merge:** `OWNER RATIFIED CRYPTO DESIGN → CONTRACTUAL BRANCH GOVERNANCE ADOPTED → GITHUB MAIN SETTINGS STILL UNPROTECTED → B3-AC25 PARTIAL / B3-AC28 BLOCKED → SOURCE MERGE HOLD → PHASE4 NOT AUTHORIZED`.


---

## 7. Binding subsequent Phase 3 exception — GOV-WVR-001 (2026-10-10)

**Owner explicitly approved Phase 3 closure WITHOUT configuring GitHub Branch Protection Settings.** [GOV-WVR-001](./gov-wvr-001-phase3b-branch-protection-owner-exception-20261010.md) is the separate, narrowly scoped waiver anticipated by §5; the owner accepts higher residual risk of unprevented direct/forced pushes while requiring **every** PR-only, check-run, immutable SHA, human sign-off and no-history-rewrite control above as manual project policy. This later signed-in-conversation decision **supersedes only the old technical-protection premerge hard-gate interpretation for Phase 3**, not the factual `protected:false` state, any frozen architectural invariant, the Phase 3 CI acceptance requirement or a distinct BE/FE source-merge authorization.

[Phase 3B-10 acceptance revalidation](./reltroner-lms-phase3b-10-ac07-ac25-formal-revalidation-20261010.md) marks `B3-AC25=PASS_SCOPED_WITH_OWNER_WAIVER` (normalized scoped pass); `B3-AC28` remains separately blocked awaiting explicit final phase exit and source-merge decision. **No GitHub Settings action is required to close Phase 3** under this owner exception. No production or Phase 4 authority is inferred.
