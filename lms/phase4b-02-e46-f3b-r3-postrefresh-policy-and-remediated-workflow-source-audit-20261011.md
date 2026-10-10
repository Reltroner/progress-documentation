# Reltroner LMS Phase 4B-02 — E46-F3B-R3 Owner Post-Refresh Action Policy Acceptance and Static Lab Harness Remediation

> **Evidence ID:** LMS-P4B02-E46-F3B-R3-20261011
> **Canonical authority:** [README](./README.md), [frozen infrastructure placement](./master-infrastructure-placement-contract.md), [frozen logical service contract](./logical-service-boundary-api-contract.md), [F3B-R2](./phase4b-02-e46-f3b-r2-origin-allowlist-evidence-and-static-first-workflow-review-20261011.md).
> **Status:** `SANDBOX_ACTIONS_POLICY_POST_REFRESH=PASS_OWNER_GUI`; `OCI_INDEX_DIGEST=3/3_OWNER_OPERATOR_PASS`; `OFFLINE_SOURCE_REVIEW=R3_STATIC_CHECKS_PASS_WITH_UNRESOLVED_RUNTIME_GAPS`; `F3B_INITIAL_DEFAULT_BRANCH_COMMIT=HOLD_NOT_AUTHORIZED`; `F3C_MANUAL_JOB=HOLD_NOT_AUTHORIZED`; `PG-R01..10=0/10`; `T02_HTTP=0/86`; `D02_RATIFICATION=HOLD`.
> **Mutation scope:** THIS DOCS PR ONLY; no changes to Reltroner/lms-trust-sandbox, LMS-BE, LMS-FE, VPS, cloud DNS, Keycloak, runtime databases or billing.

## 1. Actions policy post-refresh acceptance (owner-provided screenshot)

The owner explicitly reports **pressing Ctrl+R and obtaining the new screenshot**, while browser URL is `https://github.com/Reltroner/lms-trust-sandbox/settings/actions`. The screenshot AFTER refresh clearly shows both options persisted:
1. Radio selected: **Allow Reltroner actions and reusable workflows**; **Allow all actions** NOT selected.
2. Checkbox selected: **Require actions to be pinned to a full-length commit SHA**.
3. Retention still **90 days**; its shortening is not a gating requirement or approved change.
4. Previous owner screenshot had `Actions policy updated` on the SHA change, followed by a later screenshot with `Default workflow permissions settings saved`. This last banner was not sufficient on its own, but **owner's explicit reload + screenshot now independently establishes selected values survived that reload**.
5. Evidence is **owner GUI post-refresh PASS**, not an independently retrieved administrative settings API response. It demonstrates control selection, not proof all future workflows are free of malicious runtime code; first candidate must still have **zero external `uses:`** and pinned OCI images.
6. Previously observed Actions billing: **$0 account budget, Stop usage Yes** and no changed budgets. Do not raise or remove this budget to get a runner scheduled.

**Decision:** `F3B_ACTIONS_ORIGIN_AND_SHA_POST_REFRESH=PASS_OWNER_GUI`. No more GUI retest requested unless future evidence shows drift. No action on existing LMS-BE tag-based CI.

## 2. Static source audit of previous R2 review ZIP

This assistant re-opened the exact previously produced review ZIP and verified all listed SHA256 entries matched the file bytes. Original files:
- `candidate.yml` sha256 `88516d1925c4b03286c27d90dfd124268dcc237395cf0a6bc958b963e55dd5e2`.
- `initial-lab.sh` sha256 `79992c8dc5c06e8a4c93c805fb80d257d48156cd3696627c8ad5e9a27e88ba3f`.
- YAML `on.workflow_dispatch` only, `permissions: {}`, one 10m `ubuntu-24.04` job, no external `uses:`, no published service `ports:`; Bash `bash -n` PASS; YAML inline shell **byte-identical after dedentation** to standalone Bash script.
- Identified static audit gaps: R2 PG-R02 treated arbitrary `psql` nonzero as expected unique conflict, R2 `FLUSHDB` did not assert fresh Redis keyspace or TTL / NX replay reservation, and PG-R01 label overstated concurrent scheduler overlap evidence. R2 `CREATE TABLE IF NOT EXISTS` could reuse an old empty fixture.
- These are candidate harness weaknesses only, NOT documented LMS production defects or confirmed vulnerabilities.

## 3. R3 revised OFFLINE review bundle — NOT A GITHUB WORKFLOW

New separate **review-only** ZIP produced in isolated assistant environment; its source files remain OUTSIDE `Reltroner/lms-trust-sandbox`. The archive is available only as a conversation artifact. Hashes are of the actual newly generated UTF-8 bytes and locally verified:

| File | SHA256 | Source assessment |
|---|---|---|
| `candidate.yml` | `0e133699da2740eef7fffcff0adbe9ddf1705343853373a9db0b9595759bdb98` | 144-line, PyYAML BaseLoader parse PASS; one manual job, zero uses, no host ports, `timeout-minutes:10`, digest-pinned images |
| `initial-lab.sh` | `404287a0f1b3202b49e687ec1c68f8396ee32e9bc832b965527e48bdefd0ee61` | 101-line, `bash -n` PASS; same inline Bash as candidate.yml |
| `README-REVIEW-ONLY.md` | `df7e3328a939285aa646cf867a35f603e7a4972002c48c84ad2e8be96e8c15f5` | explicitly states hold/risk limitations |
| `SHA256SUMS.txt` | `c7f58ad942b0aa9668b064aeebb5f8efcdfd21a909a38bdc41fedc1dde0feb44` | contains the three file hashes above |
| ZIP archive | `07e230b0764798734975d76ebb6d0f6364d2633ecdb8595ba0aad637d95cafc0` | SHA256 of packed archive bytes; NOT committed to GitHub |

### R3 remediation performed

- PG-R02: invoke `psql -v VERBOSITY=sqlstate -v ON_ERROR_STOP=1` on intentionally failing duplicate transaction, require nonzero **and** SQLSTATE **23505** in the captured error output; still assert inserted first nonce absent and preexisting nonce retained.
- PG-R03: require `DBSIZE=0` on fresh disposable Redis8 service prior to writes; use `SET lab:nonce:r3 1 NX PX 65000`; check exists, `PTTL > 0`, `DBSIZE=1` before any `FLUSHDB`, require `DBSIZE=0` afterwards, independently check SQL claim retained and SQL duplicate denied.
- PG-R01: label reduced to **two processes launched in parallel and only one claimant**, not proof that scheduler overlap or a deterministic race barrier has been observed. Strong overlap proof would need another deliberately controlled concurrency scenario before a stronger certification.
- Fixture guard: `CREATE TABLE lab_nonce_claims` now fails if an old table exists; check exactly `PGHOST=postgres`, `PGPORT=5432`, `PGDATABASE=lms_synthetic`, `PGUSER=lab_client`.
- Verified Bash syntax and YAML parse after remediation; program checks confirm manual-only trigger, `permissions: {}`, exactly one job, standard runner, 10-minute cap, no external `uses:`, zero host-published database ports and Bash/YAML inline exact content equality.

**Scope boundary:** An ephemeral Redis `FLUSHDB` is **destructive** and still requires stronger assurance of network target identity than checking `DBSIZE` and service DNS names. Runtime job container image and Bash `/dev/tcp` socket connect timeout, actual PostgreSQL18/Redis8 versions, ShellCheck/actionlint, optional OCI attestations/vulnerability evidence, and runtime test output remain NOT VERIFIED. Host mapping absence does not prevent all outbound registry traffic; do not assert universal zero-network. No verified DB tests have been run in this session. The synthetic-only design is not proof of production middleware behavior, signed on-wire JWS or real HTTP T02.

## 4. Next fixed gates before first default-branch commit

1. **F3B-R4 read-only source and risk review:** inspect R3 exact source SHA, evaluate Github Actions job container effective shell/path/entrypoint and image version provenance, supply chain, Bash RESP framing and connection timeout (plus guard for Redis service identity). A source bug is STOP, never fix it inside a live default-branch workflow as the first attempt.
2. **F3B-FIRST-COMMIT explicit owner decision** only after code review final and risk report, with exact pinned commit payload and no production secrets. This consent is distinct from repo-creation permission and GUI setting changes. No first commit is allowed by this document.
3. **F3C-FIRST-MANUAL-RUN explicit owner decision** only after first workflow verified on default branch, $0 spending stop policy preserved, one-job 10-minute constraints verified and required failure models reviewed. If public runner blocked by budget, STOP; do not increase budget automatically.
4. Under any outcome retain architectural freeze; PostgreSQL18/Redis8 actual PG-R01..10 `0/10`, canonical HTTP T02 `0/86`, D02 owner design/production HOLD.

**Current checkpoint:** `E46_F3A_PASS_PUBLIC_EMPTY_REPO -> E46_F3B_POST_REFRESH_SECURITY_PASS_OWNER_GUI -> OCI_MANIFEST_3_OF_3_OWNER_PASS -> R2_AUDIT_WEAKNESSES_REMEDIATED_IN_OFFLINE_R3_STATIC_SOURCE -> F3B_RUNTIME_RISK_REVIEW_PENDING -> F3B_FIRST_SANDBOX_COMMIT_HOLD -> F3C_FIRST_MANUAL_RUN_HOLD -> PG_R_0/10 -> T02_HTTP_0/86 -> D02_HOLD -> PRODUCTION_NOT_AUTHORIZED`.


## 5. R4 operator ZIP-integrity acceptance and independent source audit (2026-10-11)

The owner Windows PowerShell5.1 reported `E46_F3B_R3_ZIP_INTEGRITY=PASS`, validating downloaded R3 ZIP SHA256 `07e230b0764798734975d76ebb6d0f6364d2633ecdb8595ba0aad637d95cafc0`. Independently, assistant checked exact R3 archive bytes, all internal SHA256SUMS, YAML and `bash -n`. **This closes only source transport/integrity.** The R3 source still lacks a bounded `/dev/tcp` TCP connect, and `DBSIZE=0` alone is insufficient assurance before destructive Redis `FLUSHDB`. A **new separate noncommitted R4 static candidate** adds GNU timeout-wrapped Redis socket attempts and GitHub service/job network/container ID consistency checks using documented job contexts. Candidate ZIP SHA256 `32af6170d2609fe137d7cf18eb184b763e9fe6bac9932e5995240716a48ad393`; Bash `-n`, YAML parse and structural checks PASS, **no runtime engines, ShellCheck/actionlint, image command availability, cryptographic Redis identity or actual job success**. [Complete R4 evidence and risk work order](./phase4b-02-e46-f3b-r4-owner-zip-integrity-and-static-client-network-risk-review-20261011.md). No additional owner GUI action required; first sandbox workflow commit and first dispatch remain NOT AUTHORIZED, PG-R 0/10, T02 0/86, D02 HOLD, production unchanged.
