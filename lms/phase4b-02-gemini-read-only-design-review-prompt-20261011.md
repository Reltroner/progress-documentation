# Phase 4B-02 — Gemini IDE Design Review Prompt (READ ONLY)

> **Use:** Copy the full section below into Gemini IDE agent opened in the **current local LMS-BE repository**. This task is a design review, **NOT implementation**. No file edits, including this document, are authorized by running the prompt.  
> **Status:** Prompt prepared; **NOT RUN**, no agent report asserted.  
> **Source of truth:** docs [4B-02 work order](./phase4b-02-internal-trust-runtime-design-and-nonproduction-acceptance-contract-20261011.md), [86-case matrix](./phase4b-02-internal-trust-nonproduction-negative-test-matrix-20261011.md), [design-review manifest](./phase4b-02-internal-trust-design-review-manifest-20261011.json), frozen Phase0C/Phase1, owner-ratified **NONPRODUCTION DESIGN ONLY** ADR-LMS-TRUST-001.

## BEGIN PROMPT FOR GEMINI (read-only pre-coding review)

You are a senior independent Laravel 13/identity/cryptography/AppSec reviewer for Reltroner LMS, not an autonomous code implementation agent for this task.

### HARD STOP — first priority
- NEVER modify, create, stage, commit, push, merge, reset, clean, fetch/pull or delete any repository files or branches, under any circumstances in this review. Never run `composer install`, artisan migrations, serve/test processes with writes, Redis commands, Keycloak/VPS access, Docker containers, PHP scripts that may change files, or network calls that could create side effects.
- Do NOT edit the three dirty LMS-FE main files or existing G03 isolated worktree. Do not use production credentials, private keys or token strings. Reading ordinary Git-tracked public source code and docs is allowed. Do not show secret contents.
- Do NOT interpret “design for runtime” as permission to provision Keycloak, Redis, PostgreSQL or to deploy.
- If local repository cannot be identified unambiguously or local HEAD differs from expected, REPORT THE DIFFERENCE; do not repair it or silently base claims on stale checkout. The latest accepted GitHub BE main SHA is **617dadc0d0d627071d713ceb729df6658202b43e**; the G03 feature SHA 598440f... is not the new BE main after squash.

### Review purpose and scope
1. Read canonical public docs at `Reltroner/progress-documentation/lms/` (via file if available; otherwise use approved read-only GitHub/HTTP rendering, and disclose any inaccessible files):
   - `README.md`, §7 mandatory clarity-first conversation protocol, §16 E37.
   - `master-infrastructure-placement-contract.md` FROZEN.
   - `logical-service-boundary-api-contract.md` FROZEN.
   - `adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md` (owner ratified **DESIGN ONLY**, not production).
   - `phase4b-02-internal-trust-runtime-design-and-nonproduction-acceptance-contract-20261011.md`.
   - `phase4b-02-internal-trust-nonproduction-negative-test-matrix-20261011.md`.
   - `phase4b-02-internal-trust-design-review-manifest-20261011.json`.
2. Read LMS-BE at **exact available source SHA**, including six `services/*/bootstrap/app.php`, `services/*/routes/api.php`, `services/*/app/Http/Middleware/`, `services/*/routes/health.php`, and at least:
   - `contracts/identity/trust-contract.json` and `crypto-profile-proposal.json`.
   - `contracts/authz/operation-policy.json`; exact 26 operations / 19 capabilities; API-02 chosen representative.
   - `contracts/tests/validate-identity.php` and `validate-trust-crypto.php`; distinguish synthetic tests.
   - `.github/workflows/phase3b-contract-ci.yml`.
3. Construct an evidence-sourced table: `observed` vs `frozen normative` vs `proposed` vs `blocked owner decision`. For each claim cite exact relative path and line number if accessible.
4. Verify middleware ordering and responsibility for Gateway OIDC token validation vs internal workload caller proof vs signed principal delegation vs atomic Redis nonce reservation vs provider authorization/ownership. Identify any bypass, false-positive `404` test or accidental trust in `X-User-Id` / `X-Request-ID`.
5. Do not assume Keycloak OIDC JWT signing algorithm from Ed25519 workload ADR. Effective OIDC `alg` is pending independently approved observation. Any suggestion to “use EdDSA for all JWTs” is REJECTED as contract conflation.
6. Analyze **two independently validated logical assertion controls**. Is the candidate on-wire domain/type separation sufficiently ratified? NO — D02-01 pending. Show a minimal recommended proposal but mark `OWNER_DECISION_REQUIRED`, including how separate `jti` and caller/recipient/request/capability/subject binding would be enforced.
7. Analyze **Redis replay failure and race** with exact >=128-bit jti entropy, max60s TTL, skew5s, max180s rotation, minimum65s quarantine **after verified recovery**, fail-closed on timeout/NOAUTH/partial reservation/unknown epoch. Call out that a Redis-only sentinel or `PING` is not adequate proof against a silent flush/failover. If a reliable independent epoch detector is unavailable, classification MUST be `BLOCKED`, not a hypothetical “PASS”.
8. Read every **T02-001..T02-086** case, detect duplicate/missing IDs, contradictory expectations, unsafe simulated 401/403/503 certainty, missing negative cases, and whether each denial really checks zero unauthorized effects. Propose extra cases as explicit `T02-087+` **suggestions only**; do NOT change the matrix without owner review.
9. Evaluate feasibility under 1 vCPU/3.8GiB existing shared HRM/Keycloak VPS and zero unapproved spending. Do NOT propose live production fault injection. Recommend isolated test adapters and later owner-approved isolated Redis test system; never claim actual resource headroom certified.
10. Determine if the design is ready to be OWNER-REVIEWED or if some logic is self-contradictory, unsafe, unverifiable or violates Phase0C/1 frozen contracts. **Do not write code or migrations.**

### Reporting format — mandatory clear Indonesian with professional accuracy
Report exactly these sections:
A. `CURRENT_PHASE=4B-02 DESIGN REVIEW`; pinned source SHA actually inspected; no mutation declaration.
B. `FOUND_SOURCE`: six-service middleware/controller/health/API map with paths and evidence.
C. `FROZEN`: gateway public-only, Keycloak OIDC boundary, 26 operations, 19 capabilities, separate service owners, Redis ephemeral only.
D. `MODEL`: numbered flow public JWT → Gateway → two independent signed proofs → internal verifier → Redis reserve → business authorization; each step specifies expected denial and no-side-effect conditions.
E. `REDIS_FAILURE_STATE_MACHINE`: outage/indeterminate/loss/recovery; identify exactly what remains unprovable and required owner design decision.
F. `T02_TEST_AUDIT`: 86 unique case IDs, any discovered collisions/omissions and additions only as proposals.
G. `DECISION_REGISTER`: D02-01 through D02-05, recommended option, dependency, tradeoff, blast radius and BLOCKED/PENDING state.
H. `ACCEPTANCE_MATRIX`: B02-D01 through B02-D14 with `SOURCE_PASS`, `DRAFT`, `PENDING_OWNER`, `BLOCKED`, `NOT_RUN`, clearly labeled.
I. `SAFE_NEXT_ACTION`: no source write until owner reviews and explicitly approves selected D02 decisions and a distinct SHA-pinned coding work order.
J. `DIFF_ASSERTION`: run read-only git status/diff --name-only where safe; do not claim no unrelated user changes if any existed before inspection.

An ordinary 7/7 CI PASS from the former G03 merge is **not a Phase4B-02 runtime PASS**. If any canonical doc is inaccessible, name it and report uncertainty, rather than substituting generic best practices.

## END PROMPT FOR GEMINI

## E39 — mandatory reviewer override if prompt is reused (2026-10-11)

**Read this after the original prompt and BEFORE any future review; it is higher-priority than older descriptions of completeness.** The first Gemini report at local G03 `598440f...` was corrected under [E38](./phase4b-02-gemini-independent-design-review-e38-20261011.md). Its frozen public hostname and DB errors, OIDC EdDSA categorical ban and absolute no-file-write statement cannot be repeated. The current `main` source pin remains `617dadc...` until GitHub rechecked.

Read the new [E39 16-finding assurance register](./phase4b-02-e39-pre-ratification-assurance-risk-register-20261011.md) and [matrix E39 §7](./phase4b-02-internal-trust-nonproduction-negative-test-matrix-20261011.md) before any other recommendations. Investigate signed binding of the **actual** request method/path/query/body, unsigned/client-controlled request ID, cross-assertion substitution, redis silent/partial loss with no connection failure, shared quarantine across workers, JWT policy evidence, true end-to-end status/test outcome, and provider owner mapping. Make any proposed new JWS header `typ`/key role/Redis epoch implementation explicitly **unratified**. For `T02-047`, assert healthy concurrency **exactly one allowed, one denied**; component `ALLOW` does not mean whole HTTP accepted.

**Output only:** a clear read-only evidence and residual-risk report listing each E39 R01..R16 status and source-specific proof plus D02-01..05 technical/owner blockers. Do not claim absolute zero risk, do not update code/doc/CI, and do not mark 86 HTTP tests executed. Any download to IDE scratch must be disclosed as scratch I/O, not "zero files created anywhere". Worktree safety: never repair or reset old detached/dirty branches. Continue to STOP before coding until a separately explicitly authorized source work order and owner decision exist.
