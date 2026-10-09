# Reltroner LMS — Phase 3A-04 FZ-04 Subordinate ADR Closure Receipt

> **Owner action:** `menutup FZ-04` (2026-10-09, Asia/Jakarta; exact clock time not stated).  
> **Authority:** Owner-approved architectural design baselines, with explicitly bounded deferred technical fields.  
> **Result:** `FZ-04 = PASS (DESIGN ONLY)`. **Phase 3A overall NOT FROZEN; Phase 3B NOT AUTHORIZED; production mutation NOT AUTHORIZED.**  
> **Read order:** Phase 0C and Phase 1 FROZEN contracts → 3A-04 direction acceptance (12 ADR-03F) → this receipt → original subordinate ADR candidates → future tested implementation evidence.

## 1. Decision basis and source provenance

The project owner first accepted all 12 `ADR-03F-01..12` recommendations, then explicitly requested `menutup FZ-04`. This authorizes recording a **bounded architecture-level disposition** for the subordinate ADR recommendations covered by FZ-04. This record never invents owner approval of unspecified cryptography/TTL/retention values or production actions.

| Source (main at review) | Evidence baseline |
|---|---|
| Documentation main | `6677ddcb48bc98f17f18a95e3a3c8de68bb3f7e6` |
| FROZEN physical / logical | blobs `b899761c9e833f9fa567055801b9ba0834ed56eb` / `cf089b8df4b5ccb1761b504ffae662a0053bf03e` |
| Identity standalone review | blob `607886947abcb721d09440c98b9a3084bdc0fc20` |
| Persistence standalone review | blob `ccd02cc3193e9df4396a53db8f6aa0099fb87a9b` |
| Catalog design candidate | blob `37dd58c64fddce8d9c49081f5510bbddfbacb491` |
| Earlier 12/12 ratification | PR #2 merged; `lms/reltroner-lms-phase3a-04-ratification-register-20261009.json` |

**Precedence:** The original review-candidate docs are archival sources as of their timestamps. Their old `NOT HUMAN-RATIFIED` labels describe **historical state** and are superseded *only for the selected accepted architectural baseline* by this dated owner-decision receipt. Their listed unresolved technical parameters remain open. The two frozen parent contracts are not amended.

## 2. Disposition of all 18 subordinate design ADRs

| ADR | Binding design disposition | Accepted bounded baseline | Explicitly unresolved (not ratified) | First hard implementation gate |
|---|---|---|---|---|
| `ADR-LMS-KC-001` | ACCEPT DESIGN BASELINE | Dedicated lms-user and lms-admin public OIDC Code+PKCE S256; lms-api resource-client role namespace, dedicated audience mapper, scoped roles and backend fail-closed checks. Preserve HRM clients and scopes unchanged. | Installed Keycloak runtime/feature checks; exact lms-api client flags, redirect/logout/secret policies; Client Scopes Evaluate effective JWT claims; FE deployment env; JWKS freshness; internal service auth and admin adapter independent ADRs. | **3B identity configuration specification before Phase 4 provisioning; Phase 4 effective-token and HRM regression checks; internal trust and role-admin ADR before their endpoints.** |
| `PD-ADR-01` | ACCEPT DESIGN BASELINE | Four service-owned logical DBs (Learning, Mentorship, Knowledge, Audit) on existing PostgreSQL instance; Gateway/Assistant have no canonical business database by default. | Exact database identifiers, roles, schema naming, DDL, migrations, grants, backup/restore. | **3B schema/grant fixtures; Phase 4 owner-DB provisioning and negative cross-write tests.** |
| `PD-ADR-02` | ACCEPT MINIMAL BASELINE WITH POLICY GATE | Learning owns enrollment and progress, initially one enrollment per principal/course with pinned curriculum revision; prior earned completion is not silently revoked. | Retake policy, archive continuation, reset/completion rubric, concurrency and unknown ID response specifics. | **3B versioned API DTO/decision matrix; Phase 5 before Learning stateful endpoints.** |
| `PD-ADR-03` | ACCEPT MINIMAL BASELINE WITH POLICY GATE | Initially capacity-one, 1:1 slot-based mentorship; PostgreSQL transactional occupancy uniqueness, never only count-before-insert. | Final booking states/occupied status, time-zone rules, cancellation/reschedule and capacity variations. | **3B policy+DDL test fixtures; Phase 7 concurrent booking and lifecycle tests.** |
| `PD-ADR-04` | ACCEPT DESIGN BASELINE | Mentorship-owned durable idempotency request record; scoped request-hash/key and response replay; same-key different payload conflicts; separate occupancy invariant. | TTL/retention, status/error shape and maximum key payload, replay policy. | **3B OpenAPI idempotency DTO; Phase 7 deterministic duplicate/concurrency/failure tests.** |
| `PD-ADR-05` | ACCEPT DESIGN BASELINE | Atomic local business-state/outbox intent; Redis at-least-once transport; consumer local inbox deduplication, leases and recoverable retry; no global exactly-once claim. | Event envelope schemas/versions, transport topology/ACL, key rotation/auth, ordering, DLQ/quarantine/retention, retry budgets. | **3B event schemas and negative fixtures; Phase 4+ broker/workers and end-to-end replay drills before event-dependent features.** |
| `PD-ADR-06` | ACCEPT DESIGN BASELINE | Knowledge-owned derived index staging, validated immutable release and atomic promotion; keep previous usable index on failure. | Exact manifest digest, ACL/version labels, source producer identity, promotion pointer, index rollback details. | **3B Knowledge ingest contract; Phase 8 authorized reindex/failure tests.** |
| `PD-ADR-07` | ACCEPT DESIGN BASELINE | Append-only audit facts and separately durable mutable administrative-operation workflow state; Audit database remains authority for audit history. | DB privileges, retention/legal policy, tamper guarantees, auditor ACL and failure handling. | **3B append-only DDL/privilege specification; Phase 6 immutable audit and outage tests.** |
| `PD-ADR-08` | ACCEPT DESIGN BASELINE | Role-admin operations require durable Audit intent then least-privilege Keycloak adapter, verified outcomes and reconciliation of ambiguous results; no distributed atomicity claim. | Operation state machine and authorization, external action idempotency, reconciliation timing, privilege/scoping and access policy. | **3B admin-operations ADR and contracts; Phase 6 negative/uncertain-result tests BEFORE role PATCH enabled.** |
| `PD-ADR-09` | ACCEPT OBLIGATION DEFER MEASURABLE PARAMETERS | Backup/restore, retention, availability, runtime/concurrency and spend governance are mandatory for release; use measurement from existing shared VPS. | Exact RPO/RTO, retention days, worker concurrency, CPU/RAM caps and monetary thresholds are NOT defined without baseline measurement. | **Phase 4 design resource preflight; Phase 11 measured operational SLO, restore, HRM nonregression before production release.** |
| `ADR-LMS-CATALOG-001` | ACCEPT DESIGN BASELINE | Source-controlled Git LMS catalog is canonical; immutable manifest produced from pinned inputs; no runtime canonical course CRUD/database. | Compiler implementation and release signing/provenance. | **3B manifest compiler/schema CI; Phase 5 Learning integration.** |
| `ADR-LMS-CATALOG-002` | ACCEPT DESIGN BASELINE | Permanent lesson ID in checked-in frontmatter (or reviewed one-time equivalent), stable cross-release aliases/tombstones and collision/integrity checks; preserve existing stable IDs. | One-time mapping across all 31 existing lessons, historic routes and migration compatibility; no proof all existing users have no progress. | **3B audited ID registry + route/search parity tests; Phase 5 pre-progress migration acceptance.** |
| `ADR-LMS-CATALOG-003` | ACCEPT DESIGN BASELINE | Deterministic SHA-256 canonical manifest version with JCS-style canonical input, separate course revision and public/internal-preview artifact channels. | Exact canonicalization inclusion, semantic revision threshold, artifact signature, retention/rollback limits. | **3B versioned schema, deterministic dual-build test; Phase 5 release publication/rollback checks.** |
| `ADR-LMS-CATALOG-004` | ACCEPT DESIGN BASELINE | Enrollments pin approved course/curriculum revision; historical learning progress and earned completions never retroactively removed on unrelated course release. | Course completion rubric, learner opt-in upgrade policy, archived visibility and API compatibility window. | **3B DTO/history contract; Phase 5 backcompat/concurrency tests.** |
| `ADR-LMS-CATALOG-005` | ACCEPT DESIGN BASELINE | Studio remains canonical editor/publisher; LMS holds references with source-attested edition, canon status and distribution/LLM-use rights only; no automatic canon promotion. | Studio authorized release registry, per-source canon proofs, license/access attributes. | **3B metadata schema contract; before Phase 8 ingestion and public/AI citation.** |
| `ADR-LMS-CATALOG-006` | ACCEPT DESIGN BASELINE | Public static export and private Knowledge ingestion are independently permission-filtered; index release pinned; deny unattested/draft/unauthorized excerpts. | Source-attested ACL policy schema, public FE build negative suite, reindex exact integration. | **3B privacy/manifest CI; Phase 8 permission/search leakage tests; FE release checks in Phase 10.** |
| `ADR-LMS-CATALOG-007` | DEFER FEATURE INITIAL V1 ACCEPT CHANGE CONTROL | Creator-generated submissions, stored journal/project bible, grading and mentor review are out of initial v1 scope; may not be implemented as incidental lesson output. | Any future storage/file sharing/grading/reviewer workflows require new data ownership, API, capabilities, privacy, audit and retention ADR. | **Only reconsider after explicit new product approval + frozen-contract change control, before coding feature.** |
| `ADR-LMS-CATALOG-008` | ACCEPT DESIGN BASELINE | Studio-owned season/episode/chapter hierarchy and Current Lore/Backstory/Wiki modes remain Studio-domain references; LMS does not replicate authoritative canon graph. | Exact attested reference relationship metadata and publication proof. | **3B optional source reference schema; Phase 8 indexing only with Studio release authority.** |

### Decision interpretation

- `ACCEPT_DESIGN_BASELINE`: design direction selected; versioned implementation contract, negative tests and operational validation still required.
- `ACCEPT_MINIMAL_BASELINE_WITH_POLICY_GATE`: minimal design selected, but product lifecycle policy MUST be specified before the affected API ships.
- `ACCEPT_OBLIGATION_DEFER_MEASURABLE_PARAMETERS`: duty to measure and restore accepted; no arbitrary RPO/RTO, throughput, TTL or cost thresholds fabricated.
- `DEFER_FEATURE_INITIAL_V1_ACCEPT_CHANGE_CONTROL`: feature intentionally excluded from v1; cannot be silently implemented; approval of the exclusion is not approval of future expansion.

**Total:** Identity 1 + Persistence 9 + Catalog 8 = **18 recorded dispositions** (16 baseline ACCEPT, 1 operational duty ACCEPT with deferred numeric settings, 1 feature scope DEFER). This counting describes record classifications, **not 18 implemented features or 18 passing tests**.

## 3. Residual binding design constraints

1. **Identity:** `lms-user` and `lms-admin` remain independent browser public clients; `lms-api` holds 19 capability roles; PKCE S256 + dedicated audience/scope isolation + claims validation. No change to existing HRM scopes or Keycloak built-ins. Installed version, mapper Evaluate, admin adapter and internal trust remain distinct future gates.
2. **Persistence:** Learning/Mentorship/Knowledge/Audit have four logical owner DBs; no cross-DB writes or global transaction. Booking occupancy and request idempotency are separate guarantees. Domain mutation commits event intent with business row; delivery is at-least-once with durable inbox. Audit’s Keycloak outcome requires reconciliation.
3. **Catalog:** Git is the canonical course authority; stable lesson IDs and tombstones; reproducible manifest hash and course revisions; protected historical progress; source-attested Studio rights and edition; no preview/canon/public data leaks. Creator submission/review feature deferred from v1.
4. **Operations:** existing Hostinger VPS resource budget remains a measured release gate; no default infrastructure purchase, Kafka, Kubernetes, Meilisearch or local LLM requirement.

## 4. Non-negotiable future implementation gates

| Phase | Must specify/test before executing related work |
|---|---|
| **3B** | OpenAPI operation/capability matrix, identity/audience/client config fixtures, private workload+delegation policy fixtures, 9 versioned event payloads, outbox/inbox negative tests, four DB schema/grants, manifest/lesson ID migration plan, public FE output privacy guard, publisher and release-to-Knowledge authentication contract |
| **4** | Explicit production change authorization; Keycloak installed-version/config validation, dedicated client provisioning, effective token claims, JWKS/rotation, private service authentication, DB rights and capacity baseline; HRM non-regression |
| **5** | Historical learner completion/rubric/retake rules, approved course revision manifest, user state and asset rollback tests |
| **6** | Admin role operation Audit intent, Keycloak outcome reconciliation/authorization, append-only/retention negative tests |
| **7** | Mentorship slot-state/timezone/cancellation rules, DB contention and durable idempotency replay tests |
| **8** | Authenticated source-attested Knowledge indexing, ACL and private snippet leak negatives, safe atomic release promotion |
| **10** | Public static build routes/search/sitemap/meta/asset checks; frontend OIDC client cutover/provenance |
| **11–12** | Measured worker/CPU/RAM/cost SLO, restore RPO/RTO, HRM coexistence and final 16-product-DoD certification |

## 5. Freeze gate update

| Gate | State after owner FZ-04 instruction |
|---|---|
| `FZ-03` | PASS — owner accepted all 12 ADR-03F directions (prior PR #2) |
| **`FZ-04`** | **PASS — all 18 subordinate candidates dispositioned with explicit hard gates** |
| `FZ-05` | PASS — v1 creator submissions/reviews and financial scope deferred |
| `FZ-06 / FZ-07` | PASS design directions; future runtime tests pending |
| `FZ-09` | PASS — standalone docs and historical ledger split merged by PR #1 |
| `FZ-02` | Traceable, final owner freeze evidence pending |
| `FZ-10` | OPEN — exact 3B work order/authorization not approved by FZ-04 request |
| `FZ-11` | OPEN — separate signed final Phase 3A design freeze decision not requested |

**Final verdict:** `3A-04 FZ-04 CLOSED — DESIGN DISPOSITION PASS → PHASE 3A FINAL FREEZE HOLD → PHASE 3B NOT AUTHORIZED`.

## 6. AI handoff and audit controls

- Never promote review-candidate source headings into production acceptance; use latest dated receipt plus binding parent documents.
- A `PASS` in this record is a **decision closure**, not runtime CI, infrastructure or security certification.
- Preserve historical combined docs and source branch SHAs; do not revise frozen invariants through this addendum.
- Any future decision to INCLUDE creator files, payments, Studio CMS or guest AI requires product/contract change control before implementation.
- This document creates neither a GitHub merge nor an infrastructure authorization by itself.

## 7. Pinned links

- [Identity candidate](./adr-lms-kc-001-identity-provisioning-review-candidate.md)
- [Persistence candidate](./reltroner-lms-phase3a-03d-persistence-event-model-20261009.md)
- [Catalog candidate](./reltroner-lms-phase3a-03e-catalog-manifest-versioning-20261009.md)
- [3A-04 Ratification Board](./reltroner-lms-phase3a-04-ratification-freeze-readiness-20261009.md)
- [Machine receipt](./reltroner-lms-phase3a-04-fz04-subordinate-adr-dispositions-20261009.json)
