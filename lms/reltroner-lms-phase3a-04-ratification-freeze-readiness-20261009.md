# Reltroner LMS — Phase 3A-04 Decision Ratification & Freeze Readiness

> **Date:** 2026-10-09 (Asia/Jakarta)  
> **Status:** **ARCHITECTURE REVIEW COMPLETE / OWNER RATIFICATION PENDING / PHASE 3A FREEZE HOLD**  
> **Mode:** Documentation-only review branch, not applied to production or application repositories.  
> **Decision authority:** Only explicit project-owner acceptance can freeze recommendations; this record is not a self-approved ADR.  
> **Next phase:** 3B NOT AUTHORIZED until an owner-approved Phase 3A design closure/branch scope.

## 0. Executive decision

`3A-04 REVIEW COMPLETE → RATIFICATION BOARD READY → FREEZE HOLD → 3B NOT AUTHORIZED`.

Three noninterchangeable statuses: **discovery PASS** means evidence observed, **design accepted** requires explicit owner decision, **implementation/runtime PASS** requires real negative/contract/integration tests. Neither docs Git commits nor an AI recommendation equate to acceptance of security or production readiness.

## 1. Pinned and classified evidence

| Source | SHA / evidence | Authority |
|---|---|---|
| Infrastructure contract, FROZEN | `b899761c9e833f9fa567055801b9ba0834ed56eb` blob | Binding I-01..I-20 |
| Service/API contract, FROZEN | `cf089b8df4b5ccb1761b504ffae662a0053bf03e` blob | Binding P1-I01..I24 |
| 03F decision register | `b902134f128836483eb28be6a58bf148ad5ae5e0` blob | 22 CC / 16 BR / 12 ADR proposals |
| Identity + Persistence historical combined file | `c2296c0c3e142843dd8a986570dea2e850958e36` blob | Design candidate, source of standalone extraction |
| Catalog + 03F historical combined file | `37dd58c64fddce8d9c49081f5510bbddfbacb491` blob | Manifest design candidate, source of 03F extraction |
| Catalog schema/fixture | `1f4f54751a1ebd3be089526ea6ed3343a96eaecf` / `b497e10e4f20a314d00fce17531c98ba26b5768a` blobs | Candidate, fixture NOT release |
| Backend app source | `Reltroner/LMS-BE@e30a61780994d85671cbf079e6b9ce899b3fe837` | Six Phase-2D foundations; no business API runtime |
| Frontend course source | `Reltroner/LMS-FE@f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7` | 3 courses, 31 lesson files, no explicit lesson MDX ID; public filtering risk |
| Studio constitution | `Reltroner/reltroner-studio@f7b6e6c73fcd81c945524cb81602d2984c6b4720` | Binding Studio narrative/canon only |
| Review baseline | `Reltroner/progress-documentation@d6715144e59816e6a026bacbf5214ed1a32a9401` | Eight files at discovery; ledger still stale |

Keycloak discovery in 03C-2A..2D-1: realm enabled; 8 observed clients; exact LMS clients absent; HRM scopes and Full Scope Allowed flags read-only checked. Those are dated SQL/GUI observations, NOT tested LMS token behavior. Phase 2D's 100 tests/725 assertions are historical foundation acceptance and were not rerun here.

### Documentation integrity correction

At inspected baseline the **03C** file concatenated Identity ADR with **03D Persistence**; **03E** concatenated Catalog with **03F Cross-Contract**; JSON register pointed to a missing standalone 03F Markdown; ledger called Phase 3A 'not started'. This branch adds standalone archival documents and a dated ledger overlay while preserving original combined files untouched. This is documentation normalization, not retroactive ADR acceptance.

## 2. Formal owner decision board: 12 candidate ADR directions

**All 12 are still PROPOSED. Do not claim even one human-ratified ADR solely from this document.**

| ID | Scope | Recommendation | Decision | Remaining gate |
|---|---|---|---|---|
| `ADR-03F-01` | Authority precedence / no crossing LMS-vs-Studio canon | Preserve distinct Studio canon vs LMS course authorities; no seventh CMS/DB | **PENDING OWNER** | OWNER |
| `ADR-03F-02` | Public static publication filtering | Public static export must deny unpublished/unknown status in pages, search, sitemap, metadata and assets | **PENDING OWNER** | OWNER |
| `ADR-03F-03` | Stable ID + historic curriculum revision model | Permanent lesson IDs, alias/tombstone registry, course-local revision; historic completions never silently revoked | **PENDING OWNER** | OWNER |
| `ADR-03F-04` | Source-attested Studio reference + rights | Only source-attested published Studio editions/licensed references enter public Knowledge and AI citations | **PENDING OWNER** | OWNER |
| `ADR-03F-05` | Knowledge ingest trigger ownership | Authenticated release worker invokes explicit private Knowledge ingest command; Knowledge alone owns job/events | **PENDING OWNER** | OWNER+3B_DETAIL |
| `ADR-03F-06` | Creator submissions/assessments v1 | DEFER server-side student creative projects, submissions, grading and mentor file review in initial v1 | **PENDING OWNER** | OWNER |
| `ADR-03F-07` | Paid product/entitlement v1 | DEFER payments/entitlements/financial ledger; Mentorship only owns its booking/session domain | **PENDING OWNER** | OWNER |
| `ADR-03F-08` | Internal workload/delegated principal auth | Authenticate internal workload and signed recipient+operation-bound principal delegation; no localhost/header trust | **PENDING OWNER** | OWNER+PRE-IMPLEMENTATION_ADR |
| `ADR-03F-09` | Admin-Keycloak audit reconciliation | Keycloak admin adapter with durable Audit operation intent and ambiguous-result reconciliation | **PENDING OWNER** | OWNER+PRE-IMPLEMENTATION_ADR |
| `ADR-03F-10` | Document split / ledger refresh | Preserve combined historical docs and split canonical reviews; update living ledger in dated addendum | **PENDING OWNER** | DOCS_PR |
| `ADR-03F-11` | Availability and capability binding | Leave 26 endpoints/19 capabilities unchanged; propose authenticated mentorship availability using booking.create.self; admin.learning.* stays reserved | **PENDING OWNER** | OWNER+3B_MATRIX |
| `ADR-03F-12` | Resource/cost governance | Keep existing low-cost infrastructure; resource ceilings, restore and runbooks based on future measurements | **PENDING OWNER** | OWNER+CAPACITY |

### Design details requiring deliberate agreement

**Internal trust:** authenticated service workload plus short-lived signed principal context, scoped to target service, caller, operation, verified `sub`, capability and expiry; no security based solely on loopback or user headers. Cryptographic format/key storage/rotation/replay/freshness must be separately specified and negatively tested before service API implementation.

**Knowledge ingest:** trusted release worker submits version-pinned, authorized source-approved catalog release to a private Knowledge ingestion interface (not one of 26 public endpoints). Knowledge validates source, ACL/license and version, durably records ingestion intent and may produce `knowledge.index.requested/completed` as owner. Git commits alone never constitute trusted Redis business events; no Gateway-owned canonical catalog DB.

**Admin role changes:** privileged Gateway/Keycloak adapter cannot atomically commit to Audit DB. Persist an authorized operation intent, call Keycloak under least privilege, record confirmed outcome, reconcile unknown result, fail closed on unavailable audit. No secrets in FE or direct Keycloak DB edit.

**Mentorship availability:** frozen endpoint exists without explicit capability mapping; recommend authenticated-first and require `mentorship.booking.create.self` for booking-oriented availability pending owner choice; no unreviewed public availability or new permission/route. `admin.learning.*` capability names are reserved; they do not authorize inventing endpoints.

**Catalog/publication:** preserve Course/Module/Path/Resource IDs; introduce stable lesson ID, release revision, aliases/tombstones, no history deletion. Public builds must deny draft/unattested Studio canon on routes/search/index/sitemap/metadata/asset references. Studio canon status and LMS publication are independent dimensions.

## 3. Product scope choices: all 16 BR IDs

| ID | Business request | Recommended first-release disposition |
|---|---|---|
| `BR-01` | Creator-facing systematic worldbuilding education / anti-stagnation | IN-SCOPE AS CONTENT/CURRICULUM (existing courses) |
| `BR-02` | Audience-facing Asthortera/continuous narrative and civilization laboratory | IN-SCOPE AS APPROVED REFERENCE/SEARCH ONLY |
| `BR-03` | Current Lore/Backstory/Wiki narrative modes | METADATA/FACET CANDIDATE only if source-attested |
| `BR-04` | Published canon immutability, edition and archival | MANDATORY INTEGRATION CONSTRAINT whenever Studio material referenced |
| `BR-05` | Creative Compound Machine and cross-domain causal narrative | TEACHING/RETRIEVAL CONTENT; not durable workflow engine |
| `BR-06` | Studio course worksheets and downloadable resources | IN-SCOPE STATIC DELIVERY |
| `BR-07` | User-generated project bible or 30-day journal persisted in LMS | DEFER FROM V1 unless owner explicitly promotes |
| `BR-08` | Assessment/rubric submission/grading/mentor review | DEFER / NEW BUSINESS FEATURE |
| `BR-09` | Mentorship with creator-output review | DEFER cross-service reviewer workflow; basic bookings remain in scope |
| `BR-10` | Paid private sessions, subscriptions, Patreon/Kickstarter | DEFER financial/commercial ledger from Mentorship |
| `BR-11` | Studio narrative editorial CMS or wiki content CRUD via LMS admin | OUT OF SCOPE / DISALLOWED BY CURRENT FROZEN CONTRACT |
| `BR-12` | Personalization, reader's private notes / favorites on Studio canon | DEFER until explicit product use case |
| `BR-13` | Source-approved Studio content searchable via universal Ctrl+K | IN-SCOPE AS FUTURE AUTHORIZED/STATIC INDEX INTEGRATION |
| `BR-14` | Guest AI or unrestricted LLM-based canon generator | OUT OF SCOPE INITIAL, authenticated Assistant only |
| `BR-15` | Cross-course creator pathways and prerequisites | IN-SCOPE AS VERSIONED CATALOG RELATION |
| `BR-16` | Institutional equivalence: every lore element = LMS entity | REJECT |

**Owner product decision required:** choose either (A) **DEFER** BR-07/08/09 (recommended minimal v1: deliverables as downloadable worksheets; learner progress and basic Mentorship still supported), or (B) **INCLUDE** persisted creator work and reviewer workflows; choosing B requires new versioned authority/API/RBAC/privacy/storage/audit contract BEFORE 3A freeze. Paid ledger/entitlements (BR-10) remain separate commercial scope, never smuggled into Mentorship booking state.

## 4. 22 cross-contract findings and release/design distinctions

| ID | Category | Evidence-based current finding class | Required next evidence |
|---|---|---|---|
| `CC-01` | Public/draft static output | P0 PRE-RELEASE BLOCKER | Build-output negative suite; public-only whitelist at every artifact stage |
| `CC-02` | Lesson identity | OPEN DESIGN / IMPLEMENTATION GAP | One-time ID registry; immutable IDs; deterministic alias migration; dual-generator parity tests |
| `CC-03` | Curriculum + historic learner state | DESIGN CONSISTENT, DRAFT | Define completion policy revision, enrolled revision upgrade opt-in, archived behavior, unknown-ID policy |
| `CC-04` | Studio canon vs course publication | DESIGN RULE REQUIRED | Two distinct status dimensions and source-attested edition; default `not_attested` |
| `CC-05` | Search provenance and preview rights | DESIGN OPEN | Independent public/private release filtering; no snippet or citation leakage; license/LLM-use approval |
| `CC-06` | Git → Knowledge event provenance | CONTRACT DESIGN GAP | Explicit authenticated internal ingestion trigger and durable job/outbox; no unowned Git-to-DB write |
| `CC-07` | Keycloak provisioning | OPEN ADR | Owner sign-off then Phase 4 controlled provisioning; HRM regressions |
| `CC-08` | Internal service workload trust | OPEN CRITICAL DESIGN | Separate ADR and abuse/negative contract suite before private domain APIs ship |
| `CC-09` | API coverage | FROZEN SEMANTIC SCOPE | OpenAPI schemas and capabilities in 3B; any new family requires change control |
| `CC-10` | Capability coverage | GAP / RESERVED CAPABILITIES | Bind to explicit current operations or leave unused; do not invent routes/roles |
| `CC-11` | Booking durability | DRAFT | PostgreSQL constraints + race tests; event outbox consistent |
| `CC-12` | Audit-Keycloak role change | OPEN CRITICAL DESIGN | Durable operation intent + outcome/reconciliation, admin adapter least-privilege |
| `CC-13` | Publisher/inbox failure | DESIGN DRAFT | Signed event schema, at-least-once, dedup, DLQ/retry/retention, replay tests |
| `CC-14` | Studio editorial release | BUSINESS RULE | Attested release artifact, publication actor, version & legal rights; no automatic canon promotion |
| `CC-15` | Creator deliverable | NEW REQUIREMENT CANDIDATE | Owner must explicitly include or defer; ADR+API+RBAC+storage/privacy if included |
| `CC-16` | Paid mentorship/membership | OUT OF SCOPE CURRENT V1 | Separate commercial/finance ADR if required; never proxy into bookings |
| `CC-17` | Long-horizon story graph | NO CONFLICT | Studio owns canonical graph; Knowledge may index attested edges; no new LMS runtime graph authority |
| `CC-18` | Frontend auth drift | OBSERVED DRIFT | Controlled FE cutover only after effective claims validation; server denies missing permission |
| `CC-19` | Observability and rollback | OPEN | Version pin policy, promotion pointer, rollback, reindex, safe retention thresholds |
| `CC-20` | Evidence/governance | DOCUMENTATION BLOCKER TO 3A FREEZE | Split into canonical docs preserving historical source; update ledger link/status and owner decisions |
| `CC-21` | Runtime capacity/cost | RELEASE GATE | Measured CPU/RAM I/O profiles, throttled workers, no optional new service by default |
| `CC-22` | CI/release-proof | OPEN | 3B six-service CI + FE publication guard; signed release artifact promotion |

### Freeze-design hard decisions

`CC-01` publication denial policy; `CC-02/03` stable IDs, revision and completion history; `CC-06` authenticated release→Knowledge owner; `CC-08` workload+principal delegation; `CC-10` availability/capability policy; `CC-12` admin Audit reconciliation; `CC-15` creator scope; `CC-20` doc/decision provenance. These need a coherent owner-ratified *direction*. Exact OAuth claims, database DDL and cryptographic assertion fixtures can be future implementation/3B work **only if explicitly gated**.

### Later implementation blockers, not fabricated design failures

Keycloak LMS clients absent; source FE potential draft exposure; no deployed manifest; unfinished DB migrations/outbox; Redis failure tests, real API, backups, load and cost limits are Phase 3B/4–12 obligations. They are **NOT PASS**, but do not require production rollout to complete a design-only 3A freeze.

## 5. Exact frozen-invariant crosswalk — 44 IDs

| Invariant | Normative subject | Future acceptance evidence | Observed scope |
|---|---|---|---|
| `I-01` | Learner origin | FE Pages contract | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-02` | Admin origin | FE Pages contract | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-03` | Gateway public hostname | Ingress test | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-04` | Keycloak authority | Issuer/claims | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-05` | OIDC trust separation | Cross-client negatives | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-06` | FE non-authority | Authorization negative suite | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-07` | Admin server auth | Admin API tests | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-08` | Private microservices | Nginx/UFW scan | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-09` | PostgreSQL business durability | PG persistence | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-10` | Logical ownership | DB owner grants | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-11` | No cross-service writes | DB grants | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-12` | Redis ephemeral | Redis outage | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-13` | Premium Hosting asset origin | Asset origin | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-14` | Cloudflare Pages frontends | Static deploy | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-15` | No KVM1 LLM inference | Process inventory | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-16` | Cloudflare not state authority | Cache purge | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-17` | Minimal public VPS ingress | TLS/port scan | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-18` | Immutable asset release | Content digest | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-19` | Versioned HTTP API | OpenAPI | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `I-20` | Avoid unjustified operational complexity | ADR/cost evidence | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I01` | Gateway no domain owner | Gateway boundary tests | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I02` | Git canonical Content Catalog | Manifest contract | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I03` | Learning state owner | Learning DB tests | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I04` | Mentorship state owner | Booking DB tests | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I05` | Knowledge derived indexes | Reindex tests | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I06` | Assistant orchestration only | Tool authorization | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I07` | Audit append-only | Append-only DB tests | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I08` | Keycloak subject authority | JWT issuer | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I09` | Two browser OIDC clients | Client scoping | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I10` | lms-api audience | Audience rejection | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I11` | Explicit capabilities | Capability matrix | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I12` | No student auth fallback | Missing-role deny | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I13` | /api/v1 namespace | OpenAPI | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I14` | No private service public exposure | Private port scan | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I15` | No cross-DB writes | DB negative grants | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I16` | No distributed transaction | Recovery design | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I17` | Transactional outbox | Outbox replay | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I18` | Static public search | FE public build | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I19` | Knowledge private search | ACL/snippet negatives | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I20` | Assistant domain API writes | Tool caller auth | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I21` | Assistant authenticated only | Guest deny | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I22` | No canonical runtime content CRUD | Route exclusion | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I23` | Instructor admin plane | Admin FE | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |
| `P1-I24` | Identity is projection only | No shared user DB | **DESIGN PRESERVED / RUNTIME UNVERIFIED** |

All 44 rows are **design-preserved only**. Crosswalk is not a claim of runtime certification or proof that a future modified design has no contradictions.

## 6. Phase 3A freeze readiness gates

| Gate | Condition | Outcome today |
|---|---|---|
| `FZ-01` | Evidence precedence and SHA sources pinned | **PASS — GitHub inspection** |
| `FZ-02` | 20+24 invariants all traced with planned acceptance | **TRACEABLE; owner acceptance pending** |
| `FZ-03` | All 12 ADR-03F proposals explicitly accepted/rejected/deferred with gate | **BLOCKED — owner action absent** |
| `FZ-04` | Identity KC-001, PD-ADR and Catalog review candidates have bounded signed dispositions | **BLOCKED — no owner signatures** |
| `FZ-05` | Creator storage/submissions/mentor review and finance v1 scope selected | **BLOCKED — product decision absent** |
| `FZ-06` | Public publication deny-by-default release policy signed | **PROPOSED; runtime FE test in 3B/10** |
| `FZ-07` | Internal delegation, Knowledge release trigger, Keycloak↔Audit reconciliation direction accepted | **BLOCKED — security ADR sign-off** |
| `FZ-08` | 26 operations/19 capabilities/9 event names/4 DB ownership remain unchanged | **PASS CONTRACT CROSSWALK; no runtime proof** |
| `FZ-09` | Canonical standalone docs + dated ledger overlay reviewed/merged | **DOCS PR IN REVIEW** |
| `FZ-10` | 3B scope/entry/exit and no production mutation rule approved | **PROPOSED** |
| `FZ-11` | Dated owner sign-off record with approved ADR IDs and hashes | **BLOCKED** |

**Result: HOLD.** Current docs show the necessary architecture, but there is **no explicit project-owner signature** for the normative decisions and scope. A GitHub draft PR does not itself constitute a decision. Owner should ratify the direction and record downstream implementation blockers separately.

## 7. Next stage: Phase 3B contract+CI acceptance protocol

**Entry:** owner-ratified 3A design/spec scope; reviewed and merged documentation; no unapproved deviation from 20+24 invariants; a scoped implementation branch and review/rollback contract. **Entry is NOT yet met.**

**Proposed 3B work:** canonical OpenAPI for 26 operations with per-route permissions and RFC7807 response/ID/cursor/idempotency schemas; internal workload/delegation and outbox/inbox JSON schema fixtures + negative tests; deterministic Catalog v1 manifest with permanent lesson IDs and publication filter; six-service PHP CI plus FE public-output negative build tests; immutable artifact/source release provenance. No live Keycloak/production DB/VPS mutations in 3B absent separate explicit authorization.

**3B exit candidate:** all scoped contract/CI suites independently green at pinned SHAs; signed provider/consumer and privacy release gates; no unknown auth fallback; no implementation/deployment false PASS. Phase 4 remains separately gated for Keycloak client setup, private routing, owner DBs and production changes.

## 8. Owner-only sign-off form — intentionally unfilled

```yaml
phase: 3A-04
owner: null
decision_timestamp: null
decision: PENDING # ACCEPT | REVISE | REJECT
accepted_document_commit: null
ratified_adr_ids: []
deferred_adr_ids_and_first_blocking_phase: []
v1_creator_artifacts_and_grading: PENDING # DEFER | INCLUDE
v1_payments_and_entitlements: PENDING # DEFER | INCLUDE
availability_route_policy: PENDING
internal_trust_direction: PENDING
knowledge_ingest_owner: PENDING
admin_role_audit_direction: PENDING
phase_3a_frozen: false
phase_3b_implementation_authorized: false
phase_4_production_mutation_authorized: false
```

**Audit rule:** AI recommendation, file presence, successful docs commit or a GitHub PR merge cannot substitute for explicit owner ratification.

## 9. Final checkpoint / reproducible handoff

`3A-04 DESIGN ASSESSMENT COMPLETE / OWNER RATIFICATION PENDING / FREEZE HOLD / PHASE 3B NOT AUTHORIZED`.

Source order for AI transfer: [physical FROZEN](./master-infrastructure-placement-contract.md) → [logical FROZEN](./logical-service-boundary-api-contract.md) → [ledger](./engineering-end-to-end-progress-ledger.md) → [KC review](./adr-lms-kc-001-identity-provisioning-review-candidate.md) → [03D persistence](./reltroner-lms-phase3a-03d-persistence-event-model-20261009.md) → [03E catalog](./reltroner-lms-phase3a-03e-catalog-manifest-versioning-20261009.md) → [03F cross-contract](./reltroner-lms-phase3a-03f-cross-contract-business-reconciliation-20261009.md) → this record.

Do not alter HRM clients, built-in scopes, frozen architecture, public DNS/TLS, OS packages, PostgreSQL, Redis, or deployed applications in Phase 3A.
