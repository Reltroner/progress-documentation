# Reltroner LMS — Phase 3A-04 FZ-10: Phase 3B Entry/Exit Contract & Conditional Implementation Authorization

> **Owner instruction:** `lanjutkan FZ-10 — Phase 3B Entry/Exit Contract & Implementation Authorization`.  
> **Decision date:** 2026-10-09, Asia/Jakarta (exact clock time not evidenced).  
> **Decision:** **FZ-10 PASS — owner-approved, narrowly scoped future non-production work order.**  
> **Activation:** **CONDITIONAL ON FZ-11 FINAL PHASE 3A FREEZE ACCEPTANCE + MERGED DOCS**; no execution immediately.  
> **Strict exclusion:** No VPS/Keycloak/PostgreSQL/Redis/DNS/Cloudflare production mutation, no full business endpoint implementation, no new paid service.

## 0. Outcome, authority and interpretation

FZ-10 fixes an executable **plan** for Phase 3B, including explicit branch/file boundaries, staged tasks, 28 measurable test/exit criteria, evidence format and stop conditions. The owner's instruction to proceed with FZ-10 ratifies this **work order** but does not waive the previous rule that 3A must be FROZEN in FZ-11 before IDE agents are assigned implementation tasks.

**Now:** `FZ-10 = APPROVED (CONDITIONAL)`; `PHASE 3A = NOT FROZEN`; `PHASE 3B = NOT YET EXECUTABLE`; `PHASE 4/PRODUCTION = NOT AUTHORIZED`.

## 1. Reviewed Git provenance and unchanged binding surface

| Source | Current exact SHA at FZ-10 review | Role |
|---|---|---|
| Documentation main | `6dbc98d32ea9416f0bdb57045ae6d2e15db16199` | Contains merged FZ-02/FZ-03/FZ-04 and both binding contracts |
| LMS-BE main | `e30a61780994d85671cbf079e6b9ce899b3fe837` | Six Laravel 13 foundation apps, PHP `^8.3`, PHPUnit `^12` requirements |
| LMS-FE main | `f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7` | Next.js 16.2.6 / Contentlayer, catalog and existing validation scripts |
| Physical 0C contract | blob `b899761c9e833f9fa567055801b9ba0834ed56eb` | 20 invariants FROZEN, text unchanged |
| Logical Phase 1 contract | blob `cf089b8df4b5ccb1761b504ffae662a0053bf03e` | 24 invariants FROZEN, 26 API operations |

Observed BE snapshot: six service-local `routes/api.php` foundations, feature tests for health/problem-details/CORS/service boundaries, separate Composer projects. **No Phase 3B CI result is claimed.** Observed FE: npm scripts already perform typecheck/lint/content/resource/orphan validations and Next build, but current generation paths lack complete published-only negative control. **No FE production exposure is claimed.**

## 2. Entry and release authorization model

1. **Entry 3B hard blocker:** FZ-11 Final Phase 3A Design Freeze Acceptance Record must be explicitly approved by project owner, merged, SHA-pinned. Merely completing this FZ-10 documentation task does not satisfy it.
2. **Git preflight:** inspect new current `LMS-BE` and `LMS-FE` branch refs, clean worktrees, base commits and existing CI. If drift from reviewed base, stop and reconcile.
3. **Scoped authorization:** once FZ-11 is satisfied, the approved Phase 3B **source-only** implementation may use new dedicated feature branches. Each work package needs an explicit file allowlist, acceptance tests and rollback/PR plan. This plan is the owner-approved scope ceiling, not permission to perform unrelated refactors.
4. **Production boundary:** no Keycloak provisioning, live JWT retrieval, DB migrations on production, SSH mutations, DNS/TLS/Cloudflare changes, Docker runtime start/stop, package upgrades or live API exposure. Phase 4 needs its own owner-authorized change window.
5. **Human/AI division:** ChatGPT/human inspect architecture, define constraints, review evidence and decide acceptance; IDE agent only writes allowed code after freeze and preflight; terminal runs only explicitly approved local CI/testing; GitHub PR/merge follows independent acceptance.

## 3. Work packages (ordered; independent branches/PR per checkpoint)

| ID | Package | Repo | Deliverable minimum | Mandatory exit IDs |
|---|---|---|---|---|
| `3B-01` | API & OpenAPI 3.1 Contracts | LMS-BE | openapi-v1.yaml/json; operation-capability-policy-matrix; RFC7807/error schemas; pagination/idempotency fixtures | B3-AC01, B3-AC02, B3-AC03, B3-AC04 |
| `3B-02` | OIDC Client and Internal Trust Contract | LMS-BE | identity-policy/schema; sanitized-invalid-token-matrix; internal-delegation-ADR/spec; client-scope-config-candidate | B3-AC05, B3-AC06, B3-AC07, B3-AC08 |
| `3B-03` | Persistence/Event Contract | LMS-BE | 4-owner-schema-contracts; 9-event-schema-fixtures; outbox-inbox-delivery-contract; booking-slot-constraint-design; admin-audit-reconciliation-spec | B3-AC09, B3-AC10, B3-AC11, B3-AC12 |
| `3B-04` | Catalog Manifest, Stable IDs & Public Privacy Guard | LMS-FE | versioned-manifest-schema+tests; 31-lesson-ID-migration-map; public-only-asset/search/route-test; Studio-provenance-policy | B3-AC13, B3-AC14, B3-AC15, B3-AC16 |
| `3B-05` | Independent Six-Service + FE CI | LMS-BE, LMS-FE | 6-service-PHP-CI-matrix; FE-content-privacy-build-checks; contract-version-lint; reproducible-lockfile-check | B3-AC17, B3-AC18, B3-AC19, B3-AC20 |
| `3B-06` | Consumer/Provider and Negative Compatibility | LMS-BE, LMS-FE | provider-consumer-snapshot-tests; negative-auth-and-object-access-fixtures; event-replay-index-version-compat-tests; private-ingest-trust-schema-tests | B3-AC21, B3-AC22, B3-AC23, B3-AC24 |
| `3B-07` | 3B Certification & Evidence Freeze | LMS-BE, LMS-FE, progress-documentation | signed-CI-evidence-index; source-SHA-matrix; risk/deferral-register; Phase3B-exit-acceptance-proposal | B3-AC25, B3-AC26, B3-AC27, B3-AC28 |

**Sequencing:** 3B-01 and 3B-02 define common contracts; 3B-03 and 3B-04 may develop in parallel once required schema and trust version are pinned; 3B-05 builds CI around pinned fixtures; 3B-06 proves compatibility/negatives; 3B-07 signs the phase evidence. Parallel coding cannot bypass gated security or release acceptance.

## 4. 26 frozen public API operations — required contract-only inventory

| ID | Method + path | Contract owner | Required capability/policy | Authorized browser context | Cross-contract consideration |
|---|---|---|---|---|---|
| `API-01` | `GET /api/v1/me` | gateway | `AUTHENTICATED_NO_NAMED_CAPABILITY` | any_valid_lms_client | Safe principal projection only |
| `API-02` | `GET /api/v1/learning/enrollments` | learning | `learning.enrollment.read.self` | lms-user | Scoped to authenticated sub |
| `API-03` | `POST /api/v1/learning/enrollments` | learning | `learning.enrollment.create.self` | lms-user | Version-pinned course enrollment |
| `API-04` | `GET /api/v1/learning/enrollments/{enrollment_id}` | learning | `learning.enrollment.read.self` | lms-user | Ownership by signed sub |
| `API-05` | `GET /api/v1/learning/courses/{course_id}/progress` | learning | `learning.progress.read.self` | lms-user | Current accepted curriculum revision |
| `API-06` | `PUT /api/v1/learning/courses/{course_id}/lessons/{lesson_id}/progress` | learning | `learning.progress.write.self` | lms-user | Stable lesson IDs; enrollment server resolved |
| `API-07` | `GET /api/v1/learning/bookmarks` | learning | `learning.bookmark.read.self` | lms-user | Owner only |
| `API-08` | `PUT /api/v1/learning/bookmarks/{content_id}` | learning | `learning.bookmark.write.self` | lms-user | Idempotent bookmark |
| `API-09` | `DELETE /api/v1/learning/bookmarks/{content_id}` | learning | `learning.bookmark.write.self` | lms-user | Owned bookmark only |
| `API-10` | `GET /api/v1/mentorship/offerings` | mentorship | `mentorship.offering.read` | PENDING_PUBLIC_PROJECTION_POLICY | Optional guest-safe offering view, policy required |
| `API-11` | `GET /api/v1/mentorship/offerings/{offering_id}` | mentorship | `mentorship.offering.read` | PENDING_PUBLIC_PROJECTION_POLICY | No private mentor attributes for guest |
| `API-12` | `GET /api/v1/mentorship/availability` | mentorship | `mentorship.booking.create.self` | authenticated_lms_user | Owner approved booking-oriented availability; no anonymous exposure |
| `API-13` | `GET /api/v1/mentorship/bookings` | mentorship | `mentorship.booking.read.self` | lms-user | Bookings for signed sub only |
| `API-14` | `POST /api/v1/mentorship/bookings` | mentorship | `mentorship.booking.create.self` | lms-user | Durable idempotency and occupancy uniqueness |
| `API-15` | `GET /api/v1/mentorship/bookings/{booking_id}` | mentorship | `mentorship.booking.read.self` | lms-user | Object authorization |
| `API-16` | `POST /api/v1/mentorship/bookings/{booking_id}/cancel` | mentorship | `mentorship.booking.cancel.self` | lms-user | Cancellation lifecycle and replay |
| `API-17` | `GET /api/v1/knowledge/search` | knowledge | `knowledge.search` | authenticated_lms_client | ACL checked in Knowledge |
| `API-18` | `POST /api/v1/assistant/query` | assistant | `assistant.use` | authenticated_lms_client | No direct state mutation |
| `API-19` | `GET /api/v1/admin/principals` | gateway+audit | `admin.principal.read` | lms-admin | Restricted Keycloak projection |
| `API-20` | `GET /api/v1/admin/principals/{principal_id}` | gateway+audit | `admin.principal.read` | lms-admin | Privileged principal projection |
| `API-21` | `PATCH /api/v1/admin/principals/{principal_id}/roles` | gateway+audit | `admin.principal.role.manage` | lms-admin | Durable audit intent and reconciliation |
| `API-22` | `GET /api/v1/admin/mentorship/bookings` | mentorship+audit | `admin.mentorship.read` | lms-admin | Admin plane only |
| `API-23` | `GET /api/v1/admin/mentorship/bookings/{booking_id}` | mentorship+audit | `admin.mentorship.read` | lms-admin | Admin plane only |
| `API-24` | `PATCH /api/v1/admin/mentorship/bookings/{booking_id}` | mentorship+audit | `admin.mentorship.manage` | lms-admin | Audit privileged edit |
| `API-25` | `GET /api/v1/admin/audit-events` | audit | `admin.audit.read` | lms-admin | Audit readonly, bounded pagination |
| `API-26` | `GET /api/v1/admin/audit-events/{audit_event_id}` | audit | `admin.audit.read` | lms-admin | Audit readonly |

**Scope note:** `AUTHENTICATED_NO_NAMED_CAPABILITY` for `GET /me` is not a new permission. Public offering read projection remains **pending explicit per-route policy**; do not claim guest auth bypass without a sanitized response policy. `mentorship.booking.create.self` for authenticated booking-oriented availability reflects owner-accepted design direction. `admin.learning.read` and `admin.learning.override` remain reserved capabilities **without fabricated public routes**. For protected API, capability, `azp`, resource ownership and service workload assertions must all be consistent.

## 5. Immutable namespace and event family locks

**Capability allowlist (19):** `learning.enrollment.read.self`, `learning.enrollment.create.self`, `learning.progress.read.self`, `learning.progress.write.self`, `learning.bookmark.read.self`, `learning.bookmark.write.self`, `mentorship.offering.read`, `mentorship.booking.read.self`, `mentorship.booking.create.self`, `mentorship.booking.cancel.self`, `knowledge.search`, `assistant.use`, `admin.principal.read`, `admin.principal.role.manage`, `admin.mentorship.read`, `admin.mentorship.manage`, `admin.learning.read`, `admin.learning.override`, `admin.audit.read`.

**Semantic events (9):** `learning.enrollment.created`, `learning.progress.updated`, `learning.course.completed`, `mentorship.booking.created`, `mentorship.booking.cancelled`, `mentorship.session.completed`, `identity.role.changed`, `knowledge.index.requested`, `knowledge.index.completed`.

Four logical database authorities: `lms_learning_db`, `lms_mentorship_db`, `lms_knowledge_db`, `lms_audit_db`. Gateway and Assistant have no default durable domain database. Redis is ephemeral transport, not correctness authority. Studio is canonical for Asthortera/editorial canon; LMS source-controlled catalog is canonical for LMS course publication. No extra service, public route, event name, capability or writable domain database is authorized.

## 6. Phase 3B acceptance tests: 28 mandatory IDs

| Test | Package | Required observed result | Current |
|---|---|---|---|
| `B3-AC01` | `3B-01` | 26 unique frozen API method+paths in versioned OpenAPI, no extra public family | **NOT RUN** |
| `B3-AC02` | `3B-01` | 19 exact capabilities declared, admin.learning.* reserved/unrouted, explicit guest-offerings policy | **NOT RUN** |
| `B3-AC03` | `3B-01` | 401/403, RFC7807, request ID, bounded pagination and idempotency schema examples validation | **NOT RUN** |
| `B3-AC04` | `3B-01` | Every operation has owned service, method, authorization rule and status/error fixture; provider mocks align | **NOT RUN** |
| `B3-AC05` | `3B-02` | Identity schema pins issuer/audience/azp, separate clients, PKCE S256, denial on missing cap | **NOT RUN** |
| `B3-AC06` | `3B-02` | Invalid/sibling client, ID-token misuse, forged/stale roles, issuer/aud mismatch negative fixtures | **NOT RUN** |
| `B3-AC07` | `3B-02` | Workload identity + signed delegation schema and recipient/caller/operation bound claims, rotation/nonce/replay negative fixture | **NOT RUN** |
| `B3-AC08` | `3B-02` | No HRM global mapper edits or unbound principal headers, Keycloak provisioning deferred Phase 4 | **NOT RUN** |
| `B3-AC09` | `3B-03` | 4 databases owner/grant spec, negative cross-read/write and migration compatibility fixtures | **NOT RUN** |
| `B3-AC10` | `3B-03` | 9 semantic event names and versioned payload schemas with source/PII bounds | **NOT RUN** |
| `B3-AC11` | `3B-03` | Outbox/inbox dedup/retry/failover contract includes commit-before-publish crash and broker duplicate tests | **NOT RUN** |
| `B3-AC12` | `3B-03` | Slot occupancy plus idempotency independent; admin role mutation Audit intent/reconciliation spec | **NOT RUN** |
| `B3-AC13` | `3B-04` | All 31 MDX lessons have audited stable IDs or versioned migration fixtures; slug renames preserve ID | **NOT RUN** |
| `B3-AC14` | `3B-04` | Manifest JSON canonicalization deterministic on repeat build; published course revision distinct from global hash | **NOT RUN** |
| `B3-AC15` | `3B-04` | Public static output negative suite excludes unpublished routes, bundled search, sitemap, metadata, asset refs | **NOT RUN** |
| `B3-AC16` | `3B-04` | Studio published canon attestation/access-rights separate from LMS publication; unattested filtered | **NOT RUN** |
| `B3-AC17` | `3B-05` | 6 independent Laravel service CI checks run and pass on locked dependencies with recorded output | **NOT RUN** |
| `B3-AC18` | `3B-05` | Next.js FE build, typecheck, lint, content/resource/orphan and public privacy tests pass on pinned FE SHA | **NOT RUN** |
| `B3-AC19` | `3B-05` | CI catches intentionally malformed OpenAPI, role escalation, catalog draft, event schema drift fixtures | **NOT RUN** |
| `B3-AC20` | `3B-05` | No direct prod DB/Keycloak/VPS, no secrets/tokens embedded in fixtures/logs, failed jobs fail closed | **NOT RUN** |
| `B3-AC21` | `3B-06` | Consumer/provider version compatibility rejects breaking differences within /api/v1 without approved strategy | **NOT RUN** |
| `B3-AC22` | `3B-06` | Negative contract suites cover unauthorized object IDs, admin context, guest service, private search snippets | **NOT RUN** |
| `B3-AC23` | `3B-06` | Outbox duplicate/out-of-order and index rollback contract tests pass using isolated deterministic simulations | **NOT RUN** |
| `B3-AC24` | `3B-06` | Knowledge release authentication/provenance contract rejects unapproved Git artifact and forged release | **NOT RUN** |
| `B3-AC25` | `3B-07` | All scoped acceptance tests/fixtures green with CI run URL, timestamp, commits and reviewer evidence | **NOT RUN** |
| `B3-AC26` | `3B-07` | 44 frozen invariants linked to tests or still explicit future runtime gates; no fake runtime certification | **NOT RUN** |
| `B3-AC27` | `3B-07` | No unapproved source/service/API/capability/event/DB ownership drift; all deviations rejected or formal ADR | **NOT RUN** |
| `B3-AC28` | `3B-07` | Signed 3B exit acceptance plus distinct Phase 4 work order/production authorization before provisioning | **NOT RUN** |

All B3 acceptance IDs are **SPECIFIED / NOT EXECUTED** as of this phase. A pass requires a real pinned commit, deterministic test command and observed logs or CI links; mere JSON fixture validity is not enough for production efficacy.

## 7. CI implementation and evidence contract

**Backend:** Independent CI for `services/gateway`, `learning`, `mentorship`, `knowledge`, `assistant`, `audit`. Use tested repo PHP/Composer lockfile versions and isolated SQLite or ephemeral nonproduction PostgreSQL only when needed. Execute formatting, PHPUnit and contract/schema lint. No shared user database, no live Keycloak token; simulate malformed assertions with non-secret fixtures. Avoid changing Composer version baselines without separately reviewed reproducibility rationale.

**Frontend:** Run repository's existing `npm ci`-compatible pinned dependency flow, contentlayer/build, typecheck/lint, content/resource/orphan checks, and new published-only artifact inspection. Verify export output, search JSON, URLs, sitemap, pre-render metadata and public assets for draft/preview-only material, including missing statuses. Refactor only within explicit Phase 3B allowlist and prove stable lesson ID mapping and backward compatibility.

**Evidence template:** work package ID, expected input SHA, actual branch/head SHA, changed file list, exact test command, exit code, CI URL, timestamp, passing/failing test IDs, sanitized stdout/stderr, negative test proof, reviewer, acceptance disposition, rollback instruction. A job marked green without full contract coverage is not acceptance.

**Exit acceptance rule:** all **28/28 B3-AC** executed and PASS for required scope, CI matrices complete, trace 44 frozen invariants to 3B tests or named later runtime gates, no new unapproved public route/capability/event, no publication data leak, no intentionally ignored contract failure; explicit owner review and 3B exit record. Runtime Phase 4/5+ still independently gated.

## 8. Hard stops / escalation

| Condition | Required action |
|---|---|
| FZ-11 missing or merged SHA unknown | **STOP** — no Phase 3B implementation, CI contract planning may be read-only |
| Unexpected Git HEAD or uncommitted changes | **STOP** — source drift preflight reconciliation |
| New public API family or permission needed | **STOP** — frozen Phase 1 contract change control |
| Studio reference lacks attested rights or publication status | **STOP public export/Knowledge ingest** — no silent canon inference |
| FE draft or private content in static build | **BLOCK release** — negative build suite remediation |
| Claim/client/signed delegation accepted without proof | **STOP integration** — identity contract tests/ADR |
| Need production VPS/Keycloak/DB/DNS/Cloudflare mutation | **STOP** — separate Phase 4 owner authorization |
| CI cannot run or a negative test falsely passes | **FAIL checkpoint** — no PR merge as PASS |
| Historical progress migration requires destructive rewrite | **STOP** — dedicated migration/rollback ADR |
| Cost/CPU/RAM evidence unavailable for a resource claim | **NO CAPACITY PASS** — defer to measured Phase 11 acceptance |

## 9. FZ-10 decision and FZ-11 dependency

Owner requested **FZ-10** completion. The 7 work packages, 26 API operation map, 19 capability lock, 9 events, 28 acceptance IDs and no-production scope are **conditionally authorized as a future Phase 3B work order**. Current Phase 3A still **NOT FROZEN**, source coding must not start yet, and no Phase 4/production action is implied.

- **FZ-10: PASS (APPROVED CONDITIONALLY)** — entry/exit and scope signed by owner instruction for work-order planning.
- **FZ-11: OPEN** — must record a separate explicit final 3A freeze decision with SHAs, accepted deferrals and 3B activation.
- **FZ-02/03/04:** source and owner approval already merged to documentation main. No additional source mutation for this FZ-10 record.

Final checkpoint: `FZ-10 WORK ORDER APPROVED (CONDITIONAL) → FZ-11 REQUIRED → PHASE 3B NOT EXECUTABLE YET`.

## 10. Handoff sources

- [Master physical FROZEN](./master-infrastructure-placement-contract.md)
- [Logical service/API FROZEN](./logical-service-boundary-api-contract.md)
- [44-invariant FZ-02 receipt](./reltroner-lms-phase3a-04-fz02-cross-contract-invariant-traceability-20261009.md)
- [18 subordinate ADR FZ-04 receipt](./reltroner-lms-phase3a-04-fz04-subordinate-adr-closure-20261009.md)
- [12 parent ADR acceptance](./reltroner-lms-phase3a-04-ratification-register-20261009.json)
- [FZ-10 machine work order](./reltroner-lms-phase3a-04-fz10-phase3b-work-order-20261009.json)
