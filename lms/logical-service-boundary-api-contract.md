# Reltroner LMS — Logical Service Boundary & API Contract

> **Document type:** Binding logical service and API contract  
> **Architecture phase:** Phase 1 — Logical Service Boundary & API Contract Discovery  
> **Status:** **FROZEN**  
> **Version:** 1.0.0  
> **Effective date:** 2026-10-07  
> **Project:** Reltroner LMS  
> **Architecture style:** Microservices  
> **Parent contract:** `lms/master-infrastructure-placement-contract.md`

---

## Current implementation status addendum — 2026-10-09 (living cross-reference, no invariant change)

> **Important historical reading rule:** This file's original `Status: FROZEN`, 2026-10-07 Phase 1 status table, “backend repository currently empty” discovery (`3.5`), and “next Phase 2” (`43`) record **the state at Phase 1 freeze time**. They must **not** be interpreted as live engineering status on 2026-10-09. All normative Phase 1 service boundaries and invariants P1-I01–P1-I24 remain unchanged and binding.
>
> **Living status and AI handoff source:** [End-to-End Engineering Progress Ledger](./engineering-end-to-end-progress-ledger.md). It tracks historical checkpoints, exact source SHA, outstanding work, risks, proposed implementation phases, and traceable final Definition of Done. If an implementation assertion conflicts with the FROZEN contract, the contract prevails until an approved ADR/versioned revision.

### 2026-10-09 verified backend checkpoint

- `Reltroner/LMS-BE/main`: **`e30a61780994d85671cbf079e6b9ce899b3fe837`**, [merge PR #1](https://github.com/Reltroner/LMS-BE/pull/1); includes pre-merge foundation freeze `56913175208bc49b4ebbf00fd889eccf1edf03e0`.
- Phase **2D Backend Foundation & Service Skeleton**: **ACCEPTED / FROZEN / MERGED**, with Gateway, Learning, Mentorship, Knowledge, Assistant and Audit independently scoped Laravel `13.35.0` applications in one repository (**not** a modular monolith).
- Verified accepted foundation inventory: **283 tracked service files** (Gateway 48, five private services 47 each), **107 locked Composer packages per service**, aggregate **100 tests/725 assertions**, **6/6** independent HTTP probes and **6/6** Composer audits reporting no advisories **at test time**. All source hashes and Git ancestry were verified in provided PowerShell acceptance logs.
- Correct latest Gateway HTTP freeze SHA is **`e3f4f9b569cc9b7d64be874fa8242a2afa98146a`**; its earlier foundation SHA `2763882589b90cff75e82e0854a94f5019ba5f66` is historical and **must not** be used as the latest Gateway comparison baseline.
- API foundation currently exposes health only; **business `/api/v1` endpoints, real Keycloak authorization, service-to-service identity, four service-owned database schemas, durable outbox, Knowledge ingestion, Assistant inference, and production runtime certification remain PENDING**. Phase 2D acceptance is **not** final-product DoD.
- `LMS-BE` snapshot contains **no repository GitHub Actions workflows**; passed local tests should be formalized into six-service CI and contract tests before future releases.

### Drift/remediation to carry into controlled future phases

- `LMS-FE` observed `main` snapshot `f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7` still shows old `sso.reltroner.com` / `lms-reltroner` in `.env.example`; cut over to the canonical `auth.reltroner.com/realms/reltroner` and two-client `lms-user`/`lms-admin` configuration **only after discovery, agreed mapping and negative tests**.
- Frontend `extractRoles()` still has UI-only fallback to `student`. Backend authorization **must deny missing capability**, as already required by P1-I12; do not silently grant permissions based on UX roles.
- Existing learner-host `/admin` and `/instructor` are **legacy UX**, not authorization boundaries; privileged workflows target `lms-admin.reltroner.com`.
- The initial **Git-owned catalog manifest**, owner-scoped PostgreSQL persistence, authenticated internal HTTP contracts, and audited administrative changes are planned obligations, not Phase 2D functionality.
- Phase **3A Cross-Service Integration Contract Discovery** and subsequent Phase 3–12 implementation stages are **candidate roadmap items**, not approved/frozen later phases. See ledger for per-gate entry/exit and full DoD traceability.

**Change-control note:** This dated addendum updates implementation context only; it does **not** authorize production mutations or modify any of the original Phase 1 ``4–45` commitments. Changes to binding semantics still require a versioned contract revision or explicit ADR.

---

## 1. Purpose

This document defines the authoritative logical service boundaries, domain ownership, API surface, identity/authorization model, service-to-service integration rules, event consistency rules, and source-of-truth boundaries for Reltroner LMS.

It is intentionally independent from implementation framework details.

This contract is derived from:

1. the frozen Phase 0 infrastructure contract,
2. read-only discovery of the existing `Reltroner/LMS-FE` repository,
3. the empty `Reltroner/LMS-BE` repository,
4. the existing static course/content model,
5. the existing Keycloak OIDC integration,
6. the required public surfaces:
   - `lms.reltroner.com`
   - `lms-admin.reltroner.com`
   - `lms-api.reltroner.com`.

No backend implementation may silently redefine domain ownership declared here.

---

## 2. Phase status

| Phase | Status |
|---|---|
| Phase 0A — VPS / Network / Runtime Discovery | ✅ PASS |
| Phase 0B — Cloudflare + Premium Hosting Discovery | ✅ PASS |
| Phase 0C — Master Infrastructure Placement Contract | ✅ FROZEN |
| Phase 1A — Existing Domain / Frontend Discovery | ✅ PASS |
| Phase 1B — Logical Service Ownership | ✅ FROZEN |
| Phase 1C — Public API Contract | ✅ FROZEN |
| Phase 1D — Identity / Authorization Contract | ✅ FROZEN |
| Phase 1E — Inter-service Consistency / Events | ✅ FROZEN |
| Phase 1 — Logical Service Boundary & API Contract | ✅ FROZEN |

Application bootstrap may begin only after this contract is committed.

---

## 3. Existing repository discovery

### 3.1 Learner frontend

The existing `Reltroner/LMS-FE` repository is a static-export Next.js application.

Observed characteristics:

- Next.js 16
- React 19
- `output: "export"`
- Contentlayer/MDX lesson content
- typed TypeScript catalog
- static course registry
- static learning-path registry
- static resource registry
- static client-side search index
- OIDC Authorization Code flow
- PKCE
- frontend route/role gates
- no backend API
- no database
- no server session
- no SSR runtime dependency

### 3.2 Existing content model

Current source-controlled content contains the following concepts:

```text
Course
├── Module
│   └── Lesson
├── Resource
└── Path membership

Learning Path
└── ordered Course references
```

Existing lesson metadata includes:

- title
- summary
- kind
- status
- level
- duration
- objectives
- outputs
- tags
- resources

Existing content statuses:

```text
draft
published
archived
```

### 3.3 Existing authentication model

Existing frontend OIDC code currently understands coarse roles:

```text
student
instructor
admin
```

Existing `/admin` and `/instructor` routes are frontend UX gates only.

They are not authorization boundaries.

### 3.4 Existing configuration drift

The current frontend still contains references to:

```text
https://sso.reltroner.com/realms/reltroner
```

while the frozen infrastructure contract establishes:

```text
https://auth.reltroner.com/realms/reltroner
```

as the canonical issuer.

This is implementation debt and must be corrected during the controlled identity cutover.

### 3.5 Backend repository

`Reltroner/LMS-BE` is currently empty.

Therefore no legacy backend domain ownership exists that must be preserved.

---

## 4. Core logical architecture

The initial logical architecture contains:

```text
                        PUBLIC CLIENTS
                 ┌──────────────┴──────────────┐
                 │                             │
                 ▼                             ▼
        Learner Frontend               Admin Frontend
        lms.reltroner.com              lms-admin.reltroner.com
                 │                             │
                 └──────────────┬──────────────┘
                                ▼
                       LMS API GATEWAY
                     lms-api.reltroner.com
                                │
           ┌────────────────────┼───────────────────────┐
           │                    │                       │
           ▼                    ▼                       ▼
     Learning Service     Mentorship Service      Knowledge Service
           │                    │                       │
           │                    │                       └─────────────┐
           │                    │                                     ▼
           │                    │                              Assistant Service
           │                    │                                     │
           │                    │                                     ▼
           │                    │                              External LLM
           │                    │
           └────────────┬───────┴───────────────────┐
                        │                           │
                        ▼                           ▼
                   Audit Service               Redis runtime

External authoritative contexts:

Keycloak
→ identity authority

Git / LMS content repository
→ course/module/lesson/path/resource content authority
```

---

## 5. Runtime services

The following runtime service boundaries are frozen for the initial backend architecture:

1. **LMS API Gateway**
2. **Learning Service**
3. **Mentorship Service**
4. **Knowledge Service**
5. **Assistant Service**
6. **Audit Service**

Keycloak is an external identity context, not an LMS microservice.

The source-controlled Content Catalog is a logical bounded context but is **not** a runtime microservice in the initial architecture.

---

## 6. Content Catalog Context

### 6.1 Authority

Canonical public course content remains source-controlled for the initial architecture.

Authority includes:

- Course
- Module
- Lesson
- Learning Path
- public Resource metadata
- content status
- lesson ordering
- module ordering
- course/path relationships
- author metadata

Current source:

```text
Reltroner/LMS-FE
content/
src/catalog/
```

A later repository decomposition may move content elsewhere, but content must remain a versioned source-controlled authority unless a future ADR explicitly introduces a runtime authoring system.

### 6.2 No initial Content CRUD API

The initial LMS API does **not** expose generic mutable CRUD endpoints such as:

```text
POST   /courses
PATCH  /courses/{id}
DELETE /lessons/{id}
```

for canonical course content.

Content publishing remains a source-controlled build/deployment workflow in the initial architecture.

This preserves:

- static-first delivery,
- reproducible builds,
- reviewable content changes,
- deterministic course versions,
- low backend load.

### 6.3 Catalog manifest

The content build pipeline must eventually emit a machine-readable versioned catalog manifest.

Conceptual shape:

```json
{
  "schema_version": 1,
  "catalog_version": "<immutable version/hash>",
  "courses": [],
  "paths": []
}
```

The manifest is the integration artifact consumed by backend services that need to validate content identifiers.

The manifest does not replace the source-controlled content authority.

---

## 7. LMS API Gateway

### 7.1 Ownership

The Gateway owns **public API ingress behavior**, not domain business state.

Responsibilities:

- JWT/OIDC token validation
- issuer/audience validation
- approved-client validation
- request/correlation ID generation
- public route versioning
- CORS enforcement
- request size limits
- rate-limit context
- service routing
- timeout policy
- public error normalization
- aggregation only where explicitly defined
- identity-provider adapter calls where infrastructure-level identity integration is required

### 7.2 Forbidden Gateway ownership

The Gateway must not become the canonical owner of:

- enrollment
- progress
- bookmarks
- course content
- mentorship bookings
- search documents
- assistant knowledge
- audit history

The Gateway should remain stateless by default.

No `lms_gateway_db` is created unless a later concrete durable Gateway-owned requirement exists.

---

## 8. Learning Service

### 8.1 Authority

Learning Service owns learner-specific LMS state.

Canonical concepts:

- Enrollment
- Course learning state
- Lesson progress
- Course completion state
- Bookmark / saved learning item
- learner-specific learning preferences when they are not identity attributes

Learning Service references source-controlled catalog identifiers but does not own canonical course content.

### 8.2 Identity reference

Learner ownership is keyed to the Keycloak principal:

```text
principal_id = OIDC subject (sub)
```

Learning Service does not own passwords, primary email verification, MFA, or external identity-provider linkage.

### 8.3 Data authority

Initial database:

```text
lms_learning_db
```

Only Learning Service may write this database.

### 8.4 Initial invariants

- one active enrollment per principal/course unless a future business rule explicitly supports repeated cohorts/runs,
- progress belongs to the authenticated principal unless an explicit privileged override is authorized,
- progress references valid catalog identifiers,
- completion state must be derivable from durable learning state,
- removal or renaming of source content must not silently destroy historical progress.

---

## 9. Mentorship Service

### 9.1 Authority

Mentorship Service owns the mentorship/private-session domain.

Canonical concepts:

- Mentor profile projection relevant to mentorship
- Mentorship Offering
- Availability Window / Slot
- Booking
- Session lifecycle
- cancellation state
- attendance/session outcome where required
- learner feedback where required
- external meeting-provider reference

### 9.2 External meeting providers

Zoom or another meeting provider is an adapter, not the source of truth for the LMS booking.

Mentorship Service remains authoritative for booking/session state.

### 9.3 Data authority

Initial database:

```text
lms_mentorship_db
```

Only Mentorship Service may write this database.

### 9.4 Financial boundary

Payment processing, accounting, payouts, and financial ledger authority are **not** included in the initial Mentorship Service contract.

If paid mentorship requires payment integration, a future financial/payment contract must define that boundary separately.

---

## 10. Knowledge Service

### 10.1 Authority

Knowledge Service owns searchable/indexed representations and permission-aware retrieval.

It may index:

- public course content
- lesson metadata
- learning paths
- approved public resources
- permission-bound LMS knowledge
- mentorship-related knowledge when explicitly allowed
- future private documents when explicitly allowed

### 10.2 Derived-state rule

Knowledge indexes are derived state.

Knowledge Service is not the canonical source of:

- course content
- enrollment
- progress
- booking state
- identity state

Indexes must be rebuildable from their authoritative sources.

### 10.3 Initial search engine

Initial implementation should prefer PostgreSQL full-text/search capabilities.

A dedicated search daemon is not introduced in Phase 1.

### 10.4 Data authority

Initial database:

```text
lms_knowledge_db
```

This database may contain:

- normalized searchable documents,
- index metadata,
- ingestion checkpoints,
- permission metadata,
- future embeddings if an ADR approves them.

---

## 11. Public static search vs authorized search

The existing learner frontend already contains a static public search index.

That architecture remains valid.

### Public search

Public course/path/lesson search should remain edge/static whenever practical:

```text
Cloudflare Pages
→ static search index
→ browser
```

### Authorized search

Private or permission-bound search uses:

```text
browser
→ lms-api.reltroner.com
→ Knowledge Service
```

### Universal Ctrl+K behavior

A future universal Ctrl+K experience may merge:

1. local/static public search results,
2. authorized Knowledge Service results.

The browser must not receive documents it is not authorized to access.

---

## 12. Assistant Service

### 12.1 Authority

Assistant Service owns AI orchestration behavior.

Responsibilities:

- authorization-aware query intake
- context assembly
- tool selection
- Knowledge Service retrieval
- limited Learning/Mentorship tool invocation through explicit APIs
- prompt/system-policy composition
- external LLM invocation
- response normalization
- safety and tool-boundary enforcement

### 12.2 Non-authority

Assistant Service must not become the canonical source of:

- learning progress
- enrollment
- mentorship bookings
- course content
- identity
- permissions

An LLM response can never directly mutate domain state.

All mutations must invoke explicit domain APIs with the same authorization/invariant checks as non-AI callers.

### 12.3 Initial persistence posture

Initial Assistant Service should remain stateless or short-lived where practical.

Short-lived conversation context may use Redis with TTL.

Durable chat history is not created by default.

If durable assistant history becomes a product requirement, a separate persistence decision must be documented before adding an assistant database.

### 12.4 Guest access

Initial permission-aware Assistant API is authenticated-only.

Guest public discovery remains supported by public course content and static search.

Guest AI access requires a future abuse/cost-control contract.

---

## 13. Audit Service

### 13.1 Authority

Audit Service owns append-only durable administrative/security audit records for LMS actions that require accountability across domains.

It answers:

```text
WHO
did WHAT
to WHICH RESOURCE
WHEN
with WHICH RESULT
```

### 13.2 Required event classes

At minimum, the audit model must support privileged events such as:

- role/permission administrative changes,
- mentorship administrative mutation,
- progress override if ever permitted,
- destructive actions,
- sensitive configuration changes,
- content release/publish actions when integrated,
- security-sensitive administrative actions.

### 13.3 Data authority

Initial database:

```text
lms_audit_db
```

Audit records are append-only from the application perspective.

### 13.4 Audit is not analytics

Audit truth must not be replaced by browser analytics or Cloudflare analytics.

---

## 14. Identity boundary

### 14.1 Keycloak ownership

Keycloak owns:

- subject identity
- credentials
- password lifecycle
- MFA
- email verification
- identity-provider federation
- primary login session
- identity-level role assignments

Canonical issuer:

```text
https://auth.reltroner.com/realms/reltroner
```

### 14.2 LMS-local data

LMS services may reference:

```text
principal_id = sub
```

but must not treat copied email/name fields as identity authority.

Copied identity attributes are projections/cache only.

### 14.3 No LMS password management

Neither learner nor admin LMS applications implement local password management.

Account credential changes remain with Keycloak/Reltroner Identity.

---

## 15. OIDC clients and API audience

The initial target trust contexts are:

```text
lms-user
lms-admin
lms-api
```

### Public browser clients

```text
lms-user
→ lms.reltroner.com

lms-admin
→ lms-admin.reltroner.com
```

Both are public OIDC clients using Authorization Code + PKCE.

### Protected resource audience

Backend access tokens must target:

```text
aud = lms-api
```

The API must validate at minimum:

- signature
- `iss`
- `aud`
- `exp`
- `nbf` where present
- authorized client / `azp` context
- required capability/permission

---

## 16. Authorization model

### 16.1 Coarse personas

Coarse realm personas may remain:

```text
student
instructor
admin
```

These are not sufficient by themselves for sensitive API authorization.

### 16.2 Capability permissions

Backend authorization is capability-oriented.

Initial permission namespace:

```text
learning.enrollment.read.self
learning.enrollment.create.self
learning.progress.read.self
learning.progress.write.self
learning.bookmark.read.self
learning.bookmark.write.self

mentorship.offering.read
mentorship.booking.read.self
mentorship.booking.create.self
mentorship.booking.cancel.self

knowledge.search
assistant.use

admin.principal.read
admin.principal.role.manage
admin.mentorship.read
admin.mentorship.manage
admin.learning.read
admin.learning.override
admin.audit.read
```

Exact implementation may use Keycloak client roles/scopes, but external API authorization must evaluate capabilities.

### 16.3 Realm-role mapping

Recommended model:

```text
Realm role
→ coarse persona

lms-api client role / permission
→ API capability
```

The backend authorizes capabilities, not frontend route labels.

### 16.4 Frontend fallback warning

The current frontend behavior that defaults an authenticated user with no recognized role to `student` is UX-only legacy behavior.

The backend must **not** default missing authorization claims to student capabilities.

Backend authorization fails closed.

---

## 17. Instructor placement

There is no separate `lms-instructor.reltroner.com` surface.

Privileged instructor workflows use:

```text
lms-admin.reltroner.com
```

with permission-limited navigation and APIs.

The current learner frontend `/instructor` route is legacy UX and is not a future security boundary.

Initial content authoring remains source-controlled rather than mutable browser CRUD.

Instructor capabilities can later include mentorship or content-review operations as explicit permissions.

---

## 18. Learner/admin frontend responsibilities

### Learner frontend

Owns presentation and local UI state for:

- public catalog browsing,
- lesson rendering,
- learning-path rendering,
- public static search,
- authenticated learner UX.

It does not own durable business state.

### Admin frontend

Owns presentation and local UI state for:

- privileged operations,
- mentorship administration,
- user/principal administration adapters,
- audit views,
- future operational dashboards.

It does not own authorization truth.

---

## 19. Public API versioning

All business API routes use:

```text
/api/v1
```

Health/readiness endpoints may exist outside business versioning:

```text
/health/live
/health/ready
```

Breaking API changes require a new major API version or explicit compatibility strategy.

---

## 20. Initial external API resource map

This section freezes resource families and ownership, not every final response field.

### 20.1 Identity / principal projection

```http
GET /api/v1/me
```

Returns an LMS-safe authenticated principal projection and effective LMS capabilities.

It must not expose tokens or Keycloak administrative internals.

### 20.2 Learning

```http
GET  /api/v1/learning/enrollments
POST /api/v1/learning/enrollments
GET  /api/v1/learning/enrollments/{enrollment_id}

GET  /api/v1/learning/courses/{course_id}/progress
PUT  /api/v1/learning/courses/{course_id}/lessons/{lesson_id}/progress

GET    /api/v1/learning/bookmarks
PUT    /api/v1/learning/bookmarks/{content_id}
DELETE /api/v1/learning/bookmarks/{content_id}
```

### 20.3 Mentorship

Public/readable offerings may be exposed without login if product policy permits:

```http
GET /api/v1/mentorship/offerings
GET /api/v1/mentorship/offerings/{offering_id}
```

Authenticated booking operations:

```http
GET  /api/v1/mentorship/availability
GET  /api/v1/mentorship/bookings
POST /api/v1/mentorship/bookings
GET  /api/v1/mentorship/bookings/{booking_id}
POST /api/v1/mentorship/bookings/{booking_id}/cancel
```

### 20.4 Knowledge

```http
GET /api/v1/knowledge/search
```

This endpoint is for backend/authorized search.

Public static search does not require this endpoint.

### 20.5 Assistant

```http
POST /api/v1/assistant/query
```

The initial contract is request/response.

Streaming transport, if later required, must be specified separately. WebSockets are not required by this contract.

### 20.6 Admin principal operations

```http
GET   /api/v1/admin/principals
GET   /api/v1/admin/principals/{principal_id}
PATCH /api/v1/admin/principals/{principal_id}/roles
```

These endpoints act through an approved Keycloak administrative adapter.

They do not create a second identity database.

### 20.7 Admin mentorship

```http
GET   /api/v1/admin/mentorship/bookings
GET   /api/v1/admin/mentorship/bookings/{booking_id}
PATCH /api/v1/admin/mentorship/bookings/{booking_id}
```

### 20.8 Admin audit

```http
GET /api/v1/admin/audit-events
GET /api/v1/admin/audit-events/{audit_event_id}
```

### 20.9 Content mutation exclusion

Generic canonical content CRUD is intentionally excluded from API v1 initial scope.

---

## 21. HTTP semantics

### 21.1 Read operations

Use:

```text
GET
```

for side-effect-free retrieval.

### 21.2 Idempotent state replacement

Use:

```text
PUT
```

for naturally idempotent learner state such as lesson progress or bookmarks.

### 21.3 Creation/commands

Use:

```text
POST
```

for creation and explicit domain commands such as booking cancellation when the command has domain semantics.

### 21.4 Partial privileged mutation

Use:

```text
PATCH
```

for controlled partial administrative updates.

### 21.5 Deletion

`DELETE` is used only where deletion is genuinely the domain behavior.

Historical/auditable business records should normally use lifecycle state rather than destructive deletion.

---

## 22. API response and error contract

### 22.1 JSON

Business APIs use JSON unless a future endpoint explicitly requires another representation.

### 22.2 Errors

Errors should use a Problem Details-compatible shape:

```json
{
  "type": "https://lms.reltroner.com/problems/example",
  "title": "Example problem",
  "status": 409,
  "detail": "Human-readable explanation.",
  "code": "DOMAIN_CODE",
  "request_id": "..."
}
```

Response media type:

```text
application/problem+json
```

Internal stack traces, SQL, filesystem paths, secrets, or service internals must never be returned publicly.

### 22.3 Request correlation

Every public API request must have a request/correlation identifier.

If a trusted incoming ID is not accepted, the Gateway generates one.

---

## 23. Collection contract

Collection APIs that can grow materially must use bounded pagination.

Cursor pagination is preferred.

Conceptual response:

```json
{
  "data": [],
  "page": {
    "next_cursor": null
  }
}
```

Unbounded `GET all` APIs are prohibited for large administrative collections.

---

## 24. External identifiers

API identifiers are opaque strings.

Clients must not infer database topology, sequence count, shard, or service internals from an identifier.

Exact UUID/ULID format is an implementation detail unless a later contract freezes it.

Catalog identifiers remain stable source-controlled IDs.

---

## 25. Idempotency

Operations vulnerable to duplicate submission must support idempotency.

At minimum:

```text
POST /api/v1/mentorship/bookings
```

must support an `Idempotency-Key` contract before production payment/booking workflows.

Other critical creation commands may adopt the same mechanism.

Idempotency records must not rely only on ephemeral Redis when correctness depends on them.

---

## 26. Service-to-service synchronous transport

Initial synchronous internal service calls use:

```text
HTTP + JSON over loopback/private VPS interfaces
```

Internal services must bind only to localhost/private interfaces.

Conceptual path:

```text
Gateway
→ 127.0.0.1 internal ingress
→ domain service
```

Requirements:

- explicit timeout,
- request ID propagation,
- authentication/trust between internal callers,
- bounded response size,
- no infinite retries,
- no public DNS dependency,
- no direct database fallback when a service is unavailable.

Internal network transport does not waive domain authorization/invariants.

---

## 27. Asynchronous transport and domain events

Redis may be used as the initial queue/event delivery transport.

However Redis is not durable business truth.

For events whose loss would break correctness, services use a transactional outbox pattern:

```text
domain transaction
    │
    ├── business row(s)
    └── outbox row
        COMMIT atomically
             │
             ▼
        publisher worker
             │
             ▼
          Redis
             │
             ▼
         consumer
```

If Redis is lost, unpublished outbox records remain durable and can be replayed.

Consumers of correctness-critical events must be idempotent.

An inbox/deduplication record may be used where repeated delivery is possible.

---

## 28. Initial domain event families

Candidate event names are frozen at semantic level; exact payload schemas are implementation work.

Learning:

```text
learning.enrollment.created
learning.progress.updated
learning.course.completed
```

Mentorship:

```text
mentorship.booking.created
mentorship.booking.cancelled
mentorship.session.completed
```

Identity integration:

```text
identity.role.changed
```

Knowledge ingestion:

```text
knowledge.index.requested
knowledge.index.completed
```

Audit:

Privileged mutations produce auditable records even when no cross-service event is needed.

---

## 29. Consistency model

Reltroner LMS does not use distributed database transactions across services.

Each service transaction is local to its owned database.

Cross-service workflows use:

- explicit synchronous calls where immediate confirmation is required,
- durable outbox/event workflows where eventual consistency is acceptable.

The system must define compensating behavior instead of attempting cross-database two-phase commit.

---

## 30. Service ownership matrix

| Concept | Authoritative owner |
|---|---|
| Password / MFA / login credentials | Keycloak |
| Subject identity / primary identity claims | Keycloak |
| Realm persona role assignment | Keycloak |
| Course | Content Catalog |
| Module | Content Catalog |
| Lesson | Content Catalog |
| Learning Path | Content Catalog |
| Public Resource metadata | Content Catalog |
| Enrollment | Learning Service |
| Lesson Progress | Learning Service |
| Course Completion | Learning Service |
| Bookmark | Learning Service |
| Mentorship Offering | Mentorship Service |
| Availability | Mentorship Service |
| Booking | Mentorship Service |
| Session lifecycle | Mentorship Service |
| Search index | Knowledge Service |
| Search ingestion checkpoint | Knowledge Service |
| AI orchestration | Assistant Service |
| Durable admin audit event | Audit Service |
| Public API routing | LMS API Gateway |
| Public static search index | Build-time frontend artifact |
| Browser UI state | Corresponding frontend only |

---

## 31. Database ownership

Initial logical databases:

```text
lms_learning_db
lms_mentorship_db
lms_knowledge_db
lms_audit_db
```

No initial durable database is required for:

```text
LMS API Gateway
Assistant Service
```

unless a concrete requirement appears.

Binding rules:

- only the owning service has write credentials,
- services do not perform cross-database joins,
- services do not reuse another service's ORM models,
- shared PostgreSQL instance does not mean shared business schema,
- migrations are service-owned.

---

## 32. Admin content model

The presence of `lms-admin.reltroner.com` does not imply runtime course CRUD.

Initial admin content behavior may include:

- read-only catalog status,
- release/version visibility,
- validation status,
- publication pipeline visibility,
- links into source-controlled authoring workflow.

Canonical content modification remains source-controlled in the initial architecture.

A future browser-native content authoring product requires a separate Content Authoring Service ADR/contract.

---

## 33. Profile ownership

Identity attributes such as:

- name,
- primary email,
- preferred username,
- credential settings,

remain Keycloak-owned.

Application-specific learning preferences may be stored by Learning Service only if needed.

Mentor-specific public/professional profile information required for mentorship belongs to Mentorship Service.

No generic shared `users` table is created merely to duplicate Keycloak.

---

## 34. Admin role management

The LMS admin API may expose limited principal/role administration through a Keycloak adapter.

Rules:

- Keycloak remains canonical,
- the LMS does not directly edit Keycloak database tables,
- only approved role/capability operations are exposed,
- every privileged change is audited,
- the admin frontend never receives Keycloak administrator credentials.

---

## 35. Security boundary

A browser can never be trusted as the authorization authority.

The following are insufficient for backend privilege:

- hidden buttons,
- route guards,
- `RoleGate`,
- frontend `student/instructor/admin` checks,
- client-supplied principal IDs.

Backend services derive principal identity from validated authentication context.

Self-service endpoints must not allow the caller to choose another principal arbitrarily.

---

## 36. Assistant tool boundary

Assistant Service may call tools only through explicitly approved interfaces.

Examples:

```text
search knowledge
read own learning progress
read own mentorship bookings
create a booking only through Mentorship API
update progress only through Learning API
```

The assistant must never:

- write another service's database,
- execute arbitrary SQL,
- bypass authorization,
- invent a successful mutation,
- treat generated text as a committed transaction.

Mutation tools must return authoritative service results.

---

## 37. Analytics posture

Analytics is initially a derived/read-model concern, not a canonical domain.

Potential sources:

- Cloudflare edge analytics,
- application metrics,
- domain events,
- PostgreSQL read models,
- audit data where semantically appropriate.

Analytics must not become the source of truth for business state.

No dedicated analytics microservice is required in Phase 1.

---

## 38. Current legacy frontend routes

Current `LMS-FE` contains:

```text
/admin
/instructor
/profile
```

Phase 1 target:

- learner account/profile experience remains on `lms.reltroner.com`,
- privileged instructor/admin workflows move to `lms-admin.reltroner.com`,
- current learner-host `/admin` and `/instructor` pages are migration/legacy UX only,
- backend authorization does not depend on those routes.

Their removal/migration belongs to implementation phases.

---

## 39. Current legacy documentation

Existing LMS auth documentation contains historical references to:

```text
sso.skill-wanderer.com
sso.reltroner.com
lms-reltroner
```

and older statements that authentication/RBAC were not yet implemented.

Those documents remain historical implementation notes.

This Phase 1 contract plus the Phase 0 infrastructure contract govern future architecture.

---

## 40. Explicitly rejected logical designs

The initial architecture rejects:

### Shared business database

```text
all LMS services
→ one shared writable schema
```

### Gateway monolith

```text
Gateway
→ owns all domain logic
→ owns all tables
```

### Frontend-owned authorization

```text
RoleGate == security boundary
```

### Runtime canonical course CRUD

without an explicit Content Authoring architecture decision.

### Assistant direct writes

```text
LLM
→ database
```

### Cross-service ORM

```text
Learning model
→ joins Mentorship model directly
```

### Redis-only correctness events

where event loss would corrupt business workflow.

---

## 41. Frozen Phase 1 invariants

### P1-I01 — Gateway is ingress, not domain owner

The Gateway owns public API ingress behavior and no default business database.

### P1-I02 — Static Content Catalog remains canonical initially

Course/module/lesson/path/resource content remains source-controlled for the initial architecture.

### P1-I03 — Learning Service owns learner state

Enrollment, progress, completion, and bookmarks belong to Learning Service.

### P1-I04 — Mentorship Service owns mentorship state

Offering, availability, booking, and session lifecycle belong to Mentorship Service.

### P1-I05 — Knowledge Service owns derived searchable state

Knowledge indexes are rebuildable and non-canonical.

### P1-I06 — Assistant is orchestration only

Assistant Service never becomes canonical business state authority.

### P1-I07 — Audit is durable and append-only

Privileged LMS actions requiring accountability are persisted by Audit Service.

### P1-I08 — Keycloak remains identity authority

The LMS does not create a competing credential/identity store.

### P1-I09 — Separate browser clients

`lms-user` and `lms-admin` are separate OIDC public-client trust contexts.

### P1-I10 — LMS API is the protected resource

Backend tokens target the `lms-api` audience.

### P1-I11 — Capability-based authorization

Backend operations authorize capabilities, not merely frontend persona labels.

### P1-I12 — No backend fallback-to-student authorization

Missing capability claims fail closed.

### P1-I13 — One public API version namespace

Initial business API surface uses `/api/v1`.

### P1-I14 — No direct public microservice exposure

Clients call only `lms-api.reltroner.com`.

### P1-I15 — No cross-service database writes

Service ownership is enforced at database-credential level.

### P1-I16 — No distributed DB transactions

Cross-service consistency uses explicit calls/events/compensation.

### P1-I17 — Durable event intent uses outbox

Redis transport is not the only copy of correctness-critical event intent.

### P1-I18 — Public search stays static where possible

Public catalog search does not require backend runtime dependency.

### P1-I19 — Permission-aware search goes through Knowledge Service

Private/authorized search is backend-enforced.

### P1-I20 — Assistant mutation uses domain APIs

AI can never bypass service invariants.

### P1-I21 — Initial Assistant is authenticated-only

Guest AI requires a later cost/abuse contract.

### P1-I22 — No browser-native canonical content CRUD initially

Admin presence does not move source-controlled course authority into a runtime database.

### P1-I23 — Instructor uses admin plane

Privileged instructor workflows use `lms-admin.reltroner.com`, not a third frontend hostname.

### P1-I24 — Identity copies are projections only

`sub` is the principal reference; copied identity attributes are not authoritative.

---

## 42. Implementation gates opened by this contract

With Phase 1 frozen, implementation planning may now begin for:

- backend repository bootstrap,
- service skeletons,
- database/user creation plans,
- internal ports/runtime assignments,
- Keycloak client migration plan,
- `lms-api` audience/permission configuration,
- learner/admin frontend separation plan,
- content catalog manifest generation,
- Learning Service persistence,
- Mentorship Service persistence,
- Knowledge indexing foundation,
- Assistant adapter foundation,
- Audit persistence,
- API contract tests.

This document still does not authorize unreviewed production mutation.

---

## 43. Next engineering phase

The next phase should establish the backend/service foundation from this contract before business features are implemented.

Recommended next phase:

```text
Phase 2 — Backend Foundation & Service Skeleton
```

Its first work must be deterministic and contract-driven:

1. repository topology decision,
2. Laravel service bootstrap strategy,
3. service runtime/port allocation,
4. DB ownership/users,
5. common API/error/request-ID contract package or specification,
6. health endpoints,
7. authentication middleware foundation,
8. CI baseline,
9. no business feature implementation until service skeleton acceptance passes.

---

## 44. Change control

This contract is **FROZEN**.

Any change to a frozen Phase 1 invariant requires:

1. a versioned update to this contract, or
2. an ADR that explicitly supersedes the affected invariant.

Silent service-boundary drift is prohibited.

---

## 45. Final logical summary

```text
Git / Content Catalog
→ Course / Module / Lesson / Path / Resource truth

Keycloak
→ Identity / credentials / login truth

LMS API Gateway
→ Public ingress / auth context / routing

Learning Service
→ Enrollment / Progress / Completion / Bookmark truth

Mentorship Service
→ Offering / Availability / Booking / Session truth

Knowledge Service
→ Derived searchable / permission-aware index

Assistant Service
→ AI orchestration over explicit domain APIs

Audit Service
→ Durable privileged-action accountability

PostgreSQL
→ Per-service durable state

Redis
→ Runtime transport/cache/queue only
```

The core rule is:

> **Content is published from source control. Identity comes from Keycloak. Domain state belongs to the owning service. Search is derived. AI orchestrates but does not own truth.**
