# 09 — AI, Universal Search, Visualization & Automation Option Register

> Status: **DESIGN CANDIDATES / NOT blanket deployment authorization**. Read LMS frozen contracts before altering search, auth, persistence, tools or public surfaces.

## Core principle
**Deterministic services own truth. AI composes explanations and optional derived artifacts. Automation executes bounded side effects.** None may silently become source of bookings, permissions, identity, canon or paid entitlement.

## Binding initial service roles
Knowledge Service manages derived searchable data and authorized retrieval; Assistant Service manages bounded LLM orchestration; public static course search stays edge/browser where practical. Assistant initial API is authenticated-only. Knowledge/search service is already among **six frozen microservices**; do not create an extra public search microservice just because a tool is popular.

## Ctrl+K / universal search
Intended UX: Ctrl+K can merge **public static search** and authorized private Knowledge results, without disclosure of owner-only, mentor-only or privileged data. Canonical course content is source-controlled and versioned. Each indexed item needs content version/source reference, permission context and rebuildable provenance.

Early proposed model:
~~~text
static public index ────────┐
                            ├── frontend search UI / Ctrl+K
authorized Knowledge API ───┘
            │
        Assistant retrieval via narrow tools
            │
       citations and source/version
~~~

Initial contract **prefers PostgreSQL FTS**. pgvector/semantic embedding, hybrid ranking and knowledge edges are optional future ADRs, not hard MVP prerequisites.

## AI chatbot vs agent
**LMS Chatbot (candidate):** ask/answer on approved knowledge, cite relevant lesson/concept, explain and compare, recommend reading, return structured visualization specs. It should fail gracefully when provider/AI budgets are exhausted. No arbitrary SQL, permissive file/network execution or unauthorized state mutation.

**Hermes Agent / OpenClaw (candidate, later):** useful only if recurring real work requires stateful context, tools or mentorship preparation. Scope to least-privilege APIs, isolated runtime and reviewed human approval for sensitive actions; not the general-public production authority. Avoid unrestricted shell, production root, Keycloak admin or DB superuser.

**LLM Wiki paradigm (candidate):** compile source-controlled concepts into derived summaries/links/provenance, not rewrite canonical lore or curriculum. Contradiction flags are suggestions for review. A full separate LLM Wiki runtime may be overengineering if existing Knowledge Service suffices.

**n8n (candidate):** deterministic third-party coordination for calendar, Meet/Zoom, approved WhatsApp/Discord/email notifications and retries. Maintain authoritative booking/payment/consent in domain services.

## Visualizations
LLM produces **validated structured specs**, frontend renders using approved components:
- causal/dependency graphs (Mermaid, React Flow or similar);
- timelines and concept maps;
- numerical charts from authorized actual values (Recharts/ECharts or similar).
Do not allow arbitrary AI HTML/JS execution and do not fabricate graph edges or numerical metrics. Always label thought-experiment diagrams separately from observed data.

## Infra and cost boundary
Owner reported Hostinger Ubuntu 24.04 VPS with pre-existing HRM, Keycloak and data services; Cloudflare Pages hosts the static learner frontend. Screenshots show a point-in-time resource snapshot and DNS/UI state, **not spare-capacity certification**.

Priority: use existing shared infra safely; measure CPU, RAM, storage, swap, queue latency and affected HRM/identity SLOs before deploying extra workers/agents. Initial external LLM inference is part of LMS frozen placement; do not assume local inference is free or safe on a 1-vCPU machine.

Avoid concurrent subscriptions/tool overlap without ROI measurement:
- Bolt.new-like frontend generators can help *prototype*, not certify Laravel microservices.
- Bold AI-like multi-channel business tools may duplicate n8n/mentorship workflows.
- Dot meeting note tools can assist **consented** review, but require data governance.
- Dot AI analytics products are distinct from Dot Kubernetes DevOps; product names must be disambiguated with verified URL/pricing before purchase.
- AI coding agents should operate in isolated branches, explicit file allowlists, bounded task scopes and tested PRs; never infer production approval from tool success.

## Option evaluation worksheet
| Candidate | Job-to-be-done | Already solved by | Extra cash/token/VPS cost | Security/privacy burden | Evidence of need | Disposition |
|---|---|---|---|---|---|---|
| pgvector | semantic search | Postgres FTS initially | measure | private indexing | pending | DEFER |
| LLM Wiki worker | derived concept relations | Knowledge Service | model compute | canon contamination | pending | DEFER |
| Hermes/OpenClaw | context-aware mentorship aid | mentor + LMS | compute/ops | high tool access | pending | DEFER |
| n8n | schedule/notification workflows | bounded services + manual process | compute/provider fees | secrets/webhooks | pending | CANDIDATE |
| chat diagrams | learning comprehension | authored visuals | model/frontend work | renderer validation | pending | CANDIDATE |

Do not install or pay until the work order, business need, owner authority and budget are explicit.

## Sources
[Frozen LMS placement](../lms/master-infrastructure-placement-contract.md) · [Frozen LMS service contract](../lms/logical-service-boundary-api-contract.md) · [LMS status](../lms/README.md).
