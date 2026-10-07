# Reltroner LMS — Master Infrastructure Placement Contract

> **Document type:** Binding infrastructure placement contract  
> **Architecture phase:** Phase 0C — Master Infrastructure Placement Contract  
> **Status:** **FROZEN**  
> **Version:** 1.0.0  
> **Effective date:** 2026-10-07  
> **Project:** Reltroner LMS  
> **Architecture style:** Microservices  
> **Supersedes:** Pre-discovery infrastructure assumptions for Reltroner LMS

---

## 1. Purpose

This document defines the authoritative physical infrastructure placement, public hostname boundaries, infrastructure responsibilities, trust boundaries, caching responsibilities, state ownership rules, and deployment constraints for Reltroner LMS.

This contract is the output of:

- **Phase 0A — VPS / Network / Runtime Discovery**
- **Phase 0B — Premium Web Hosting + Cloudflare Discovery**
- **Phase 0C — Infrastructure Placement Freeze**

No Phase 1 logical service implementation may override this document implicitly.

Any future architectural change that conflicts with a frozen invariant in this document requires an explicit architecture decision record (ADR) or a versioned revision of this contract.

---

## 2. Phase status

| Phase | Status |
|---|---|
| Phase 0A — VPS / Network / Runtime Discovery | ✅ PASS |
| Phase 0B — Cloudflare + Premium Web Hosting Discovery | ✅ PASS |
| Phase 0C — Master Infrastructure Placement Contract | ✅ FROZEN |
| Phase 1 — Logical Service Boundary & API Contract | ⏭ NEXT |
| Application bootstrap / implementation | 🔒 BLOCKED until Phase 1 contract is defined |

Phase 0 is complete.

---

## 3. Binding architecture principle

Reltroner LMS follows this infrastructure model:

```text
EDGE DELIVERS
ORIGIN STORES
CORE COMPUTES
POSTGRES REMEMBERS
REDIS ACCELERATES
KEYCLOAK IDENTIFIES
API AUTHORIZES
```

Additional binding rules:

1. **Public hostname does not equal microservice.**
2. **Frontend does not own business truth.**
3. **Cloudflare is edge/control infrastructure, not business truth.**
4. **Premium Web Hosting is an asset origin, not the LMS application core.**
5. **The VPS is the stateful application core.**
6. **PostgreSQL is the durable application state authority.**
7. **Redis contains only replaceable runtime/ephemeral state.**
8. **Keycloak owns identity; LMS backend owns LMS authorization.**
9. **Internal microservices are not publicly addressable.**
10. **Infrastructure complexity must be justified by measurable need.**

---

## 4. Required public LMS hostnames

Reltroner LMS has exactly three primary public application hostnames:

| Hostname | Responsibility |
|---|---|
| `lms.reltroner.com` | Learner / user experience |
| `lms-admin.reltroner.com` | Administrative experience |
| `lms-api.reltroner.com` | Public LMS backend/API entry point |

Supporting public infrastructure hostnames:

| Hostname | Responsibility |
|---|---|
| `auth.reltroner.com` | Canonical Reltroner OIDC / Keycloak identity authority |
| `assets.reltroner.com` | Public immutable LMS asset delivery |

There must not be public hostnames such as:

```text
learning-api.reltroner.com
mentorship-api.reltroner.com
knowledge-api.reltroner.com
assistant-api.reltroner.com
```

for internal service exposure in the initial architecture.

All externally reachable LMS backend traffic enters through:

```text
https://lms-api.reltroner.com
```

---

## 5. Authoritative physical topology

```text
                                  INTERNET
                                     │
                                     ▼
                        ┌────────────────────────┐
                        │      CLOUDFLARE        │
                        │   EDGE CONTROL PLANE   │
                        │                        │
                        │ Authoritative DNS      │
                        │ TLS edge               │
                        │ CDN / cache            │
                        │ Security rules         │
                        │ Rate limiting          │
                        │ Pages                  │
                        │ Optional thin Workers  │
                        └────────────┬───────────┘
                                     │
              ┌──────────────────────┼─────────────────────────┐
              │                      │                         │
              ▼                      ▼                         ▼
      USER EXPERIENCE        ADMIN EXPERIENCE             PUBLIC API
           PLANE                   PLANE                     PLANE
              │                      │                         │
   lms.reltroner.com      lms-admin.reltroner.com           │
              │                      │                         ▼
              ▼                      ▼              lms-api.reltroner.com
      Cloudflare Pages       Cloudflare Pages                 │
       static-first           static-first                    ▼
                                                       Cloudflare proxy
                                                              │
                                                              ▼
                                                        Hostinger VPS
                                                              │
                                                            Nginx
                                                              │
                                                        LMS API ingress
                                                              │
                      ┌───────────────────────────────────────┼────────────────────┐
                      │                                       │                    │
                      ▼                                       ▼                    ▼
               Learning Service                       Mentorship Service     Knowledge Service
                      │                                       │                    │
                      └──────────────────────┬────────────────┴────────────┬───────┘
                                             │                             │
                                             ▼                             ▼
                                   Assistant orchestration           Background workers
                                             │
                                             ▼
                                   External LLM inference
                                         (initially)

                                                              │
                                   ┌──────────────────────────┴───────────────────────┐
                                   ▼                                                  ▼
                            PostgreSQL 18                                          Redis 8
                            durable truth                                         ephemeral
```

Supporting asset plane:

```text
assets.reltroner.com
        │
        ▼
Cloudflare CDN / edge
        │
        ▼
Hostinger Premium Web Hosting
Malaysia origin
        │
        ├── images
        ├── diagrams
        ├── PDF
        ├── slide decks
        ├── public audio
        ├── downloads
        └── immutable release artifacts
```

Identity plane:

```text
auth.reltroner.com
        │
        ▼
VPS Nginx
        │
        ▼
Keycloak
        │
        └── realm: reltroner
```

---

## 6. Current discovered infrastructure facts

The following facts were verified during Phase 0 discovery and form the basis of this placement contract.

### 6.1 VPS

Current VPS baseline:

- Ubuntu 24.04 LTS
- KVM virtualized
- approximately 1 vCPU
- approximately 4 GB RAM
- 2 GB swap
- approximately 48 GB root filesystem
- Nginx
- PHP 8.4 FPM
- PostgreSQL 18
- Redis 8
- Keycloak as a native/systemd service
- Docker is not currently installed

Current externally reachable TCP ports verified:

```text
22   SSH
80   HTTP
443  HTTPS
```

The following verified services are not externally reachable:

```text
5432 PostgreSQL
6379 Redis
7800 internal Java runtime
8080 Keycloak application HTTP
9000 Keycloak management/runtime
```

UFW is active with:

```text
default incoming: deny
default outgoing: allow
22/tcp: rate-limited
80/tcp: allowed
443/tcp: allowed
```

PostgreSQL and Redis are bound to loopback.

### 6.2 Existing PostgreSQL databases

Current PostgreSQL instance already contains:

```text
hrm_db
keycloak_db
postgres
```

Reltroner LMS will share the physical PostgreSQL instance initially while preserving strict logical ownership.

### 6.3 Redis

Current Redis:

- runs natively on VPS
- listens on loopback only
- authentication is required
- must remain non-public

### 6.4 Keycloak

Current canonical identity service:

```text
https://auth.reltroner.com
```

Canonical realm issuer:

```text
https://auth.reltroner.com/realms/reltroner
```

The previously configured hostname:

```text
sso.reltroner.com
```

does not resolve and is not canonical.

Any existing LMS frontend configuration pointing to `sso.reltroner.com` is configuration drift and must be corrected during a controlled implementation phase, not during discovery.

### 6.5 Cloudflare

Cloudflare Free is currently used as the authoritative DNS platform for `reltroner.com`.

Discovered capabilities already in use include:

- Cloudflare Pages
- Cloudflare Workers
- DNS authority
- TLS edge certificates
- security rules
- analytics

The account currently has substantial unused Worker request capacity relative to observed usage.

Cloudflare Workers remain an optional thin edge layer only and are not the default LMS application runtime.

### 6.6 Premium Web Hosting

Current Hostinger Premium Web Hosting allocation:

| Resource | Contracted allocation |
|---|---:|
| Disk | 25 GB |
| RAM | 2048 MB |
| CPU | 1 core allocation |
| Inodes | 400,000 |
| Max processes | 80 |
| PHP workers | 40 |
| Website/addon capacity | 25 |
| Bandwidth | Unlimited |

Current observed usage at discovery time:

- approximately 0.57 GB account storage consumed
- approximately 45.7K inodes consumed
- substantial available headroom
- weekly backup
- backup location: Singapore
- shared hosting server location: Malaysia
- SSH access enabled

Physical top-level hosted domain directories observed over SSH:

```text
alhamratrade.com
reltroner.com
```

Premium Web Hosting CLI runtime observed:

- PHP CLI 8.2
- Composer available
- Node.js not installed
- npm not installed

The web PHP handler may differ from CLI PHP and was observed in hPanel as PHP 8.4.

The shared host filesystem capacity reported by `df` is not Reltroner's contractual storage allocation. The 25 GB hPanel account quota is authoritative.

---

## 7. Hostname placement matrix

| Hostname | Placement | Edge mode | Runtime | State authority |
|---|---|---|---|---|
| `lms.reltroner.com` | Cloudflare Pages | Pages/global edge | Next.js static-first | None |
| `lms-admin.reltroner.com` | Cloudflare Pages | Pages/global edge | Next.js static-first | None |
| `lms-api.reltroner.com` | Cloudflare → VPS | Proxied | Nginx + LMS API ingress | Backend services |
| `auth.reltroner.com` | VPS | Existing production topology preserved | Nginx + Keycloak | Identity state |
| `assets.reltroner.com` | Cloudflare → Premium Hosting | Proxied/cached | Static origin | None |
| PostgreSQL | VPS localhost | Not public | PostgreSQL 18 | Durable business truth |
| Redis | VPS localhost | Not public | Redis 8 | Ephemeral only |
| Internal LMS services | VPS internal | Not public | Dedicated runtime/process boundaries | Own logical DB state |

---

## 8. Learner frontend contract

### Hostname

```text
https://lms.reltroner.com
```

### Placement

```text
Cloudflare Pages
```

### Runtime posture

The learner frontend must remain **static-first**.

Current LMS Pages deployment already builds with:

```text
npm run build
output: out
```

The architecture should preserve static delivery for public/guest content whenever practical.

Suitable public/static concerns include:

- course catalog
- public course pages
- public lesson content
- creator pages
- public documentation
- public frameworks
- public diagrams
- SEO pages
- static metadata

The learner frontend does not own durable authenticated state.

Authenticated concerns such as:

- enrollment
- progress
- bookmarks
- learner profile
- projects
- mentorship
- private knowledge
- assistant state

must use the backend through `lms-api.reltroner.com`.

---

## 9. Admin frontend contract

### Hostname

```text
https://lms-admin.reltroner.com
```

### Placement

```text
Cloudflare Pages
```

The admin frontend must be independently deployable from the learner frontend even if both applications later share one frontend repository or monorepo.

The following remain Phase 1 or implementation decisions:

- exact repository topology
- monorepo vs separate frontend repositories
- shared design-system packaging
- build pipeline details

The admin frontend is **not** an authorization boundary.

Hiding UI controls is not authorization.

All admin permissions must be enforced server-side by the backend.

---

## 10. OIDC / identity contract

Canonical identity authority:

```text
https://auth.reltroner.com
```

Canonical issuer:

```text
https://auth.reltroner.com/realms/reltroner
```

Realm:

```text
reltroner
```

Learner and admin applications must use distinct OIDC clients.

Candidate client identities:

```text
lms-user
lms-admin
```

Candidate redirect boundaries:

```text
https://lms.reltroner.com/auth/callback
https://lms-admin.reltroner.com/auth/callback
```

Exact client IDs, role mappings, scopes, audiences, and token claims are Phase 1 identity/API contract decisions.

OIDC authentication answers:

```text
Who is this principal?
```

LMS backend authorization answers:

```text
What may this principal do?
```

The presence of a valid Keycloak token alone must never imply admin permission.

---

## 11. LMS API contract

### Public hostname

```text
https://lms-api.reltroner.com
```

This is the only public LMS backend/API entry point.

Request path:

```text
Browser / client
    │
    ▼
Cloudflare
    │
    ▼
Nginx
    │
    ▼
LMS API ingress / gateway boundary
    │
    ▼
Internal domain services
```

Responsibilities of the public API ingress may include:

- authentication context validation
- authorization context propagation
- request normalization
- correlation/request ID creation
- rate-limit context
- service routing
- external error normalization

The API ingress must not become the owner of all business logic.

Exact API resources, route namespaces, service interfaces, and transport contracts are deferred to Phase 1.

---

## 12. Internal microservice exposure contract

Internal microservices must not be directly reachable from the public Internet.

They must not receive public DNS records.

They must not listen on public interfaces unless a future ADR explicitly changes this contract.

Preferred binding patterns:

```text
127.0.0.1:<internal-port>
```

or Unix sockets where appropriate.

The VPS public exposure target remains:

```text
22
80
443
```

only.

Microservice architecture means separate business ownership and deployable/runtime boundaries; it does not require one VM, one VPS, or one public hostname per service.

---

## 13. Initial microservice placement

Initial LMS domain services are colocated on the existing VPS because the infrastructure is intentionally resource-efficient.

Candidate logical services include:

- API Gateway / ingress
- Learning Service
- Mentorship Service
- Knowledge Service
- Assistant orchestration / worker

These names describe planned logical boundaries. Their exact responsibilities remain Phase 1 work.

Initial placement:

```text
ONE VPS
│
├── Nginx
├── Keycloak
├── LMS API ingress
├── Learning Service
├── Mentorship Service
├── Knowledge Service
├── Assistant worker/orchestration
├── PostgreSQL
└── Redis
```

The project explicitly rejects infrastructure sprawl merely to imitate distributed deployment.

---

## 14. Container policy

Docker is not currently installed on the VPS.

Docker must not be installed merely because the project uses microservices.

The existing native stack is valid:

```text
Nginx
systemd
PHP-FPM
PostgreSQL
Redis
Keycloak
```

Containerization may be introduced only when it provides a concrete operational benefit supported by an ADR.

The initial architecture does not require:

- Docker
- Kubernetes
- service mesh
- Kafka
- RabbitMQ
- Elasticsearch
- Meilisearch
- local LLM runtime

unless a later phase demonstrates a concrete requirement.

---

## 15. PostgreSQL placement and ownership

Physical placement:

```text
VPS
127.0.0.1:5432
PostgreSQL 18
```

PostgreSQL is the durable source of truth for LMS application/business state.

Initial logical database candidates:

```text
lms_learning_db
lms_mentorship_db
lms_knowledge_db
```

A gateway database is not mandatory.

```text
lms_gateway_db
```

may exist only if durable state is identified that is truly gateway-owned.

Binding database ownership rules:

1. Each service owns its own business data.
2. A service must not write another service's database.
3. Cross-service ORM relationships are prohibited.
4. Direct cross-service database joins are not the application integration model.
5. Shared physical PostgreSQL does not imply shared logical ownership.
6. Cross-domain integration occurs through explicit service contracts/events defined in later phases.

---

## 16. Redis placement and ownership

Physical placement:

```text
VPS
127.0.0.1:6379
Redis 8
```

Redis may be used for:

- cache
- queues
- locks
- temporary workflow state
- rate counters
- short-lived idempotency
- runtime/session support where justified
- ephemeral coordination/events

Redis must not be the only copy of:

- learner progress
- enrollment
- mentorship bookings
- canonical course state
- canonical profile data
- durable audit records
- financial/revenue state

If Redis is lost, business truth must survive.

---

## 17. Asset origin contract

### Public hostname

```text
https://assets.reltroner.com
```

### Placement

```text
Cloudflare edge/cache
        │
        ▼
Hostinger Premium Web Hosting
Malaysia origin
```

Suitable content:

- public images
- diagrams
- PDFs
- slide decks
- public audio
- downloadable resources
- versioned public exports
- immutable release artifacts

Unsuitable placement:

- canonical LMS database
- Redis authority
- Keycloak
- long-running queues/daemons
- WebSocket/realtime infrastructure
- search engine daemon
- LLM inference
- primary LMS business API
- large long-term video streaming catalog

Initial LMS asset soft quota:

```text
10 GB
```

This is an operational soft quota, not the full account limit.

Unused shared-hosting capacity must remain available for other Reltroner workloads and operational headroom.

---

## 18. Immutable asset policy

LMS public assets should be version-addressed or content-addressed.

Preferred examples:

```text
/releases/2026-10-07-a91f3/slides/course-01.pdf
/assets/sha256/a8/a8f923....webp
```

Avoid mutable cache identities such as:

```text
/slides/latest.pdf
/images/course-banner.png
```

when the bytes may change without the URL changing.

For immutable public assets, target cache semantics:

```http
Cache-Control: public, max-age=31536000, immutable
```

New content should normally produce a new URL rather than relying on frequent global cache purges.

Premium Web Hosting is a deployment/origin target, not the canonical source of truth.

---

## 19. Asset source-of-truth contract

Asset delivery flow:

```text
Canonical source / production artifact pipeline
        │
        ▼
Versioned artifact / manifest
        │
        ▼
Premium Web Hosting
        │
        ▼
Cloudflare edge/cache
        │
        ▼
User
```

Manual File Manager uploads must not become the sole source of truth.

Premium weekly backups are a recovery layer, not the canonical content repository.

---

## 20. Cloudflare contract

Cloudflare is the authoritative edge/control platform for LMS.

Target LMS placement:

```text
lms.reltroner.com
→ Cloudflare Pages

lms-admin.reltroner.com
→ Cloudflare Pages

lms-api.reltroner.com
→ Cloudflare proxy
→ VPS origin

assets.reltroner.com
→ Cloudflare proxy/cache
→ Premium Web Hosting origin
```

Cloudflare Workers are allowed only as **thin edge capabilities** when a measurable requirement exists, for example:

- lightweight routing
- same-origin bridge where justified
- small request/response transformation
- edge security logic
- signed asset routing

Workers must not become an accidental replacement for the stateful LMS backend.

Existing non-LMS production routes must not be changed merely to make infrastructure visually uniform.

---

## 21. TLS contract

Cloudflare zone encryption was discovered in `Full` mode.

The desired production target for proxied LMS origins is:

```text
Full (strict)
```

However, this must not be changed blindly because the setting may affect existing proxied hostnames.

The required migration order is:

```text
1. Validate origin certificates for all affected proxied origins
2. Verify direct origin HTTPS
3. Verify hostname/certificate compatibility
4. Verify existing proxied applications
5. Change to Full (strict) in a controlled maintenance step
6. Re-test all affected hostnames
```

No Phase 0 DNS/TLS mutation is authorized by this contract.

---

## 22. CORS contract

Approved browser application origins:

```text
https://lms.reltroner.com
https://lms-admin.reltroner.com
```

Authenticated LMS APIs must not use:

```text
Access-Control-Allow-Origin: *
```

The API must use an explicit origin allowlist.

A broad wildcard such as:

```text
*.reltroner.com
```

must not be used unless a later contract explicitly requires it.

---

## 23. Browser session / credential boundary

Learner and admin applications must be treated as separate browser origins.

Preferred authentication pattern:

```text
OIDC Authorization Code + PKCE
```

Broad cookies such as:

```text
Domain=.reltroner.com
```

should be avoided unless a later requirement proves they are necessary.

Host-scoped credentials are preferred.

Centralized Keycloak SSO may provide user convenience without requiring all Reltroner applications to share application session cookies.

---

## 24. Backend token validation contract

The backend must not treat a valid signature as sufficient authorization.

At minimum, backend token validation must consider relevant claims such as:

- issuer (`iss`)
- audience (`aud`)
- expiration (`exp`)
- not-before (`nbf`) where applicable
- authorized party/client identity
- scopes / roles / permissions

Canonical issuer:

```text
https://auth.reltroner.com/realms/reltroner
```

Exact backend audience and permission model are Phase 1 decisions.

---

## 25. Admin authorization contract

Admin frontend visibility is never authoritative.

All privileged operations must be enforced in the backend.

Future permissions should be capability-oriented, for example:

```text
admin.course.read
admin.course.create
admin.course.update
admin.course.publish
admin.user.read
admin.user.suspend
admin.mentorship.read
admin.mentorship.manage
admin.analytics.read
admin.audit.read
```

Exact permissions and role bundles are Phase 1 authorization work.

---

## 26. Search placement

Universal search and Ctrl+K/search experiences may use the Knowledge domain.

Initial stateful search authority should remain within the LMS backend architecture and may use PostgreSQL capabilities first.

Public static search indexes may later be generated for suitable public content if that materially reduces backend load.

Private, user-specific, mentorship, admin, or permission-bound content must be resolved through an authorization-aware backend search path.

A dedicated search daemon must not be added without a measured requirement.

---

## 27. AI placement

Current VPS capacity is not an LLM inference node.

The initial architecture is:

```text
LMS Assistant orchestration
        │
        ├── authorization
        ├── retrieval
        ├── context assembly
        ├── tool invocation
        │
        ▼
External LLM inference
```

The current KVM1 must not run local LLM inference.

A future dedicated AI node may replace external inference if capacity, cost, privacy, or latency requirements justify it.

---

## 28. Failure-domain behavior

The architecture intentionally allows partial availability.

### If VPS is unavailable

Potentially still available:

- static learner frontend
- static admin frontend shell
- Cloudflare-cached assets
- public static content already delivered through Pages/edge

Unavailable or degraded:

- authenticated API operations
- progress writes
- mentorship operations
- backend search
- admin mutations
- Keycloak-dependent fresh authentication

### If Premium Web Hosting is unavailable

Expected:

- LMS API can remain available
- identity can remain available
- learner/admin Pages can remain available
- already cached assets may remain available
- asset cache misses may fail

### If Redis is unavailable

Expected:

- durable PostgreSQL truth survives
- runtime/queue/cache capabilities may degrade

### If PostgreSQL is unavailable

Expected:

- durable stateful LMS operations fail closed
- public static frontend content may remain available

### If a frontend Pages deployment fails

Expected:

- backend API remains independently deployable/available
- learner and admin deployments should not be unnecessarily coupled

---

## 29. Backup and recovery authority

```text
Git / source repositories
→ application source truth

PostgreSQL backups
→ business-state recovery

Premium Hosting weekly backup
→ secondary asset-origin recovery

Cloudflare cache
→ never source of truth

Redis
→ never source of truth
```

Backups do not replace reproducible deployment artifacts.

---

## 30. Deployment authority

### Learner frontend

```text
GitHub
→ Cloudflare Pages
→ lms.reltroner.com
```

### Admin frontend

```text
GitHub
→ Cloudflare Pages
→ lms-admin.reltroner.com
```

### Backend

```text
GitHub
→ controlled deployment
→ VPS
→ Nginx / runtime boundaries
```

### Asset releases

```text
Canonical artifact source
→ versioned release upload
→ Premium Web Hosting
→ Cloudflare edge/cache
```

Direct production source editing in File Manager or ad-hoc server modification is not the deployment model.

---

## 31. Repository topology — intentionally deferred

Existing repositories include:

```text
Reltroner/LMS-FE
Reltroner/LMS-BE
```

Phase 0C does not freeze whether backend microservices will remain in one repository or move to multiple repositories.

Likewise, Phase 0C does not freeze whether learner/admin frontend applications use one monorepo or separate repositories.

What is frozen:

- learner and admin are separate deployment surfaces
- internal backend services are separate logical/service ownership boundaries
- internal services must remain independently evolvable at contract level

Repository decomposition is a Phase 1 / implementation architecture decision.

---

## 32. Resource governance

Current infrastructure is intentionally constrained and must stay efficient.

Do not add the following by default:

- Docker solely for microservice aesthetics
- Kubernetes
- service mesh
- Kafka
- RabbitMQ
- Elasticsearch
- Meilisearch
- local LLM runtime
- additional stateful databases without need

Prefer the infrastructure already available:

```text
Cloudflare
Cloudflare Pages
Nginx
PHP-FPM
systemd
PostgreSQL
Redis
Keycloak
Premium Web Hosting
```

Complexity must be earned by a concrete requirement.

---

## 33. Observability baseline

Every request entering the public LMS API should receive a correlation identifier such as:

```text
X-Request-ID
```

It should propagate across internal service calls.

Minimum structured log context should include:

- timestamp
- request/correlation ID
- service name
- environment
- route or operation
- status/result
- duration
- safe principal reference where appropriate

Logs must not contain:

- passwords
- access tokens
- refresh tokens
- full session cookies
- Keycloak client secrets
- database passwords
- private keys

Exact observability implementation is a later-phase concern.

---

## 34. Admin audit requirement

Privileged admin mutations require durable auditability.

The backend must eventually be able to answer:

```text
WHO
did WHAT
to WHICH RESOURCE
WHEN
with WHICH RESULT
```

Candidate auditable actions include:

- course publish/unpublish
- user suspension
- role/permission assignment
- mentorship administrative actions
- destructive content actions
- sensitive configuration changes

Audit ownership and event format are Phase 1 decisions.

---

## 35. Explicitly prohibited initial placements

The following are prohibited unless a later ADR changes the contract.

### Premium Web Hosting must not host

- canonical LMS PostgreSQL state
- canonical Redis state
- Keycloak
- primary LMS backend API
- persistent worker daemons required for correctness
- WebSocket infrastructure
- local search daemon
- local LLM inference
- cross-service database proxy logic

### Cloudflare Pages must not own

- durable learner state
- durable admin state
- authorization truth
- canonical progress
- canonical mentorship bookings
- canonical audit state

### Redis must not own

- irreplaceable business truth

### Frontend must not own

- authorization decisions
- privileged admin truth
- canonical business state

### Internal services must not

- receive direct public DNS exposure
- bypass service ownership by writing another service's database

---

## 36. Frozen invariants

The following invariants are binding from Phase 0C onward.

### I-01 — Learner hostname

```text
lms.reltroner.com = learner/user frontend
```

### I-02 — Admin hostname

```text
lms-admin.reltroner.com = admin frontend
```

### I-03 — Public backend hostname

```text
lms-api.reltroner.com = only public LMS backend/API entry point
```

### I-04 — Identity authority

```text
auth.reltroner.com = canonical Reltroner OIDC/Keycloak authority
```

### I-05 — Separate OIDC trust contexts

Learner and admin use separate OIDC client identities.

### I-06 — Frontend authorization is non-authoritative

UI state never grants privilege.

### I-07 — Server-side admin enforcement

All admin privilege is enforced server-side.

### I-08 — Internal service privacy

Internal microservices are not publicly addressable.

### I-09 — Durable truth

PostgreSQL is the durable LMS business-state authority.

### I-10 — Logical ownership

Each domain service owns its own logical data.

### I-11 — No cross-service direct writes

No service may directly write another service's database.

### I-12 — Redis is ephemeral

Redis contains no irreplaceable business truth.

### I-13 — Premium Hosting role

Premium Web Hosting is the LMS public asset origin, not the application core.

### I-14 — Frontend delivery

Cloudflare Pages is the target delivery platform for learner and admin LMS frontends.

### I-15 — No KVM1 LLM inference

The current VPS must not run local LLM inference.

### I-16 — Cloudflare is not truth

Cloudflare edge/cache is not a canonical business-state store.

### I-17 — Minimal VPS public ingress

Only explicitly required public ingress is exposed; internal data/services remain private.

### I-18 — Immutable asset strategy

Public LMS asset releases are versioned/immutable wherever practical.

### I-19 — Versioned API contract

Public backend APIs are versioned.

### I-20 — Complexity must be justified

New infrastructure is introduced only after a measurable or contractual requirement exists.

---

## 37. Deferred to Phase 1

Phase 0C deliberately does **not** freeze the following:

- exact Learning Service responsibility
- exact Mentorship Service responsibility
- exact Knowledge Service responsibility
- exact Assistant Service responsibility
- exact API resource paths
- synchronous vs asynchronous service-to-service transport
- domain events
- outbox/inbox strategy
- user/profile ownership
- enrollment ownership
- progress model
- course/module/lesson aggregate boundaries
- mentorship aggregate boundaries
- search indexing model
- assistant tool contracts
- audit service ownership
- admin permission matrix
- exact Keycloak audience/scope mapping
- repository decomposition
- frontend monorepo vs split repository
- CI/CD implementation details

These are Phase 1 concerns and must be derived from explicit domain/service-boundary discovery.

---

## 38. Phase 1 entry criteria

Phase 1 may begin only when:

- Phase 0A is PASS
- Phase 0B is PASS
- this Phase 0C contract is committed
- no unresolved infrastructure blocker contradicts this document

Phase 1 begins with logical service boundary and API contract discovery.

No application bootstrap should be treated as authoritative before that contract exists.

---

## 39. Implementation mutation gate

This document does not itself authorize immediate production mutation.

The following remain gated until their implementation phase:

- creating `lms-admin.reltroner.com`
- creating `lms-api.reltroner.com`
- creating `assets.reltroner.com`
- changing Cloudflare proxy status
- changing Cloudflare zone TLS mode
- correcting LMS Pages OIDC variables
- creating LMS PostgreSQL databases
- creating LMS database users
- creating Nginx LMS vhosts
- creating systemd/PHP-FPM LMS service boundaries
- deploying backend code
- provisioning admin frontend

Implementation must be deterministic, evidence-driven, and separately accepted.

---

## 40. Change-control rule

This contract is **FROZEN**.

A future change that conflicts with any frozen invariant must use one of:

1. a versioned update to this contract with explicit rationale, or
2. an ADR that explicitly supersedes the affected invariant.

Silent architectural drift is prohibited.

---

## 41. Final infrastructure summary

```text
lms.reltroner.com
→ Cloudflare Pages
→ learner application

lms-admin.reltroner.com
→ Cloudflare Pages
→ administrative application

lms-api.reltroner.com
→ Cloudflare
→ VPS / Nginx
→ LMS API ingress
→ internal microservices

auth.reltroner.com
→ VPS / Keycloak
→ canonical identity authority

assets.reltroner.com
→ Cloudflare edge/cache
→ Hostinger Premium Web Hosting
→ immutable public LMS artifacts

PostgreSQL 18
→ VPS loopback
→ durable application/business state

Redis 8
→ VPS loopback
→ ephemeral runtime infrastructure
```

The architectural shorthand is:

> **Cloudflare delivers. Premium Hosting originates public artifacts. VPS computes and owns state. PostgreSQL remembers. Redis accelerates. Keycloak identifies. LMS API authorizes.**
