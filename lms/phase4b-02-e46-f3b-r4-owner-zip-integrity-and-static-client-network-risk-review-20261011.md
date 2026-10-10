# Reltroner LMS Phase 4B-02 — E46-F3B-R4 Owner-Verified R3 ZIP + Independent Static CI/Network Risk Audit

> **Evidence record:** `LMS-P4B02-E46-F3B-R4-20261011`  
> **Status:** `R3_OWNER_WINDOWS_ZIP_SHA256=PASS`; `R3_INDEPENDENT_STATIC_AUDIT=PASS_SCOPED_WITH_GAPS`; `R4_INERT_REMEDIATED_CANDIDATE=CREATED_STATIC_PASS`; `FIRST_SANDBOX_WORKFLOW_COMMIT=NOT_AUTHORIZED`; `FIRST_MANUAL_RUN=NOT_AUTHORIZED`.  
> **Authority:** [LMS canonical README](./README.md); [master placement](./master-infrastructure-placement-contract.md); [logical service contract](./logical-service-boundary-api-contract.md); [R3 static source](./phase4b-02-e46-f3b-r3-postrefresh-policy-and-remediated-workflow-source-audit-20261011.md); [E46-F2/F3 policy and budget governance](./phase4b-02-e46-f2-owner-github-actions-policy-billing-evidence-and-manual-pg18-redis8-sandbox-contract-20261011.md).  
> **Mutation boundary:** DOCS PR #46 ONLY. Sandbox, LMS-BE, LMS-FE, HRM, Keycloak, Cloudflare, VPS, production and billing unchanged. No docker/image pull/runner/database operation.

## 1. Windows owner evidence and exact SHA

The owner ran the PowerShell 5.1 command against `$env:USERPROFILE\Downloads\LMS-E46-F3B-R3-remediated-review-only.zip` and pasted output:
```text
E46_F3B_R3_ZIP_INTEGRITY=PASS
REAL_DATABASE_TESTS=NOT_RUN
FIRST_WORKFLOW_COMMIT=NOT_AUTHORIZED
```
The script checks the archive against exact expected SHA256 `07e230b0764798734975d76ebb6d0f6364d2633ecdb8595ba0aad637d95cafc0`. This proves checksum equality on owner's downloaded ZIP at execution time only, not audit acceptance or authorization of its contents.

Independently, the assistant read the same mounted ZIP at `/mnt/data/LMS-E46-F3B-R3-remediated-review-only.zip`, verified archive SHA256 `07e230b0764798734975d76ebb6d0f6364d2633ecdb8595ba0aad637d95cafc0`, inspected four members and recomputed all three source hashes:
- `candidate.yml` `0e133699da2740eef7fffcff0adbe9ddf1705343853373a9db0b9595759bdb98`
- `initial-lab.sh` `404287a0f1b3202b49e687ec1c68f8396ee32e9bc832b965527e48bdefd0ee61`
- `README-REVIEW-ONLY.md` `df7e3328a939285aa646cf867a35f603e7a4972002c48c84ad2e8be96e8c15f5`
The recomputed hashes match `SHA256SUMS.txt`. `unzip -t`/read passed, `bash -n` PASS, PyYAML **BaseLoader** parsed `on.workflow_dispatch` and Bash inline script equals the standalone file after whitespace normalization. One job, `ubuntu-24.04`, 10-minute limit, `permissions: {}`, no external `uses:`, no service `ports:`, digest-pinned OCI image refs. This is structural parsing, **not** actionlint, ShellCheck, live engine proof, or security of all statements.

## 2. Security- and correctness-relevant R3 source findings

| Risk | Level | Exact R3 observation | R4 disposition |
|---|---|---|---|
| `R4-01` unbounded Redis socket *open* | P1 / runtime blocker | `exec 9<>/dev/tcp/redis/6379` has a five-second **read** timeout but no independent TCP connect timeout; the GitHub job's 10-minute limit is too coarse. | R4 candidate wraps the whole Redis session in `timeout -k 1s 8s bash -c`; however GNU timeout availability within the pinned image is not yet proven. |
| `R4-02` destructive Redis target identity | P1 / authorization blocker | `DBSIZE=0` + `redis_version=8.x` + `redis` hostname do **not** authenticate an *intended disposable* service; R3 explicitly sends `FLUSHDB`. | R4 source adds read-only GitHub `job.container.{id,network}` and `job.services.{postgres,redis}.{id,network}` inputs, enforces shared nonempty network and distinct container IDs plus exact repo `Reltroner/lms-trust-sandbox` and `GITHUB_ACTIONS=true`. These are **runner metadata assurances, not cryptographic endpoint attestation**; residual risk remains. |
| `R4-03` dependency provenance | P2 / pre-run blocker | Job image is digest-pinned PostgreSQL, with expected `psql`, `bash`, `timeout` and command support; no actual process capability or SBOM/OCI signature check. | Require runtime version and CLI presence checks during controlled first job; source review and image provenance separately remain pending. |
| `R4-04` response parser robustness | P2 / pre-run review | R3 minimal Bash RESP line parser handles only fixed predefined Redis commands and scans partial INFO body; no general RESP/client library. | R4 bounds child lifetime; no claim of generic RESP support, full protocol correctness or Redis ACL safety. |
| `R4-05` test coverage semantics | P2 / evidence boundary | PG-R01 proves launched clients with one claim, **not precise scheduler overlap**; PG-R02 tests one SQLSTATE 23505 rollback path; PG-R03 SQL-denial after Redis loss, **not LMS middleware**. | Keep explicit scoped labels; advanced true race, WAL/standby, owner grants and signed HTTP remain separate gates. |
| `R4-06` budget/supply chain | P2 / governance | Owner GUI showed Actions budget $0 Stop usage Yes, GitHub public standard runner free; no budget enforcement experiment. | Never raise spending cap or switch to paid runner to get CI green. Origin Reltroner-only + require action SHA were persisted in owner refresh screenshot; zero external `uses:`. |

**Source location:** R3 standalone Bash `initial-lab.sh` lines 1–101; YAML mirrors it. R4 code is an **unexecuted candidate**; there is no claim that GitHub-hosted runner/OCI services actually accepted the contract.

## 3. Confirmed GitHub technical semantics and limitations

Official current docs confirm that a job running inside a container and its named service containers are on a job-specific Docker bridge network, use labels `postgres`/`redis` for DNS, and do **not** require published host ports: https://docs.github.com/en/actions/tutorials/use-containerized-services/use-docker-service-containers .

GitHub `job` context exposes `job.container.id/network` and `job.services.<service_id>.id/network` for a running job:
https://docs.github.com/en/actions/reference/workflows-and-actions/contexts .

GitHub's container documentation says job-container default `run` shell is `sh`; our candidate explicitly sets `defaults.run.shell: bash`. `--network` and `--entrypoint` are unsupported in `container.options`. We must not claim image entrypoint/process compatibility until the bounded job actually starts. Source:
https://docs.github.com/en/actions/how-tos/write-workflows/choose-where-workflows-run/run-jobs-in-a-container .

Job-service networking and job-context validation reduce blast radius, but they do **not** prove an arbitrary TCP peer is harmless if runners/DNS/registry/image are compromised. Likewise no host-published port does not mean all egress is blocked. No production endpoints or credentials are ever approved in this lab.

## 4. R4 static review-only output, exact bytes

A new separate ZIP was authored from R3 **without using GitHub sandbox or production**. It contains:

| File | SHA256 of exact UTF-8 bytes | Offline static status |
|---|---|---|
| `candidate.yml` (159 lines) | `3b737d2181c6bd15c710edce7071dcaee036ae4d90a83d57ecdd435a5786a02e` | PyYAML BaseLoader PASS; trigger manual only; job context step env metadata, digest-pinned 3 image references, no external `uses`, no host `ports` |
| `initial-lab.sh` (109 lines) | `49aabab25ed8129ab1e5970517b4ead9083917f130207343933b038131eb2a2d` | `bash -n` PASS; standalone script equals YAML inline run text; timeout subprocess and metadata precondition included |
| `README-REVIEW-ONLY.md` | `4c13eb697efe1208e3401f792ccd2a4bee92cfaeac1c409e39c19e964b0950bd` | explicit no-execution limits |
| `SHA256SUMS.txt` | `4df1e5322278ea3558f80f446a95ccb0c4589f464af30453b7f05ea80420d9a9` | three members hash recorded |
| **ZIP** `LMS-E46-F3B-R4-static-review-only.zip` | **`32af6170d2609fe137d7cf18eb184b763e9fe6bac9932e5995240716a48ad393`** | 7,435 bytes; exact archive verified on assistant container, shared separately as a conversation artifact |

**R4 is NOT a verified final runnable release.** Image GNU `timeout`, Bash `/dev/tcp`, `psql`, Redis RESP behavior, GitHub context values, service identity and runtime remain untested. Using Bash `timeout` is an improvement candidate only, not a proof that connection error paths are safe in the real image.

## 5. Exact next gates and deterministic operator instruction

**Current user action:** none needed for R3 checksum; R3 ZIP integrity is PASSED. R4 ZIP optional for independent review; do not unzip into code workspace or copy `candidate.yml` to `.github/workflows`.

**Next engineering gate R4-R5:** independent static review of R4 source and all high-severity blockers. Confirm job/container metadata context supported; verify proposed image-client/tooling capabilities and safety of `FLUSHDB` target before F3B permission. If needed, split initial trial into a **non-destructive `DEL` rehearsal** and later separately consented destructive `FLUSHDB` evidence, but do NOT count `DEL` as actual PG-R03 FLUSH proof. Alternative candidate should not silently weaken SQL replay integrity contract.

**F3-B-FIRST-COMMIT:** remains `NOT AUTHORIZED` because consent to create empty repository and change Actions settings did not authorize installing executable workflows. Before first commit, give owner exact reviewed source hashes, approved image digests, runtime risk list and diff. Only a specific `ALLOW_F3B_FIRST_WORKFLOW_COMMIT=YES` can unblock.

**F3-C-FIRST-MANUAL-RUN:** remains `NOT AUTHORIZED`, must be separately approved after deployment into sandbox default branch and before any `workflow_dispatch`. Failed budget stop at $0 cannot authorize increasing budget; if blocked STOP.

**Current invariant accounting:** E40 Windows 30/30 and E45 local PDO_SQLite 8/8 exploratory PASS; real PG18/Redis8 PG-R01..10 `0/10`, HTTP T02 `0/86`; D02 owner trust design ratification HOLD; BE/FE source and production remain untouched.
