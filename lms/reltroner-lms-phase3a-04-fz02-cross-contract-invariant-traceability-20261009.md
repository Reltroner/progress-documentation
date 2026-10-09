# Reltroner LMS — Phase 3A-04 FZ-02 Final Cross-Contract Invariant Traceability Acceptance

> **Date:** 2026-10-09, Asia/Jakarta. Exact clock time not attested.  
> **Project-owner action:** `tutup FZ-02 — Final Cross-Contract Invariant Traceability Acceptance`.  
> **Gate result:** **FZ-02 PASS — 44/44 NORMATIVE INVARIANTS TRACEABLE / DESIGN ACCEPTED**.  
> **Important:** **0/44 newly runtime-certified by this review; no Phase 3A final freeze; Phase 3B and production NOT AUTHORIZED**.

## 0. Scope, authority and boundaries

Use the **exact normative wording** of 20 I-xx (Phase 0C) and 24 P1-Ixx (Phase 1) at SHA-pinned Git blobs. Every row maps accepted 03F/subordinate ADR decisions, relevant 03F cross-contract findings, proposed global DoD and *future* evidence. **This acceptance does not verify code, production deployment, token issuance, tests or third-party security.**

Source pins: [Physical contract](./master-infrastructure-placement-contract.md) blob `b899761c9e833f9fa567055801b9ba0834ed56eb`; [Logical contract](./logical-service-boundary-api-contract.md) blob `cf089b8df4b5ccb1761b504ffae662a0053bf03e`; documentation-main baseline `78fb7db76b7a5b423825d687f0adc58ed88101ee`; [12 accepted parent ADRs](./reltroner-lms-phase3a-04-ratification-register-20261009.json); [18 bounded subordinate ADR dispositions](./reltroner-lms-phase3a-04-fz04-subordinate-adr-dispositions-20261009.json).

**Source precedence:** Frozen I/P1 invariant wording outranks this matrix. Documentation classification is **DESIGN TRACEABILITY**, not implementation verification. New normative deviations require a versioned parent-contract revision/ADR and explicit approval; no implicit alteration.

## 1. Outcome summary

| Criterion | Result |
|---|---|
| Physical invariant IDs present and normatively pinned | **20/20** |
| Logical invariant IDs present and normatively pinned | **24/24** |
| Duplicated or unmapped invariant IDs | **0** |
| Mapping to owner-ratified parent/subordinate ADR | **44/44** |
| Mapping to proposed product DoD | **44/44** |
| Future test/verification requirement per ID | **44/44** |
| Real runtime acceptance verified by FZ-02 | **0/44 (not executed)** |
| Frozen invariant changes made during review | **0** |
| Gate acceptance | **FZ-02 CLOSED — design-level owner acceptance** |

## 2. Physical infrastructure: I-01 through I-20

| ID | Frozen title | Exact authoritative requirement | Accepted ADR trace | Proposed DoD | 03F finding | Planned verification | First hard gate | Evidence status |
|---|---|---|---|---|---|---|---|---|
| `I-01` | Learner hostname | lms.reltroner.com = learner/user frontend | `ADR-03F-01` | DOD-11 | — | Learner hostname resolves and Cloudflare Pages static journey smoke tests | 3B schema; Phase 10 FE release | DESIGN TRACE / TEST PENDING |
| `I-02` | Admin hostname | lms-admin.reltroner.com = admin frontend | `ADR-03F-01`, `ADR-LMS-KC-001` | DOD-11 | — | Admin hostname isolated from learner and origin-level auth tests | 3B spec; Phase 10 FE rollout | DESIGN TRACE / TEST PENDING |
| `I-03` | Public backend hostname | lms-api.reltroner.com = only public LMS backend/API entry point | `ADR-03F-08` | DOD-12, DOD-04 | CC-08 | Only lms-api public API ingress; no private service exposed via DNS/ports | 3B trust; Phase 4 port scan | DESIGN TRACE / TEST PENDING |
| `I-04` | Identity authority | auth.reltroner.com = canonical Reltroner OIDC/Keycloak authority | `ADR-LMS-KC-001` | DOD-03 | CC-07, CC-18 | Live OIDC issuer/JWKS and audience negative claims verification | 3B config fixtures; Phase 4 runtime | SOURCE_CLIENT_DRIFT_AND_CLIENT_ABSENCE_REMAIN |
| `I-05` | Separate OIDC trust contexts | Learner and admin use separate OIDC client identities. | `ADR-LMS-KC-001` | DOD-03, DOD-11 | CC-07, CC-18 | Two public OIDC clients code+PKCE exact origin/redirect and cross-client denial | 3B/4 + FE Phase 10 | LMS_CLIENTS_NOT_PROVISIONED |
| `I-06` | Frontend authorization is non-authoritative | UI state never grants privilege. | `ADR-LMS-KC-001` | DOD-03 | CC-18 | Missing or spoofed frontend roles cannot grant backend capability | 3B API matrix; Phase 4 auth tests | FE_ROLE_FALLBACK_UX_ONLY_MUST_NOT_BECOME_AUTH |
| `I-07` | Server-side admin enforcement | All admin privilege is enforced server-side. | `ADR-LMS-KC-001`, `PD-ADR-08` | DOD-03, DOD-08 | CC-12 | Admin routes require admin-client context, required capability and audited adapter | 3B tests; Phase 6 admin API | DESIGN TRACE / TEST PENDING |
| `I-08` | Internal service privacy | Internal microservices are not publicly addressable. | `ADR-03F-08` | DOD-02, DOD-12 | CC-08 | Deny direct public access to all five non-Gateway service ingress paths | 3B trust; Phase 4 | DESIGN TRACE / TEST PENDING |
| `I-09` | Durable truth | PostgreSQL is the durable LMS business-state authority. | `PD-ADR-01` | DOD-02, DOD-06, DOD-07, DOD-08 | — | Durable writes in owned PG databases survive Redis loss and restart | 3B DDL; Phase 4+ | DESIGN TRACE / TEST PENDING |
| `I-10` | Logical ownership | Each domain service owns its own logical data. | `PD-ADR-01` | DOD-01, DOD-02 | — | Domain database roles restrict access to own schema/database | 3B grants; Phase 4 | DESIGN TRACE / TEST PENDING |
| `I-11` | No cross-service direct writes | No service may directly write another service's database. | `PD-ADR-01` | DOD-02 | — | Cross-service write credential negative suite | 3B grant spec; Phase 4 | DESIGN TRACE / TEST PENDING |
| `I-12` | Redis is ephemeral | Redis contains no irreplaceable business truth. | `PD-ADR-05` | DOD-14 | CC-13 | Redis flushed/unavailable does not lose committed domain or critical event intent | 3B fixtures; Phase 4/11 | DESIGN TRACE / TEST PENDING |
| `I-13` | Premium Hosting role | Premium Web Hosting is the LMS public asset origin, not the application core. | `ADR-03F-12` | DOD-11, DOD-12 | — | Static assets served from Premium Hosting, not running app core | Phase 10/11 live delivery proof | DESIGN TRACE / TEST PENDING |
| `I-14` | Frontend delivery | Cloudflare Pages is the target delivery platform for learner and admin LMS frontends. | `ADR-03F-12` | DOD-11 | — | Learner/admin Cloudflare Pages independent build and deploy | Phase 10 | DESIGN TRACE / TEST PENDING |
| `I-15` | No KVM1 LLM inference | The current VPS must not run local LLM inference. | `ADR-03F-12` | DOD-10, DOD-15 | CC-21 | VPS process inventory excludes local LLM; provider budget/authorization | Phase 9/11 | VPS_CAPACITY_MEASUREMENT_OPEN |
| `I-16` | Cloudflare is not truth | Cloudflare edge/cache is not a canonical business-state store. | `ADR-LMS-CATALOG-001`, `PD-ADR-05` | DOD-05, DOD-14 | — | Purge caches and rebuild without losing canonical catalog or learner DB state | 3B artifact contract; Phase 5/11 | DESIGN TRACE / TEST PENDING |
| `I-17` | Minimal VPS public ingress | Only explicitly required public ingress is exposed; internal data/services remain private. | `ADR-03F-08` | DOD-12 | CC-08 | Public ingress TLS/UFW probe allows only approved listeners | Phase 4/11 | DESIGN TRACE / TEST PENDING |
| `I-18` | Immutable asset strategy | Public LMS asset releases are versioned/immutable wherever practical. | `ADR-LMS-CATALOG-003` | DOD-05, DOD-11 | CC-19 | Pinned jsDelivr/public artifacts retain immutability, alias rollback | 3B hash spec; Phase 5/10 | DESIGN TRACE / TEST PENDING |
| `I-19` | Versioned API contract | Public backend APIs are versioned. | `ADR-03F-11` | DOD-04 | CC-09, CC-10 | OpenAPI route inventory enforces /api/v1 versioned API | Phase 3B | DESIGN TRACE / TEST PENDING |
| `I-20` | Complexity must be justified | New infrastructure is introduced only after a measurable or contractual requirement exists. | `ADR-03F-12` | DOD-01, DOD-15 | CC-21 | Resource-cost ADR and measured load justify any added infra | 3B review; Phase 11 | MEASURABLE_OPERATIONAL_BUDGET_OPEN |

## 3. Logical/API: P1-I01 through P1-I24

| ID | Frozen title | Exact authoritative requirement | Accepted ADR trace | Proposed DoD | 03F finding | Planned verification | First hard gate | Evidence status |
|---|---|---|---|---|---|---|---|---|
| `P1-I01` | Gateway is ingress, not domain owner | The Gateway owns public API ingress behavior and no default business database. | `ADR-03F-01`, `PD-ADR-01` | DOD-02, DOD-04 | — | Gateway routes and authorization only, no domain persistence database | 3B contract; Phase 4 | DESIGN TRACE / TEST PENDING |
| `P1-I02` | Static Content Catalog remains canonical initially | Course/module/lesson/path/resource content remains source-controlled for the initial architecture. | `ADR-LMS-CATALOG-001` | DOD-05 | CC-02 | Pinned Git compiled immutable catalog; no runtime canonical content DB | 3B/5 | CANONICAL_MANIFEST_NOT_IMPLEMENTED |
| `P1-I03` | Learning Service owns learner state | Enrollment, progress, completion, and bookmarks belong to Learning Service. | `PD-ADR-02`, `ADR-LMS-CATALOG-004` | DOD-06 | CC-03 | Learning-only durable enrollment/progress/completion/bookmark tests against catalog revision | 3B schema; Phase 5 | DESIGN TRACE / TEST PENDING |
| `P1-I04` | Mentorship Service owns mentorship state | Offering, availability, booking, and session lifecycle belong to Mentorship Service. | `PD-ADR-03`, `PD-ADR-04` | DOD-07 | CC-11 | Mentorship DB booking/slot uniqueness, idempotency, availability/session tests | 3B DTO; Phase 7 | DESIGN TRACE / TEST PENDING |
| `P1-I05` | Knowledge Service owns derived searchable state | Knowledge indexes are rebuildable and non-canonical. | `PD-ADR-06`, `ADR-LMS-CATALOG-006` | DOD-09 | CC-05, CC-06 | Derived indexes rebuild, staged publish and ACL enforcement tests | 3B protocol; Phase 8 | DESIGN TRACE / TEST PENDING |
| `P1-I06` | Assistant is orchestration only | Assistant Service never becomes canonical business state authority. | `ADR-03F-08` | DOD-10 | CC-05, CC-08 | Assistant tool cannot become owner of domain writes or source canon; permission tests | 3B trust; Phase 9 | DESIGN TRACE / TEST PENDING |
| `P1-I07` | Audit is durable and append-only | Privileged LMS actions requiring accountability are persisted by Audit Service. | `PD-ADR-07`, `PD-ADR-08` | DOD-08 | CC-12 | Append-only Audit + admin operation intent and recovery | 3B schema; Phase 6 | DESIGN TRACE / TEST PENDING |
| `P1-I08` | Keycloak remains identity authority | The LMS does not create a competing credential/identity store. | `ADR-LMS-KC-001` | DOD-03 | CC-07 | OIDC subject bound to Keycloak; no independent LMS passwords/users | Phase 4 | DESIGN TRACE / TEST PENDING |
| `P1-I09` | Separate browser clients | `lms-user` and `lms-admin` are separate OIDC public-client trust contexts. | `ADR-LMS-KC-001` | DOD-03, DOD-11 | CC-07, CC-18 | Separate lms-user/lms-admin login context, admin origin checks | Phase 4/10 | LMS_CLIENTS_NOT_PROVISIONED |
| `P1-I10` | LMS API is the protected resource | Backend tokens target the `lms-api` audience. | `ADR-LMS-KC-001` | DOD-03 | CC-07 | Wrong audience accepted? Must reject; valid access token targets lms-api | Phase 4 | DESIGN TRACE / TEST PENDING |
| `P1-I11` | Capability-based authorization | Backend operations authorize capabilities, not merely frontend persona labels. | `ADR-LMS-KC-001`, `ADR-03F-11` | DOD-03, DOD-08 | CC-10 | Per-route authorized capability + principal ownership; no persona bypass | 3B OpenAPI; Phase 4/6 | DESIGN TRACE / TEST PENDING |
| `P1-I12` | No backend fallback-to-student authorization | Missing capability claims fail closed. | `ADR-LMS-KC-001` | DOD-03 | CC-18 | Missing claim results 401/403 fail-closed, no student default | 3B matrix; Phase 4 | DESIGN TRACE / TEST PENDING |
| `P1-I13` | One public API version namespace | Initial business API surface uses `/api/v1`. | `ADR-03F-11` | DOD-04 | CC-09 | All 26 frozen endpoints covered by versioned /api/v1 schema; no invented routes | Phase 3B | DESIGN TRACE / TEST PENDING |
| `P1-I14` | No direct public microservice exposure | Clients call only `lms-api.reltroner.com`. | `ADR-03F-08` | DOD-02, DOD-12 | CC-08 | Network/service caller negatives prevent direct browser access to domain apps | Phase 4 | DESIGN TRACE / TEST PENDING |
| `P1-I15` | No cross-service database writes | Service ownership is enforced at database-credential level. | `PD-ADR-01` | DOD-02 | — | Scoped DB user privilege denies cross-service UPDATE/INSERT | 3B grant schema; Phase 4 | DESIGN TRACE / TEST PENDING |
| `P1-I16` | No distributed DB transactions | Cross-service consistency uses explicit calls/events/compensation. | `PD-ADR-05`, `PD-ADR-08` | DOD-07, DOD-14 | CC-12, CC-13 | No cross-DB transaction; outbox/idempotency/reconciliation under failure | 3B event/test schema; Phase 7/11 | DESIGN TRACE / TEST PENDING |
| `P1-I17` | Durable event intent uses outbox | Redis transport is not the only copy of correctness-critical event intent. | `PD-ADR-05` | DOD-14 | CC-13 | Atomic local outbox and consumer inbox survive broker duplication/crashes | 3B fixtures; Phase 4/11 | DESIGN TRACE / TEST PENDING |
| `P1-I18` | Public search stays static where possible | Public catalog search does not require backend runtime dependency. | `ADR-LMS-CATALOG-006` | DOD-09, DOD-11 | CC-01, CC-05 | Public static search build excludes draft/private records; no backend dependency | 3B FE privacy CI; Phase 10 | FE_DRAFT_FILTER_SOURCE_RISK |
| `P1-I19` | Permission-aware search goes through Knowledge Service | Private/authorized search is backend-enforced. | `ADR-LMS-CATALOG-006`, `PD-ADR-06` | DOD-09 | CC-05 | Private search checks ACL before data/snippet/citation; stale rights fail closed | Phase 8 | DESIGN TRACE / TEST PENDING |
| `P1-I20` | Assistant mutation uses domain APIs | AI can never bypass service invariants. | `ADR-03F-08` | DOD-10 | CC-08 | All Assistant mutations invoke authorized domain APIs via validated delegation | 3B internal trust; Phase 9 | DESIGN TRACE / TEST PENDING |
| `P1-I21` | Initial Assistant is authenticated-only | Guest AI requires a later cost/abuse contract. | `ADR-03F-12` | DOD-10 | — | Guest Assistant calls denied; bounded authenticated AI provider usage | Phase 9 | DESIGN TRACE / TEST PENDING |
| `P1-I22` | No browser-native canonical content CRUD initially | Admin presence does not move source-controlled course authority into a runtime database. | `ADR-LMS-CATALOG-001`, `ADR-03F-07` | DOD-05, DOD-11 | CC-09 | No public browser-native lesson/course CRUD; source-controlled release only | 3B endpoint allowlist; Phase 10 | DESIGN TRACE / TEST PENDING |
| `P1-I23` | Instructor uses admin plane | Privileged instructor workflows use `lms-admin.reltroner.com`, not a third frontend hostname. | `ADR-LMS-KC-001` | DOD-11 | — | Instructor privileged flows routed via lms-admin, no third origin | Phase 10 | DESIGN TRACE / TEST PENDING |
| `P1-I24` | Identity copies are projections only | `sub` is the principal reference; copied identity attributes are not authoritative. | `ADR-LMS-KC-001`, `PD-ADR-02` | DOD-03, DOD-06 | — | Business state keyed on signed sub, copied identity fields not authoritative | 3B DTO; Phase 4/5 | DESIGN TRACE / TEST PENDING |

## 4. Targeted contradictions and implementation gaps — not silent PASS

- `CC-01`, tied to `P1-I18` and source-controlled catalog/public frontend obligations: inspected FE route/index source does not filter drafts in all relevant generation paths. **P0 pre-release blocker** until FE negative build artifacts are verified; no production leak was proven.
- `CC-07/18` tied to `I-04/05`, `P1-I08..12`: production Keycloak discovery reported LMS clients absent; FE historical config has legacy issuer/client, and UI fallback is not backend authorization. Future Keycloak/FE acceptance remains mandatory.
- `CC-08` tied to private boundaries `I-08/17`, `P1-I14/20`: internal workload+principal trust direction accepted but specific signed assertion/rotation/replay is not yet specified or tested.
- `CC-06` tied to `P1-I05/17/19`: authenticated Git release → Knowledge ingestion actor and durable job/event schema need Phase 3B contract; no direct Git event-to-DB authority.
- `CC-11/12/13` tied to durable state, transactions and audit: PostgreSQL constraints, outbox/inbox replay and Keycloak reconciliation remain implementation/failure-test gates.
- `CC-02/03/04/05/14/19`: lesson ID/course revision, source-attested Studio canon and public/private index release approval remain schema/CI/runtime gates. No canonical course CRUD or canon-rights shortcut is permitted.
- `CC-21/22`: resource capacity and CI proof need future measured evidence; **the 1-vCPU shared-VPS baseline is not a throughput certificate**.

**Conclusion:** No *approved architectural deviation* from the 44 parent invariant rules is asserted by this crosswalk. Risk classifications remain open, not falsely treated as runtime compliance.

## 5. Compatibility locks beyond the 44 IDs

The approved 3A-03F/04 design preserves **six microservices**, 26 initial public operations, 19 capability values, nine event type names, and four service-owned logical databases. Studio editorial/canon authority is external to LMS runtime course catalog. BR-07/08/09 and financial BR-10 are excluded/deferred from v1; no new API family or seventh canonical service is accepted.

**Two separate test dimensions:** (a) **contract compatibility** means these design ownership/routing/identity constraints remain binding; (b) **real implementation conformance** requires Phase 3B CI and Phase 4–12 integration/operations tests with branch/commit/time/reviewer evidence. The fact that an acceptance plan exists cannot be substituted for the result of its test.

## 6. Decision receipt and remaining gates

Owner decision: `FZ-02 = ACCEPT`. Evidence: current user message `tutup FZ-02 — Final Cross-Contract Invariant Traceability Acceptance` dated 2026-10-09 Asia/Jakarta. Owner acceptance is limited to **44/44 source-to-ADR-to-DoD-to-future-evidence mapping and absence of newly accepted exceptions**. The sign-off does not state that any individual deployed LMS microservice passes live endpoint/security tests.

- **FZ-02 CLOSED** at design level after this record.
- **FZ-03 PASS:** 12 parent ADR directions previously accepted.
- **FZ-04 PASS:** 18 bounded subordinate design dispositions previously accepted.
- **FZ-10 OPEN:** exact Phase 3B scope/entry/exit, separate implementation authorization.
- **FZ-11 OPEN:** explicit final 3A freeze acceptance record with signed source pins and residual implementation gates.
- The docs PR must be reviewed/merged, then record its final SHA as provenance; a branch-local receipt is not automatically present on `main`.

## 7. AI handoff

Start with the two FROZEN contracts, then this 44-row traceability receipt, then [the living ledger](./engineering-end-to-end-progress-ledger.md) and [3A-04 owner register](./reltroner-lms-phase3a-04-ratification-register-20261009.json). Do not infer closure of FZ-10/FZ-11 from closure of FZ-02, or runtime certification from 44 mapped rows.
