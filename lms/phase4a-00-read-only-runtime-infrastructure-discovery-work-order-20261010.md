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
| P4A00-AC07 | Nginx/PHP-FPM/service unit and ports/socket/public/private routing matrix | **PARTIAL_OPERATOR** E13: bind addresses observed, process ownership/Nginx/FPM/private routing missing |
| P4A00-AC08 | Keycloak effective issuer/JWKS/client/audience and HRM nonregression baseline | **PENDING_RUNTIME** |
| P4A00-AC09 | Four PostgreSQL DB/role/grant existence vs intended owned state | **PENDING_RUNTIME** |
| P4A00-AC10 | Redis topology, memory/keyspace/replay posture with no secret exposure | **PARTIAL_OPERATOR** E13: redis-server binary 8.2.10/loopback 6379; actual server version, keyspace, memory/replay unobserved |
| P4A00-AC11 | Cloudflare Pages real Production/main skipped state at eb01a4d2 + active deployment SHA | **PENDING_RUNTIME** (old Preview only E10) |
| P4A00-AC12 | External vantage-point DNS/TLS for exact approved hostnames | **TOOL_UNAVAILABLE** E11, operator read-only pending |
| P4A00-AC13 | Hosting asset origin, immutable URL/capacity and CDN status | **PENDING_RUNTIME** |
| P4A00-AC14 | HRM coexistence capacity + backup/monitoring/recovery metadata | **PARTIAL_OPERATOR** E13: aggregate host capacity read; HRM/Keycloak process budgets/backups/recovery metadata still pending |
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
| P4A-G04 | Four DB roles/databases/grants unverified (PENDING_RUNTIME) | Ownership and cross-write constraints cannot be certified | DB implementation/grants plan, migration/rollback and permission-negative tests after read-only inventory |
| P4A-G05 | Redis replay state and reset detection unverified (PENDING_RUNTIME) | Replay-fail-open hazard; explicit >=65s quarantine/fault injection deferred | Separate reviewed runtime safety implementation and nonproduction fault simulation before production |
| P4A-G06 | VPS service isolation/capacity unknown (PENDING_RUNTIME) | Shared Keycloak/HRM resource contention on historical small VPS | Measured memory/CPU/disk/worker/socket budget and no extra infrastructure purchase by assumption |
| P4A-G07 | Cloudflare Production/main new merge skip unverified (PENDING_RUNTIME) | Unintended build/release confusion, potential live pages mismatch | Read-only UI receipt; production Pages changes require independent release approval |
| P4A-G08 | External DNS/TLS/Pages/admin and asset origin unverified (TOOL_UNAVAILABLE) | Ingress/public/private separation and origin certificate checks pending | Explicit topology and user-accepted HTTP negative/positive test plan after evidence |
| P4A-G09 | Source OIDC/API capability/auth contract not runtime-integrated (DEFERRED_PHASE4+) | Keycloak/HRM regressions and privilege escalation must be prevented | Per-client admin/user token tests in isolated later sandbox; do not fetch live tokens in Phase 4A-00 |
| P4A-G10 | Backup/restore, outbox correctness and observability uncertified (PENDING_RUNTIME) | Cannot guarantee durability or deploy rollback | Metadata inventory now; destructive recovery/restore drills only with isolated environment and new authorization |
| P4A-G11 | Local primary FE old HEAD/3 changes (OPERATOR_OBSERVED) | Risk of wiping unfinished work on forced reset/pull | Owner inventory and preservation before a separately authorized local fast-forward, stash or worktree change |
| P4A-G12 | Docs/contract chronologically stale source headers (HISTORICAL) | AI confusion if using old dated text as current authority | Always canonical README -> newest ledger -> frozen contract; do not retroactively rewrite frozen snapshots |

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
