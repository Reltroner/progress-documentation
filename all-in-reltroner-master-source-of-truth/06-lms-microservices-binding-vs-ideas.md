# 06 — Reltroner LMS Microservices: Actual Contract vs Discussion

> Domain: LMS technology. This is an archive crosswalk, **not a modified architectural contract, work order, deployment approval or live status receipt**.

## Binding: bounded microservices, NOT modular monolith
The HRM engineering discipline (discover → freeze contracts → implement → test → accept → deploy with controlled change) is reusable. The HRM monolith topology is **not**. Frozen Reltroner LMS initial runtime boundaries:

| Microservice | Domain ownership |
|---|---|
| **API Gateway** | externally accessible LMS backend entry, authenticated routing/gateway contract, public trust boundary |
| **Learning** | learner enrollment, progress, bookmarks and project-domain state subject to contract |
| **Mentorship** | offers, entitlement/booking lifecycle and mentorship state |
| **Knowledge** | derived searchable index, metadata, authorized retrieval |
| **Assistant** | permission-aware LLM orchestration and bounded tool calls |
| **Audit** | append-only security/privileged-action audit records |

These are **six independently scoped Laravel applications** within the accepted backend repository, not an Eloquent modular monolith. Content Catalog is version-controlled authority, not an initial runtime seventh service.

## Frozen public surfaces and authority
~~~text
lms.reltroner.com          → learner frontend, Cloudflare Pages / static-first
lms-admin.reltroner.com    → separate admin frontend boundary
lms-api.reltroner.com      → ONLY public LMS backend/API ingress
auth.reltroner.com         → Keycloak, identity authority
assets.reltroner.com       → immutable public LMS assets (placement contract)

Gateway → private Learning/Mentorship/Knowledge/Assistant/Audit interfaces
      NO independent public hostnames for those five services
~~~

- **Keycloak canonical issuer** in frozen LMS contract: `https://auth.reltroner.com/realms/reltroner`.
- OIDC client contract: `lms-user`, `lms-admin`; protected API audience `lms-api`.
- The earlier suggestion to establish a new public realm automatically is **superseded as an unratified idea**; do not change realm without ADR/owner permission.
- Roles are not the same as API capabilities. Missing permission fails closed; no default student authorization based on frontend role fallback.
- Keycloak owns credentials/password, MFA, federation and primary identity; LMS owns local learning/mentorship business authorization and user learning data. Never mirror passwords or make copied email the stable principal.
- User requested **Reltroner-branded UI/UX**; this does not authorize custom password verification by Laravel. Keycloak theme/account UX and potential account UI integration need contract-compliant discovery/implementation.

## Frozen persistence placement
- PostgreSQL **18**: durable, service-owned state, logical DB/credential isolation; not a shared business schema. Learning, Mentorship, Knowledge and Audit own initial durable DBs. No direct cross-service SQL/ORM.
- Redis **8**: replaceable ephemeral session/cache/queue/locks/replay where explicitly permitted by live security contract. Shared physical daemon does not imply unsafe shared keyspace/cross-service privileges.
- Cloudflare: edge/static delivery and DNS, **not** business state.
- Premium Hosting: immutable public asset origin when approved, not the business-data core.
- Hostinger Ubuntu 24.04 VPS: selected compute context, colocated with existing HRM/Keycloak constraints; do not assume free resource capacity from one CPU/memory screenshot.
- Initial LLM inference external; **do not place large local models or open autonomous agents on existing critical VPS without capacity/security proofs**.
- Initial placement contract does **not** mandate Docker, Kubernetes, Kafka, Meilisearch, dedicated vector DB or extra public domains.

## Static-first + account path
Guest should read public courses/lessons and use static public search without server business-state dependency. The frozen initial assistant API is **authenticated only**, contrary to some early “guest chatbot” brainstorms.

Authenticated learning/mentorship uses authorized gateway/domain APIs. The initial frontend is a static Next.js 16 export; do **not** assume server-side BFF/session cookies, Next.js SSR or new cross-domain cookies are already adopted. Browser/Auth architecture must be reviewed against *existing* frozen OIDC PKCE and trust contracts.

## Search + chatbot
- Initial public Ctrl+K can use frontend static search index.
- Private search requests go to authorized Knowledge Service.
- Universal UX may combine public and authorized results without leaking protected content.
- Initial Knowledge search favors PostgreSQL text search; pgvector embeddings/hybrid ranking are future **ADR-candidate** additions.
- Assistant may call narrow Knowledge/Learning/Mentorship APIs with explicit capabilities; model output is **never** durable identity/entitlement/booking truth.

## Event and audit discipline
Service state mutations remain owned by the domain service, with immutable/auditable records as required. Event/outbox/Redis placement must follow the frozen trust/replay contract and work orders. n8n or AI agents cannot become state authority. No distributed writes without explicit consistency rule and idempotency safeguards.

## Live-scope status marker (2026-10-11)
LMS Phase 3B nonproduction source/contract gates were accepted; Phase 4A read-only discovery closed with known residual issues; Phase 4B G03 source-only ADR metadata alignment merged in BE `main=617dadc0d0d627071d713ceb729df6658202b43e`, CI 7/7; **production and live trust/Redis/key custody gates not certified**. For current state, re-read [LMS README](../lms/README.md) and [ledger](../lms/engineering-end-to-end-progress-ledger.md) before action.

## Primary frozen authorities
[Physical placement contract](../lms/master-infrastructure-placement-contract.md) · [Logical/API contract](../lms/logical-service-boundary-api-contract.md) · [Current engineering ledger](../lms/engineering-end-to-end-progress-ledger.md)
