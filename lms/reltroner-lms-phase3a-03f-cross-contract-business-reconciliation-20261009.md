# Reltroner LMS — Phase 3A-03F Cross-Contract Review & Business Requirement Reconciliation

> **Record ID:** LMS-3A-03F-REVIEW-20261009  
> **Date / reporting timezone:** 2026-10-09 / Asia-Jakarta  
> **Status:** CROSS-CONTRACT REVIEW COMPLETE AS DESIGN / OPEN DECISIONS / **NOT FROZEN** / NOT IMPLEMENTED  
> **Scope:** source-based design review and business-requirement reconciliation only; no source-code, VPS, Keycloak, PostgreSQL, Redis, GitHub file mutation, or deployment.  
> **Decision owner:** project owner (ratification pending).  
> **Architecture:** independently deployable six Laravel microservices in one backend monorepo; not modular monolith.  
> **Evidence quality:** GitHub source trees/files were reviewed; no current production build, effective token, database integration, or end-to-end test execution asserted.

## 0. Executive decision — read before using in another AI

**Phase 3A-03F design review result: `COMPLETE WITH OPEN DESIGN GATES`**. No observed contradiction requires altering 20 frozen physical invariants I-01..I-20 or 24 frozen logical invariants P1-I01..P1-I24. All extension requirements are **proposals**, not silently incorporated into the 26 frozen API operations, 19 frozen capability names, four databases, or nine event families. The implementation readiness gate remains CLOSED until explicit ratification and 3B acceptance criteria.

**Highest-impact new observed concern:** the pinned LMS-FE source builds static route parameters for **all** courses, lessons, and paths, including draft entities, and generates search records without a publication-status filter. There is a plausible unintended-publication **source/build risk**. It is **NOT evidence of actual public deployment leakage**, because a built production artifact and hosted pages were not inspected. Ensure no unpublished Studio canon enters public/static generated artifacts. Record `CC-01` as P0 **release blocker**, not as an already exploited production vulnerability.

**New business/domain question:** existing creator courses include downloadable templates and promised final deliverables; no demonstrated backend upload/submission/assessment/mentor-review capability. Those features must be either explicitly deferred or accepted with a new versioned API/capability/storage/privacy/retention contract. Do not infer submission CRUD merely because a lesson says “journal” or “project.”

**Document governance observation:** GitHub's file `lms/reltroner-lms-phase3a-03c-2d-provisioning-adr-review-20261009.md` is a combined 821-line record: lines 1–75 contain 3A-03C-2C evidence, 76–199 contain a preliminary ADR, 200–448 contain Identity ADR-LMS-KC-001 candidate, and 449–821 contain Phase 3A-03D Persistence/Event Model. Its title does **not** describe its whole contents. Retain it for provenance; create separate standalone canonical ADRs in a controlled **documentation-only** follow-up, with explicit statuses and stable links. Living ledger is not yet refreshed for 3A-03C…03F.

## 1. Live repository directory verification

At GitHub `Reltroner/progress-documentation/main` observed commit `4478c9fdb3ab0c11024dcb2396cd26280b4ab364`, the `lms/` directory contained **seven** files:

| File | Live blob SHA | Classification |
|---|---|---|
| `master-infrastructure-placement-contract.md` | `b899761c9e833f9fa567055801b9ba0834ed56eb` | Binding physical contract; FROZEN |
| `logical-service-boundary-api-contract.md` | `cf089b8df4b5ccb1761b504ffae662a0053bf03e` | Binding service and API contract; FROZEN |
| `engineering-end-to-end-progress-ledger.md` | `866cc8c3b126ee6fae0cab8ac5160552cf41ad4a` | Living progress/DoD ledger; current phase stale |
| `reltroner-lms-phase3a-03c-2d-provisioning-adr-review-20261009.md` | `c2296c0c3e142843dd8a986570dea2e850958e36` | Combined Identity evidence/ADR and Persistence/Event draft; not human ratified |
| `reltroner-lms-phase3a-03e-catalog-manifest-versioning-20261009.md` | `b568a6d59260bc7774a494609c7aae23d2595bb3` | Catalog design candidate, not frozen |
| `reltroner-lms-catalog-manifest-v1.candidate.schema.json` | `1f4f54751a1ebd3be089526ea6ed3343a96eaecf` | Draft JSON Schema, not a production compiler |
| `reltroner-lms-catalog-manifest-v1.partial-example.json` | `b497e10e4f20a314d00fce17531c98ba26b5768a` | Partial fixture, not a real release |

Other authoritative snapshots:
- `Reltroner/LMS-BE@e30a61780994d85671cbf079e6b9ce899b3fe837`: accepted Phase 2D foundation only. Six API route files contain `<?php`; no domain DB migrations tracked.
- `Reltroner/LMS-FE@f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7`: 3 course definitions (1 published, 2 draft); 10 modules; 31 MDX lesson paths; 2 learning paths (1 published, 1 draft); 28 resource IDs; static Contentlayer build.
- `Reltroner/reltroner-studio@f7b6e6c73fcd81c945524cb81602d2984c6b4720`, `content/principles/reltroner-studio-master-source-of-truth.md`, blob `a8a77066ad7de30a6a806a818e5483bd1fa85688`, **binding Studio constitution v2.2**, updated 2026-10-08. Studio authority covers Studio creative IP, narrative, canon, modes, edition and brand; it does **not** supersede LMS infrastructure/identity/service authority.

### 1.1 Precedence and authority resolution

1. Phase 0C FROZEN: infrastructure topology, hosting, database isolation, public ingress, minimum spending.
2. Phase 1 FROZEN: six service responsibilities, API families, OIDC trust, event semantics, catalog source control, data ownership.
3. Studio binding constitution **for Studio subject matter**: Current Lore/Backstory/Wiki modes, canon release gates/editions, Creative Compound Machine, audience/creator value, IP integrity.
4. Reviewed ADRs **only after owner sign-off**: concrete identity config, outbox mechanics, manifest/schema/ID compatibility, service-call trust, etc.
5. Living ledger: observational status/evidence; cannot overwrite normative contracts.
6. Current source: descriptive implementation truth, not automatic architecture authority.

Where a proposed business feature conflicts with #1/#2, use an impact-specific ADR/versioned revised contract; NEVER silently grant an exception.

## 2. Business value model and domain separation

Studio's apex product structure is one intellectual engine and two value paths:
- **Creator-facing:** Creative Compound Machine; methodology, systems thinking, worldbuilding anti-stagnation, creator education.
- **Audience-facing:** Asthortera/The Abyss of Comfort civilizational simulation; experience and narrative, with Current Lore/Backstory/Wiki cognitive modes.
- Studio's content operating system seeks evergreen library/canon compounding, not a generic feed or SaaS dashboard. Published canon is effectively immutable; drafts remain creatively mutable; semantic revision requires versioned edition/release.

**Engineering conclusion:** LMS courses are **educational delivery**, not Studio canon authority. Studio-authored IP may appear as approved source-attested references or educational examples. The Studio constitution does not obligate six new services, a content CMS, graph DB, temporal simulation engine, publishing platform, paid-access accounting ledger, or a learner portfolio system in LMS v1.

### 2.1 Six-service authority crosswalk

| Service | Owns (frozen) | Studio-derived permissible extension under existing routes | Prohibited/extra-ADR boundary |
|---|---|---|---|
| Gateway | External JWT validation, capability routing, principal projection, request correlation | Forward `catalog_version` metadata without becoming its authority | Cannot own canon, enrollment, booking, role grants or submissions |
| Learning | Enrollment, lesson progress, completion, bookmarks | Stable course/lesson revision context; creator course deliverable description; version-pinned completion | Actual uploaded creator artifacts, grading, mentor feedback require new privacy/storage/API policy; cannot edit Studio canon |
| Mentorship | Offerings, availability, bookings, sessions | Contextual `course_id` or methodology source reference in offering; approved course snapshot | No payment ledger, shared user-creation DB, direct Learning writes or canonical curriculum edits |
| Knowledge | Rebuildable public/private search index + ingestion checkpoint | Approved Studio provenance/edition, source-attested narrative mode facets, authorized public/private index | No writable canon, auto-approval of drafts, prompt-generated facts elevated to canon, raw private source leaks |
| Assistant | Authenticated orchestration, RAG, tools through domain APIs | Mode-aware explanations and cited canonical/edition source; creator learning guidance | No canonical writing, hidden mutation, learner-private data leak, invented canon status, guest AI by default |
| Audit | Durable append-only privileged/security events; admin workflow | Trace accepted privileged release events if integrated, privacy-sensitive role changes | Cannot falsely claim Git commits automatically produce events; no cross-system transaction with Keycloak |

## 3. Cross-contract review matrix — authoritative vs design vs gaps

| ID | Topic | Reconciliation | State | Required next gate |
|---|---|---|---|---|
| CC-01 | Public/draft static output | FE static route generation/search uses all records; publication filter missing in inspected functions. Draft courses exist. Potential unintended exposure; hosted artifacts unverified. | **P0 PRE-RELEASE BLOCKER** | Build-output negative suite; public-only whitelist at every artifact stage |
| CC-02 | Lesson identity | Course/module/path/resources have explicit IDs; MDX lacks first-class immutable lesson ID; `_id` vs `courseSlug:slug` differ in search pipelines. | OPEN DESIGN / IMPLEMENTATION GAP | One-time ID registry; immutable IDs; deterministic alias migration; dual-generator parity tests |
| CC-03 | Curriculum + historic learner state | Progress endpoint uses stable `{course_id}/{lesson_id}`; revised manifest proposes pinned course revision. No tables/APIs implemented. | DESIGN CONSISTENT, DRAFT | Define completion policy revision, enrolled revision upgrade opt-in, archived behavior, unknown-ID policy |
| CC-04 | Studio canon vs course publication | Studio's `published_canon` cannot be inferred from LMS `published` or public URL. | DESIGN RULE REQUIRED | Two distinct status dimensions and source-attested edition; default `not_attested` |
| CC-05 | Search provenance and preview rights | Public edge search, private Knowledge and Assistant share references but different entitlements and audiences. | DESIGN OPEN | Independent public/private release filtering; no snippet or citation leakage; license/LLM-use approval |
| CC-06 | Git → Knowledge event provenance | Frozen `knowledge.index.requested/completed` families do not specify who authenticates a Git release into Knowledge workflow. | **CONTRACT DESIGN GAP** | Explicit authenticated internal ingestion trigger and durable job/outbox; no unowned Git-to-DB write |
| CC-07 | Keycloak provisioning | Exact `lms-user/lms-admin/lms-api` clients absent at observed realm; Identity ADR design candidate. | OPEN ADR | Owner sign-off then Phase 4 controlled provisioning; HRM regressions |
| CC-08 | Internal service workload trust | Loopback not auth; signed assertion/workload identity proposed, format/rotation/replay still open. | **OPEN CRITICAL DESIGN** | Separate ADR and abuse/negative contract suite before private domain APIs ship |
| CC-09 | API coverage | 26 frozen external operations; no canonical course mutation or submit/review endpoints. | FROZEN SEMANTIC SCOPE | OpenAPI schemas and capabilities in 3B; any new family requires change control |
| CC-10 | Capability coverage | 19 capabilities frozen; `admin.learning.*` has no initial public admin Learning API; `mentorship/availability` authorization policy unspecified. | GAP / RESERVED CAPABILITIES | Bind to explicit current operations or leave unused; do not invent routes/roles |
| CC-11 | Booking durability | Slot occupancy and idempotency are independent DB guarantees; booking/API design pending. | DRAFT | PostgreSQL constraints + race tests; event outbox consistent |
| CC-12 | Audit-Keycloak role change | Role action spans separate Keycloak and audit authority; no distributed commit. | OPEN CRITICAL DESIGN | Durable operation intent + outcome/reconciliation, admin adapter least-privilege |
| CC-13 | Publisher/inbox failure | Redis ephemeral; outbox/inbox proposed; no runtime tests. | DESIGN DRAFT | Signed event schema, at-least-once, dedup, DLQ/retry/retention, replay tests |
| CC-14 | Studio editorial release | Studio canon freeze editorial flow is distinct from LMS catalog build and from Git commit visibility. | BUSINESS RULE | Attested release artifact, publication actor, version & legal rights; no automatic canon promotion |
| CC-15 | Creator deliverable | Course says produce project bible/journal; backend submissions, private data and reviews absent. | **NEW REQUIREMENT CANDIDATE** | Owner must explicitly include or defer; ADR+API+RBAC+storage/privacy if included |
| CC-16 | Paid mentorship/membership | Studio mentions memberships/funding; initial Mentorship has no payment/payout/ledger authority. | OUT OF SCOPE CURRENT V1 | Separate commercial/finance ADR if required; never proxy into bookings |
| CC-17 | Long-horizon story graph | Studio season/episode/chapter; lore modes, causal dependency preservation. LMS manifest currently only references Studio. | NO CONFLICT | Studio owns canonical graph; Knowledge may index attested edges; no new LMS runtime graph authority |
| CC-18 | Frontend auth drift | `.env.example` references legacy issuer/client; UI role fallback to student. | OBSERVED DRIFT | Controlled FE cutover only after effective claims validation; server denies missing permission |
| CC-19 | Observability and rollback | Catalog and Knowledge versions need consistency through deployment/rollback. | OPEN | Version pin policy, promotion pointer, rollback, reindex, safe retention thresholds |
| CC-20 | Evidence/governance | Identity ADR file contains concatenated 3A-03C and 3A-03D docs; ledger not refreshed. | **DOCUMENTATION BLOCKER TO 3A FREEZE** | Split into canonical docs preserving historical source; update ledger link/status and owner decisions |
| CC-21 | Runtime capacity/cost | 1 vCPU/~4GB VPS shared with HRM/Keycloak; FTS/outbox/indexing/LLM calls increase load. | RELEASE GATE | Measured CPU/RAM I/O profiles, throttled workers, no optional new service by default |
| CC-22 | CI/release-proof | 3A design tests are specified only; FE build and BE implementation not certified. | OPEN | 3B six-service CI + FE publication guard; signed release artifact promotion |

### 3.1 Source-to-production disclaimer for CC-01

Inspected source:
- `src/app/(learn)/courses/[slug]/page.tsx`: `generateStaticParams()` enumerates all courses/aliases.
- `src/app/(learn)/courses/[slug]/lessons/[lesson]/page.tsx`: uses `getAllLessonRouteParams()`.
- `src/lib/content/lesson-registry.ts`: `getAllLessonRouteParams()` iterates `getAllCourses()` with no status gate.
- `src/app/(learn)/paths/[slug]/page.tsx`: `generateStaticParams()` enumerates all paths.
- `scripts/generate-search-index.ts`: maps all `courses`, `learningPaths`, and parsed lesson files.
- `src/lib/content/search-index.ts`: `getSearchIndex()` maps all registry courses/lessons/paths.
- `src/catalog/courses/*.ts`: two courses marked `draft`.

**Not tested:** actual built `out/`, pages served by Cloudflare, origin cache, routing/auth middleware; do not assert public exposure occurred. Static output, if publicly deployed, must not be treated as access-controlled just because React hides links.

## 4. API-operation and capability reconciliation

Frozen **26** `/api/v1` operations: `me=1`, Learning=8, Mentorship=7, Knowledge=1, Assistant=1, Admin principal=3, Admin mentorship=3, Admin audit=2. Business endpoint families **do not** include project submissions, assessments, Studio editorial authoring or payment processing. Do not create extra route families under generic `POST /courses`, `PATCH /lessons` or an unapproved learner upload API.

Frozen **19** capabilities: Learning (6), Mentorship (4), Knowledge/Assistant (2), Admin (7). Keycloak ADR candidate stores them as `lms-api` client roles at `resource_access['lms-api'].roles`; this is not runtime-verified. `lms-user` and `lms-admin` are separate browser trust contexts; no default privilege from persona, `production_user`, frontend UI role, or just authenticating.

| Operation ambiguity | Required policy decision |
|---|---|
| `GET /api/v1/me` | Authenticated principal; effective capabilities sanitized; no invented `me.read` permission |
| `GET /api/v1/mentorship/offerings[/{id}]` | Public vs authenticated guest policy; if public, forbid private mentor metadata |
| `GET /api/v1/mentorship/availability` | Authenticated? Should require existing offering capability or new dedicated permission? Do not silently alter frozen 19 names |
| `GET /api/v1/knowledge/search` | Required `knowledge.search`; per-document ACL separate and enforced by Knowledge |
| `POST /api/v1/assistant/query` | `assistant.use`; downstream tool calls need independently authorized delegated permissions |
| `admin.learning.read/override` | Capabilities are reserved but have no initial explicit admin-learning route; default deny, no phantom API |
| `PUT .../progress` | Path IDs stable; enrollment revision server-resolved, not arbitrary user-provided `catalog_version` |
| `PATCH .../principals/{id}/roles` | Keycloak + Audit transaction split with uncertainty reconciliation; not made safe by signing JWT alone |

Potential **new business endpoint** impact (`NEW API FAMILY`) is a change proposal, not v1 work:
- project/submission creation, revision, private storage, attachment, grading/feedback, rubric, mentor review;
- source-backed Studio canon publication/release management;
- payments, subscriptions, access entitlements.
If scoped into current version, author a separate ADR with explicit effect on 26 route families, 19-capability namespace and DoD. Otherwise defer and keep worksheets client-side/download-only.

## 5. Persistence, events, and catalog versioning reconciliation

### 5.1 Durable domain truth remains four databases

| DB | Authority | New requirement resolution |
|---|---|---|
| `lms_learning_db` | Enrollment, learner progress, completion, bookmarks | Store stable `course_id`, `lesson_id`, approved `course_revision`, historical completion policy and outbox; **no Studio canon content** |
| `lms_mentorship_db` | Offers, slots, booking, sessions, durable `Idempotency-Key` records | Store versioned course/methodology reference snapshot as context; avoid cross-DB joins; no payment ledger |
| `lms_knowledge_db` | Search/index derived release/checkpoints | Rebuildable from authorized immutable LMS catalog and attested Studio reference releases; strict ACL/visibility |
| `lms_audit_db` | Append-only privileged events and durable administrative operation intent/outcome | Cannot claim Keycloak external role mutation and Audit commit as atomic; reconciliation required |

Gateway/Assistant have no mandatory durable DB; Redis remains ephemeral. Each producer owns `outbox_events` as needed and each consumer's durable correctness effects require `inbox_events` in its own DB. Public content releases originate Git; no Git-owned runtime SQL business table is created to make events easier.

### 5.2 Catalog → Learning

- `schema_version=1` (candidate) describes shape; `catalog_version=sha256(...)` identifies manifest; `course.revision` binds learner progress, not every unrelated manifest change.
- Course/module/path/resource IDs are already explicit in FE snapshot. MDX lesson ID and cross-release aliases must be introduced once and never regenerated from mutable path.
- Lesson ordering and chapter ordinals are not unique durable identities.
- Enrollment only into eligible released courses. Completion derives from required lesson set at the enrollment's accepted curriculum revision; later course updates must not silently erase prior completion.
- Historic manifest version availability, release retention, migration and course upgrade policy remain decisions. No speculative forever-retention commitment.

### 5.3 Catalog/Studio → Knowledge → Assistant

**Recommended authenticated ingest sequence (not yet a frozen transport contract):**

1. Studio editorially releases specific eligible canonical sources/editions through its own Git/release flow; creator approval/rights recorded outside Knowledge.
2. LMS catalog compiler builds a validated immutable manifest with distinct `lms_status`, `release_class`, `studio_canon_status`, `studio_source_commit` and rights/visibility attestation for eligible references.
3. Approved deploy/release workflow sends a **signed/authenticated internal ingestion request** to Knowledge (or an approved trusted worker), with artifact URI, digest, release metadata; no new public browser endpoint required.
4. Knowledge validates digests, provenance, release class, rights and ACL; persists `ingestion_job` and `knowledge.index.requested` in one Knowledge-owned database transaction as applicable.
5. Worker builds a new derived versioned index, validates ACL/content completeness, atomically switches current index pointer, and emits `knowledge.index.completed` with status outcome as contract defines.
6. Assistant query pins an allowed index release; citations carry **actual** source/release/edition provenance. Draft and `not_attested` items cannot be described as Studio published canon.

The exact ownership of `knowledge.index.requested` **is not yet frozen**. The numbered sequence is a candidate solution to CC-06 requiring sign-off. It avoids pretending a Git commit itself is already a durable cross-service event. Published/archived Studio canon and educational `published` courses are independent status dimensions.

### 5.4 Outbox and reconciliation

Frozen event types (9):

- `learning.enrollment.created`
- `learning.progress.updated`
- `learning.course.completed`
- `mentorship.booking.created`
- `mentorship.booking.cancelled`
- `mentorship.session.completed`
- `identity.role.changed`
- `knowledge.index.requested`
- `knowledge.index.completed`

At-least-once transport (Redis) + transactional outbox + consumer dedup; no Redis-only correctness, cross-database 2PC, or exactly-once global assertion. The Keycloak adapter may emit `identity.role.changed` only after canonical mutation outcome has been verified and recorded; ambiguous results stay reconcilable, never announce false success. Audit mutation intent must exist durably before attempting a security-sensitive cross-authority operation, and failures cannot be silently dropped.

## 6. Studio business requirement triage — avoid scope creep

| BR ID | Studio/source requirement or product possibility | Proposed disposition for **LMS initial architecture** | Needed if promoted |
|---|---|---|---|
| BR-01 | Creator-facing systematic worldbuilding education / anti-stagnation | **IN-SCOPE AS CONTENT/CURRICULUM** (existing courses) | Stable lessons, outcomes, release version |
| BR-02 | Audience-facing Asthortera/continuous narrative and civilization laboratory | **IN-SCOPE AS APPROVED REFERENCE/SEARCH ONLY** | Studio attestation, mode/source metadata; no LMS canon writer |
| BR-03 | Current Lore/Backstory/Wiki narrative modes | **METADATA/FACET CANDIDATE** only if source-attested | Index schemas, source citations, no invented modes |
| BR-04 | Published canon immutability, edition and archival | **MANDATORY INTEGRATION CONSTRAINT** whenever Studio material referenced | Versioned provenance, canon release attestation, no silent semantic rewrite |
| BR-05 | Creative Compound Machine and cross-domain causal narrative | **TEACHING/RETRIEVAL CONTENT**; not durable workflow engine | Avoid LLM-generated canonical dependency graph |
| BR-06 | Studio course worksheets and downloadable resources | **IN-SCOPE STATIC DELIVERY** | Pinned asset release URLs, broken-link check |
| BR-07 | User-generated project bible or 30-day journal **persisted in LMS** | **DEFER FROM V1 unless owner explicitly promotes** | Learner-owned submission/entity/API/file storage privacy, consent, retention, rubrics |
| BR-08 | Assessment/rubric submission/grading/mentor review | **DEFER / NEW BUSINESS FEATURE** | Role+object permissions, API/version, audit, Learning vs Mentorship data ownership |
| BR-09 | Mentorship with creator-output review | **DEFER cross-service reviewer workflow**; basic bookings remain in scope | Signed limited cross-service data access, consent, session artifacts |
| BR-10 | Paid private sessions, subscriptions, Patreon/Kickstarter | **DEFER financial/commercial ledger from Mentorship** | Separate payments/entitlements authority, no debt in core learning DB |
| BR-11 | Studio narrative editorial CMS or wiki content CRUD via LMS admin | **OUT OF SCOPE / DISALLOWED BY CURRENT FROZEN CONTRACT** | Major contract revision, Studio editorial approval, separate ownership model |
| BR-12 | Personalization, reader's private notes / favorites on Studio canon | **DEFER until explicit product use case** | New principal privacy/ACL/retention, decision if Learning bookmark family extends |
| BR-13 | Source-approved Studio content searchable via universal Ctrl+K | **IN-SCOPE AS FUTURE AUTHORIZED/STATIC INDEX INTEGRATION** | Separate public vs private rights, rebuild, citation, performance |
| BR-14 | Guest AI or unrestricted LLM-based canon generator | **OUT OF SCOPE INITIAL**, authenticated Assistant only | Abuse/cost/rights contract, prompt/data policy |
| BR-15 | Cross-course creator pathways and prerequisites | **IN-SCOPE AS VERSIONED CATALOG RELATION** | Stable IDs, ordered path validation, cycle checks, completion meaning |
| BR-16 | Institutional equivalence: every lore element = LMS entity | **REJECT** | Creates false domain ownership and runaway service complexity |

**Why defer is a positive explicit decision:** supporting downloadable templates and course outcomes does not require server-side submissions. A future phase can add it when a concrete learner-to-mentor feedback loop and privacy model are approved. Do not implement product architecture based on inferred monetization hopes alone.

## 7. Decision register and ratification gates

| ID | Proposed decision | Recommendation | Owner action / status |
|---|---|---|---|
| ADR-03F-01 | Authority precedence / no crossing LMS-vs-Studio canon | Keep frozen LMS topology + Studio canon publication authority separate | RECOMMENDED; sign-off pending |
| ADR-03F-02 | Public static publication filtering | Enforce published/approved-only route/search/asset build, deny drafts by default | RECOMMENDED; test harness Phase 3B / FE release |
| ADR-03F-03 | Stable ID + historic curriculum revision model | Approve 03E candidates, specify one-time migration and long-term alias/tombstones | RECOMMENDED; sign-off pending |
| ADR-03F-04 | Source-attested Studio reference + rights | Require edition/status/release evidence and access/license policy for every imported reference | RECOMMENDED; sign-off pending |
| ADR-03F-05 | Knowledge ingest trigger ownership | Authenticated internal release-to-Knowledge request; Knowledge owns ingest job and events | PROPOSED; open protocol/auth design |
| ADR-03F-06 | Creator submissions/assessments v1 | **Defer** initial server-side storage/review unless owner chooses scope expansion | NEEDS EXPLICIT PRODUCT DECISION |
| ADR-03F-07 | Paid product/entitlement v1 | Exclude financial ledger and paid access from existing six-service v1 scope | RECOMMENDED; sign-off pending |
| ADR-03F-08 | Internal workload/delegated principal auth | Separate signed identity + workload authentication, fail closed | CRITICAL ADR STILL OPEN |
| ADR-03F-09 | Admin-Keycloak audit reconciliation | Durable operation intent and verified outcomes; no fake atomicity | CRITICAL ADR STILL OPEN |
| ADR-03F-10 | Document split / ledger refresh | Preserve combined historical file; issue separate 03C/03D canonical docs and 03F status overlay | DOCUMENTATION SIGN-OFF PENDING |
| ADR-03F-11 | Availability and capability binding | Document policy for `mentorship/availability` and unused admin-learning capabilities, no silent new route | OPEN CONTRACT DECISION |
| ADR-03F-12 | Resource/cost governance | Prefer PostgreSQL FTS, Redis outbox, external LLM; schedule bounded workers on shared 1-vCPU VPS | RECOMMENDED; measured release budget pending |

### 7.1 Phase 3A design closure — necessary prerequisites (no runtime test claim)

- [ ] Project owner records a positive/negative ratification decision for 03C-2D Identity ADR candidate, 03D Persistence ADR candidates and 03E Catalog candidate; do not mistake 'recommended' for 'FROZEN'.
- [ ] Decide BR-07/08/09: learner artifact/submission/mentor assessment is **deferred** (recommended) or included with expanded contract/versioned API/permissions/data/storage scope.
- [ ] Specify denial-by-default publication filter on all public FE generation paths and list production build artifact checks.
- [ ] Resolve or explicitly gate CC-06 (Git release → authenticated Knowledge ingestion request + producer authority) and CC-10 route-policy ambiguity.
- [ ] Approve separate ADR direction for internal service caller identity, delegation, role revocation freshness, key rotation and spoofing protections (implementation blocked until detailed signed spec).
- [ ] Approve durable audit intent/outcome/reconciliation design for Keycloak administrative mutations; existing HRM no-change constraint explicit.
- [ ] Give standalone canonical identity and persistence documents clear decision status, linking to original concatenated historical evidence rather than erasing it.
- [ ] Refresh `engineering-end-to-end-progress-ledger.md` with 03A–03F evidence, exact referenced SHAs, statuses and open blockers; do not rewrite normative contracts.
- [ ] Trace all 20 I-xx and 24 P1-Ixx to planned acceptance evidence; no signing without a source-to-test matrix.
- [ ] Explicitly record Phase 3A design closure decision and what is deferred to 3B/4–12. **No implementation begins merely because this review is complete.**

### 7.2 Phase 3B/implementation acceptance gates (NOT executed in this review)

- **FE-PRIV-01:** Public export has zero routes, pages, metadata, sitemap entries, JSON search records, and bundled indexes for draft/preview-only content; missing status defaults deny.
- **FE-PRIV-02:** Alias, archived, source-attested published references remain valid; no published route redirects to drafts/private URLs.
- **CM-01:** Manifest canonicalization deterministic under repeated builds; checksum and schema version reflect approved inputs; course revision separate from global hash.
- **CM-02:** Stable lesson IDs unchanged under slug/path rename and graph repairs; moved/split semantic content requires reviewed mapping.
- **LR-01:** Historical enrollments continue to refer to accepted curriculum revision; earned completions not retroactively revoked.
- **KC-01:** Wrong issuer/audience/`azp`/capability denied; client roles filtered and no student default backend authorization.
- **INT-01:** Forge/spoof/replay/stale internal delegations denied by private service.
- **EV-01:** Crash after DB commit before Redis dispatch, duplicated broker deliveries, out-of-order event and Redis outage recover without losing business truth.
- **KN-01:** Private/unattested draft content never surfaced in public snippet, search, embedding, or Assistant citation; invalid releases never promoted.
- **AD-01:** Keycloak role-change ambiguous response remains auditable and reconcilable without false success.
- **MT-01:** Concurrent bookings cannot both allocate capacity-one slot, regardless of different idempotency keys.
- **OPS-01:** HRM auth/scopes/worker unaffected; measured VPS performance/cost/safety adequate.

All tests are *proposed requirements*, not PASS evidence.

## 8. Invariant and global DoD traceability (44 frozen invariants, 16 proposed product DoDs)

### 8.1 Infrastructure invariants I-01..I-20

| Invariant grouping | 03F effect | Disposition |
|---|---|---|
| I-01..I-03 learner/admin/backend hostnames | Separate static FE, only public Gateway | PRESERVED |
| I-04..I-07 Keycloak trust, client separation, authorization | 03C Identity ADR pending signing; no learner-to-admin escalation | PRESERVED AS RULE, UNTESTED |
| I-08 private services, I-17 public ingress | No direct external domain API, authenticated internal trigger | PRESERVED, INTEGRATION TEST OPEN |
| I-09..I-12 PostgreSQL ownership/Redis ephemeral | 4 DBs + source-controlled catalog + outbox | PRESERVED, IMPLEMENTATION PENDING |
| I-13..I-14 hosting/static frontend | Assets versioned, Pages static | PRESERVED |
| I-15..I-16 AI/Cloudflare nonauthority | External LLM, Cloudflare not source of truth | PRESERVED |
| I-18 immutable assets, I-19 versioned API | Release manifests/references source-pinned, 26 routes remain | PRESERVED |
| I-20 justification for complexity | Do not create new service/DB/CMS without proof | PRESERVED |

### 8.2 Logical invariants P1-I01..P1-I24

| Invariant grouping | 03F effect | Disposition |
|---|---|---|
| P1-I01..I07 ownership | Six-service owners remain distinct; Studio canon separate from LMS curriculum | PRESERVED |
| P1-I08..I12 identity & capabilities | JWT+Keycloak+capabilities, no frontend fallback | PRESERVED; 03C proof pending |
| P1-I13..I14 API ingress | 26 frozen routes / Gateway only | PRESERVED |
| P1-I15..I17 no cross-DB write, no distributed TX, outbox | Local durable producer and consumer receipts | PRESERVED; 03D pending ratification |
| P1-I18..I19 public/private search | Draft never public; Knowledge private ACL | PRESERVED; FE gap to remediate |
| P1-I20..I21 Assistant authorization | Only via domain APIs, authenticated-only initial | PRESERVED |
| P1-I22..I24 content CRUD exclusion, instructor admin plane, identity projections | Source-controlled catalog, no shared user DB | PRESERVED |

### 8.3 Global DoD 01..16 classification

| DoD | Affected contract/review | Current evidence state |
|---|---|---|
| DOD-01 governance | 03A–03F and owner ratifications | PENDING |
| DOD-02 service/runtime independence | Phase 2D skeleton + Phase 4 deploy | PARTIAL FOUNDATION |
| DOD-03 identity | 03C ADR / Keycloak clients absent | PENDING |
| DOD-04 API/OpenAPI | 26 routes, schema not implemented | PENDING |
| DOD-05 catalog/history | 03E + publication filter | DRAFT |
| DOD-06 Learning durable journey | 03D + 03E | PENDING |
| DOD-07 Mentorship | 03D slot/idempotency | PENDING |
| DOD-08 Audit/admin | 03C + 03D reconciliation | PENDING |
| DOD-09 Knowledge | 03E + 03F ingest/ACL | PENDING |
| DOD-10 Assistant | 03C + 03E provenance | PENDING |
| DOD-11 learner/admin FE | FE-PRIV + OIDC cutover | PENDING |
| DOD-12 private/TLS boundaries | Phase 4/11 probes | PENDING |
| DOD-13 CI/CD | Phase 3B and release jobs | PENDING |
| DOD-14 reliability/backup | Outbox, restore/failure drills | PENDING |
| DOD-15 performance/spending | 1-vCPU shared runtime measured before capacity promises | PENDING |
| DOD-16 release certification | Evidence-based final signoff | PENDING |

## 9. Proposed documentation-only change set (NOT APPLIED)

Do **not** silently rewrite binding contracts or delete historical combined files. A future docs-only change (explicitly approved) may:

1. Create `lms/reltroner-lms-phase3a-03f-cross-contract-business-reconciliation-20261009.md` using this standalone review text, status `DESIGN REVIEW COMPLETE / NOT FROZEN`.
2. Copy 03D content from historical file lines 449–821 into a standalone `lms/reltroner-lms-phase3a-03d-persistence-event-model-20261009.md`, preserving exact content and original source link, marking review candidate.
3. Add standalone Identity ADR from lines 200–448 as `lms/adr-lms-kc-001-identity-provisioning.md` with provenance to original, retaining `NOT HUMAN-RATIFIED` until signed.
4. Update living ledger sections 0, 2, 3, 10, 11, 12 and 14 with dated append-only checkpoint log. Pin reviewed file/blob/commit IDs and list CC-01..22 and BR-01..16, keeping 20+24 invariants unchanged.
5. Optionally create a single decision index linking all ADRs/fixtures and an explicit source hierarchy. Do **not** promote pending candidates to FROZEN, edit `LMS-FE` or `LMS-BE`, or provision anything as a side effect of archival.

### 9.1 Minimal living-ledger status overlay — ready to review

```markdown
### Phase 3A-03F (2026-10-09) — Cross-contract review
- Result: design review complete; architecture ratification and freeze PENDING.
- Sources: Studio constitution v2.2, six-service LMS-BE baseline, LMS-FE catalog snapshot,
  Keycloak 3A-03C evidence, 3A-03D Persistence draft and 3A-03E Manifest draft.
- High-impact FE source risk: draft content is included in static route/search generation
  without a publication filter; production leakage not verified; release blocked pending test.
- No change to frozen 20 physical / 24 logical invariants; 26 API operations,
  19 capabilities, nine event families and four logical DB ownership domains preserved.
- Business expansion: learner submissions/review and paid flows explicitly deferred pending
  owner decision and a versioned contract; Studio canon authority remains external to LMS.
- Unresolved: internal service trust, Keycloak/admin Audit reconciliation, Knowledge
  release ingestion origin, manifest/ID historical policy, FE public publication gates,
  authoritative ADR sign-offs, cross-release compatibility and CI acceptance.
- No production mutation and no code implementation were performed for 3A-03F.
```

## 10. Next deterministic engineering action

**Checkpoint:** `3A-03F DESIGN REVIEW COMPLETED / CONTRACT FREEZE BLOCKED`. The next work item should be **3A-04 — Decision Ratification + Phase 3A Freeze Readiness**, *not* immediate provisioning or Laravel implementation. Specifically: review CC-01/02/06/08/12/15/20 and ADR-03F-01..12; decide whether creator artifact storage/submissions are in v1; accept or revise all nonfrozen ADR drafts; normalize documentation; define exact Phase 3B entry/exit controls. Once sign-offs are recorded, move to 3B *contract+CI design/implementation*, and keep Phase 4 (provisioning) separately gated.

**Hard stop:** source design does not demonstrate production security, correctness, privacy or publication readiness. No token, key, production DB, DNS/TLS, invoice, package upgrade or deployment action is authorized by this document.

---

## Source references (read using connected GitHub)

1. `https://github.com/Reltroner/progress-documentation/tree/main/lms`
2. `https://github.com/Reltroner/progress-documentation/blob/main/lms/master-infrastructure-placement-contract.md`
3. `https://github.com/Reltroner/progress-documentation/blob/main/lms/logical-service-boundary-api-contract.md`
4. `https://github.com/Reltroner/progress-documentation/blob/main/lms/engineering-end-to-end-progress-ledger.md`
5. `https://github.com/Reltroner/progress-documentation/blob/main/lms/reltroner-lms-phase3a-03c-2d-provisioning-adr-review-20261009.md`
6. `https://github.com/Reltroner/progress-documentation/blob/main/lms/reltroner-lms-phase3a-03e-catalog-manifest-versioning-20261009.md`
7. `https://github.com/Reltroner/progress-documentation/blob/main/lms/reltroner-lms-catalog-manifest-v1.candidate.schema.json`
8. `https://github.com/Reltroner/progress-documentation/blob/main/lms/reltroner-lms-catalog-manifest-v1.partial-example.json`
9. `https://github.com/Reltroner/reltroner-studio/blob/main/content/principles/reltroner-studio-master-source-of-truth.md`
10. `https://github.com/Reltroner/LMS-FE/tree/f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7`
11. `https://github.com/Reltroner/LMS-BE/tree/e30a61780994d85671cbf079e6b9ce899b3fe837`

---

_Extracted without semantic changes from historical combined source `reltroner-lms-phase3a-03e-catalog-manifest-versioning-20261009.md` (blob `37dd58c64fddce8d9c49081f5510bbddfbacb491`). Review complete, **NOT phase freeze**._
