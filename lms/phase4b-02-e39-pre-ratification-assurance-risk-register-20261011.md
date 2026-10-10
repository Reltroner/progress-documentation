# LMS Phase 4B-02 E39 — Pre-ratification Assurance and Residual-Risk Register

> **ID:** `LMS-P4B02-E39-ASSURANCE-20261011`  
> **Status:** **DESIGN RED-TEAM CROSS-CHECK COMPLETE / RATIFICATION GATE NOT SATISFIED**. The phase is design-only; no PHP source, Redis, Keycloak, Cloudflare, PostgreSQL, HRM or production mutation.  
> **Observed BE main:** `617dadc0d0d627071d713ceb729df6658202b43e`. **Docs branch:** `docs/lms-phase4b02-trust-design-acceptance-20261011`, child of docs main `183372371b3a40a0349ac390848911273ccd2361`. Verify fresh HEAD before any subsequent work.  
> **Inputs:** E37 design work order, 86-case matrix, owner-supplied Gemini E38 review/reconciliation and E38 independent errata register. Preserve frozen Phase0C/Phase1 and ratified **nonproduction design-only** ADR-LMS-TRUST-001.  
> **Important honesty boundary:** Neither an LLM nor a design document can guarantee **zero risk, zero technical debt or exhaustive absence of missing requirements**. The evidence-supported goal is **zero *known unaddressed in-scope design contradictions* at a versioned design freeze**, which requires explicit closure proof per item and independent runtime gates. That condition is **NOT yet met**.

## 1. E39 executive assurance verdict

- **E38 corrections F01–F07:** accepted as external report errata and independently reconciled: frozen public API **`https://lms-api.reltroner.com`**, precisely four DBs `lms_learning_db`, `lms_mentorship_db`, `lms_knowledge_db`, `lms_audit_db`, zero BE repo modification **reported** (IDE scratch files created), Ed25519 workload vs effective OIDC alg separate, >=65s quarantine only after verified recovery, per-stage bounded authorized DB reads, and no fictional header/epoch owner ratification.
- **E39 high-risk additions:** signed proofs lack an owner-approved **method/path/query/body request binding**, no final anti-mix-and-match relationship between two JWS roles, selective Redis nonce loss detection not proven, multi-worker quarantine not proven, real OIDC token evidence absent, domain owner mapping and true HTTP tests not executed.
- **Current outcome:** `P4B02_DESIGN_RATIFICATION=HOLD`; `0/86` real T02 acceptance tests executed; all `D02-01..05` still owner decision candidates, and D02-02/D02-05 additionally blocked by **technical evidence**. A human accepting a design proposal must not be mistaken for proving Redis safety.
- **Docs defect treatment:** Do not delete or silently relabel existing T02 IDs; attach E39 interpretive errata and propose explicit future tests while keeping **86 canonical draft IDs** and **zero runtime PASS**. No new public operation or database.

## 2. Risk overview (16 numbered findings)

| ID | Severity | What is not yet proved / specified | Dependency | Evidence status |
|---|---|---|---|---|
| `E39-R01` | HIGH | Request-to-proof cryptographic binding | D02-01 | `OPEN_DESIGN_DECISION` |
| `E39-R02` | HIGH | Cross-token mix-and-match and header provenance | D02-01 | `OPEN_DESIGN_DECISION` |
| `E39-R03` | HIGH | Two roles do not imply independent compromise resistance | D02-01/D02-04 | `OPEN_THREAT_MODEL` |
| `E39-R04` | CRITICAL | Silent replay key loss while Redis PING remains healthy | D02-02 | `BLOCKED_TECHNICAL_PROOF` |
| `E39-R05` | HIGH | Multi-worker quarantine and trusted time source | D02-02 | `OPEN_DESIGN_DECISION` |
| `E39-R06` | HIGH | Redis nonce namespaces and dual reservation integrity | D02-01/D02-02 | `OPEN_TEST_PROOF` |
| `E39-R07` | HIGH | Business idempotency is not cryptographic replay protection | D02-03 | `OPEN_DOMAIN_DEPENDENCY` |
| `E39-R08` | HIGH | JWT/JWKS policy not observed in Keycloak | D02-05 | `BLOCKED_EVIDENCE` |
| `E39-R09` | HIGH | Capability/subject ownership mapping not grounded in a live owner model | D02-01/D02-05 | `OPEN_MODEL` |
| `E39-R10` | MEDIUM | HTTP deny classification and compatibility not finalized | D02-03 | `OPEN_COMPATIBILITY` |
| `E39-R11` | HIGH | Security acceptance based on only synthetic/local tests | B02-D09/D10/D12 | `NOT_RUN` |
| `E39-R12` | MEDIUM | Security key lifecycle and JWS parser attack surface | D02-01/D02-04 | `OPEN_DESIGN_DECISION` |
| `E39-R13` | HIGH | Private network/edge trust assumptions unverified | B02-D08/D11 | `NOT_RUN` |
| `E39-R14` | MEDIUM | Test matrix verdict ambiguity | B02-D09/D10 | `DOC_FIX_CAN_BE_APPLIED` |
| `E39-R15` | HIGH | Test and runtime provenance gap after squash merge | B02-D01/D12 | `OPEN_RUNTIME_PROOF` |
| `E39-R16` | MEDIUM | Negative assertion side-effects stage unclear | B02-D10 | `DOC_FIX_CAN_BE_APPLIED` |

## 3. Full deterministic remediation and closure evidence per item

### E39-R01 — Request-to-proof cryptographic binding

**Risk/observed design gap:** Frozen policy binds operation_id/request_id, but not canonical method, target path, query/body or content digest end-to-end; a valid proof might be detached from the specific private HTTP message.

**Required safe remediation / evidence to close:** Design and owner-ratify canonical request-target + signed payload hash or equivalent tamper-proof binding, with proxy normalization, GET query and write JSON body coverage; test mutation after signing.

**Linked decision/gate:** `D02-01` · **Current:** `OPEN_DESIGN_DECISION`.

### E39-R02 — Cross-token mix-and-match and header provenance

**Risk/observed design gap:** Two independently verifiable JWS without explicit relationship can be paired incorrectly; X-Request-ID may originate from an untrusted client.

**Required safe remediation / evidence to close:** Independent role-scoped JWS, workload/delegation key roles, fresh gateway-controlled correlation/binding and cryptographic linkage to the actual workload proof; reject user-supplied asserted principal headers.

**Linked decision/gate:** `D02-01` · **Current:** `OPEN_DESIGN_DECISION`.

### E39-R03 — Two roles do not imply independent compromise resistance

**Risk/observed design gap:** Both proofs being signed by a single compromised Gateway key does not establish two independent security principals; role separation without custody separation may be weak.

**Required safe remediation / evidence to close:** Write threat model distinguishing independently validated logical controls vs independently controlled signer identities; pin per-role/per-caller allowed signer keys or explicitly document trust-root limit and key compromise response.

**Linked decision/gate:** `D02-01/D02-04` · **Current:** `OPEN_THREAT_MODEL`.

### E39-R04 — Silent replay key loss while Redis PING remains healthy

**Risk/observed design gap:** Redis-only epoch marker, PING, process-local timer, or persistent marker without selective-deletion detection cannot reliably prove consumed nonce integrity.

**Required safe remediation / evidence to close:** Prove independent loss/epoch evidence for restart, failover, flush, selective eviction, process restart and network split; otherwise deny all protected requests or submit explicit revised ADR. A design approval alone cannot pass this gate.

**Linked decision/gate:** `D02-02` · **Current:** `BLOCKED_TECHNICAL_PROOF`.

### E39-R05 — Multi-worker quarantine and trusted time source

**Risk/observed design gap:** One process clock/quarantine state may disagree with another worker; host wall-clock jumps, restart and delayed detection may defeat assumed 65s lifetime.

**Required safe remediation / evidence to close:** Design shared trusted recovery gate, maximum clock error, monotonic time measurement, restart-safe quarantining, per-process mandatory cold-deny and transition tests; 65s only after verified recovery.

**Linked decision/gate:** `D02-02` · **Current:** `OPEN_DESIGN_DECISION`.

### E39-R06 — Redis nonce namespaces and dual reservation integrity

**Risk/observed design gap:** Both assertions may collide in same key identity namespace; two independent SET NX PX writes are not a single transaction, and ambiguous partial success can tempt auto-retry.

**Required safe remediation / evidence to close:** Proof-type domain-separated replay keys, typed collision handling, strict deny on any partial/indeterminate reservation, and real parallel-worker fault injection; never process a handler before both authoritative reservations.

**Linked decision/gate:** `D02-01/D02-02` · **Current:** `OPEN_TEST_PROOF`.

### E39-R07 — Business idempotency is not cryptographic replay protection

**Risk/observed design gap:** A burned nonce after 503 cannot simply be retried; a replacement signed proof can still duplicate a business command unless durable idempotency is separately applied.

**Required safe remediation / evidence to close:** Specify client retry policy, explicit no-reuse of expired/jti, domain idempotency keys with owner-scoped durable PostgreSQL and outbox behavior for mutating operations; no cross-owner writes or new DB by assumption.

**Linked decision/gate:** `D02-03` · **Current:** `OPEN_DOMAIN_DEPENDENCY`.

### E39-R08 — JWT/JWKS policy not observed in Keycloak

**Risk/observed design gap:** Contract retains a blocking OIDC alg sentinel; JWKS kty alone does not conclusively identify every effectively issued JWT/client authorization profile.

**Required safe remediation / evidence to close:** Read-only non-sensitive discovery of effective issuer, signed access-token protected alg/kid and relevant client/audience/capability mapper configuration under owner-approved scope, then independent strict alg allowlist review; no raw tokens in logs.

**Linked decision/gate:** `D02-05` · **Current:** `BLOCKED_EVIDENCE`.

### E39-R09 — Capability/subject ownership mapping not grounded in a live owner model

**Risk/observed design gap:** Signed principal_sub alone is not a safe direct database numeric user_id; capability source must be exact client-role namespace, and resource ownership may require scoped DB reads.

**Required safe remediation / evidence to close:** Define stable verified principal identity mapping, resource-owner DB query join/tenant scope, and strict capability intersection; test cross-owner/cross-client with actual isolated fixture data. No direct client-header identity.

**Linked decision/gate:** `D02-01/D02-05` · **Current:** `OPEN_MODEL`.

### E39-R10 — HTTP deny classification and compatibility not finalized

**Risk/observed design gap:** A missing endpoint 404 is invalid trust evidence; 401 vs 403 vs dependency 503 plus safe Problem Details must not contradict the frozen response contract.

**Required safe remediation / evidence to close:** Approve error/status and stable machine code contract before route wiring, prove protected route middleware executed and denies have no unauthorized reads, writes, outbox, or data disclosure.

**Linked decision/gate:** `D02-03` · **Current:** `OPEN_COMPATIBILITY`.

### E39-R11 — Security acceptance based on only synthetic/local tests

**Risk/observed design gap:** G03 287/0 and 7/7 CI validate source contracts but no real two-signature HTTP, concurrent Redis failures, Keycloak audience/JWKS or provider handler boundary.

**Required safe remediation / evidence to close:** Execute real isolated provider route and fault injection; pin SHA/key-fingerprint, actual status, handler and outbox counters; 404 never counts as auth rejection. Separate main CI proof.

**Linked decision/gate:** `B02-D09/D10/D12` · **Current:** `NOT_RUN`.

### E39-R12 — Security key lifecycle and JWS parser attack surface

**Risk/observed design gap:** Design does not yet fully accept malformed critical headers, inline jwk/x5c, oversized duplicated HTTP headers, typ substitution, key reuse, rotation/revocation and secret leakage paths.

**Required safe remediation / evidence to close:** Approve signer/verifier library and strict JWS serialization/parser policy, max header/body bounds, fail-closed key resolution, test key lifecycle and secret hygiene; no private key in Git.

**Linked decision/gate:** `D02-01/D02-04` · **Current:** `OPEN_DESIGN_DECISION`.

### E39-R13 — Private network/edge trust assumptions unverified

**Risk/observed design gap:** Removing CORS on providers is not network isolation; IPv6, proxy headers, internal port binding, nginx path forwarding and service SSRF still need independent checks.

**Required safe remediation / evidence to close:** Future isolation test proving only Gateway publicly exposed and internal egress/request allowlists; no DNS/VPS/firewall changes within design work order.

**Linked decision/gate:** `B02-D08/D11` · **Current:** `NOT_RUN`.

### E39-R14 — Test matrix verdict ambiguity

**Risk/observed design gap:** T02-017/031/045/063/077 are component-level ALLOW examples, not sufficient whole HTTP ALLOW, while T02-047 expects one concurrency winner/one loser not blanket DENY_AUTHN.

**Required safe remediation / evidence to close:** Append binding interpretation errata to existing 86 stable test IDs and add machine-readable expected outcomes only after owner acceptance; do not count whole HTTP PASS from a single stage.

**Linked decision/gate:** `B02-D09/D10` · **Current:** `DOC_FIX_CAN_BE_APPLIED`.

### E39-R15 — Test and runtime provenance gap after squash merge

**Risk/observed design gap:** Gemini reviewed old clean HEAD 598440f whereas BE current main is 617dadc; contents of four edited blobs matched, but a feature local worktree is not main SHA and cannot certify code execution.

**Required safe remediation / evidence to close:** Require exact new BE main for future isolated worktree and independent runtime and CI SHA verification; preserve FE three dirty entries and existing worktrees.

**Linked decision/gate:** `B02-D01/D12` · **Current:** `OPEN_RUNTIME_PROOF`.

### E39-R16 — Negative assertion side-effects stage unclear

**Risk/observed design gap:** Earlier Gemini said every denial must imply zero DB reads, which is impossible for certain scoped owner checks; early signature failure should never reach business DB.

**Required safe remediation / evidence to close:** Instrument per-stage permissible bounded authz lookup vs unauthorized access; require zero business write/outbox and no sensitive leak on denied calls; no premature controller invocation.

**Linked decision/gate:** `B02-D10` · **Current:** `DOC_FIX_CAN_BE_APPLIED`.


## 4. Falsifiable design signoff gate, not subjective confidence

**Definition of reviewable candidate:** All E38 material discrepancies corrected in documents; every E39-`R01..R16` has a deliberate resolution: `DESIGN_APPROVED_WITH_SCOPE`, `IMPLEMENTATION_TEST_REQUIRED`, or `BLOCKS_IMPLEMENTATION`, with concrete acceptance proof and owner. No item may become `CLOSED` solely because an AI said “safe”. Documents can archive a **design candidate** with explicit blockers; they cannot convert missing Redis-loss or OIDC evidence to PASS.

**Definition of design ratification:** Owner signs off exact SHA of chosen on-wire proof encoding and signer/verification boundaries, replay safety/threat model and recoverability, Problem Details mapping, isolated zero-cost nonprod key custody, and OIDC observation plan. This approves **design choices**, NOT their successful implementation.

**Definition of nonproduction runtime acceptance (later, not part of this gate):** All applicable T02 cases and any newly owner-adopted cases run in isolated true HTTP system; actual signatures/headers/verified owner mapping + concurrent nonces + loss/failover + recovery verified, zero unauthorized effects, pass exact SHA CI and independent human review. Deny by default while any safety dependency unproven.

**No guarantee of no rollback:** At source stage use isolated SHA-pinned feature PRs, CI/negative tests and explicit owner merge gate. Deployment, migrations, cross-service swaps and actual rollback require separately authorized execution plan and evidence. No destructive Git reset/clean or touching older FE dirty checkout.

## 5. Test-case coverage addition candidates (NOT part of original 86)

Maintain `T02-001..T02-086` **unchanged** and `0/86` executed. Four Gemini proposals `T02-087..T02-090` (foreign realm, inline JWS `jwk/x5c`, truncated request/media type, backward clock jump) remain **PROPOSED**. The E39 gap-to-test additions below are **suggestions**, not owner-adopted T02 identifiers until versioned approval:

| Candidate ID | Stimulus to add if owner accepts | Required result / proof |
|---|---|---|
| `T02-091` | Tamper HTTP method/path/route parameters after token signing | Deny, zero unauthorized data/side effects |
| `T02-092` | Tamper canonical query or JSON body after signing, use same operation ID | Deny unless signed request digest matches actual bytes/approved canonical representation |
| `T02-093` | Mix two independently valid JWS from different Gateway requests sharing client-supplied X-Request-ID | Deny cross-proof substitution; trusted freshness and binding cannot rely on user header alone |
| `T02-094` | Swap JWS type or key role with otherwise valid signature | Deny role confusion; pin allowed key role |
| `T02-095` | Send duplicate/oversized assertion headers and unsupported critical JWS headers | Deny safely with bounded CPU/memory |
| `T02-096` | Selectively evict/flush a used jti while Redis remains reachable and PING healthy | Deny until independently proven replay-safe, or BLOCKED_TECHNICAL_PROOF |
| `T02-097` | Restart multiple provider workers with inconsistent recovery/epoch knowledge | All workers deny until shared recovery gate proven |
| `T02-098` | Reuse same jti value across workload/delegation proof namespaces | Deny collision or prove typed key separation without privilege confusion |
| `T02-099` | JWKS key rotation and malicious same-kid key replacement | Deny untrusted key transition; secure owner-approved OIDC rotation |
| `T02-100` | Valid realm role that is not approved `lms-api` capability | Deny; no realm-role shortcut |
| `T02-101` | Authenticated user maps to unrelated owner/tenant DB principal | Deny unauthorised records despite valid sub |
| `T02-102` | Retry a side-effecting operation after burned replay nonce with a new valid proof | Preserve domain idempotency; no duplicate durable business result |
| `T02-103` | Jump wall clock forward/back while monotonic recovery timer and multiple workers running | Continue deny or fail closed, no early quarantine exit |
| `T02-104` | Malicious forwarded Host/proxy/request target to alter recipient or route selection | Deny wrong target; Gateway/private ingress and signed target remain consistent |

**Proposed number if all adopted:** `86 + 4 + 14 = 104` cases. **No new case has been added to the canonical 86-case test matrix in E39**; its status remains `86_DRAFTED / 0_EXECUTED`.

## 6. Decisions and stop

| D02 decision | E39 review direction | Current authoritative status |
|---|---|---|
| `D02-01` | Candidate two strongly role-separated JWS with independently verified proofs, strict key scopes, signed exact operation+HTTP request binding and proof-mix rejection | **PENDING_OWNER_WIRE_RATIFICATION** |
| `D02-02` | Demonstrate independent loss detector for selective eviction/restart/failover; coordinated fail-closed multiworker >=65s verified-recovery quarantine; or owner review ADR alternative | **BLOCKED_TECHNICAL_PROOF** |
| `D02-03` | Proposed sanitized 503 safety dependency error + 401/403 context, compatible with frozen OpenAPI and no unsafe retry | **PENDING_OWNER_CONTRACT_APPROVAL** |
| `D02-04` | Local only / zero unapproved spend, ephemeral nonprod test-only keys, separated role keys and fake Redis fault adapter; real isolated Redis tests need distinct owner approval | **PENDING_OWNER_ENV_APPROVAL** |
| `D02-05` | Observed signed Keycloak JWT/JWKS/issuer/aud/azp & mapper evidence under owner-approved read-only access; pin strict alg/rotation policy independently of workload Ed25519 | **BLOCKED_EFFECTIVE_ALG_EVIDENCE** |

**Do not ratify 4B-02 as completed, merge a runtime coding PR, issue keys, or deploy.** If source documents are merged for archival they remain `DESIGN_PACKAGE_PREPARED_WITH_BLOCKERS`, and owner decision ratification must be a separately scoped, explicitly approved versioned action.

**Checkpoint:** `P4B01_G03_MERGED -> P4B02_E37_DESIGN_DRAFT -> E38_INDEPENDENT_ERRATA -> E39_RISK_REGISTER_16_OPEN_OR_TEST_REQUIRED -> D02_01..05_NOT_RATIFIED -> REAL_HTTP_0_OF_86 -> SOURCE_RUNTIME_NOT_AUTHORIZED -> PRODUCTION_NOT_AUTHORIZED`.
