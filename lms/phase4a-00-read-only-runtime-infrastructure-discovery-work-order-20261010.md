# Reltroner LMS - Phase 4A-00 Read-Only Runtime & Infrastructure Discovery

> **Status:** OWNER-AUTHORIZED FOR READ-ONLY DISCOVERY; GATES PARTIAL; RUNTIME CERTIFICATION NOT ACHIEVED
> **Owner instruction received:** 2026-10-10 Asia/Jakarta: authorize Phase 4A-00 read-only runtime/infrastructure discovery, work order, preflight, gap/acceptance mapping; explicitly prohibit production mutation, provisioning, deployment, application main merges, and frozen architecture modification without subsequent permission.
> **Work order ID:** LMS-P4A-00-20261010
> **Binding source:** [LMS canonical AI entry](./README.md) -> [Phase 0C frozen physical placement](./master-infrastructure-placement-contract.md) -> [Phase 1 frozen logical/API](./logical-service-boundary-api-contract.md) -> [FZ-11 design freeze](./reltroner-lms-phase3a-fz11-final-design-freeze-acceptance-20261009.md), [FZ-10 scoped test contract](./reltroner-lms-phase3a-04-fz10-phase3b-entry-exit-authorization-20261009.md), [ADR-LMS-TRUST-001](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md), [BRANCH-GOV-001](./branch-gov-001-main-branch-contractual-protection-20261010.md), [GOV-WVR-001](./gov-wvr-001-phase3b-branch-protection-owner-exception-20261010.md) and [dated engineering ledger](./engineering-end-to-end-progress-ledger.md).
> **Hard boundary:** This authorizes OBSERVATION and DESIGN OF FUTURE WORK ONLY. It is NOT approval of Phase 4 implementation/4B, new runtime/clients/DBs/secrets, production releases or modifications. No credentials or private keys may enter this documentation or its PR.

## 1. Scope, authority and non-goals

1. Inspect current pinned source on GitHub, immutable frozen contract IDs and prior owner-accepted Phase 3 evidence.
2. Perform safe, low-impact READ-ONLY inventories of existing VPS/operating system, Nginx/PHP-FPM/service boundaries, Keycloak effective realm/client configuration, PostgreSQL roles/database metadata, Redis posture, Cloudflare Pages/DNS/TLS, Premium Hosting public asset delivery, backup observations and HRM coexistence **only where an authorized operator/session actually has visibility**.
3. Write an evidence-first gap matrix with explicit PROVEN_SOURCE, PROVEN_OPERATOR_UI, HISTORICAL_AS_OF, TOOL_UNAVAILABLE, PENDING_RUNTIME or FAIL_OBSERVED status. Missing observations never become FAIL or PASS by inference.
4. Produce bounded candidate implementation packages, capacity estimates (measured before suggested allocation), negative-test proposals, stop/rollback gates, and owner sign-off question(s) **without executing those packages**.

**Forbidden:** any deployment/retry/purge/rollback; writes to server, DNS, TLS/Cloudflare, Keycloak, PostgreSQL or Redis; service start/restart/reload; Nginx -T/config dump; artisan migrate/seed; Docker or package installation; issuing live signing keys or fetching tokens; revealing env/credentials; direct application main writes; deleting branches/worktrees; aggressive network or port scans; modifying HRM. Do not run unreviewed generated shell scripts with broad privileges. Do not record sensitive raw output publicly.

## 2. Deterministically pinned preflight - findings already observed

| Evidence ID | Source / exact main SHA | Observation | Scope and limit |
|---|---|---|---|
| P4A00-E01 | Reltroner/LMS-BE main a2672d0085fe84b55520f8f52f41a8c7fc8568a0 | GitHub main verified, [push-main Actions 37970800113](https://github.com/Reltroner/LMS-BE/actions/runs/37970800113) 7/7 completed/success | Source and CI; **not** deployed six services |
| P4A00-E02 | Reltroner/LMS-FE main eb01a4d2c924299b929aebf0f4826b94cf341fc6 | GitHub main verified, [push-main Actions 37987959614](https://github.com/Reltroner/LMS-FE/actions/runs/37987959614) 2/2 completed/success; 19/19 catalog tests, published-only output and 25/25 static pages; old Contentlayer exception absent in inspected CI logs | Source/static export, **not** public Pages release |
| P4A00-E03 | progress-documentation main 47d17dda0f359f97c14a6c4c4f96ae622f25d3dd | Canonical README, ledger through section 38, frozen contracts and acceptance receipts present; no open docs PR at discovery | This is the **pre-work-order** docs main; later docs merge SHA must be recorded separately |
| P4A00-E04 | Phase 3B owner closure/architecture | 28/28 accepted for nonproduction scope: 27 scoped (including branch-rule waiver), 1 trace-only; 44/44 physical/logical invariant trace rows. Phase 3A FZ-11 frozen. | **0 newly live-certified invariants** by Phase 3; global product DoD incomplete |
| P4A00-E05 | BE service repository | Six separate Laravel service directories: gateway, learning, mentorship, knowledge, assistant, audit. Six services/*/routes/api.php files contain only the PHP opening tag at current main; gateway bootstrap registers separate health.php and standard error middleware. | The 26 frozen public method/path operations are **contract/mocks**, not proven business HTTP handlers/runtime |
| P4A00-E06 | FE source .env.example at current main | Keys include NEXT_PUBLIC_OIDC_AUTHORITY and NEXT_PUBLIC_OIDC_CLIENT_ID; example values still reference legacy sso.reltroner.com and lms-reltroner instead of canonical auth.reltroner.com/realms/reltroner and separate lms-user/lms-admin. | **Tracked template drift**, not evidence of effective Cloudflare/browser/runtime environment variables |
| P4A00-E07 | BE contracts/identity | trust-contract.json retains PENDING_SECURITY_ADR markers; crypto-profile-proposal.json retains CANDIDATE_NOT_OWNER_RATIFIED_SECURITY_ADR. Later owner-ratified ADR-LMS-TRUST-001 is authoritative for design. | **Temporal source metadata drift**, not authority to edit frozen contracts or provision real tokens |
| P4A00-E08 | GitHub governance | BE and FE main protected:false in branch API; manual BRANCH-GOV-001 and scoped GOV-WVR-001 are the applicable owner policy. | Waived only for Phase 3; do not claim machine protection or later release waiver |
| P4A00-E09 | Owner-supplied local Windows record | Earlier isolated PR5 Windows regression clean with 19/19 and negative absent-staging exit 1. Two temporary verification worktrees subsequently removed non-force, all target ancestry checks passed; primary FE checkout still had 3 tracked/untracked entries at last owner audit and an old local main HEAD. | Local operator report, not a fresh main-synced local proof; **do not reset/clean primary checkout** |
| P4A00-E10 | Owner Cloudflare Pages UI | Supplied deployment detail ID 8f0dbc2a-dfcf-4644-8a4c-d97480c854b9 showed **Preview** skip on prior d0e4d74 source. Main eb01a4d2 commit subject begins [CF-Pages-Skip]. | Actual **Production/main** deployment history for eb01a4d2 and final active deployment **not yet observed** |
| P4A00-E11 | Public endpoints attempted by assistant | Standard read-only fetch for lms, lms-admin, lms-api/health, auth realm well-known configuration and assets did **not** yield usable host evidence in current tool environment; environment-level resolver returned no usable addresses. | TOOL_UNAVAILABLE: cannot infer DNS absence, downtime, listener posture or TLS misconfiguration |
| P4A00-E12 | Phase 0A/0B historical physical discovery | Ubuntu 24.04, KVM VPS approximately 1 vCPU/4 GiB RAM/2 GiB swap/48 GiB disk; Nginx/PHP 8.4 FPM, PostgreSQL 18, Redis 8, native Keycloak and HRM coexistence; prior Cloudflare zone Full TLS. | HISTORICAL_AS_OF 2026-10-07, **not live measured in Phase 4**. Do not treat numbers/versions/ports as current |

**Evidence discipline:** Proof categories above are explicit. Do not label all Phase 4 runtime resources PASS merely because Phase 3 GitHub Actions passed on SQLite/array/sync test configuration. Confirm source heads again before any next action.

## 3. Frozen placement map vs required actual observations

| System / ownership | Frozen expectation | Read-only evidence still needed |
|---|---|---|
| Learner | lms.reltroner.com, static frontend via Cloudflare Pages | Public DNS, effective hostname mapping, active Production deployment SHA and no draft/archived exposure |
| Admin | lms-admin.reltroner.com, independent browser client and Pages deployment | DNS, actual admin Pages project/client/redirect, cross-client denial design; no admin APIs claimed live |
| Public API Gateway | lms-api.reltroner.com -> Cloudflare proxy -> VPS Nginx -> Gateway only | Observed edge/origin route and TLS, Nginx public listener/service mapping, minimal external ingress |
| Private Laravel services | Learning, Mentorship, Knowledge, Assistant, Audit: private/loopback only | Read-only process/service/sockets inventory; negative public exposure **planned**, no active scans now |
| Identity | auth.reltroner.com/realms/reltroner, lms-user and lms-admin browser clients, lms-api audience; HRM unaffected | Live OIDC discovery metadata, redacted Keycloak client IDs/redirect/origin/capability/audience inventory, HRM baseline |
| PostgreSQL | Four distinct LMS owner DBs: lms_learning_db, lms_mentorship_db, lms_knowledge_db, lms_audit_db; no direct cross-write | pg version/listening addresses; database existence, role grants and owner-only boundaries via read-only catalog views, no DDL |
| Redis | Local/private and replaceable runtime transport, queue/cache/replay, not durable business truth | Version, bind/auth posture, keyspace/eviction and memory headline without values, replay loss/recovery design only (no fault injection) |
| Content Catalog | Git-owned allowlisted published LMS content, separate from Studio published canon/attestation | Manifest SHA, source release provenance, FE output-only privacy already CI-tested; release lineage still must be tracked |
| Knowledge / search / AI | PG FTS initially; external LLM initially; no required local LLM on KVM1 | Candidate capacities and vendor cost/limits; no Meilisearch/Kafka/K8s/LLM daemon assumed |
| Assets | assets.reltroner.com through Cloudflare/Premium Hosting; immutable versioned assets | Public origin, cache policy and exact release paths; avoid any manual canonical-only upload |
| Security/ops | Existing HRM/Keycloak retained; backup/restore, TLS Full (strict) future gated, minimal open ports | Service inventory, disk growth, backups last-success metadata, certificate issuance/expiry, redacted observability and operator authority |

## 4. Operator-only read-only collection protocol

**This assistant currently has read-only GitHub data but no authenticated Cloudflare, VPS SSH, Keycloak admin or database session. Do not claim those were inspected.** The human operator must choose any permissible access and return *sanitized evidence*, not credentials. Always preserve a timestamp, scope, access identity class (not actual user/token), commands, and before/after=NO_MUTATION.

### 4A-00/P1 - Windows local Git and DNS/HTTPS (PowerShell 5.1, no source changes)

~~~
$ErrorActionPreference = 'Stop'
$BE = 'C:\Projects\lms-reltroner-backend'
$FE = 'C:\Projects\lms-reltroner-studio'
git -C $BE rev-parse HEAD
git -C $BE status --porcelain=v1 --untracked-files=all
git -C $BE remote -v
git -C $FE rev-parse HEAD
git -C $FE status --porcelain=v1 --untracked-files=all
git -C $FE worktree list --porcelain
# These do not fetch/reset/checkout. Do not paste actual private .env content.
Resolve-DnsName lms.reltroner.com -Type A -ErrorAction Continue
Resolve-DnsName lms-admin.reltroner.com -Type A -ErrorAction Continue
Resolve-DnsName lms-api.reltroner.com -Type A -ErrorAction Continue
Resolve-DnsName auth.reltroner.com -Type A -ErrorAction Continue
Resolve-DnsName assets.reltroner.com -Type A -ErrorAction Continue
~~~

Do not run Windows git pull/reset/clean: the primary FE checkout was previously observed old and dirty. DNS queries only establish one resolver's answers at one time, not correctness of production paths.

### 4A-00/P2 - VPS basic inventory (SSH after operator has authenticated, read-only)

Run selectively, as an unprivileged operator where possible. Do not paste public IPs, process environment, database data, host tokens or account secrets into GitHub.

~~~sh
date -u '+%Y-%m-%dT%H:%M:%SZ'
cat /etc/os-release
uname -sr
uptime
free -h
swapon --show
df -hT
df -i
nproc
php -v
nginx -v
psql --version
redis-server --version
systemctl is-active nginx php8.4-fpm postgresql redis-server keycloak 2>/dev/null || true
ss -lntH
~~~

Record service-unit names if they differ. Listener inventory is OBSERVED_ONLY, never a request to bind or expose ports. Do not use nginx -T, printenv, phpinfo, ps eww, systemctl cat/show Environment, journalctl dumps, cat .env, pg_dump, redis-cli CONFIG GET requirepass, or public port scanning. If any command needs elevated privileges, **record BLOCKED_BY_ACCESS** and request a separately scoped reviewed escalation, not sudo by default.

### 4A-00/P3 - Keycloak/PG/Redis/Cloudflare GUI and permitted metadata

- Keycloak: observe realm issuer/version/JWKS metadata and actual LMS client *public identifiers*, redirect URI policies, scopes, admin client isolation, lms-api audience. Observe existing HRM client realm/redirect invariants. DO NOT create/update clients, assign roles, obtain user tokens, expose secrets, or touch HRM.
- PostgreSQL: from an already authorized catalog-read-only session, observe server version, existing database names/owners, effective roles and logical access policy; redact usernames and all connection strings. DO NOT create roles/DBs, grant/revoke, run migrations, read business rows, or test cross-service writes yet.
- Redis: read-only process/version/bind, configured persistence/eviction metadata when authorized; never FLUSHALL, DEL, SET/NX, restart, ACL changes, or replay-fault testing in this work order.
- Cloudflare: open Pages project lms-fe -> Deployments -> environment Production -> branch main; capture source SHA eb01a4d2 and whether skipped/no deployment occurred; record **currently active Production deployment SHA separately**. Also inspect preview deployment branch on 5f2ac1f if needed. Observe, do not retry/delete/redeploy. DNS/TLS and Full vs Full (strict) read-only screenshots or redacted tables; no zone-wide toggle.
- Premium Hosting: observe assets path/immutable release structure and limits without copying private account or billing details; do not upload or change CDN/cache.
- Existing VPS backups/HRM: confirm available backups/last success/size and resource usage **metadata only**; no restore drill or HRM mutations.

## 5. Acceptance matrix - preliminary gate disposition

PASS_SOURCE = verified from current GitHub/documented owner decision; PARTIAL_OPERATOR = scoped owner-provided evidence; PENDING_RUNTIME = direct observation missing; TOOL_UNAVAILABLE = assistant environment cannot inspect. A PENDING gate is **not** failure of the service.

| Gate | Mandatory exit evidence | Current evidence/disposition |
|---|---|---|
| P4A00-AC01 | Explicit scope and owner read-only authorization recorded | **PASS_OWNER** (this instruction) |
| P4A00-AC02 | BE/FE/docs main SHA, PRs, fresh push-main CI and no source drift | **PASS_SOURCE** E01-E03; local FE separate |
| P4A00-AC03 | Both frozen parents, 44 invariants and ratified ADR/waiver precedence | **PASS_DOCUMENT** E04 |
| P4A00-AC04 | Six-service source layout, tests/API implementation state, FE/OIDC templates | **PASS_SOURCE** E05-E07 |
| P4A00-AC05 | Local primary clone state/dirty changes, no destructive synchronization | **PARTIAL_OPERATOR** E09, fresh local status PENDING |
| P4A00-AC06 | Fresh timestamped VPS CPU/RAM/swap/disk/inode/capacity and version output | **PASS_OPERATOR_READ_ONLY** E13; single timestamped snapshot, not load test or six-service capacity certification |
| P4A00-AC07 | Nginx/PHP-FPM/service unit and ports/socket/public/private routing matrix | **PARTIAL_OPERATOR** E13-E17: active units/PIDs; three enabled Nginx symlinks verified to matching sites-available targets; only pool file `www.conf` (22,133 bytes); effective upstream/listener routes, FPM pool content, LMS six-service private exposure NOT VERIFIED |
| P4A00-AC08 | Keycloak effective issuer/JWKS/client/audience and HRM nonregression baseline | **PARTIAL_OPERATOR / LMS CLIENT PROVISIONING GAP OBSERVED** E18-E22: issuer/JWKS verified; 8 listed clients lack `lms-user`/`lms-admin`, 17 listed scopes have no LMS-named scope, 6 realm roles and 11 auth flows observed; current token/session/login/brute-force policies recorded. HRM Phase 6 frozen identity/client/flow details are historical accepted baseline, not fresh live behavior. Dedicated OIDC `roles` mapper and `aud=lms-api` claim, client overrides, LMS PKCE/JWT, HRM live nonregression remain UNVERIFIED. No mutations. |
| P4A00-AC09 | Four PostgreSQL DB/role/grant existence vs intended owned state | **PARTIAL_OPERATOR / ACCESS_BLOCKED** E13-E17/E25: PostgreSQL `18/main` online and local TCP accepting connections; Unix-socket psql catalog query as OS user deploy for DB postgres was denied by pg_hba.conf (no local entry). No authenticated SQL, existence/ownership of four LMS DBs, role GRANTs or cross-write isolation proof; DO NOT escalate or modify HBA. |
| P4A00-AC10 | Redis topology, memory/keyspace/replay posture with no secret exposure | **PARTIAL_OPERATOR / ACCESS_BLOCKED** E13-E14/E25: Redis unit active, loopback 6379, process identity and RSS observed; four anonymous INFO requests (server, memory, persistence, keyspace) returned NOAUTH. Metadata/ACL/effective server configuration, eviction, durability and replay reset safety remain UNVERIFIED; DO NOT supply secrets or weaken Redis authentication. |
| P4A00-AC11 | Cloudflare Pages real Production/main skipped state at eb01a4d2 + active deployment SHA | **PASS_OPERATOR_CLOUDFLARE_UI (SCOPED)** E23: Pages project lms-fe shows Production/main eb01a4d with No deployment available; current active Production deployment remains f2d4041. GitHub FE main verified as eb01a4d2c924299b929aebf0f4826b94cf341fc6. Automatic deployments enabled; phase3-dev Preview releases existed. This is not a live HTTPS/site-content proof, preview privacy audit or guarantee for future commits. |
| P4A00-AC12 | External vantage-point DNS/TLS for exact approved hostnames | **PARTIAL_OPERATOR_EXTERNAL_VANTAGE** E24/E26: Windows DNS+HTTPS confirms lms/auth/hrm resolve and curl HTTP 200/302/302, exit 0, TLS_VERIFY 0; Windows and VPS cannot resolve lms-admin/lms-api/assets (Windows curl exit 6). Cloudflare 16/16 zone records omit these three names; zone mode Full, NOT Full (strict). No all-host TLS chain, effective origin certificate validation or API/Admin/asset routes. Full AC12 NOT PASSED. |
| P4A00-AC13 | Hosting asset origin, immutable URL/capacity and CDN status | **PARTIAL_OPERATOR / ASSET_HOSTNAME_NOT_RESOLVING** E24/E26: assets.reltroner.com absent from displayed Cloudflare 16/16 records, DNS failed on VPS and Windows, HTTPS curl exit 6. Premium Hosting origin, storage capacity, immutable artifact paths, cache/CDN and provider backup remain UNVERIFIED; do not infer origin storage missing or delete/create assets. |
| P4A00-AC14 | HRM coexistence capacity + backup/monitoring/recovery metadata | **PARTIAL_OPERATOR** E13-E15/E26: VPS still 1 vCPU, 3.8 GiB RAM/2.6 GiB available, root 48G/42G available, all six checked systemd units active; Keycloak Java RSS ~664 MiB. /var/backups contains 39 files visible, newest mtime 2026-10-10T01:45:52Z; reltroner-postgres-backup.timer last triggered 03:20:14Z and next scheduled following day. Timer existence/trigger and file count DO NOT prove successful/recoverable offsite PostgreSQL or provider backups. HRM peak budget/recovery remains OPEN. |
| P4A00-AC15 | Redacted security/secret custody/process permission inventory (metadata only) | **PENDING_RUNTIME** |
| P4A00-AC16 | Per-gap owner, criticality, concrete negative tests, blast radius, rollback, cost and forward gates | **PARTIAL_DESIGN** section 6; requires runtime facts |
| P4A00-AC17 | No mutation, no secrets, no unauthorized application merge, reviewed evidence | **PASS_SCOPE_SO_FAR**; repeat at exit |
| P4A00-AC18 | Final AI-portable discovery receipt with owner acceptance and next implementation work order | **PENDING_OWNER_FINAL** |

**Phase 4A-00 exit is NOT passed** while fresh runtime observations above are pending. Do not use a green status total as proof that later Phase 4 implementation is authorized. Required runtime negative tests (real JWT failures, principal confusion, Redis flush/recovery, DB GRANT denials, port exposures, HRM regression) are **design-only plans here**, and must not be executed on production under read-only permission.

## 6. Gap register and later phase sequencing (planning only)

| ID | Gap / evidence class | Risks and scope | Required owner decision before mutation |
|---|---|---|---|
| P4A-G01 | Source BE 26 APIs contract-only, six api.php skeletons (PROVEN_SOURCE) | No business endpoints/capability middleware actually observed; CI source fixture green is not live E2E | Choose bounded Phase 4B provider/gateway contract/identity implementation package after fresh capacity and trust design |
| P4A-G02 | FE .env.example legacy issuer/client (PROVEN_SOURCE) | Wrong issuer/client if template reused; actual production env unknown | Review effective runtime OIDC and separate learner/admin plans; no blind template/Cloudflare env cutover |
| P4A-G03 | BE crypto-status pending marker despite owner ADR (PROVEN_SOURCE) | Runtime could misread source metadata; Ed25519 proof not implemented | Ratified ADR reconciliation and real dual-control runtime tests as separate source PR/work order |
| P4A-G04 | Four LMS PostgreSQL database owners/grants UNVERIFIED; nonprivileged read BLOCKED E25 (OBSERVED_DENIAL) | Existing 18/main cluster online/accepting, but Unix-socket connection as deploy to postgres returned pg_hba.conf no matching entry. This says nothing about the existence/owners/GRANTs of lms_learning_db, lms_mentorship_db, lms_knowledge_db, lms_audit_db or server health. Do not treat deliberate isolation as a defect | Inventory only via an independently authorized catalog-readable DBA/operator session; otherwise preserve ACCESS_BLOCKED and design isolated future permission-negative test package, no sudo -u postgres, HBA edit, credential reuse or DDL in 4A-00 |
| P4A-G05 | Redis persistence/memory/keyspace/replay state UNVERIFIED; unauthenticated INFO BLOCKED E25 (OBSERVED_DENIAL) | Local Redis listening/active; NOAUTH returned for INFO server/memory/persistence/keyspace without Redis authentication. This supports a command-access boundary only; cannot certify ACL design, persistence, eviction, state durability or reset/replay fail-closed behavior | Obtain metrics via already authorized read-only operations monitoring/GUI if available; otherwise record ACCESS_BLOCKED. Keep replay reset/fail-closed and >=65s quarantine fault simulation for separately owner-authorized isolated implementation, no AUTH password, CONFIG/ACL edits, key enumeration or mutation now |
| P4A-G06 | VPS service isolation/capacity PARTIAL E13-E15/E26 (SINGLE-TIME OBSERVATIONS) | Repeated VPS snapshots show 1 vCPU, ~3.8 GiB RAM/2.6 GiB available, 48G root/42G available, low instantaneous load and incumbent Keycloak/HRM processes; no six-service worker budget, PHP-FPM pool isolation, peaks, log/database growth or service-specific accounting. Do not infer capacity sufficiency | Preserve incumbent HRM/Keycloak; compute resource/worker/socket budget from sustained historical monitoring before a separately owner-authorized staged placement, with zero additional spending assumption |
| P4A-G07 | FE PR5 Production/main skip VERIFIED E23 (OWNER_OPERATOR_CLOUDFLARE_UI); residual release-governance risk OPEN | GitHub source main eb01a4d2 differs intentionally from active published Production f2d4041; automatic deployments enabled so current [CF-Pages-Skip] convention alone is no permanent deployment guard; several older phase3-dev previews have accessible deployment URLs per UI but current public exposure and lifecycle not verified | Preserve current active Production, plan independent build/deploy authorization, pinned release hash, preview access/privacy and rollback controls for future implementation; no Cloudflare toggles/redeploy/purge during 4A-00 |
| P4A-G08 | Cross-vantage DNS/TLS E26 VERIFIED FOR CURRENT 3 HOSTS; 3 FUTURE LMS HOSTS NOT RESOLVING (PROVEN_OPERATOR_TWO_VANTAGES) | lms/auth/hrm resolve from VPS+Windows and Windows HTTPS 200/302/302 with TLS_VERIFY=0 + curl exit 0. lms-admin/lms-api/assets do not resolve on either vantage and absent in 16/16 Cloudflare zone record snapshot. Zone mode Full (not strict), so origin certificate verification and private ingress constraints remain unproven. Nonresolving curl TLS_VERIFY=0 has NO verification meaning | Keep three missing hosts as separate Phase4 provisioning work; obtain scoped origin certificate audit before any controlled Full (strict) zone-level migration, never blindly toggle or infer live app fault |
| P4A-G09 | **LMS browser clients absent and no LMS-named scope shown** E20-E22 (OPERATOR_GUI); API audience/capability runtime still unverified | Complete visible 8-client realm list lacks `lms-user` and `lms-admin`; 17-client-scope inventory lacks LMS-named scope. Generic OIDC `roles` mapper was NOT inspected (provided screenshot is SAML `role_list`). `aud=lms-api` could use a protocol mapper/dedicated client scope; no effective-token proof. Historical frozen HRM identity gates and present production/demo scopes must stay untouched | Future independently authorized nonproduction client provisioning/audience mapper design with exact redirection, Authorization Code + PKCE S256, capability denial, HRM nonregression; no client creation, mapper edits or live token generation in 4A-00 |
| P4A-G10 | Backup/restore, outbox correctness and observability NOT CERTIFIED E26 (BACKUP_TIMER_OBSERVED) | reltroner-postgres-backup.timer registered and triggered 2026-10-10 03:20:14 UTC; /var/backups 39 readable entries and newest file timestamp 01:45:52 UTC, likely distinct from PG backup cycle. These facts do NOT prove backup content, success, offsite copy, tested restore, retention or HRM recovery | One hPanel Premium+VPS backup/snapshot/monitoring screenshot batch and optionally authorized systemd service-result metadata; no opening backup contents, restore, dump, package change, timer restart or purchase |
| P4A-G11 | Local primary FE old HEAD/3 changes (OPERATOR_OBSERVED) | Risk of wiping unfinished work on forced reset/pull | Owner inventory and preservation before a separately authorized local fast-forward, stash or worktree change |
| P4A-G12 | Docs/contract chronologically stale source headers (HISTORICAL) | AI confusion if using old dated text as current authority | Always canonical README -> newest ledger -> frozen contract; do not retroactively rewrite frozen snapshots |
| P4A-G13 | Independently deployable LMS admin frontend NOT FOUND E24 plus hostname NOT RESOLVING E26 (OBSERVED) | Frozen Phase0C requires separately deployable lms-admin.reltroner.com. Operator Pages admin lookup NOT FOUND; hostname absent from 16/16 visible Cloudflare DNS records and fails VPS+Windows DNS with Windows curl exit 6. Not universal DNS NXDOMAIN or proof of permanent service absence | Independently approved Phase4B plan for admin Pages project, DNS, OIDC browser-client PKCE and private Gateway capability boundaries; no provisional DNS/service creation in 4A-00 |

**Suggested non-authorized sequencing:** 4A-00 observations & final receipt -> separately ratified Phase 4B minimal nonproduction runtime placement/trust work order (negative tests and no HRM impact) -> resource/security approvals -> bounded implementation PR(s) with pinned SHAs, CI and rollback -> *separate* production release gate. Do not infer 4B authorizations from a 4A-00 discovery sign-off.

## 7. Evidence intake and exit handoff

One evidence record per observation: ID; collected_at (UTC and WIB); environment; actor role; exact command/UI location; permitted read scope; sanitized output summary; baseline/observed difference; contract invariant IDs; conclusion with classification; hash/link to restricted raw evidence if needed; gaps; recommended negative test; risk/owner; next decision. **No passwords, access tokens, cookies, private keys, client secrets, .env content, databases rows, customer/student data or private IPs in public GitHub documentation.** Redact before pasting into chat.

The Phase 4A-00 receipt is **PARTIAL** until P4A00-AC06..15 are observed to the extent applicable, with any inaccessible gates explicitly accepted/deferred by owner and an independently signed Phase 4A-00 exit decision. On completion, append one new ledger section; do not create a separate report for each minor observation.

**CURRENT DECISION:** PHASE3 CLOSED/FROZEN -> PHASE4A-00 READ-ONLY DISCOVERY OWNER AUTHORIZED -> SOURCE/GOVERNANCE BASELINE PASS -> RUNTIME OPERATOR EVIDENCE PENDING -> PHASE4 IMPLEMENTATION / PRODUCTION NOT AUTHORIZED.

## 8. VPS runtime observation E13 - owner SSH read-only receipt (2026-10-10)

**Evidence class:** OWNER_SUPPLIED_OPERATOR_READ_ONLY. Command output at **2026-10-10T08:49:24Z = 2026-10-10 15:49:24 WIB**. This public evidence intentionally omits VPS public IP, login origin and operator identifiers. The operator executed sudo -v before collection; that validated/cached a sudo credential and is not evidence of any runtime configuration mutation.

| Area | Exact observation and evidence limitation |
|---|---|
| OS/kernel | Ubuntu 24.04.5 LTS / Linux 6.8.0-139-generic x86_64; uptime 18 days 10:36; load average 0.00/0.00/0.00 **at that instant only** |
| CPU | **1 online logical CPU**; six-service worker capacity cannot be assumed |
| Memory | **3.8 GiB total, 1.2 GiB used, 500 MiB free, 49 MiB shared, 2.5 GiB buff/cache, 2.6 GiB available**. Available is a reclaimable-memory estimate, not memory reserved for LMS |
| Swap | Swapfile 2 GiB, **256 KiB used**, approximately 2 GiB available |
| Disk | Root ext4 **48 GB total, 5.9 GB used, 42 GB available, 13% used**; 224,940/6,422,528 root inodes used (**4%**); separate /boot and /boot/efi |
| Installed CLI/binaries | PHP CLI **8.4.25**, psql **client 18.6**, redis-server **binary 8.2.10**. Do **not** infer PHP-FPM, PostgreSQL daemon or Redis process versions directly from these binaries |
| DB and cache sockets | PostgreSQL **127.0.0.1 and ::1:5432**, Redis **127.0.0.1 and ::1:6379** listening; this is a bind-address snapshot, not firewall/ACL/replay/cross-service-access proof |
| All-interface sockets | TCP **22, 80, 443** bound to 0.0.0.0 and [::]; binding to all interfaces does not establish public connectivity or policy correctness |
| Other local sockets | TCP **7800, 8080, 9000, 57800, 37371** on IPv4-mapped loopback; **65529** on localhost; local DNS 53. No PID/service attribution supplied; do not guess their identities |
| Maintenance banner | **16 package updates available; System restart required**. This is a risk/future change-window input, NOT permission to install updates, restart, reboot, reload or change configuration |

**Gate delta:** AC06 PENDING to **PASS_OPERATOR_READ_ONLY**. AC07, AC10, AC14 PENDING to **PARTIAL_OPERATOR**. Invariant-level runtime certification is still unproven. AC08 (Keycloak), AC09 (DB roles/grants), AC11 (Cloudflare Production/main), AC12 (external DNS/TLS), AC13 (assets), AC15 (process/secret permissions), AC16 and AC18 remain open. One vCPU and low instantaneous load are insufficient to approve six independently running Laravel services alongside Keycloak/HRM.

**Next low-impact read-only observation:** At a fresh timestamp, run systemctl is-active for nginx, php8.4-fpm, postgresql, redis-server and keycloak; run ss -lntp and a short sanitized ps -eo pid,comm,rss,%cpu --sort=-rss | head. Observe process owners and memory without exposing env/arguments or contents of Nginx/Keycloak configs. If unprivileged process info is missing, record PENDING and do not escalate automatically. Cloudflare Production/main for FE merge eb01a4d2 is still unverified.

**Boundary:** Phase 4A-00 remains in progress. No deployment, provisioning, service mutation, package update/reboot, database modification, production CI action or Phase 4B authorization.

## 9. Service unit and process RSS observation E14 - owner SSH read-only receipt (2026-10-10)

**Evidence class:** OWNER_SUPPLIED_OPERATOR_READ_ONLY. Observed at **2026-10-10T09:13:12Z = 2026-10-10 16:13:12 WIB**. Collected through five systemctl is-active lookups, unprivileged ss -lntp, process metadata-only ps -eo PID/COMMAND/RSS/%CPU and nginx -v. No secrets/environment, application/database rows or SSH source identifiers are included. No sudo invocation is part of this second command block.

### Actual service state and versions (scoped to checks run)

| Unit/process evidence | Result | What remains unverified |
|---|---|---|
| nginx.service | **active** according to systemd; nginx binary **1.24.0 (Ubuntu)** | Exact effective Nginx server blocks, upstream/FPM sockets, HTTP/API origin routes, TLS and public firewall behavior |
| php8.4-fpm.service | **active** | Pool owners, socket-to-service map, service-specific worker/pool memory limits and Laravel six-service runtime deployment |
| postgresql.service | **active** | Actual PostgreSQL server version/database owners, roles, grants and four LMS database existence |
| redis-server.service | **active** | Effective Redis active-server version, ACL/persistence/eviction/keyspace and fail-closed replay state |
| keycloak.service | **active** | Keycloak Java MainPID matching, actual issuer/JWKS/clients/audience, HRM regression baseline |
| ss -lntp | Socket inventory unchanged from E13; **Process/PID column empty** on this nonprivileged read | Cannot assign listener 7800/8080/9000/57800/37371/65529 or public 22/80/443 to process without another authorization-compatible observation |

### Largest displayed resident sets

Linux ps RSS values are **KiB**, not a per-service uniquely attributed memory budget. Shown processes were only the first 17 rows sorted by RSS. PostgreSQL shared pages and other shared libraries mean simply summing all process RSS can double count.

| PID (observation only) | Executable name reported by ps | RSS KiB | Approx MiB | CPU % |
|---|---|---:|---:|---:|
| 5032 | java | 679808 | 663.9 | 0.2 |
| 473765 | php8.4 | 53336 | 52.1 | 0.0 |
| 450192 | php-fpm8.4 | 42544 | 41.5 | 0.0 |
| 450193 | php-fpm8.4 | 39988 | 39.1 | 0.0 |
| 395249 | monarx-agent | 36940 | 36.1 | 0.0 |
| 450182 | postgres | 34760 | 33.9 | 0.0 |
| 450174 | php-fpm8.4 | 32240 | 31.5 | 0.0 |
| 450205 | postgres | 26688 | 26.1 | 0.0 |
| 305395 | redis-server | 14716 | 14.4 | 0.3 |

**Classification:** Java is the single largest RSS entry, but **PID 5032 has not been independently tied to keycloak.service**. Likewise php-fpm workers have not been assigned to HRM or any LMS service, and php8.4 CLI is not inferred to be a background worker without context. The process snapshot is compatible with the initial overall free -h values E13 but does not by itself explain all host memory (page cache, shared memory, processes below sample cutoff).

**Gate delta:** AC07 remains **PARTIAL_OPERATOR** with actual 5/5 active systemd observations and Nginx version; AC10 remains **PARTIAL_OPERATOR** with redis-server active and one process RSS; AC14 remains **PARTIAL_OPERATOR** with selected RSS. AC08 **PENDING_RUNTIME** despite keycloak.service active: no OIDC realm/clients or HRM behavioral validation. No new acceptance gate is marked full PASS; AC06 PASS_OPERATOR_READ_ONLY from E13 remains valid only for its timestamped single baseline.

**Next authorized read-only observation (as unprivileged user):**

~~~
date -u '+%Y-%m-%dT%H:%M:%SZ'
for svc in nginx php8.4-fpm postgresql redis-server keycloak; do
  echo "=== $svc ==="
  systemctl show "$svc" --property=MainPID,ActiveState,SubState --no-pager
done
ps -p 5032 -o pid,ppid,comm,rss,%cpu
ps -eo pid,ppid,comm,rss,%cpu --sort=-rss | head -n 22
~~~

Systemd MainPID may be 0 for forking/oneshot wrapper units; if no stable PID can be attributed, report PARTIAL instead of guessing. Do not paste process command arguments, printenv, full unit definitions, service Environment or private config. Avoid sudo escalation and port scans; do not modify or reload any service.

**Hard STOP:** No claim of production-ready six-service capacity on the 1-vCPU host, no automatic OS updates/reboot, Redis write/fault testing, database changes, Keycloak/HRM mutations, Nginx edits, Cloudflare releases or Phase 4B permission. Phase 4A-00 remains open.

## 10. Process ancestry observation E15 - owner SSH read-only receipt (2026-10-10)

**Evidence class:** OWNER_SUPPLIED_OPERATOR_READ_ONLY. Timestamp **2026-10-10T09:36:56Z = 2026-10-10 16:36:56 WIB**. Observed from `systemctl show ... --property=MainPID,ActiveState,SubState`, `ps -p 5032 -o pid,ppid,comm,rss,%cpu`, and `ps -eo pid,ppid,comm,rss,%cpu --sort=-rss | head -n 22`. No secrets, service environment or command lines were inspected.

| systemd unit / process | Observed identity | Narrow conclusion / residual evidence |
|---|---|---|
| nginx | systemd MainPID **289723**, active/running; `nginx` worker PID **289725**, PPID 289723, RSS 10,592 KiB | Nginx master/worker related; public-port listener PID and virtual-host/upstream mapping remain unverified |
| php8.4-fpm | systemd MainPID **450174**, active/running; workers **450192** and **450193** have PPID 450174, RSS 42,544 and 39,988 KiB; master RSS 32,240 KiB | Actual PHP-FPM worker ancestry now observed; pool-to-HRM/LMS assignment, limit/queue policy and private service sockets not yet observed |
| postgresql | systemd MainPID **0**, ActiveState active, SubState exited; `postgres` PID **450182** PPID 1, RSS 34,760 KiB; other PostgreSQL processes descendants | `active/exited` for umbrella unit must NOT be interpreted as database outage. Live cluster identity/version/service readiness, database owners and grants remain unverified |
| redis-server | systemd MainPID **305395**, active/running, matches `redis-server` PID 305395, RSS **14,712 KiB** | Runtime process identity confirmed; no ACL, eviction, keyspace, replay or failure recovery verification |
| keycloak | systemd MainPID **4934**, active/running; `java` PID **5032** with PPID 4934, RSS **679,808 KiB (~663.9 MiB)** / 0.2% CPU | **Process-family attribution to Keycloak confirmed at snapshot**; process memory is not full Keycloak container/cgroup footprint, and issuer/JWKS/clients/audience/HRM regression remain NOT VERIFIED |
| other process | `php8.4` PID **474600** with PPID 1, RSS **53,424 KiB** | Cannot assign standalone PHP CLI process to HRM, cron or LMS without additional evidence; do not kill or restart |

**Gate delta:** AC07 and AC14 **remain PARTIAL_OPERATOR**, now with direct service PID/PPID lineage; AC08 remains **PENDING_RUNTIME** because Keycloak process state != OIDC client/realm/auth verification. AC09 remains PENDING despite observed postgres children; AC10 remains PARTIAL despite confirmed Redis PID. AC06 timestamped host-capacity snapshot already passed under its exact read-only scope. No Phase 4A-00 final exit, Phase 4B or production release authorization.

**Next least-invasive read-only inventory:**

~~~sh
date -u '+%Y-%m-%dT%H:%M:%SZ'
echo '=== POSTGRESQL CLUSTERS (METADATA ONLY) ==='
pg_lsclusters 2>/dev/null || true
echo '=== PHP-FPM POOL CONFIG FILENAMES ONLY ==='
find /etc/php/8.4/fpm/pool.d -maxdepth 1 -type f -name '*.conf' -printf '%f\n' 2>/dev/null
echo '=== NGINX ENABLED SITE FILENAMES ONLY ==='
find /etc/nginx/sites-enabled -maxdepth 1 \( -type f -o -type l \) -printf '%f\n' 2>/dev/null
echo '=== PHP-FPM/NGINX SERVICE AND PROCESS SNAPSHOT ==='
systemctl is-active nginx php8.4-fpm postgresql redis-server keycloak
~~~

This reads metadata/names only and must not copy configuration contents. It does NOT establish actual routed FPM pools, nor all private/public exposure gates. No sudo default, no `nginx -T`, `php-fpm -tt`, `printenv`, `cat /etc/...conf`, database credentials, `systemctl cat`, reload, migration or service update. Sanitize hostname/tenant-related filenames if needed before public archival.

**Security/architecture constraint:** Existing Keycloak/HRM and the 1-vCPU host are incumbents. Six independently deployable Laravel source services do not imply six runtime deployments. Revalidate budget and least-privilege boundaries before any future separately authorized implementation. This E15 changes only evidentiary classification.

## 11. PostgreSQL cluster and web runtime filenames E16 - owner SSH read-only receipt (2026-10-10)

**Evidence class:** OWNER_SUPPLIED_OPERATOR_READ_ONLY; timestamp **2026-10-10T09:42:49Z = 2026-10-10 16:42:49 WIB**. Command output included `pg_lsclusters`, `find` of PHP-FPM pool filenames and Nginx sites-enabled entries (no file contents), and `systemctl is-active`. The pasted terminal echo includes duplicate/malformed-looking fragments, but the returned observation sections are readable; this receipt does not claim the echoed input is an exact command replay. No source or service mutation is evidenced.

| Scope | Actual result | Interpretation and limits |
|---|---|---|
| PostgreSQL cluster | `18 main 5432 online postgres`; data directory `/var/lib/postgresql/18/main`, log path `/var/log/postgresql/postgresql-18-main.log` | **Live PostgreSQL 18/main cluster online** at query time, consistent with earlier loopback socket and postgres process evidence. This does not prove that `lms_learning_db`, `lms_mentorship_db`, `lms_knowledge_db`, `lms_audit_db` exist, nor validate per-service ownership, login roles or GRANTs. Do not inspect data rows |
| PHP-FPM pool filenames | Only `www.conf` listed under `/etc/php/8.4/fpm/pool.d` | Exactly one visible `.conf` pool file in the inspected directory. Does **NOT** prove only one effective runtime pool across all versions/paths or the absence of additional socket/service integration; no six LMS-specific pool names are observed |
| Nginx sites-enabled | `auth.reltroner.com`, `default`, `hrm.reltroner.com.conf` | Three enabled entry names shown. No LMS-named site observed **in this location**, but other includes/paths or proxy mapping were not inspected. No claim that LMS hosts are absent or unreachable in reality |
| Service states | nginx, php8.4-fpm, postgresql, redis-server, keycloak all `active` | Reconfirms E14's service-unit status, **not** application-level health, HTTP routing, JWT acceptance or DB permission readiness |

**Gate delta:** `P4A00-AC07` remains **PARTIAL_OPERATOR** (file inventory narrows unknown runtime placement; no upstream/pool content). `P4A00-AC09` becomes **PARTIAL_OPERATOR** strictly because the cluster itself is online; **four LMS databases, ownership and grants remain UNVERIFIED**, so the mandatory AC09 acceptance is not passed. No change to AC08 OIDC, AC10 Redis security, AC11 Cloudflare release, AC12 DNS/TLS, AC14 HRM capacity/backup, or AC15 process/secret posture. These observations do not authorize creating six pools or new Nginx sites.

**Risk/capacity:** On the observed 1-vCPU/3.8-GiB host, independent Laravel microservice process/pool/worker sizing and protection of existing Keycloak/HRM need later reviewed allocation. Current source architecture consists of six services, but there is **no evidence that six distinct services have been deployed**.

**Next read-only commands (unprivileged, metadata only, no configuration contents):**

~~~sh
date -u '+%Y-%m-%dT%H:%M:%SZ'
echo '=== POSTGRESQL NONINVASIVE READINESS ==='
pg_isready -h 127.0.0.1 -p 5432
echo '=== NGINX ENABLED SITE TARGET PATHS ==='
find /etc/nginx/sites-enabled -maxdepth 1 \( -type f -o -type l \) -printf '%f -> %l\n' 2>/dev/null
echo '=== PHP-FPM POOL FILE ATTRIBUTES ==='
find /etc/php/8.4/fpm/pool.d -maxdepth 1 -type f -name '*.conf' -printf '%f %s bytes\n' 2>/dev/null
~~~

Observe only readiness and metadata. `pg_isready` does not validate four application databases or database grants; successful client connection is not claimed. Do not run SQL with privilege escalation or print configurations/credentials without a separately reviewed evidence plan. No `sudo`, package installation, reload, restart, migrations, database writes, Cloudflare actions or Phase 4B authorization.

**Status:** Phase 4A-00 remains **IN PROGRESS** with E13/E14/E15/E16 operator receipts archived; no production implementation authority.

## 12. PostgreSQL connection-readiness and filesystem-link metadata E17 (2026-10-10)

**Evidence class:** OWNER_SUPPLIED_OPERATOR_READ_ONLY, captured at **2026-10-10T09:48:14Z = 2026-10-10 16:48:14 WIB**. Commands: `pg_isready -h 127.0.0.1 -p 5432` and `find` metadata-only listings for Nginx enabled sites and PHP 8.4-FPM pool files. No sudo, database SQL, secret, application config content, service reload or modification was supplied.

| Area | Observation | Specific limitation |
|---|---|---|
| PostgreSQL connection readiness | `127.0.0.1:5432 - accepting connections` | PostgreSQL responds as ready for connection attempts on loopback. **No successful authenticated connection, user or database query, application schema, privilege or cross-write denial is evidenced**. This narrows the cluster-online subproof of AC09 but **does not PASS AC09** |
| Nginx enabled symlink: identity | `auth.reltroner.com -> /etc/nginx/sites-available/auth.reltroner.com` | File-target mapping only; does not prove listener/vhost routing, TLS or effective included config |
| Nginx enabled symlink: default | `default -> /etc/nginx/sites-available/default` | File-target mapping only; no conclusion on default-host exposure |
| Nginx enabled symlink: HRM | `hrm.reltroner.com.conf -> /etc/nginx/sites-available/hrm.reltroner.com.conf` | File-target mapping only; no HRM nonregression behavioral certification |
| PHP-FPM pool metadata | `www.conf 22133 bytes` (under /etc/php/8.4/fpm/pool.d) | One observed pool configuration filename/size. **Contents, effective pool count, FPM socket mapping and allocation to HRM or LMS remain unknown** |

**Gate delta:** `P4A00-AC07` stays **PARTIAL_OPERATOR** (symlink targets and pool size added). `P4A00-AC09` stays **PARTIAL_OPERATOR** (readiness positive, but all LMS service-owned DB/role/GRANT and auth proofs missing). `P4A00-AC08` remains PENDING, `AC10` PARTIAL, `AC11` PENDING and no other gate is upgraded. This evidence does not justify assuming LMS hostnames are deployed on this Nginx instance or that all six Laravel services can run safely on the shared 1-vCPU VPS.

**Recommended next high-value read-only observation (no privileged DB session):** Inspect the canonical public OIDC discovery metadata on `auth.reltroner.com/realms/reltroner/.well-known/openid-configuration`, collecting only issuer, JWKS URI and public metadata presence, not user/admin tokens or secrets. A public OIDC discovery response does NOT establish `lms-user`/`lms-admin` client registrations, `lms-api` audience, or HRM login correctness. Perform DB catalog/role/GRANT metadata inspection only with an already authorized database read-only account and an agreed redaction plan; do not use `sudo -u postgres` by default.

**Status:** Phase 4A-00 remains IN PROGRESS. No application, infrastructure, identity, DB, Redis or Cloudflare changes; Phase 4B/production NOT AUTHORIZED.

## 13. Canonical Keycloak OIDC discovery E18 - owner SSH read-only receipt (2026-10-10)

**Evidence type:** OWNER_SUPPLIED_OPERATOR_READ_ONLY. Observed timestamp **2026-10-10T09:52:45Z = 2026-10-10 16:52:45 WIB**. Performed from the VPS with a public GET request using `curl --fail --silent --show-error --max-time 15` against the realm's HTTPS `/.well-known/openid-configuration` endpoint. `set -o pipefail` was enabled and a Python JSON parser selected four specific non-secret metadata fields. The output yielded parseable metadata and no reported HTTP/curl error. This is a single **VPS network vantage point**, not a comprehensive external-user DNS/TLS survey. No secrets, cookies, authentication tokens, administrator console access, database records or JWTs were used.

| Item | Observed public metadata | Confidence and limitation |
|---|---|---|
| Canonical issuer | `https://auth.reltroner.com/realms/reltroner` | **Exact string match** to frozen Phase 0C/Phase 1 issuer; matches canonical identity authority for discovery metadata only |
| JWKS URI | `https://auth.reltroner.com/realms/reltroner/protocol/openid-connect/certs` | The URI is **advertised**; this probe did NOT fetch JWKS, confirm active signing keys/kids, select algorithms, or verify any JWT signature |
| authorization_endpoint | `True` (present and truthy) | Field exists; authorization flow, redirect URI, PKCE S256, token exchange, login and session policies were NOT executed |
| token_endpoint | `True` (present and truthy) | Field exists; endpoint functional behavior, clients' audience and token issuance NOT executed |

**Gate delta:** `P4A00-AC08: PENDING_RUNTIME -> PARTIAL_OPERATOR`, strictly the public realm OIDC metadata/issuer subgate. **Not a full AC08 PASS**: effective Keycloak clients `lms-user` and `lms-admin`, protected API audience `lms-api`, client-specific redirect URIs/web origins, JWT signature validation, JWKS key lifecycle, authorization capability mapping and existing HRM nonregression are all outstanding. `P4A00-AC12` remains **TOOL_UNAVAILABLE** as defined for independent external-vantage all-host DNS/TLS checks: a single curl from the existing VPS is useful positive identity-origin evidence but not external comprehensive TLS/hostname proof. Cloudflare Pages `Production/main` state (AC11) remains PENDING.

**Temporal source caution:** A correct public issuer does not fix the legacy `sso.reltroner.com` and `lms-reltroner` values previously observed in frontend `.env.example`; actual deployed FE and Keycloak client settings are not established by this request. No template/configuration, app code or Keycloak change is authorized in Phase 4A-00.

**Safe next operator observation:** From the same SSH session, retrieve only the public JWKS **key metadata counts/types/algorithms** (not full `n`, `x`, `y`, or private JWK fields). A public JWKS read can establish keyset retrieval but still does not certify JWT verification or client/audience behavior. Effective client inventory should be collected from an already-authorized Keycloak GUI session with client secrets and sensitive account metadata excluded, and without initiating user authentication.

**No-mutation boundary:** No Keycloak realm/client edits, issuance of test/live JWTs, admin login automation, secret extraction, production cutover, Cloudflare changes, LMS application PR, deployment or Phase 4B permission. **Phase 4A-00 remains IN PROGRESS.**

## 14. Public Keycloak JWKS retrieval E19 - owner SSH read-only receipt (2026-10-10)

**Evidence classification:** OWNER_SUPPLIED_OPERATOR_READ_ONLY; observed at **2026-10-10T09:58:09Z = 2026-10-10 16:58:09 WIB**. Authorized VPS operator used a public HTTPS `curl --fail --silent --show-error --max-time 15` GET of the JWKS URI discovered in E18 with a Python parser that emitted only per-key `kty`, `use`, `alg` and `kid_present`, plus total key count. The pasted shell echo has a visibly malformed/partial fragment but the resulting Python output clearly lists the count and two key metadata lines; **do not claim byte-for-byte command echo integrity**. No JWK public modulus/material, private keys, JWTs, cookies, access tokens, client secrets, or user credentials were copied into this evidence.

| Public JWKS property | Observed value | Supported conclusion and limitation |
|---|---|---|
| Public JWKS GET | Succeeded with parseable JSON and `keys` list of length **2** | The advertised JWKS URI is reachable **from the VPS at observation time**. No separate public-client vantage point, cache-rotation stability, response certificate analysis or token validation was performed |
| Key 0 | `kty=RSA`, `use=sig`, `alg=RS256`, `kid_present=True` | Keycloak **advertises** an RSA verification-signature key for RS256; no signature was verified, no actual token `kid` matched, no client-specific accepted-algorithm policy proven |
| Key 1 | `kty=RSA`, `use=enc`, `alg=RSA-OAEP`, `kid_present=True` | Keycloak **advertises** a key used for encryption; it is **not** proof of a second signing key nor of RSA-OAEP JWT signature verification |

**Binding contract distinction:** [ADR-LMS-TRUST-001](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md) ratifies **Ed25519/EdDSA only for separate internal service workload and delegated-principal assertions in nonproduction design**, not for Keycloak-issued browser/API access JWT signatures. E19's observed `RS256` OIDC signing-key metadata and `RSA-OAEP` encryption-key metadata therefore **do not conflict with the internal Ed25519 decision**. Neither algorithm acceptance nor real signature validation is runtime-certified by this JWKS metadata check.

**Gate delta:** `P4A00-AC08` stays **PARTIAL_OPERATOR**, with JWKS retrieval (rather than merely advertised URI) now positively observed. This does **not** prove JWKS/key rotation or issuer-audience-expiration verification, client registrations `lms-user`/`lms-admin`, protected resource audience `lms-api`, PKCE S256, capabilities or HRM login nonregression. `P4A00-AC12` remains **TOOL_UNAVAILABLE** for the larger independent external-vantage DNS/TLS scope and `P4A00-AC11` remains PENDING Cloudflare Production/main verification.

**Next approved read-only operator GUI collection:** In an **already authorized** Keycloak Admin Console session, select realm `reltroner` and inspect Clients by exact client ID `lms-user`, `lms-admin` and `lms-api` **if present**. Record only whether each exact ID exists, public/confidential client type, allowed redirect origin hostnames and intended audience mapper/scope names; redact any client secrets, user accounts, access tokens, realm signing-key material and unnecessary private URL parameters. Observe only; **do not save or edit**, assign permissions, generate/test tokens, change HRM client or attempt production authentication. If an exact client is absent, record NOT_FOUND rather than creating it. A Keycloak GUI screenshot alone does not prove JWT behavior; negative/positive token tests belong to a future separately approved isolated work order.

**Hard boundary:** No software/configuration changes, test token issuance, production deployment or Phase 4B authorization. Phase 4A-00 remains **IN PROGRESS**.

## 15. Keycloak reltroner client-list GUI evidence E20 (2026-10-10)

**Evidence class:** OWNER_SUPPLIED_KEYCLOAK_ADMIN_GUI_READ_ONLY, in-browser screenshot received 2026-10-10. The captured UI shows Keycloak **current realm `reltroner`**, Manage > Clients > Clients list, with list count/pagination **1-8 of 8** and no visible search text/filter. The screenshot filename is not a trusted UTC/WIB clock source; **exact collection timestamp is not independently determined**. This public ledger stores the **sanitized evidence findings only**, not the screenshot, browser address bar, session context or admin account identifier.

### Exact observed Client IDs

| UI client ID | Shown in realm list | Scope of conclusion |
|---|---|---|
| `account` | YES | Built-in named client shown |
| `account-console` | YES | Built-in named client shown |
| `admin-cli` | YES | Built-in named client shown |
| `broker` | YES | Built-in named client shown |
| `hrm-demo-web` | YES | Existing HRM-related client ID shown; **no functional HRM login or authorization test performed** |
| `hrm-web` | YES | Existing HRM-related client ID shown; preserve unchanged |
| `realm-management` | YES | Built-in/realm-management named client shown |
| `security-admin-console` | YES | Security admin-console named client shown |
| **`lms-user`** | **NOT LISTED** | Frozen learner browser client is missing from the eight listed entries; **runtime provisioning gap observed in this GUI snapshot** |
| **`lms-admin`** | **NOT LISTED** | Frozen independent admin browser client missing from the eight listed entries; **runtime provisioning gap observed in this GUI snapshot** |
| **`lms-reltroner` (legacy FE example)** | **NOT LISTED** | Template legacy ID not found in this observed realm; no assertion about other realms or effective deployed FE env |
| **`lms-api`** | **NOT LISTED AS CLIENT** | **NOT sufficient to prove missing audience**. Frozen contract specifies `aud=lms-api`; the effective audience may be configured through client scope/audience mapper rather than a dedicated Clients-list record. Inspect separately |

The GUI displays the type column as **OpenID Connect** for all eight observed entries. It does **not** show access type/public/confidential posture, individual client attributes, Valid Redirect URIs, Web Origins, token audience/mapper settings, secret custody or runtime token behavior.

**Frozen source contract reference:** [Phase 1 Logical Service Boundary & API, section 15](./logical-service-boundary-api-contract.md) specifies `lms-user` for `lms.reltroner.com`, `lms-admin` for `lms-admin.reltroner.com` (separate public browser clients using Authorization Code + PKCE), and API access tokens with `aud=lms-api`. Owner accepted Phase 3 contracts/CI and E18/E19 issuer/JWKS proof do **not** demonstrate that these runtime registrations existed before this GUI observation.

### Gate and gap disposition

- `P4A00-AC08 = PARTIAL_OPERATOR / PROVISIONING GAP OBSERVED`, **NOT PASS** and no automatic remediation. Keycloak issuer and JWKS public metadata previously PASS scoped subchecks; **two required LMS browser-client IDs visibly absent** from the complete current-realm list.
- `P4A-G09` updated with observed absence of `lms-user`/`lms-admin`, linked to FE legacy template drift. This gap is a **future provisioning dependency**, not permission to create missing clients now.
- `P4A00-AC11` Cloudflare Pages Production/main state, `AC12` comprehensive external DNS/TLS, and `AC14` HRM coexistence/regression remain unresolved. Existing HRM-related client IDs visible are **presence only**, not behavioral or permissions certification.
- Do not infer that absent `lms-reltroner` in this realm proves the frontend is failing, since effective environment/realm in active deployments has not been inspected.
- Do not infer that absence of `lms-api` on this Clients page disproves `aud=lms-api`: client scopes, protocol mappers and effective token issuance remain to be inventoried.

**Next least-invasive GUI action:** Without saving or editing, open **Client scopes** in current realm and record **only** scope names and whether any LMS/audience mapper naming exists; scope/mappers may require per-client viewing when the browser clients are eventually provisioned in a separately approved phase. Alternatively inspect the existing **`hrm-web` > Settings** only for non-secret high-level fields, avoiding exposing redirect query values or sensitive account information. **Do not** click Create client, Import client, Save, Credentials, Roles assignment, or issue tokens. No Keycloak admin API mutation, changes to HRM, realm, client scope, DNS, Cloudflare, or production configuration are authorized.

**Overall status:** Phase 4A-00 READ-ONLY DISCOVERY IN PROGRESS. Required LMS client creation/SSO cutover and real JWT/audience denial testing belong to a separate future owner-authorized implementation work order; Phase 4B / production NOT AUTHORIZED.

## 16. Batch Keycloak scope, realm-role, session, token and authentication-policy GUI evidence E21-E22 (2026-10-10)

**Evidence collection:** Owner-provided read-only screenshot of realm `reltroner` Client scopes (E21), two screenshots of a mapper details page and Realm roles (E22), and operator-supplied GUI text exports/pastes for Realm settings > Sessions/Tokens/Security defenses/Login and Authentication > Flows (E22). These were received during 2026-10-10 in the chat; **exact independently attested screenshot capture times are unavailable**. The evidence below is a sanitized summary; no Admin Console account name, browser session URL, client secret, token, user identity or entire screenshot is committed. Screen/text evidence is not a production behavioral test and no Keycloak state mutation was requested.

### E21 - complete visible client scopes list: 17/17

| Scope name | Assignment type shown | Protocol shown |
|---|---|---|
| acr | Default | OpenID Connect |
| address | Optional | OpenID Connect |
| AuthnContextClassRef | Default | SAML |
| basic | Default | OpenID Connect |
| email | Default | OpenID Connect |
| hrm-demo-identity | None | OpenID Connect |
| hrm-production-identity | None | OpenID Connect |
| microprofile-jwt | Optional | OpenID Connect |
| offline_access | Optional | OpenID Connect |
| organization | Optional | OpenID Connect |
| phone | Optional | OpenID Connect |
| profile | Default | OpenID Connect |
| role_list | Default | SAML |
| roles | Default | OpenID Connect |
| saml_organization | Default | SAML |
| service_account | None | OpenID Connect |
| web-origins | Default | OpenID Connect |

**Conclusion:** No explicitly LMS-named client scope appears in this observed 17-entry realm list. Absence of LMS-named scope is not conclusive absence of a resource audience protocol mapper. **Assignment type `None` for the two HRM scopes is a realm-level assigned-type field, NOT proof the scope is unassigned from the corresponding HRM clients.** HRM frozen Phase 6 §6 records scope-to-client association historically. `offline_access` is available as an *optional scope*; this **does not prove any active HRM/LMS access token includes it**.

### E22 - inspected mapper is SAML `role_list`, not OIDC `roles`

The submitted Mapper details screenshot shows **Mapper type `Role list`**, mapper name `role list`, **Role attribute name `Role`**, SAML Attribute NameFormat `Basic`, Single Role Attribute OFF, and a blank Friendly Name. This is a **SAML role-list mapper**, not the OIDC `roles` client-scope protocol mapper. **No generic OIDC role/audience mapper was inspected and `aud=lms-api` remains unverified.** Viewing an editable mapper form is not evidence that Save was used; no mutation reported.

### E22 - Realm roles: visible 6/6

| Role name | Composite (GUI) | Notes |
|---|---|---|
| default-roles-reltroner | True | Composite default realm role |
| demo_user | False | Historical Phase 6 demo identity classification |
| offline_access | False | Built-in role; presence does not prove use |
| production_user | False | Historical Phase 6 production identity classification |
| service_account | False | Historical Phase 6 nonhuman/service classification |
| uma_authorization | False | Built-in authorization role |

These observed identity roles match the HRM historical identity-class taxonomy, but **do not prove effective account assignments or live HRM environment isolation**.

### E22 - Realm settings > Sessions (operator-visible fields)

| Setting | Observed |
|---|---|
| SSO Session Idle | 30 minutes |
| SSO Session Max | 10 hours |
| Client Session Idle | 0 minutes |
| Client Session Max | 0 minutes |
| Offline Session Idle | 30 days |
| Client Offline Session Idle | 0 minutes |
| Offline Session Max Limited | Disabled |
| Login timeout | 5 minutes |
| Login action timeout | 5 minutes |

**Interpretation guard:** zero client-session override values may denote inherit/default behavior in Keycloak; do **not** claim unlimited client sessions. Offline session configuration availability does not establish `offline_access` has been requested/granted by a client.

### E22 - Realm settings > Tokens

| Setting | Observed |
|---|---|
| Default Signature Algorithm | RS256 |
| Revoke Refresh Token | Disabled |
| Access Token Lifespan | 5 minutes |
| Access Token Lifespan For Implicit Flow | 15 minutes |
| OAuth 2.0 Device Code Lifespan | 10 minutes |
| OAuth 2.0 Device Polling Interval | 5 (unit not reliably captured in submitted text) |
| Lifetime of Request URI for Pushed Authorization Request | 1 minute |
| Client Login Timeout | 1 minute |
| User-Initiated Action Lifespan | 5 minutes |
| Default Admin-Initiated Action Lifespan | 12 hours |

**Interpretation guard:** an Implicit Flow *lifespan setting* is **not proof that the implicit grant is enabled** on any client; HRM Phase 6 baseline specifically says client Implicit Flow OFF. Revoke Refresh Token Disabled is a real policy setting to include in future LMS session/revocation risk review, not permission to toggle or remediate this realm now. Current RS256 setting is consistent with E19's advertised Keycloak signing-key metadata; runtime JWT validation is still UNVERIFIED.

### E22 - Realm settings > Security defenses, brute-force fields

| Setting | Observed |
|---|---|
| Brute Force Mode | Lockout temporarily |
| Max login failures | 10 |
| Maximum Secondary Authentication Failures | 0 |
| Strategy to increase wait time | Multiple |
| Wait increment | 1 minute |
| Max wait | 15 minutes |
| Failure reset time | 12 hours |
| Quick login check milliseconds | 1000 |
| Minimum quick login wait | 1 minute |

These are visible policy fields, not a stress/lockout test or confirmation of every effective Keycloak security header.

### E22 - Authentication > Flows (visible 11/11)

`browser` (built-in), `clients` (built-in), `direct grant` (built-in), `docker auth` (built-in), `first broker login` (built-in), `registration` (built-in), `reset credentials` (built-in), **`browser-hrm-demo-v2`**, **`browser-hrm-production-v2`**, `browser-hrm-demo` (Not in use), `browser-hrm-production` (Not in use).

The `v2` flows are present as expected from HRM Phase 6 frozen contract §5. The supplied list does **not** prove which specific HRM client currently has the matching browser-flow override, nor re-execute cross-environment auth denial. Both `v2` entries have a description referring to production HRM; this could be a cosmetic description mismatch on the demo flow, not an observed security failure. Built-in `direct grant` flow **existing** does NOT imply Direct Access Grants are enabled for HRM clients.

### E22 - Realm settings > Login (operator-visible fields)

| Field | Observed |
|---|---|
| User registration | Off |
| Forgot password | Off |
| Remember me | Off |
| Enable Passkeys | Off |
| Email as username | Off |
| Login with email | On |
| Duplicate emails | Off |
| Verify email | Off |
| Edit username | Off |

These settings are realm-wide; they do not establish a complete client-local authentication-policy acceptance or business-authorization behavior.

### Frozen HRM evidence reuse - no duplicate GUI probes required

Owner directed reuse of **[HRM Phase 6 Keycloak-side frozen receipt](https://github.com/Reltroner/reltroner-hr-app/blob/main/docs/engineering/PHASE-6-KEYCLOAK-SIDE-COMPLETE-FROZEN.md)** (freeze 2026-09-22) plus **[HRM master architecture](https://github.com/Reltroner/reltroner-hr-app/blob/main/docs/engineering/ARCHITECTURE-CONTRACT.md)**. HRM Phase 6 provides historical acceptance of confidential `hrm-web`/`hrm-demo-web`, distinct secrets, exact production/demo callbacks and postlogout URIs, PKCE S256 and disabled grant surfaces, Full Scope Allowed OFF, identity scope mapper `reltroner_identity_class` and two `browser-hrm-*-v2` gates; negative classification, cross-environment SSO-cookie denial and persistence were historically tested. User explicitly reports no Keycloak GUI changes since documenting these contracts. Treat this as **FROZEN_HISTORICAL + OWNER_NONMUTATION_ATTESTATION**, not as an independently re-executed current HRM auth test. Do not change HRM or demand screenshot re-proving every frozen Phase 6 assertion.

### Phase 4A-00 Keycloak discovery exit disposition vs implementation gates

**SCREENSHOT/GUIONLY DISCOVERY INPUT: SUFFICIENT FOR PLANNING**, with **P4A00-AC08 still PARTIAL / LMS PROVISIONING GAP OBSERVED**. Existing `lms-user` and `lms-admin` missing (E20), no LMS scope name in 17/17 scope list (E21), `aud=lms-api` effective mapper/token still UNVERIFIED (SAML mapper screenshot cannot support it). JWT cryptographic negative testing, registration of new clients/scopes, PKCE redirect acceptance, HRM live regression and Keycloak client-specific actual override checks remain **later separately authorized scoped implementation/test** unless owner explicitly asks for more read-only evidence. **Do not claim Phase 4A-00 or 18 overall gates closed**, because Cloudflare, DNS/TLS, database owner grants, Redis security, backups and operator sign-off are still pending.

**Batch acceptance:** No additional Keycloak GUI screenshot is mandatory for a Phase 4A-00 *discovery-only handoff*, assuming owner accepts historical HRM evidence reuse and explicit unresolved LMS runtime identity gaps. An optional, nonblocking one-screen check of OIDC `Client scopes -> roles -> Mappers` (not SAML `role_list`) could narrow generic mapper unknowns, but it cannot establish `aud=lms-api` in a token before the LMS browser clients and their audience policies exist. It must NOT trigger extra clients, Save, Evaluate, Credentials or token issuance.

**Next phase-4A work area:** Return to read-only PostgreSQL database/owner/GRANT inventory, Redis effective runtime configuration metadata, and Cloudflare Production/main evidence; protect existing HRM and Keycloak. **NO runtime or production mutation / Phase 4B authorization.**

## 17. Cloudflare Pages Production/main operator receipt E23 (2026-10-10)

**Evidence class:** OWNER_SUPPLIED_CLOUDFLARE_DASHBOARD_TEXT. User pasted the visible Cloudflare Pages Deployments view for project lms-fe; the assistant did NOT independently authenticate to Cloudflare or query the account API. UI-relative ages are not treated as exact UTC timestamps. This documentation intentionally omits the Cloudflare account identifier, browser session URL and all secrets.

| Audit object | Current operator UI evidence | Qualification |
|---|---|---|
| Cloudflare Pages project | lms-fe linked to Reltroner/LMS-FE | UI project/repository association |
| Production branch / automation | Production; main; **Automatic deployments enabled** | Future deployment is potentially possible; selected current source commit skip is NOT a permanent policy guarantee |
| Domains displayed | lms.reltroner.com and lms-fe-3gl.pages.dev | Project hostname association, not external DNS/TLS/HTTP reachability validation |
| FE PR5 merge in Production list | main, eb01a4d, commit message begins [CF-Pages-Skip], deployment **No deployment available** | **Positive skip proof** for pinned FE source-only merge; GitHub FE main full SHA separately verified: eb01a4d2c924299b929aebf0f4826b94cf341fc6 |
| Current active Production at page top | main, **f2d4041**, approximately **four months old**, immutable Pages deployment URL https://ac5969f7.lms-fe-3gl.pages.dev | Active Production shown is OLDER than GitHub source main; latest source was not promoted to live deployment. Independent HTTP content and effective OIDC runtime config NOT inspected |
| Other main entries | cc3d9c1 (PR3) and d0e4d74 (PR4) showed **No deployment available** | Consistent with limited source-only/no-new-production-deployment rule for these displayed commits |
| Newer maintenance Preview entries | 5f2ac1f, 01028a8, d0e4d74, 83bb987 were **No deployment available** | These previews were skipped on those specific entries |
| Older phase3-dev Preview entries | Several older commits (including 9795489, 33706d0, 7c3b6df, f8ecafa, 5eca610, 60eba10, 3ee0ee0) displayed actual Pages Preview URLs | Preview publication DID occur historically; this is distinct from Production. Preview access controls, content privacy and current availability require later scoped read-only audit |
| History pagination | **Showing 1-15 of 54**, page 1 of 4 | Do not claim all 54 rows have been audited |

**Gate disposition:** P4A00-AC11 moves PENDING_RUNTIME to **PASS_OPERATOR_CLOUDFLARE_UI (SCOPED)** for exact Production/main PR5 skip and displayed active Production SHA. This is a read-only operator-dashboard proof, NOT independently verified Cloudflare API history, live-site HTTP body hash, effective frontend OIDC settings, preview privacy, or proof of permanent production-deployment safeguards.

**Gap disposition:** P4A-G07 historical PR5 deployment-skip evidence is RESOLVED. **Open risk remains**: automatic deployments are enabled, GitHub FE source is ahead of the active deployed release, and Preview URLs were published for earlier phase3-dev commits. No inference of sensitive data exposure without preview artifact inspection.

**Next controlled read-only discovery batch:** Cloudflare Pages Custom domains status for lms-fe and any distinct lms-admin frontend project; external-vantage DNS/TLS checks (AC12); separate PostgreSQL four intended LMS owned databases/roles/grants inventory (AC09), Redis effective memory/auth/persistence posture (AC10), and assets origin (AC13). Record Cloudflare Preview policy/lifecycle for later reviewed release governance without deleting or purging anything.

**Hard stop:** No Build/Deploy/Retry/Delete, Pages settings toggles, automatic-deployment disablement, preview purge, DNS edits, secrets, app merge, HRM/Keycloak mutation or Phase 4B/production authorization. Phase 4A-00 remains IN PROGRESS.

## 18. Cloudflare custom-domain and admin Pages search E24 (2026-10-10)

**Evidence class:** OWNER_SUPPLIED_CLOUDFLARE_DASHBOARD_TEXT and OWNER_REPORTED_NOT_FOUND. The user copied project lms-fe > Custom domains and separately wrote that lms-admin.reltroner.com was NOT FOUND after a request to inspect independent Pages admin frontend. No independently established exact capture time; record as dated 2026-10-10. The Cloudflare account identifier, private dashboard URL and any operator/session identifiers are intentionally omitted. No Cloudflare API authentication by this assistant.

| Item | User-supplied observation | Scoped outcome |
|---|---|---|
| Pages project | lms-fe, linked to Reltroner/LMS-FE | Matches E23 project name |
| Learner custom domain | lms.reltroner.com, **Active**, **SSL enabled** | **Operator UI subcheck PASS**: Pages recognizes this domain and reports SSL enabled. Not a full external DNS/TLS certificate, origin, content or live SSO test |
| Admin frontend | Owner statement: **lms-admin.reltroner.com = NOT FOUND** | In the context of the requested independent Pages admin frontend lookup, no project/domain was reported found. This does NOT establish authoritative DNS NXDOMAIN, HTTP status, every project/account inventory, or permanent nonexistence |
| Production deployment | E23 last verified: active Production displayed as f2d4041, and FE source commit eb01a4d was No deployment available | E24 does not re-observe a deployment. E23 remains authoritative on its dated snapshot |

**Frozen physical design:** Phase 0C master placement requires an independently deployable static admin frontend at lms-admin.reltroner.com. Separate browser identity contexts lms-user and lms-admin are frozen Phase 1 contract requirements, with both IDs absent in E20 current realm client list. **Admin frontend is not the authorization boundary**; its absence cannot be fixed by assigning greater Keycloak permissions to the learner app.

**Gate delta:** P4A00-AC11 remains **PASS_OPERATOR_CLOUDFLARE_UI (SCOPED)** from E23 for the specific PR5 Production skip. P4A00-AC12 remains **NOT PASSED**: only one Cloudflare Pages custom-domain SSL enabled status observed, no independent external-vantage DNS/TLS across all hostnames. P4A00-AC13 assets origin stays PENDING. P4A-G08 updated for the learner UI evidence and remaining DNS/TLS unknowns. New **P4A-G13** tracks operator-reported admin Pages project/hostname lookup absence as a future independently authorized frontend deployment dependency, not an instruction to create anything now.

**Fast next read-only batch:** Collect existing PostgreSQL database/owner/role grants *only via already authorized read-only catalog access* (no business rows, superuser escalation or credentials), plus sanitized Redis INFO runtime metadata (version, memory, persistence, keyspace total counts) without password, key names, ACL secrets or writes. A future Cloudflare zone DNS/SSL settings screenshot can narrow AC12 if needed, but this owner UI alone is not an external DNS/TLS check. Record access-denied as ACCESS_BLOCKED and move on; do not get stuck trying privileged sessions.

**Hard stop:** No Create Pages project, Add custom domain, DNS edit, TLS mode switch, Build/Deploy/Retry, Keycloak client provisioning, Redis key mutation, PostgreSQL DDL, sudo-based privilege changes, production maintenance or Phase 4B/production authorization. Phase 4A-00 remains IN PROGRESS.

## 19. PostgreSQL and Redis authentication-boundary evidence E25 (2026-10-10)

**Evidence class:** OWNER_SUPPLIED_UNPRIVILEGED_READ_ONLY_ACCESS_ATTEMPTS; observed at **2026-10-10T10:57:53Z = 17:57:53 WIB**. The user ran a PostgreSQL catalog-only SELECT through psql -X -w -d postgres and four local Redis INFO section calls. The pasted shell echo contains a malformed concatenation but the recorded database refusal, fallback ACCESS_BLOCKED marker and all four Redis responses are clear. This evidence is about **access permission boundaries**, not system failure. No database row data, Redis keys/values, app tokens, password, connection string or private IP were returned.

| Test | Observation | Correct classification |
|---|---|---|
| PostgreSQL catalog SELECT (target: four LMS database names) | Local Unix-domain socket to database postgres as OS user deploy returned FATAL: no pg_hba.conf entry for host [local], user deploy, database postgres, no encryption; fallback printed POSTGRESQL_CATALOG_ACCESS_BLOCKED | **ACCESS_BLOCKED_BY_EXISTING_HBA**. SQL SELECT did **not** execute, so ZERO database rows or role/owner/GRANT information can be inferred. A denied local socket connection does not contradict prior pg_isready TCP accepting or 18/main online |
| Redis INFO server | NOAUTH Authentication required | **ACCESS_BLOCKED_BY_REDIS_AUTH**; cannot inspect effective server version |
| Redis INFO memory | NOAUTH Authentication required | **ACCESS_BLOCKED_BY_REDIS_AUTH**; memory/eviction limit and policy remain unknown |
| Redis INFO persistence | NOAUTH Authentication required | **ACCESS_BLOCKED_BY_REDIS_AUTH**; RDB/AOF posture remains unknown |
| Redis INFO keyspace | NOAUTH Authentication required | **ACCESS_BLOCKED_BY_REDIS_AUTH**; no keyspace/DB usage claim and no key enumeration |

**Gate delta:** AC09 remains **PARTIAL_OPERATOR / ACCESS_BLOCKED**; AC10 remains **PARTIAL_OPERATOR / ACCESS_BLOCKED**. AC15 security inventory remains PENDING rather than inferred PASS from two denied commands. These responses are **not** evidence that the four LMS DBs are missing, that existing HRM or Keycloak database access is broken, that Redis is unavailable, or that Redis replay protection is effective. They do show unauthenticated access to those specific requests was denied at the time. Access-blocked is a legitimate discovery outcome, not a call to relax controls.

**Gap update:** G04 and G05 retain the necessary runtime metadata and future negative-test requirements; they now cite a concrete denied-read observation. No new drift is automatically classified as a production defect. The historical 1-vCPU VPS and existing identity/HRM workloads remain protected.

**Fast closeout without additional authentication:** Do not repeat the same denied commands or attempt alternate credentials. If an **already approved database catalog viewer** exists in the established operator workflow, request only aggregate database name/owner and redacted GRANT metadata through that authorized interface; otherwise mark DB ownership UNKNOWN / ACCESS_BLOCKED for this discovery and make read-only access an owner decision in the next scoped work order. For Redis, prefer existing authorized monitoring/dashboard screenshots of version, memory, persistence, eviction and anonymous access-denial policy if available; otherwise retain UNKNOWN / ACCESS_BLOCKED. Do not use sudo -u postgres, alter pg_hba.conf, take passwords from running app env, pass Redis AUTH credentials in chat, change Redis ACL, or disable protections.

**Next unblocked Phase 4A-00 work:** a batched read-only Cloudflare DNS/TLS zone summary (AC12), Premium Hosting asset origin and immutable path inventory (AC13), and backup/observability metadata/HRM coexistence (AC14/15). Separate final sign-off AC18 will explicitly accept residual blocked observations or authorize a future narrow read-only inspection; no assumption that blocked = PASS. No further mutations or Phase 4B/production authorization.

## 20. Cross-vantage DNS/TLS, VPS resource and backup timer E26 (2026-10-10)

**Evidence category:** OWNER_SUPPLIED_OPERATOR_READ_ONLY_CROSS_VANTAGE. Snapshot A: VPS as unprivileged SSH account at **2026-10-10T11:13:15Z**. Snapshot B: Windows PowerShell client at **2026-10-10T18:13:31+07:00 = 11:13:31Z**. User pasted a truncated/malformed portion of the bash command echo, but complete labeled result sections can be interpreted; do not attest exact byte-for-byte command execution from the echo. No remote shell/file edits, state-changing commands or access escalation reported. This public receipt does not reproduce external client public IP, VPS IP, dashboard account ID, bearer/Redis/DB secrets or personal account information.

### E26-A / E26-B DNS and HTTPS matrix

| Exact hostname | VPS getent A lookup | Windows Resolve-DnsName A query | Windows curl HTTPS HEAD | Classification |
|---|---|---|---|---|
| lms.reltroner.com | RESOLVES | RESOLVED (CNAME, A) | HTTP **200**, ssl_verify_result **0**, curl exit **0** | **DNS_RESOLVES / CLIENT_TLS_OK**, learner public service reachable at that instant |
| auth.reltroner.com | RESOLVES | RESOLVED (A) | HTTP **302**, ssl_verify_result **0**, curl exit **0** | **DNS_RESOLVES / CLIENT_TLS_OK**, HTTP redirect is not outage evidence |
| hrm.reltroner.com | RESOLVES | RESOLVED (A) | HTTP **302**, ssl_verify_result **0**, curl exit **0** | **DNS_RESOLVES / CLIENT_TLS_OK**, HTTP redirect is not outage evidence |
| lms-admin.reltroner.com | NOT RESOLVED | LOOKUP_FAILED | HTTP **000**, curl exit **6** (could not resolve host) | **HOSTNAME_NOT_RESOLVING** from both tested vantage points; HTTPS **NOT TESTED** |
| lms-api.reltroner.com | NOT RESOLVED | LOOKUP_FAILED | HTTP **000**, curl exit **6** | **HOSTNAME_NOT_RESOLVING**; intended sole public LMS API Gateway not established |
| assets.reltroner.com | NOT RESOLVED | LOOKUP_FAILED | HTTP **000**, curl exit **6** | **HOSTNAME_NOT_RESOLVING**; Premium Hosting asset origin/storage state still unknown |

**Crucial TLS interpretation:** Windows output printed \`TLS_VERIFY=0\` even when DNS failed for the last three hostnames. With **curl exit 6**, curl did not reach a TLS handshake; the printed numeric zero is **NOT evidence of TLS verification success**. Only the first three rows with **curl exit 0** support verified HTTPS at the Windows client trust store. This checks client-to-endpoint HTTPS from one non-VPS vantage, **not** complete certificate-chain audit, Cloudflare-to-origin certificate validation, or provider TLS Full (strict) readiness.

### E26-C: Cloudflare zone record and encryption context (same owner evidence batch)

Operator's prior zone DNS screenshot/text displayed **16/16 records** in reltroner.com: \`lms.reltroner.com\` CNAME to \`lms-fe-3gl.pages.dev\`, \`auth\` and \`hrm\` A DNS-only entries. No listed record for \`lms-admin\`, \`lms-api\` or \`assets\`; absence agrees with two-vantage failed lookups (do not overstate authoritative NXDOMAIN or all historical states). Cloudflare **SSL/TLS Overview** screenshot shows current zone encryption mode **Full**, **NOT Full (strict)**. Automatic mode is shown; no zone-level TLS change was made. Displayed Traffic Served Over TLS for last 24h: **45 None (not secure)** and **126 TLS v1.3**. These are aggregated zone traffic labels; they do not attribute an insecure request to LMS, Keycloak, HRM or specific route, nor justify altering settings now.

**Frozen architecture effect:** independent Pages admin frontend and DNS, only-public LMS API Gateway hostname, and immutable Premium asset hostname have not been provisioned in the observed DNS zone. This is a **future provisioning dependency**, not a reason to alter HRM/Keycloak Nginx, existing Pages or production Cloudflare security mode now. Full-to-Full(strict) migration requires origin certificate + all affected hostname regression proof and separately approved change window.

### E26-D: VPS resource persistence and backup-surface metadata

| Field | Observed VPS value | Constraint |
|---|---|---|
| CPU/load | **1 logical CPU**, uptime 18 days 13h, load average **0.05/0.03/0.00** | Single time window, no historical peak/placement budget |
| RAM/swap | **3.8 GiB total / 1.2 GiB used / 2.6 GiB available**, swap **2 GiB / 256 KiB used** | Available not reserved for LMS; protect incumbent HRM/Keycloak |
| Disk | Root ext4 **48G total, 5.9G used, 42G available (13%)** | No data growth/storage projection |
| Services | nginx, php8.4-fpm, postgresql, redis-server, keycloak, cron all **active** | Not proof of six LMS deployed service runtimes |
| Java RSS | **679856 KiB (~664 MiB)** in top process list (Keycloak family previously attributed E15) | RSS not exclusive Java/cgroup memory consumption |
| PostgreSQL | **18/main** port 5432 **online** | Database owner/role grants still ACCESS_BLOCKED E25 |
| /var/backups | Directory mode **drwxr-xr-x**, **39 files readable within depth 2**; newest file mtime **2026-10-10T01:45:52Z** | File counts/times **do not** establish PG backup success, integrity, offsite storage, retention or restore |
| Timers | **reltroner-postgres-backup.timer** last trigger **2026-10-10T03:20:14Z**, next **2026-10-11T03:24:01Z**; \`dpkg-db-backup.timer\` last trigger **2026-10-10T01:45:52Z**; certbot.timer registered | Last trigger is **not success status**; newest /var/backups mtime matching dpkg timer is **not** PG backup proof |
| Tools | pg_dump, pg_basebackup, redis-cli installed; restic, borg, rclone not found in PATH | Binary presence does NOT imply configured backup/recovery plan |

### Gate deltas and exact scope

- **P4A00-AC12: TOOL_UNAVAILABLE -> PARTIAL_OPERATOR_EXTERNAL_VANTAGE**. Two-vantage DNS plus Windows verified client TLS for 3 currently existing hosts; other 3 target hostnames fail DNS from both tested vantage points; origin strict-TLS still unverified. **Full AC12 NOT PASSED.**
- **P4A00-AC13: PENDING_RUNTIME -> PARTIAL_OPERATOR / ASSET_HOSTNAME_NOT_RESOLVING**. DNS not provisioned in visible zone; Premium Hosting asset origin, immutable URL and CDN policy all still **UNVERIFIED**.
- **P4A00-AC14 stays PARTIAL_OPERATOR**; registered PG backup timer and /var/backups metadata are nonzero evidence, but cannot validate backup success or disaster recovery. P4A00-AC15 still PENDING.
- **P4A-G06/G08/G10/G13** refined with measured capacity, DNS findings and timer caution; no claims of misconfiguration on unprovisioned Phase4 target hostnames.
- **P4A00-AC11** unchanged: pinned FE PR5 Cloudflare Production/main skip remains scoped PASS E23; Windows live 200 is of the **old active Production deployment**, not proof that Phase3 FE GitHub/main is deployed.
- **P4A00-AC09/10** remain PARTIAL / ACCESS_BLOCKED from E25; do not reattempt auth or weaken controls.

**Remaining one-batch read-only operator evidence:** Hostinger hPanel Premium Web Hosting backup status/last timestamp/retention, Premium subdomain/document-root listing for \`assets.reltroner.com\` (if none, mark NOT FOUND), VPS Backups/Snapshots status/retention/last timestamp, and VPS Monitoring/Usage chart (if available). Optionally, an unprivileged \`systemctl show reltroner-postgres-backup.service --property=Result,ExecMainStatus,ExecMainCode,ActiveState,SubState,ExecMainStartTimestamp,ExecMainExitTimestamp --no-pager\` can narrow service-result evidence, but is not a restore test. Do not open/archive backup contents or list user files.

**Stop:** No creation of missing DNS entries/Pages projects, no Full(strict) toggle, certificate replacement, privileged DB/Redis auth, package update, filesystem mutation, backup trigger/restore, deploy or Phase 4B/production authorization. Phase 4A-00 remains **IN PROGRESS**, pending owner hPanel evidence and AC18 sign-off.

## 21. E27 — batched local Git, VPS backup-job status, runtime security and capacity discovery (2026-10-10)

**Evidence class:** OWNER_SUPPLIED_POWERSHELL_AND_UNPRIVILEGED_SSH_READ_ONLY. Windows operator collection **2026-10-10T18:26:42+07:00**; VPS timestamp **2026-10-10T11:26:45Z**. Source: operator-provided E27 terminal record; public documentation contains sanitized evidence only, **not** local user paths, VPS IP, SSH identities, raw logs, environment/config contents, tokens or backup data. Commands enumerated local Git metadata and bounded VPS service, process, permission and resource metadata. No sudo/privileged read, application merge, service operation, backup trigger or restore reported.

| E27 sub-evidence | Observed | Correct boundary |
|---|---|---|
| Windows backend checkout | main at `a2672d0085fe84b55520f8f52f41a8c7fc8568a0`, dirty entry count **0** | Local pinned BE source matches accepted GitHub main E01; no fetch/reset |
| Windows frontend checkout | main at **`f2d40417d0eea71e2c3e329ec6e32933b3e6cbd7`**, dirty entry count **3** | Older than GitHub FE main `eb01a4d2c924299b929aebf0f4826b94cf341fc6`; **preserve all three modifications/untracked entries**; their content was not inspected |
| PostgreSQL backup service | `reltroner-postgres-backup.service`: `Result=success`, `ExecMainCode=1` (systemd 'exited'), **`ExecMainStatus=0`**, began 03:20:14Z and exited 03:20:15Z on 10 Oct | **SUCCESSFUL_SERVICE_EXECUTION_OBSERVED**, not validated SQL dump, backup integrity, storage destination, offsite copy or restore. Do not misread `ExecMainCode=1` as a process exit failure |
| Additional one-shot services | `dpkg-db-backup.service` and `certbot.service` each reported `Result=success`, `ExecMainStatus=0` | Service run only; no restore or certificate-renewal end-to-end certification |
| HRM background execution | `reltroner-hrm-queue.service` active/running, `reltroner-hrm-scheduler.timer` listed at minute cadence | Existing incumbent CPU/RAM/IO workloads belong in LMS placement budget |
| Security services | `ufw.service` active/exited; `fail2ban` inactive | Firewall **rules**, effective external reachability and alternate abuse defenses **not inspected**; inactive fail2ban alone is not vulnerability proof |
| Systemd unit metadata | Redis unit `User=redis`, `PrivateTmp=yes`, `ProtectSystem=yes`, `ProtectHome=yes`, `NoNewPrivileges=yes`; Keycloak `User=keycloak`, `ProtectSystem=full`, `ProtectHome=yes`, `NoNewPrivileges=yes`; Nginx/PHP-FPM/PG/cron attributes also collected | Selected sandboxing **settings**, not full service security certification; default/explicit `no` values elsewhere are not independently verified exploits |
| Selected paths | /etc/nginx/sites-enabled, /etc/php/8.4/fpm/pool.d, /etc/letsencrypt, /var/backups: `755 root:root`; enabled Nginx names auth/default/hrm and single `www.conf` PHP-FPM pool name | Directory and filename inventory only; no config contents/permission checks on secrets or route mapping |
| Backup directory | 39 visible files within selected depth, mtimes aggregated | Cannot attribute file contents to PostgreSQL backup or prove integrity |
| VPS brief repeat | 1 vCPU; RAM ~3.8 GiB total, ~2.6 GiB available; swap 2 GiB; disk 48 GB total / 42 GB free; ~4% inode use; low brief load/vmstat | One instant, not safe headroom for six production microservices |
| TCP classification | `awk` multiline syntax error | **E27 SOCKET_AUDIT_INVALID**; corrected in E27R below |
| Collection exit | `SSH_EXIT_CODE=0` despite the above pipeline syntax failure | Wrapper exit 0 does **not** establish all subchecks passed; maintain the explicit defect |

**Gate change E27:** P4A00-AC05 remains **PARTIAL_OPERATOR** (BE fresh-clean, FE dirty old HEAD, work preserved); AC14 is **PARTIAL_OPERATOR_IMPROVED** (positive PG systemd backup success and incumbent worker/scheduler); AC15 moves **PENDING_RUNTIME -> PARTIAL_OPERATOR_METADATA_ONLY**; AC07 stays PARTIAL with invalid E27 socket subcheck; AC06 prior scoped PASS corroborated. E25 AC09/10 remain **ACCESS_BLOCKED**, not reattempted.

## 22. E27R — socket classification and HRM background revalidation (2026-10-10)

**Evidence class:** OWNER_SUPPLIED_CORRECTIVE_UNPRIVILEGED_SSH_READ_ONLY. Windows **2026-10-10T23:11:47+07:00**; VPS **2026-10-10T16:11:51Z**. Read-only corrective Bash command successfully emitted all expected classification and HRM unit/timer metadata. The script printed `CORE_FAILURES=0` and `E27R_CORRECTIVE_GATE=PASS`, **but returned SSH exit code 2** because the terminal reported `bash: line 78: exit: 0 ... numeric argument required`. A CRLF/carriage-return artifact is a plausible explanation **but not independently proven**. Therefore **SCRIPT_EXIT_SIGNAL_INVALID**; classify each completed subcheck on its evidence and do **not** upgrade the whole script to clean exit PASS. No need to repeat existing output merely to suppress this known formatting defect.

| Port group | Observed listening bind class | Interpretation |
|---|---|---|
| TCP 22, 80, 443 | ALL_INTERFACES | Listener exposure class, **not** verified firewall allowance or real internet reachability |
| TCP 5432, 6379 | LOOPBACK | PostgreSQL/Redis socket bind isolation **observed**, not credential/grant/ACL or service-to-service isolation proof |
| TCP 8080, 9000, 7800, 37371, 57800, 65529 | LOOPBACK | Internal listeners observed; attribution to a specific process/service and Nginx upstream routes unverified |
| TCP 53 | OTHER_BIND | **Indeterminate from classifier**; cannot assume publicly exposed DNS or specific resolver without interface details |

**HRM repeat:** `reltroner-hrm-queue.service` active/running, OS user deploy, main PID observed, start **2026-10-10T15:28:22Z**. One-shot `reltroner-hrm-scheduler.service` execution at **16:11:00Z** ended `Result=success`, `ExecMainStatus=0`; unit idle/dead afterward is normal for completed one-shot execution, while `reltroner-hrm-scheduler.timer` was active/waiting with next 16:12Z trigger. PG backup timer remained next scheduled **2026-10-11T03:24:01Z**.

**Gate:** AC07 still **PARTIAL_OPERATOR / PORT_BIND_CLASSES_OBSERVED** because process identity, effective Nginx public-vs-private route and negative public exposure testing remain absent. AC14 still **PARTIAL_OPERATOR** with more precise HRM coexistence workload metadata; AC15 **PARTIAL_OPERATOR_METADATA_ONLY**. Unsuccessful final SSH numeric exit does **not** mean application failure and must remain in audit provenance.

## 23. E28 — Hostinger seven-day resource charts, provider backups, asset-origin operator attestation (2026-10-10)

**Evidence class:** OWNER_SUPPLIED_HOSTINGER_HPanel_UI_SCREENSHOT_AND_TEXT plus OWNER_ASSET_NONPROVISIONING_ATTESTATION, observed/reported on 10 October 2026 (exact provider screenshot/backup-UI capture clock and displayed backup timezone **not independently verified**). Do not archive raw screenshots with browser tabs/accounts, provider account identifiers or private dashboard URLs in public GitHub. This is provider UI evidence, not provider API attestation or tested restore.

| Area | Read-only observation | Limit |
|---|---|---|
| hPanel VPS Server Usage, selected **Last week** | CPU plotted approximately **2% baseline** with occasional small spikes; RAM chart near **1.2 GiB** and nearly level; disk chart around **5.9 GB**, essentially flat | Visual chart estimates, not machine-precise percentiles, process-specific usage, peak load testing or a resource reservation |
| Network charts | Intermittent inbound and outbound peaks on chart | Per-point time aggregation and units-of-rate not established; **no Mbps/second claim** |
| VPS automated backup cadence | **Weekly** displayed | Frequency known; recovery-point objectives not guaranteed |
| Two visible Hostinger VPS backup entries | **2026-10-05 05:49**, **5.83 GB**, Lithuania, Ubuntu 24.04 LTS; **2026-09-28 00:13**, **5.34 GB**, Lithuania, Ubuntu 24.04 LTS | Existing provider-listed backup records; timestamps as displayed, timezone unverified; cannot assert integrity or restore success |
| Provider storage/restore UI | Provider states backups stored separately from main VPS; **30m estimated restore** displayed; older backups replaced automatically | Distinct provider backup surface observed; **30m is an estimate, NOT measured RTO**; exact retention guarantee, cryptographic integrity, DR exercise and recovery consistency UNKNOWN |
| Paid upgrade offer | Optional daily-backup add-on shown at **Rp52.900/month** | **NO_PURCHASE / NO_UPGRADE**; not a required Phase4A discovery spend; backup risk to be approved separately |
| Asset origin | Owner explicitly states `assets.reltroner.com` never provisioned in Cloudflare, Vercel or Hostinger; E26 independently observed DNS nonresolution from Windows+VPS and no record in the shown Cloudflare zone list | **OWNER_ATTESTED_NOT_PROVISIONED + DNS_UNRESOLVED**, not an independent complete vendor-account API audit or proof of lack of other stored files |
| Premium Web Hosting backups | **NOT PROVIDED / NOT INSPECTED** | Must not label PASS or pretend Provider backups cover any separate Premium Hosting account |

**Risk model:** Weekly VPS recovery could lose several days of data if this were the only usable recovery point; separate PG backup **job-success metadata** E27 reduces ambiguity but does not prove a successfully restorable recent database or offsite copy. A 30-minute restore estimate is not a measured end-to-end RTO for HRM, Keycloak, PostgreSQL and Redis. The observed low CPU baseline on 1 vCPU cannot certify simultaneous six-service request, queue, replay, event durability and failure-state requirements.

**Gate deltas:** AC06 remains **PASS_OPERATOR_READ_ONLY (scoped capacity discovery)** with provider historical chart support; AC13 advances **PARTIAL_OPERATOR -> GAP_OBSERVED / OWNER_ATTESTED_NOT_PROVISIONED** (not overall acceptance PASS); AC14 remains **PARTIAL_OPERATOR_IMPROVED** with two independently listed weekly off-host VPS backups, but untested restore, retention, RPO/RTO and Premium backups unknown. Other gate statuses unchanged.

## 24. Phase 4A-00 final evidence audit and owner-review closure candidate (E29; 2026-10-10)

> **Status: FINAL AUDIT PREPARED / DISCOVERY-ONLY CLOSURE CANDIDATE — NOT OWNER-SIGNED; NOT ALL 18 GATES PASS.** This is an assessment of existing evidence **E01–E28 including E27R**, not new runtime testing. The term *final audit* does not mean production readiness, complete test coverage or authority to start Phase 4B.

### 24.1 Normative authority and provenance

Normative hierarchy unchanged: [Phase 0C frozen physical placement](./master-infrastructure-placement-contract.md) (20 physical invariants) -> [Phase 1 frozen logical/API boundaries](./logical-service-boundary-api-contract.md) (24 logical invariants) -> owner-adopted [FZ-11 freeze](./reltroner-lms-phase3a-fz11-final-design-freeze-acceptance-20261009.md) and [ADR-LMS-TRUST-001](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md) -> current [README](./README.md) + append-only [engineering ledger](./engineering-end-to-end-progress-ledger.md). Phase3 **28/28 owner-accepted in scoped nonproduction**, **44/44 invariant trace entries**, **0 newly live-certified** by Phase3; do **not** upgrade 44 to runtime PASS. Accepted source pins previously verified: BE main `a2672d0085fe84b55520f8f52f41a8c7fc8568a0`, FE main `eb01a4d2c924299b929aebf0f4826b94cf341fc6`; 7/7 and 2/2 corresponding earlier successful push-main CI, **not** live six-service proof. Local FE remains older/dirty and must not be overwritten. No source repo update in this work order.

### 24.2 Definitive 18-gate discovery ledger (evidence-scoped, as of E28)

| Gate | Final audit classification | Evidence establishing it; exact residual gap |
|---|---|---|
| **AC01** Scope/owner | **PASS_OWNER_READ_ONLY_SCOPE** | Owner authorized discovery only; no broader sign-off implied |
| **AC02** Source SHA/CI | **PASS_SOURCE_SCOPED** | E01–E03 BE/FE/docs GitHub pins and historical CI; new current remote CI/drift not re-polled in E27/E28 |
| **AC03** Architecture authority | **PASS_DOCUMENT_TRACE** | E04 frozen Phase0C/Phase1, FZ-11/ADR hierarchy and 44 trace rows; no live certifications |
| **AC04** Source topology/templates | **PASS_SOURCE_SCOPED** | E05–E07 six independent Laravel source services, API skeletons, FE OIDC template drift |
| **AC05** Local checkout safety | **PARTIAL_OPERATOR / FE_DIRTY_OLD_HEAD** | E09/E27 BE main clean; FE local `f2d40417...`, 3 dirty entries, versus newer remote main; no clean FE baseline, preserve work |
| **AC06** VPS capacity | **PASS_OPERATOR_READ_ONLY_SCOPED** | E13/E26/E27 1 vCPU, ~3.8GiB, ~42GB root available; E28 7-day usage charts. **Not** placement/load-test authorization |
| **AC07** Runtime isolation/routing | **PARTIAL_OPERATOR / BIND_ONLY** | E13–E17/E27R units, three enabled sites, single www FPM pool, 5432/6379 loopback, 22/80/443 all-interface, other loopback; no effective route/firewall/client-to-origin negative tests; E27R final SSH exit defective |
| **AC08** Identity/HRM | **PARTIAL_OPERATOR / LMS_CLIENTS_ABSENT** | E18–E22 issuer/JWKS/realm GUI, 8 client list excludes lms-user/lms-admin; no real aud=lms-api, PKCE, LMS JWT/capability denial or fresh HRM live regression |
| **AC09** PostgreSQL ownership | **PARTIAL_OPERATOR / ACCESS_BLOCKED** | E16/E17 cluster 18/main online/ready; E25 local SQL catalog read rejected by HBA; four owner databases/GRANTs not proven; do not circumvent |
| **AC10** Redis security/replay | **PARTIAL_OPERATOR / ACCESS_BLOCKED** | E13/E27R loopback, process/service, E25 NOAUTH to INFO; no ACL/memory/persistence/replay-loss fail closed proof |
| **AC11** Pages Production/main | **PASS_OPERATOR_CLOUDFLARE_UI_SCOPED** | E23–E24 production skip for FE eb01a4d and active old f2d4041, learner domain active/SSL; no content/preview policy/full release governance |
| **AC12** DNS/TLS | **PARTIAL_OPERATOR_EXTERNAL_VANTAGE / THREE_TARGET_HOSTS_UNRESOLVED** | E26 Windows+VPS DNS, Windows HTTPS 200/302/302 with exit 0/TLS verification for lms/auth/hrm; admin/API/assets fail DNS/exit6. Cloudflare zone Full not strict; origin TLS not established |
| **AC13** Assets | **GAP_OBSERVED / NOT_PROVISIONED_OWNER_ATTESTED** | E26 unresolved assets hostname, E28 owner says no Hostinger/Vercel/Cloudflare origin; storage/versioned CDN/immutable cache policy untested |
| **AC14** Backup/HRM coexistence | **PARTIAL_OPERATOR_IMPROVED / RECOVERY_UNTESTED** | E27 PG backup job `Result=success` exit0, HRM queue/scheduler; E28 two weekly Hostinger Lithuania backup entries + 30m provider estimate, 7d usage; no restore test/RPO/RTO/retention validation or Premium backup |
| **AC15** Security/secret custody | **PARTIAL_OPERATOR_METADATA_ONLY** | E27 unit sandboxing, service owners, directory modes, UFW active and fail2ban inactive; rules, complete permissions, secret custody and effective Nginx/PKI policy unverified |
| **AC16** Gap/risks/rollback/cost | **PARTIAL_DESIGN / OWNER_REVIEW_READY** | G01–G13 and §24.3 decisions/risks plus §24.4 future negative-test/rollback package proposals; design is not performed testing nor adopted sign-off |
| **AC17** Scope integrity | **PASS_SCOPE_SO_FAR / OBSERVED** | No reported provisioning/restart/write/merge in E01–E28 operator discovery. Does not independently prove host change history; E27R exit defect preserved, no false clean-script success |
| **AC18** Final portable handoff/sign-off | **PENDING_OWNER_FINAL_ACCEPTANCE** | E29 final candidate drafted in both append-only docs; **no user instruction explicitly accepting residuals and closing 4A-00 yet** |

**Tally (discovery, not runtime): 7 PASS of explicitly limited scope (AC01–04, 06, 11, 17); 10 PARTIAL/GAP/PENDING_OWNER_REVIEW (AC05, 07–10, 12–16); 1 PENDING FINAL OWNER DECISION (AC18).** Each scoped PASS remains narrowly qualified; **18/18 PASS is false**. Gate and architecture runtime certification counts remain separate.

### 24.3 Residual gap register and decision owner

| Gap | Priority | Designated decision owner | Needed next evidence / disposition |
|---|---|---|---|
| **G01** BE public API 26 contract routes not implemented | HIGH | LMS architecture/product owner | Separately authorize bounded gateway/provider implementation, source CI then negative API tests |
| **G02** FE `.env.example` legacy issuer/client | HIGH | FE/identity owner | Verify effective current config vs frozen issuer, select independent user/admin credentials and release pins |
| **G03** BE trust-status metadata drift vs ratified ADR | HIGH | Security/BE owner | Reconcile metadata in separate authorized code PR; Ed25519 signer/replay tests remain future |
| **G04** PostgreSQL four DB ownership/grants unknown, HBA denies inspection | HIGH | DB operator + project owner | Explicit approved catalog-only viewer or ACCEPT_ACCESS_BLOCKED; later service-DB negative write tests |
| **G05** Redis auth/persistence/replay metadata unknown, anonymous INFO denied | HIGH | Runtime/security owner | Approved monitoring viewer or ACCEPT_ACCESS_BLOCKED; atomic jti/replay-loss quarantine tests later |
| **G06** 1-vCPU service isolation/peak resource budget unknown | HIGH | VPS capacity/release owner | Budget incumbent Keycloak/HRM worker+cron+PG+Redis and six LMS units before placement |
| **G07** Pages skip proven but automatic deployments/preview policy | MEDIUM-HIGH | Frontend release owner | Deployment SHA and artifact privacy/preview guard design; no live content assumption |
| **G08** API/admin/assets missing DNS and origin Full not strict | HIGH | DNS/TLS/platform owner | Individually authorize future provisioning/strict-TLS origin audit, preserve existing HRM/auth |
| **G09** lms-user/lms-admin absent, lms-api audience unproven | HIGH | Identity/security owner | Separately authorize new clients/mappers, PKCE and denial tests without altering HRM gates |
| **G10** Backup/restore, outbox and observability not certified | HIGH | DR/operations owner | Approve recovery objectives, integrity/checksum and isolated restore drill plan; verify event durability |
| **G11** Local FE old/dirty checkout | MEDIUM | Local source owner | Preserve 3 modifications, reconcile only with separate exact-SHA authorization; no reset |
| **G12** Dated doc headers potentially stale | LOW-MEDIUM | Documentation owner | Use README + newest ledger overlay; frozen historical sections remain unchanged |
| **G13** Admin Pages missing | HIGH | Frontend/identity release owner | Independently deployable admin client/project plan; never grant admin capability through learner client |

**Classification guards:** Existing protective authentication denials are **ACCESS_BLOCKED**, not evidence of broken DB/cache. Missing never-provisioned LMS targets are **GAP_OBSERVED**, not outages of a prior live LMS runtime. Keycloak RS256 public OIDC JWKS **must not** be conflated with Ed25519 **internal service** ADR. Weekly provider backups do **not** resolve transactional recovery or eliminate the need for a restore drill. Premium Web Hosting backup evidence was not collected; explicitly UNKNOWN.

### 24.4 Future work-package dependencies, acceptance negatives, rollback and spending (PROPOSED ONLY)

1. **P4B-00 authority/capacity gate:** Owner decision on residual AC05/07–10/12–16 and AC18; exact BE/FE/docs SHA reconfirmation; no-cost first placement study on 1-vCPU VPS, persistent resource monitoring and HRM/Keycloak safeguards; STOP if concurrent worker/DB/identity budgets cannot be met.
2. **P4B-identity/trust nonproduction:** Provision separate learner/admin PKCE S256 browser contexts and lms-api audience only after explicit authorization; prove wrong issuer/aud, absent capability, expired/replayed tokens, principal mixups and HRM demo/production cross-environment denial. Internal Ed25519/JWS 60s/5s/180s/jti + >=65s recovery quarantine per approved ADR; never simulate Redis failure on current shared production host without dedicated work order.
3. **P4B-private data/services:** Four isolated domain DB ownership/grant paths, private five business services, sole public Gateway, event outbox/delivery durability, wrong-DB write denial and public port exposure negative tests. No ad hoc `sudo -u postgres`, HBA relaxation or anonymous Redis unlock for discovery.
4. **P4B-static delivery/asset/release:** Independently deployable learner/admin Pages clients; separately authorized DNS `lms-admin`, `lms-api`, `assets`; versioned immutable origin/cache rules; confirm release SHA, draft/archived privacy and Preview policy; Cloudflare Full-to-Full(strict) only after per-host origin certificate + existing auth/hrm regression and a change window. Existing learner production remains on prior active release until explicit cutover.
5. **P4B-DR & operations:** Define acceptable RPO/RTO, confirm actual PG backup artifact success, encryption/access/retention and offsite consistency, perform isolated restore and integrity validation with rollback design, baseline HRM queue/scheduler and expiry/monitoring; neither 30m provider UI estimate nor successful systemd run substitutes tested recovery.

**Proposed rollback boundary:** Git/GitHub preserve approved immutable commit trees, Cloudflare preserve existing active Pages production, VPS retain incumbent Nginx/Keycloak/HRM/PG/Redis configs and service availability, DB migration/identity rollback only under explicit migration plan and integrity precondition; never promise untested automatic reversal of data/identity writes. **Cost:** no package purchases or VPS upgrade in 4A-00; optional Hostinger daily backups offer **Rp52.900/mo** observed but not selected/approved. Capacity inadequacy may force a later explicit budget decision; no invented cost forecast or implicit spending authority.

### 24.5 Final audit disposition and exact owner decision still needed

**Outcome:** `P4A-00_E29_FINAL_EVIDENCE_AUDIT_PREPARED`; read-only discovery inputs are **sufficient to request owner review/closure with explicit open risks**. **Phase 4A-00 formally remains IN PROGRESS / AC18 PENDING_OWNER_FINAL** until the owner explicitly either (A) accepts this scoped discovery handoff **with each residual PENDING/ACCESS_BLOCKED/GAP and no runtime PASS implied**, or (B) directs a narrowly bounded additional read-only follow-up. The present request to **audit and append records** is documentation authorization, **not** a standalone sign-off that all gates passed, nor authorization for Phase 4B or production.

**No mutation / governance:** Append-only evidence amendment under a documentation-only PR; do not edit frozen contracts, overwrite prior E01–E26 observations, touch LMS-BE/LMS-FE, modify local dirty FE, change Cloudflare/Hostinger/VPS/Keycloak/PostgreSQL/Redis, test restore or deploy. Any future source merge, client/DB provisioning, trust keys, DNS setup, feature implementation, release or paid plan requires separate exact-scope owner approval.

**Handoff checkpoint:** `PHASE0C+1_FROZEN -> PHASE2D_ACCEPTED -> PHASE3A_DESIGN_FROZEN -> PHASE3B_NONPROD_28/28_ACCEPTED -> PHASE4A_E01-E28_OBSERVED -> E29_FINAL_AUDIT_CANDIDATE -> AC18_PENDING_OWNER -> PHASE4B/PRODUCTION_NOT_AUTHORIZED`.

## 25. E30 — Complete G01–G13 read-only source + operator evidence reconciliation (2026-10-10)

> **OWNER WORK REQUEST:** "Selesaikan discovery G01 sampai G13"; interpret as **complete observable discovery and explicit classification/handoff for all thirteen known gaps**, not permission to implement them. The separate instruction to update README mandates deterministic beginner-to-professional explanation. **NO Phase4B, cloud, runtime or source application writes.** This E30 is a **supplement to** E29, not a retroactive alteration of historical E01–E28 evidence.

### 25.1 Method, exact source pins and validation boundary

- **Read-only live GitHub main verification (2026-10-10):** `Reltroner/LMS-BE/main = a2672d0085fe84b55520f8f52f41a8c7fc8568a0`; `Reltroner/LMS-FE/main = eb01a4d2c924299b929aebf0f4826b94cf341fc6`; `Reltroner/progress-documentation/main = 5ce584e2858b8f23170d2a63c9eb66048b8a4f6d` at the discovery preflight. Source-tree structure and targeted public source files were read with GitHub APIs, not executed; no independent fresh Actions run or production SSH access performed for E30.
- **GitHub BE concrete review:** `services/{gateway,learning,mentorship,knowledge,assistant,audit}/routes/api.php` each exactly **6 bytes, `<?php\n`**, blob **b3d9bbc7f3711e882119cd6b3af051245d859d04**; Gateway `routes/health.php` defines `/health/live` and `/health/ready`, `bootstrap/app.php` registers health routes plus RequestId and ProblemDetails error middleware. Gateway/Learning sampled `app/Http/Controllers` contain only `Controller.php` and `HealthController.php`. **No assertion that every possible handler file elsewhere was exhaustively inspected**, but none of the six published Laravel `api.php` files implements the frozen 26 business routes.
- **BE contract trust proof:** `contracts/README.md` specifies exactly 26 OpenAPI method/path contracts and 19 capabilities as **contract-only**; `contracts/persistence/README.md` expressly says four DBs/outbox are schema-only, no SQL migration, DB user or Redis broker provisioned; `contracts/identity/trust-contract.json` carries `PENDING_SECURITY_ADR`, `contracts/identity/crypto-profile-proposal.json` carries `CANDIDATE_NOT_OWNER_RATIFIED_SECURITY_ADR`, while later [ADR-LMS-TRUST-001](./adr-lms-trust-001-internal-signing-and-replay-ratification-20261010.md) ratified **nonproduction** Ed25519 design. This is provenance drift, not permission to change frozen standards.
- **GitHub FE concrete review:** `.env.example` points to legacy `sso.reltroner.com` / `lms-reltroner`; `src/lib/auth/oidc-config.ts` reads public env variables and selects authorization-code flow; `oidc-client.ts` uses browser `sessionStorage`, relying on oidc-client-ts default PKCE. `src/lib/auth/auth-roles.ts` has a **frontend-only authenticated student fallback**; `src/app/admin/page.tsx` has `ProtectedRoute` + client-side `RoleGate` and explicitly says real admin capabilities require backend/server authorization. `next.config.ts` uses `output: "export"` (static frontend); legacy `docs/auth/sso-architecture-roadmap.md` and `keycloak-lms-sso-chunk-1.md` contain dated identity-client/issuer claims **inconsistent with current frozen target**. Do not mistake client-side `RoleGate` or fallback for backend capability enforcement; do not assume deployed FE uses source `.env.example`.
- **Operator provenance reused, not re-probed:** E20–E22 Keycloak GUI, E23–E24 Cloudflare Pages, E25 security denials, E26 cross-vantage DNS/TLS, E27/E27R unit/socket/process, E28 Hostinger backup/monitoring and explicit operator origin absence. Access to live Cloudflare account, Hostinger, Keycloak admin, restricted PostgreSQL catalogs, authenticated Redis and user-local dirty FE files **not available to this GitHub-only pass**.

### 25.2 G01–G13 disposition matrix — evidence versus future engineering work

**Read column carefully:** `DISCOVERY_CLASSIFIED` means the cause/state and missing proof are identified; it does **not** mean an implementation gap is fixed or that Phase4A 18/18 gates PASS.

| Gap | Beginner-friendly observed truth, with evidence origin | E30 discovery disposition | Remaining change / acceptance (future authorization only) |
|---|---|---|---|
| **G01 — Business API implementation** | **Six source Laravel applications exist**, but all six `services/*/routes/api.php` files contain only `<?php`; gateway health + error handling exist. 26 API operations are OpenAPI/authorization contracts, **not running business endpoints** (BE main, GitHub source). | **DISCOVERY_CLASSIFIED / NOT_IMPLEMENTED_BUSINESS_ROUTES** | Phase4B engineering PRs: provider handlers, authorization, persistence, API contract tests + real private/public HTTP positive/negative tests; no backend deploy now |
| **G02 — FE issuer/client template drift** | FE `.env.example` uses legacy `sso.reltroner.com` and `lms-reltroner` instead of current `auth.reltroner.com/realms/reltroner` + independent `lms-user/lms-admin`. Existing FE uses code-flow client-side OIDC; actual currently deployed Cloudflare env **unknown**. `auth-roles.ts` student fallback is **UX-only**, and not backend capability proof (FE main). | **DISCOVERY_CLASSIFIED / SOURCE_TEMPLATE_DRIFT + LIVE_CONFIG_UNVERIFIED** | Separate approved FE/identity work: verify effective env; isolate learner/admin flows, align redirect/logout/origin/PKCE and source templates, test failed wrong-client/role access; **never silently write Cloudflare env** |
| **G03 — Cryptographic contract status drift** | BE trust-contract still says `PENDING_SECURITY_ADR`, crypto-profile says `CANDIDATE_NOT_OWNER_RATIFIED_SECURITY_ADR`, whereas dated **ADR-LMS-TRUST-001 is ratified as DESIGN ONLY**. Synthetic signature tests do not prove real dual-control HTTP or Redis replay behavior. | **DISCOVERY_CLASSIFIED / STALE_SOURCE_STATUS_METADATA** | Later security PR may reconcile *non-normative* stale status under authority, implement real Ed25519 + pinned per-service key ownership, jti atomic single use, TTL/skew/rotation/recovery negative tests |
| **G04 — Four PostgreSQL DB/GRANT owners** | PG18 cluster online, listener 5432 loopback, but `psql` catalog read as unprivileged deploy was denied by existing HBA **before SELECT executed** (E25/E27R). BE schema design **does not provision DBs**. No proof existing DB names/owners/GRANT. | **DISCOVERY_CLASSIFIED / ACCESS_BLOCKED_BY_SECURITY; EFFECTIVE_LMS_DB_EXISTENCE=UNKNOWN** | Only already approved catalog viewer or separately owner-authorized DB work order; four owner-isolated DBs, no cross-write, permissions/migrations in nonproduction before promotion; no sudo/HBA edits now |
| **G05 — Redis runtime and replay** | Redis process active at loopback 6379, anonymous `INFO` denied `NOAUTH` (E25/E27R); version/ACL/memory/persistence unretrieved, atomic replay guard and Redis-loss quarantine **not runtime tested**. | **DISCOVERY_CLASSIFIED / ACCESS_BLOCKED_BY_SECURITY; REPLAY_RUNTIME_UNVERIFIED** | Authorized metrics viewer and dedicated nonproduction failure simulation: duplicate jti denial, store unavailable fail closed, >=65s quarantine per ADR, memory/eviction and queue safety |
| **G06 — VPS service budget and isolation** | 1 vCPU, 3.8GiB RAM, 48GB disk; seven-day charts low CPU (~2%) and stable ~1.2GiB RAM/~5.9GB disk; existing Keycloak/HRM queue/scheduler/PG/Redis already use resources; single FPM `www.conf` pool name observed. Low CPU **is not** six-service peak headroom (E26–E28). | **DISCOVERY_CLASSIFIED / CAPACITY_DATA_PRESENT; SIX_SERVICE_SAFETY_UNPROVEN** | Approved future per-service FPM/queue/budget design, load/cgroup/process peaks, SLO and HRM coexistence/rollback conditions before allocating RAM/CPU; no spending without owner |
| **G07 — Cloudflare release/preview governance** | Pages `lms-fe` Production/main **eb01a4d** displays `No deployment available`; active hosted release is older `f2d4041`, automatic deployments enabled, historical `phase3-dev` previews exist; preview privacy/history not exhaustively audited (E23–E24). | **DISCOVERY_CLASSIFIED / SOURCE_RELEASE_SHA_DIVERGENCE_KNOWN; POLICY_GAP_OPEN** | Owner-approved release SHA controls, content/privacy/preview and rollback checks before any new deployment; preserve active production |
| **G08 — DNS and origin TLS** | Existing lms/auth/hrm resolve with external HTTPS success; lms-admin/lms-api/assets DNS fails from Windows+VPS and missing shown Cloudflare zone records. Zone `Full`, **not `Full (strict)`**. No proof of origin certificate validation (E26). | **DISCOVERY_CLASSIFIED / THREE_HOSTS_NOT_PROVISIONED_AT_OBSERVED_ZONE; STRICT_ORIGIN_TLS_UNVERIFIED** | Separate domain/API Gateway/asset provisioning with exact origin mapping, cert and pre/post HRM+Keycloak negative/regression tests before considering Full(strict); no zone switch now |
| **G09 — LMS identity clients and audience** | Keycloak public issuer/JWKS known; E20 realm client inventory 8 entries **does not list `lms-user` or `lms-admin`**. `aud=lms-api` mapper/token proof absent. Existing HRM frozen identity history is not new live regression. FE role UI is not API capability enforcement. | **DISCOVERY_CLASSIFIED / LMS_BROWSER_CLIENTS_NOT_LISTED; AUDIENCE=UNVERIFIED** | Owner-authorized separate browser clients, strict redirect/PKCE S256, aud/azp/iss enforcement, admin-vs-learner and HRM environment denial; no Keycloak changes in discovery |
| **G10 — Backup/restore, observability, durable events** | PG one-shot backup unit reports `Result=success`/exit0; Hostinger weekly off-host listed backups 5.83GB/5.34GB + 30m *estimated* restore; 7-day charts exist. Actual backup integrity, isolated restore, RPO/RTO, alerts, outbox and event durability **NOT tested** (E27/E28, BE persistence contract). | **DISCOVERY_CLASSIFIED / JOB_SUCCESS_OBSERVED; RECOVERY_AND_EVENT_DURABILITY_UNVERIFIED** | Define data-loss and recovery budgets, validate real artifacts, controlled isolated restore with permission, monitor alerts, idempotent event publish/inbox negative tests; no production restore now |
| **G11 — Dirty local FE checkout** | Operator E27: Windows BE main correct + clean; local FE main old SHA `f2d40417...`, **3 dirty entries**; their filenames/content not available through GitHub, ancestry not revalidated. | **DISCOVERY_CLASSIFIED / PRESERVE_UNINSPECTED_LOCAL_CHANGES** | Only owner-local read-only `git status` and `git worktree` when separately needed; never clean/reset/pull over changes; future isolated worktree plan |
| **G12 — Dated docs and stale execution headers** | Current README still contains historical early Phase4 pending statements; old FE `docs/auth/sso-architecture-roadmap.md` refers to `sso.skill-wanderer.com`/legacy `lms-reltroner`, incompatible with current frozen contract. Living ledger supersedes historical status **only**, not frozen norm (source/README). | **DISCOVERY_CLASSIFIED / HISTORICAL_DRIFT; GOVERNANCE_REMEDY_PROPOSED** | This PR adds latest README E30 overlay, mandatory clarity-first handoff and append-only ledger/work-order entry; retain archival docs, no silent destructive rewrite |
| **G13 — Admin frontend independence** | FE main has `src/app/admin/page.tsx` behind a **client-side UX role gate**, but no independent `lms-admin.reltroner.com` Pages project was reported, DNS fails and Keycloak lms-admin client missing (FE source E20/E24/E26). **Admin screen != independent admin app/API authorization boundary.** | **DISCOVERY_CLASSIFIED / ADMIN_UX_PRESENT; INDEPENDENT_ADMIN_HOST_NOT_PROVISIONED** | Approved separate Pages admin build/domain/PKCE client plus server-side admin capability denial; do not promote learner `/admin` as proof |

### 25.3 Readiness accounting, critical path and no-premature-closure

**All thirteen gap IDs now have a deterministic evidence-based triage (13/13 DISCOVERY_TRIAGED). Zero new implementation remediations, migrations, configurations, tests or production releases were performed (0/13 IMPLEMENTATION_CLOSED_BY_E30).** The seven scoped PASS / ten partial-or-gap / one owner-pending **E29 AC01–AC18** final audit classification is **unchanged**. `AC18` owner sign-off is explicitly **NOT implied** by this instruction to "finish discovery" or by merging a docs PR. Some details remain `ACCESS_BLOCKED` or `UNVERIFIED` despite classification; the inability to observe them is exactly the residual risk, not a claim of FULL_DISCOVERY_TECHNICAL_PROOF.

**Critical path dependencies (conceptual, not execution approval):**

`Owner review + 4A closure acceptance (AC18)`
→ `P4B scope, resource budget, source SHAs, no-spend constraints and nonproduction boundary`
→ `G09 identity + G03 workload trust`
→ `G04 DB owners + G05 Redis replay + G01 provider/API implementations`
→ `G13 independent admin + G08 DNS/strict origin review + G02 FE config + G07 pinned release`
→ `G10 isolated DR/event tests and G06 HRM coexistence/peak capacity validation`
→ `separate production release gate`.

Dependencies can be designed in parallel; **none** is implicitly authorized by an arrow. **G11** local dirty files must be preserved before any local source synchronization; **G12** documentation/handoff is the only permitted modification in this PR.

**Deterministic next owner decisions:**
1. Review the updated **docs-only PR #39** (three files, no app/runtime edits) and decide its documentation merge independently of phase acceptance.
2. Explicitly accept or reject the **Phase4A discovery handoff with open G01–G13 implementation/verification residues** (AC18). An accepted discovery handoff does **not** upgrade partially met gates to PASS.
3. Only after separately authorizing a **new Phase4B design/work-order scope** may coding agents change BE/FE, privileged operators provision Keycloak/PG/Redis, or human GUI actions create Pages/DNS/asset origins; production release requires another authorization.

**No-mutation and security stop:** Do not create routes, identities, databases, Redis keys, new hostnames, admin projects, DNS/TLS policies, buy daily backups, execute backup/restore, change HRM/Keycloak, merge source apps, update local dirty FE, or change frozen architecture under Phase4A. This E30 only adds reviewable documentation and read-only source facts.

**E30 checkpoint:** `PHASE4A_E29_FINAL_AUDIT_CANDIDATE -> G01-G13_13/13_DISCOVERY_TRIAGED -> GAPS_REMAIN_IMPLEMENTATION_OPEN -> AC18_OWNER_PENDING -> PHASE4B_NOT_AUTHORIZED -> PRODUCTION_NOT_AUTHORIZED`.
