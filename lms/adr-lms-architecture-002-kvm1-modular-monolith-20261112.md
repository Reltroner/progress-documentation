# ADR-LMS-ARCH-002 — KVM 1 Capacity-First Modular Monolith

> **Decision date:** 2026-11-12 (Asia/Jakarta)
> **Decision owner:** Reltroner project owner; architecture choice requested with discretion to select microservices or modular monolith.
> **Architectural recommendation:** **ADOPT A MODULAR MONOLITH as the target LMS backend architecture.**
> **Change-control status:** **PROPOSED / OWNER REVIEW REQUIRED BEFORE RATIFICATION AND IMPLEMENTATION.** This ADR is a nonproduction recommendation and a migration contract candidate. It does **not** silently amend frozen Phase 0C/1 source-of-truth contracts, does not authorize runtime changes, and is not evidence of a successful refactor.
> **Scope:** Reltroner LMS backend runtime on Hostinger KVM 1; preserve learner/admin client isolation, immutable content publishing, existing HRM and Keycloak availability, and all source-backed business/security contracts.
> **Evidence baseline:** progress-documentation `main@933e9e8e07f497cacacc0b370f996e1114fadb2b`; LMS-BE `main@617dadc0d0d627071d713ceb729df6658202b43e`, read on 2026-11-12. Current live VPS measurements on this decision date are **NOT AVAILABLE**.

## 1. Decision and precise interpretation

Move from **six independently bootstrapped Laravel applications** (Gateway, Learning, Mentorship, Knowledge, Assistant, Audit) to **one deployable Laravel 13 application** with five strongly bounded domain modules and an HTTP API ingress layer. One application does **not** mean one OS process: the target may have a bounded PHP-FPM worker pool and a bounded asynchronous queue worker, independently measured against host capacity.

Use a **modular monolith**, not an unstructured "gateway monolith": Gateway/HTTP has no business-state ownership; domain modules own rules and data through documented interfaces. Keep a versioned public `/api/v1` contract, server-side permissions, durable event intent, and explicit tests that prevent cross-module persistence coupling.

This is an **architecture target**. No production migration, deployment, database merge, Keycloak configuration change, Redis reset, PHP-FPM reload, DNS change, or frozen contract amendment occurs merely because this document exists.

## 2. Why the previous architecture has an unfavorable cost profile

The accepted 2026-10-10 Phase 4A observation describes the incumbent Hostinger VPS as **1 vCPU / 3.8 GiB RAM / 2 GiB swap / 48 GB root**, with approximately **1.2 GiB used RAM / 2.6 GiB available** and roughly **42 GB free disk** *at a historical snapshot*. Nginx, PHP 8.4-FPM, PostgreSQL 18, Redis 8, Keycloak, HRM queue and scheduler already coexist. The hPanel 7-day chart estimates were near 2% baseline CPU but are not peak-load or percentile data. A Keycloak-family Java process was observed around 664 MiB RSS; RSS is not equivalent to exclusive/cgroup memory.

The GitHub backend at the pinned SHA has six largely parallel Laravel skeletons with independent `composer.json`/lockfiles, `artisan` boots, tests and health routes. All six `services/*/routes/api.php` are `<?php` placeholders, **not** 26 implemented domain handlers. CI's six service jobs prove source tests only, not measured production traffic or real HTTP integration. Consequently, changing the structure *before* implementing the 26 operations is less costly than preserving distributed runtime overhead solely to conform to an earlier unmeasured architecture preference.

Independent services could eventually be useful for scaling, isolation and team ownership, but these benefits have not been demonstrated for the current single-core host. The capacity decision is about **measurable operational efficiency and simpler correctness**, not claiming sixfold memory savings or pretending that a monolith cures host-level single points of failure.

## 3. Deployment topology — target

```text
Learner browser             Admin browser
lms.reltroner.com           lms-admin.reltroner.com
Cloudflare Pages            Separate Cloudflare Pages
         |                        |
         +------------+-----------+
                      |
           Cloudflare -> lms-api.reltroner.com
                      |
             VPS Nginx / TLS
                      |
          ONE Laravel application
          ONE bounded LMS PHP-FPM pool
                      |
          API ingress (not domain owner)
                +-----+-----+--------+----------+--------+
                |           |        |          |        |
             Learning   Mentorship Knowledge Assistant Audit
                |           |        |          |        |
                +------ explicit in-process contracts --+
                      |
             PostgreSQL 18 (durable truth)
             Redis 8 (replaceable runtime state)
             Bounded queue/scheduler workers
                      |
             External LLM API (if enabled)

Separately preserved:
auth.reltroner.com -> existing Keycloak/HRM trust posture
Git-published Content Catalog -> canonical course contents
assets.reltroner.com -> Cloudflare/Premium Hosting immutable assets
```

No new Kubernetes, Docker, Kafka, message broker, Elasticsearch/Meilisearch or local LLM inference is required. No new paid VPS is authorized or required by this design.

## 4. Target repository and module boundaries

Target conceptual repository layout (not yet implemented):

```text
LMS-BE/
  app/
    Http/
      Controllers/Api/V1/
      Middleware/
      Requests/
      Resources/
    Modules/
      Learning/
        Application/ Domain/ Infrastructure/ Contracts/
      Mentorship/
        Application/ Domain/ Infrastructure/ Contracts/
      Knowledge/
        Application/ Domain/ Infrastructure/ Contracts/
      Assistant/
        Application/ Domain/ Infrastructure/ Contracts/
      Audit/
        Application/ Domain/ Infrastructure/ Contracts/
    Shared/
      Identity/ Authorization/ Events/ Observability/
  bootstrap/
  config/
  database/
    migrations/
  routes/
    api.php
  contracts/
    openapi/ authz/ identity/ persistence/ compatibility/ schemas/ tests/
  tests/
    Unit/ Feature/ Contract/ Architecture/ Security/ Performance/
  composer.json
  composer.lock
  artisan
```

Implementation may use a different exact folder shape if an IDE coding audit proves stronger Laravel integration; any deviation must preserve the following **enforceable dependencies**:

1. **Ingress-only HTTP layer**: route controllers handle authentication, validation, response translation, rate limiting and dispatch; no business rules or canonical domain tables live in Gateway.
2. **Domain ownership**: Learning owns enrollments/progress/bookmarks; Mentorship owns offerings/bookings/sessions; Knowledge owns authorized derived indexes; Assistant orchestrates external inference only; Audit owns durable append-only accountability.
3. **Cross-module integration**: depend on public application interfaces, commands/queries or versioned in-process events; do not import another module's Eloquent model or directly mutate another module's tables.
4. **Domain isolation tests**: static dependency rules, migration ownership, negative permission tests and forbidden import/write fixtures must fail CI when module boundaries are violated.
5. **Single release/Composer graph**: one locked Laravel dependency graph, one tested deployable artifact, one database migration release sequence with explicit backwards compatibility.
6. **Background tasks**: initially a small bounded queue worker under explicit limits; scheduled tasks guarded to prevent duplicate execution. Critical event intent is committed durably, not entrusted solely to Redis.
7. **No local content CRUD source takeover**: course/module/lesson/path content remains Git- and publication-manifest-owned.

**Single runtime is not a single security principal by magic.** In-process boundaries lose the protection of separate service credentials/processes. Authorization and architectural tests therefore become mandatory. Do not claim equivalent isolation to six separately deployed services.

## 5. Preserve stable external and business contracts

**No intentional public API change**: preserve the 26 frozen method+path operations, `/api/v1`, 19 capability identifiers, versioned Problem Details responses, request correlation, idempotency semantics, OIDC issuer/audience/client checks, and 9 named domain-event families. Use generated/fixture compatibility comparisons against the pinned `contracts/` baseline.

**Security**: Keycloak remains the only canonical credential/identity authority. Preserve separate `lms-user` and `lms-admin` OAuth/OIDC contexts and exact `aud=lms-api`, expected issuer, `azp`, lifetime, signature/JWKS validation, server-side resource ownership and capabilities; never use a frontend persona as privileged proof. HRM's existing realm/client behavior must not be changed by this refactor.

**Workload/delegation ADR**: ADR-LMS-TRUST-001 specifies Ed25519 dual assertions for *networked* internal service calls as a **ratified nonproduction design**. With in-process module dispatch, a signed Gateway-to-module workload hop is not present. A new ratified security disposition must mark *only that no-longer-existent internal network hop* as inapplicable; it must **not** remove Keycloak JWT validation, permission enforcement, anti-replay controls for any remaining network integration, key-handling duties where still applicable, or previously frozen negative tests without an explicit replacement. While any old HTTP internal-service endpoint survives transition, its original fail-closed Ed25519/replay obligations remain.

**State**: PostgreSQL remains durable authority; Redis remains replaceable. Booking uniqueness, progress idempotency, append-only audit, event outbox/inbox, retries, dead-letter handling, and external provider non-authority must survive. No LLM may write canonical tables directly. Keep public/static search distinct from permission-aware search.

## 6. Database strategy — explicitly staged, not an accidental merge

**Migration entry:** Do **not** create or delete production LMS databases merely to change the application folders. Preserve the previously specified four logical owners (Learning, Mentorship, Knowledge, Audit) and any actually provisioned owner databases until audited. The Phase 4A PostgreSQL catalog inspection was blocked by existing pg_hba policy; the creation state of four LMS databases was **not proven**. Never bypass HBA or infer they exist.

**Preferred eventual simplification, subject to an independently approved database-security amendment:** one physical PostgreSQL instance and one LMS database with domain-specific schemas (`learning`, `mentorship`, `knowledge`, `audit`), explicit grants, migration ownership and strict tested data-access boundaries. If a shared application credential has write privileges across schemas, **separate database-credential isolation no longer holds**: document that weakened property clearly and substitute reviewable policy, integration tests and database-level append-only/uniqueness constraints. A consolidated database is not an initial prerequisite for the modular monolith and must not be forced without benchmark and data/security sign-off.

**Migration sequencing:** keep the existing four-DB design temporarily if it minimizes risk and connection budgets permit, then benchmark separately whether consolidating schemas materially helps latency/connection count. Never execute multi-DB data moves without a verified backup, schema parity, integrity/count reconciliation, tested down-migration or forward-fix, and owner release approval.

## 7. Frozen-contract changes that require explicit supersession

The following are **PROPOSED REVISIONS**, not already ratified changes:

| Source | Original norm | Proposed disposition |
|---|---|---|
| Phase 0C architecture-style and placement sections 12–13 | Independent private microservice runtimes | Replace six deployables with one Laravel runtime; retain one public API ingress and no public internal endpoints |
| Phase 0C I-08 | Internal microservices are not publicly addressable | Preserve stronger outcome: no private module is independently routable from the Internet |
| Phase 0C I-10 / I-11 | Each service owns logical data; no cross-service writes | Retain domain ownership; revise enforcement for same-process modules, with database design under separate approval |
| Phase 1 §5 / §26 | Six runtime services; internal HTTP+JSON transport | Five modules + one ingress in one deployable; explicit in-process interfaces |
| Phase 1 §31 / P1-I15 | Four separate owned DBs and DB-level write credentials | Preserve initially; schema consolidation requires separate permission/security ADR |
| Phase 1 §40 | Reject Gateway owning all business logic | **Preserve the rejection**: ingress-only, domain-owned modular monolith is not a Gateway-owned big ball of mud |
| ADR-LMS-TRUST-001 | Signed workload/delegation for private network hops | Retain while those hops exist; propose retirement **only** for removed same-process hops after a reviewed security proof |

All other Phase 0C I-01..I-20 and Phase 1 P1-I01..P1-I24 requirements must be crosswalked before adopting a replacement normative version. No historical freeze/evidence files are rewritten or deleted. On approval, publish an explicit versioned contract supersession and update the canonical README/ledger with the decision's effective date and precise affected provisions.

## 8. Implementation plan — smallest reversible packages

| Stage | Scope | Evidence required | Mutation permission |
|---|---|---|---|
| A — Decision and baseline | Review this ADR; freeze BE/FE/docs SHAs; obtain safe incumbent HRM/Keycloak/PG/Redis resource metrics | Signed-off architectural decision and no unexplained baseline gaps | Docs PR only |
| B — New Laravel shell | Introduce a **single** Laravel application and module namespace in a separate BE feature branch; preserve historical six-app source until parity | PHP syntax/static architecture tests; one Composer lock; health/error/request ID regressions | Source only, separate owner-approved PR |
| C — API/domain parity | Route all 26 operations into modules with real OIDC validation, authorization, handlers, persistence and negative tests | Exact OpenAPI/golden diff, 19 capabilities, cross-client 401/403, idempotency, persistence/races | Source + isolated test DB only |
| D — Data/events/trust parity | Owner-scoped persistence, durable audit/outbox, queue, external LLM orchestration; retire only obsolete internal hop trust | Nonprod PostgreSQL/Redis positive+negative, recovery, replay, Keycloak/HRM nonregression | No production mutation |
| E — Capacity comparison | Measure prior architecture candidate vs modular candidate under reproducible identical load; measure incumbent contention | p50/p95/p99, throughput, PHP-FPM process/PSS/RSS, CPU, RAM, swap, queue lag, PG connections, errors and HRM/Keycloak latency | Controlled nonproduction load only |
| F — Production cutover | Backup+restore proof, resource-approved Nginx/PHP-FPM/systemd rollout, independent release controls, minimal exposure | Exact image/commit SHA, smoke+negative tests, 24h observation plan, rollback decision | Separate written owner authorization |
| G — Retire legacy | Remove obsolete services/CI/multiple lockfiles only after verified new runtime and rollback window | No traffic to old internals, stable API/DB/audit, safe repository history retained | Separate cleanup PR |

**Stage ordering cannot substitute for acceptance**. The refactor must not artificially mark unresolved Phase 4A G01–G13 and Phase 4B trust/DB/Redis/identity gaps as closed. In particular, static contract fixtures and six-service skeleton CI are not production API proof.

## 9. Resource management and benchmark gates

Before setting fixed limits, obtain refreshed VPS idle/peak measurements and a bounded workload model that includes HRM traffic, Keycloak authentication, PostgreSQL maintenance/backups, Redis, Nginx and cron. Report memory with proportional/cgroup interpretation where available, not a naive sum of RSS. Sample service CPU and memory, swap-in/out, OOM events, FPM active/idle workers/queue, DB active connections, disk space, API error rate, and p95 under expected traffic; differentiate measurements from plans.

Prefer a **single dedicated LMS PHP-FPM pool** with measured `pm` policy and child cap, a capped queue worker, OPcache and a shared codebase/lockfile. Worker count, PHP `memory_limit`, `pm.max_children`, and Keycloak JVM sizing are **TBD by test**; never blindly copy example values into live configs. Protect headroom for both normal peaks and operational bursts. Do not consume all currently "available" RAM, and do not treat swap as production RAM.

Candidate promotion conditions (thresholds to be approved against measured baseline): no host OOM or sustained swapping; no material HRM/Keycloak latency regression; no unbounded FPM/queue/DB concurrency; acceptable API latency/error SLO under target traffic; a reproducible cost/operational simplification over the six-service baseline. If capacity cannot be proven on one vCPU, reduce concurrency, defer optional workloads, keep inference external, and/or revisit host sizing with an explicit cost decision. **Do not invent percentage savings or capacity certification.**

## 10. Rollback and safety

The current GitHub backend skeleton is not proof that six services are live. Preserve old source and contract fixtures for comparison; use code-level git revert/forward-fix if a nonproduction branch fails. Do not use `git reset --hard`, `git clean -fd`, forced Git history rewrites, or data-destructive migrations as convenience operations.

For production, record exact prior release and new release SHAs, a tested database-compatible return path, process/port ownership, backup object integrity and isolated restoration evidence before cutover. New schema or data changes that prevent rollback must be staged backward-compatibly or require an approved forward-only recovery plan. Cutover must preserve existing HRM, Keycloak, DNS, and Cloudflare environments. On failed auth, missed audit, replay bypass, domain-policy denial or incumbent regression: **STOP / ROLLBACK**, never fail open.

## 11. Acceptance checklist and open decisions

- [ ] Owner approves **architecture supersession** and exact affected Phase 0C/1 invariants.
- [ ] A distinct decision covers any database credential/schema isolation change.
- [ ] ADR-LMS-TRUST-001 receives scoped in-process security disposition, without weakening any still-networked hop.
- [ ] One Laravel codebase has mechanical module isolation tests and real business API handlers.
- [ ] 26 API method+paths, 19 capabilities, 9 event families and all frozen invariant rows have a published before/after trace.
- [ ] External OIDC issuer/aud/azp/signature and learner/admin cross-context denial tested.
- [ ] PostgreSQL booking/audit/outbox correctness, Redis loss/recovery, migration and restore verified in isolation.
- [ ] HRM/Keycloak nonregression and live VPS capacity proven at intended concurrency.
- [ ] Final PR/CI + immutable SHAs + separate production release/rollback approval recorded.

**Current disposition:** `ARCHITECTURE_RECOMMENDATION=MODULAR_MONOLITH`; `TARGET_IMPLEMENTATION=NOT_STARTED`; `SOURCE_MAIN_UNCHANGED`; `VPS_MUTATION=NONE`; `FROZEN_PARENT_CONTRACTS=STILL_BINDING_UNTIL_APPROVED_SUPERSESSION`.

## 12. Evidence and related records

- [Canonical LMS source navigation](./README.md)
- [Phase 0C Master Infrastructure Placement Contract](./master-infrastructure-placement-contract.md)
- [Phase 1 Logical Service Boundary & API Contract](./logical-service-boundary-api-contract.md)
- [Phase 4A-00 historical VPS runtime resource and gap evidence](./phase4a-00-read-only-runtime-infrastructure-discovery-work-order-20261010.md)
- [ADR-LMS-TRUST-001 (ratified nonproduction design)](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md)
- [End-to-End Engineering Ledger](./engineering-end-to-end-progress-ledger.md)
- [LMS-BE six-service source tree at pinned commit](https://github.com/Reltroner/LMS-BE/tree/617dadc0d0d627071d713ceb729df6658202b43e/services)
- [LMS-BE existing six-service CI matrix](https://github.com/Reltroner/LMS-BE/blob/617dadc0d0d627071d713ceb729df6658202b43e/.github/workflows/phase3b-contract-ci.yml)

This ADR does not modify the separate LMS-FE static build or claim any new Keycloak, VPS, Cloudflare, database or Redis production state.
