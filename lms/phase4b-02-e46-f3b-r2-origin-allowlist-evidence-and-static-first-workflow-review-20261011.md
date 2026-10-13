# Reltroner LMS Phase 4B-02 — E46-F3B-R2 Sandbox Allowlist Screenshot and First Workflow Static Candidate

> **Document ID:** `LMS-P4B02-E46-F3B-R2-20261011`  
> **Status:** `ACTIONS_OWNER_ONLY_RADIO_AND_SHA_ON=VISIBLE`; `ACTIONS_PERMISSION_SAVE=PENDING_RELOAD_CONFIRMATION`; `CANDIDATE_WORKFLOW=OFFLINE_STATIC_CHECK_PASS_NOT_RUNTIME_TESTED`; `FIRST_DEFAULT_BRANCH_COMMIT=NOT_AUTHORIZED`; `FIRST_MANUAL_RUN=NOT_AUTHORIZED`.  
> **Hierarchy:** [canonical README §7](./README.md), [master infrastructure placement contract](./master-infrastructure-placement-contract.md), [logical service boundary API contract](./logical-service-boundary-api-contract.md), [E46-F3B security/budget/OCI evidence](./phase4b-02-e46-f3b-owner-actions-zero-budget-security-review-and-oci-preflight-20261011.md).  
> **Non-goal:** This file MUST NOT be moved to `.github/workflows` or executed absent two independent approvals. No production / LMS-BE / LMS-FE / VPS mutation.

## 1. Most recent owner screenshot: what is actually established

Source screenshot `github.com/Reltroner/lms-trust-sandbox/settings/actions`:
- Selected radio **Allow Reltroner actions and reusable workflows**.
- Checkbox **Require actions to be pinned to a full-length commit SHA** checked.
- Retention remains **90 days**.
- Top GitHub success banner reads **Default workflow permissions settings saved.** That banner identifies a **DIFFERENT settings subsection**, not the Actions permissions Save button.
- Therefore screenshot proves the **desired Actions control values are DISPLAYED together**, but does **NOT** independently prove the radio/check box changes persisted after reloading the page. Do not classify the action-origin policy as PERSISTED/CONFIRMED yet. Earlier screenshot independently displayed `Actions policy updated.` with SHA enabled but Allow all selected.
- Operator final read-only verification required: press browser refresh `Ctrl+R` while on the **sandbox**, NOT LMS-BE, then capture the top Actions permissions showing **Reltroner-only selected + SHA checked**. If radio reverts after refresh, select it again, click the **Actions permissions section Save** directly beneath SHA, refresh again, and inspect. No other settings or budgets should be changed.
- Retain Actions Account budget `$0 / Stop usage Yes`; no claim of free-all-services guarantee. There is no first sandbox Git commit or Actions run on latest connected GitHub inspection.

## 2. Single-job zero-external-action first workflow architecture (candidate only)

**Candidate image references from 2026-10-11 owner Windows public registry manifest proof:**
- Job and PostgreSQL service: `docker.io/library/postgres@sha256:74935e72241653ca55e0414067e6d8763aceb8a810eb51b452253ec3dcfc4336` (owner-validated `linux/amd64` child `sha256:885953109528ad3dfc90362b1a6f50a78620b5315be19f187753d267e484dc5b`).
- Redis service: `docker.io/library/redis@sha256:2c2dff791878316e3b083188be0d578423b24813cdda5de0e80ea4f7b3e6bfd6` (child `sha256:6e9101032a2126aeeb4b1e862ac77d2fcf26b831ae37e5ff2e69169f82ddd411`).
- Third initially verified `ubuntu@sha256:534baea6a22c03a63003dbc8dbe78fe34bc0d7e595d9a9dc9834884ff530eb55` remains an **unused candidate**. Reusing PostgreSQL's digest as both job and service reduces image selection and gives a `psql` CLI candidate. No unconditional claim that GitHub Actions can run every required Bash primitive in this image without runtime inspection.

**No extra package installation** in candidate. A small native Bash RESP client uses the PostgreSQL job image's proposed Bash `/dev/tcp/redis/6379` stream rather than assuming Redis client is preinstalled. Because RESP source needs careful framing, bounded socket read timeouts, version parsing and no plaintext logging, both the Bash implementation and job image must pass source review before default-branch bootstrap; Bash's `/dev/tcp` connect timeout remains a known risk bounded by GitHub job `timeout-minutes: 10`. No access to owner Windows Docker or production.

**YAML candidate invariant summary:**
- Trigger exactly `workflow_dispatch`; `permissions: {}`; `concurrency` fixed to prevent concurrent runs; no auto-cancel, PR/push/schedule, marketplace `uses`, artifacts, cache, package publication, production secrets, GitHub environment or paid larger runner.
- Single job on standard GitHub hosted `ubuntu-24.04` (public repo), `timeout-minutes: 10`, image `postgres@sha256:...`, `--cpus=1 --memory=2048m` candidate job bounds.
- `services.postgres` PostgreSQL18 pinned digest and `services.redis` Redis8 pinned digest, with `--cpus`/memory limits and explicit health checks. Do **not** define `ports:`; job and services communicate only over Github's per-job internal Docker network, by the `postgres` and `redis` service names. No public DB host port.
- Synthetic-only PostgreSQL user/database/password (intentionally not production-like) and no GitHub production `.env`, SSH, OIDC deployment credential or external endpoint.
- First trial only PG-R01 / R02 / R03; more advanced restart/WAL/standby/load/owner DB grants gates need separate topology, scope and owner approval.
- Actual server version checks: SQL `server_version_num` must be 18.x, Redis `INFO server redis_version` must be major 8. Incorrect/missing versions cause hard STOP.

## 3. First test semantics and hard exit criteria (NOT executed)

| Gate | Real test stimulus | Required evidence | Scope caveat |
|---|---|---|---|
| PG-R01 | Two independent `psql` client processes concurrently attempt same `PRIMARY KEY` SQL claim | Exactly one `RETURNING` winner, other 0 rows, DB count 1 | SQL durable uniqueness only; no API/JWS on-wire integration |
| PG-R02 | One PostgreSQL transaction reserves workload+delegated nonces; second conflicts with pre-existing claim | Failed transaction, first nonce absent after rollback, existing remains; valid two-proof txn reserves both | SQL atomicity only |
| PG-R03 | Real disposable Redis8 `SET` then `FLUSHDB`, while PostgreSQL already recorded nonce | Redis key gone, SQL claim retained, second SQL claim cannot be inserted | Proof SQL-as-authority can reject after cache loss in this *synthetic lab*, not that LMS replay middleware does so |

**Hard safety boundaries:** Redis `FLUSHDB` is only valid inside the disposable Github Actions **service** container. Never run this against any real/shared/production Redis. SQL schema `lab_nonce_claims` is disposable. Fail if any fixture table is already populated, DB hostname/user/database differs from expected synthetic namespace, container versions differ, health fails, job exceeds timeout, a duplicate is accepted or any expected error logs sensitive credentials. **Not a proof of PG-R04..10, not T02-001..086, not Keycloak effective JWT issuer/JWKS, and not a production release.**

## 4. Offline candidate artifacts prepared in assistant scratch session

**Candidate source files prepared but NOT uploaded to the sandbox, docs branch, or runner:**

| Artifact | SHA256 of local UTF-8 bytes | Offline assessment |
|---|---|---|
| `candidate.yml` | `88516d1925c4b03286c27d90dfd124268dcc237395cf0a6bc958b963e55dd5e2` | PyYAML BaseLoader parse PASS; manual-only trigger, no `uses`, one job, 10-min limit, pinned image refs, no `ports:` by structural checks |
| `initial-lab.sh` | `79992c8dc5c06e8a4c93c805fb80d257d48156cd3696627c8ad5e9a27e88ba3f` | `bash -n` PASS only, 93 lines; **not** executed |
| `README-REVIEW-ONLY.md` | `63b680a277ddd7e926c2a26a058ece84c66bcb5b72874e17e8ea779a3c82a146` | security scope and authorization disclaimer |

The independent static checks are **not** GitHub Actions syntax/execution conformance, ShellCheck validation or runtime behavior. Source artifacts remain a **chat-provided review bundle**, not persistent Git repository source; another AI must obtain that bundle before claiming exact source auditing or authorizing bootstrap. No digests for these user-visible files imply they were already committed. No action upload or image layer download was made by the assistant during the offline checks.

## 5. Deterministic next gates and evidence status

**F3-B-A policy persistency:** owner refreshes the `lms-trust-sandbox` Actions General page, sends screenshot showing origin Reltroner-only and full SHA ON. If still Reltroner-only and SHA after reload, mark `PASS_OWNER_GUI_POST_REFRESH`; otherwise Save correct subsection and retry. Never touch LMS-BE settings to accomplish this.

**F3-B-B static source review:** independent human/agent reads local ZIP/candidate code, verifies SHA256, GitHub YAML permissions/trigger/service network and package assumptions; run `bash -n` and YAML parse locally; verify image digests still resolve to the approved linux/amd64 images; inspect Bash RESP and SQL idempotency/rollback semantics. These are preflight proofs, not container/runtime PASS.

**F3-B-C first default-branch bootstrap:** **NOT AUTHORIZED**. Only after complete reviewed exact workflow source and explicit owner `ALLOW_FIRST_SANDBOX_WORKFLOW_COMMIT` shall bootstrap create first `main` commit. A workflow on default branch becomes dispatchable, so a design file is never silently copied into `.github/workflows`.

**F3-C first manual workflow run:** **NOT AUTHORIZED**, and must never be inferred from F3-B-C approval. Requires explicit `ALLOW_FIRST_REAL_PG18_REDIS8_CI_RUN` owner approval after verifying review/source policy, $0 stop-usage budget and runtime topology. Do not override $0 spending limits if runner is blocked.

**Snapshot:** F3-A PASS; F3-B digest metadata proof owner PASS 3/3; origin+SHA radio screen both visible but persistence pending browser refresh; Bash/YAML candidate static checks PASS; OCI signatures/client/job runtime NOT TESTED; F3-B commit HOLD; F3-C run HOLD; PG-R=0/10; T02=0/86; D02 owner ratification HOLD; no production changes.


## 6. F3B-R3 post-refresh screenshot superseding source policy gate (2026-10-11)

**Supersedes R2's persistence uncertainty:** owner explicitly pressed `Ctrl + R` and supplied another screenshot of the sandbox Actions General page; `Allow Reltroner actions and reusable workflows` radio and **full-length SHA** checkbox still selected. **`ACTION_ORIGIN_POLICY=PASS_OWNER_GUI_POST_REFRESH`** (not directly fetched settings API), with 90-day retention unchanged. No additional Actions GUI edits are needed. The assistant also reopened R2 review ZIP, validated all SHA256SUMS, Bash syntax and YAML structure, then found R2 static semantics gaps; a new **R3 offline candidate bundle** addresses 23505 unique-violation proof, Redis fresh keyspace + NX/PX TTL preconditions and PG-R01 claim precision. [Complete F3B-R3 handoff and candidate SHA evidence](./phase4b-02-e46-f3b-r3-postrefresh-policy-and-remediated-workflow-source-audit-20261011.md). Neither old nor new candidate was committed to sandbox; 0 branches, 0 runs, 0 real PG-R and HTTP T02. Work remains on runtime/image/shell security review before separate first-commit and first-run owner approval.
