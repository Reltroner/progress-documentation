# RS-DEPLOY-SHA-005 — Deployment SHA Parity Debugging, Fail-Closed Convergence and Production Recovery

> **Dated acceptance record:** 2026-11-18 (WIB / UTC+07:00).  
> **Implementation authority:** [Reltroner Statistics](https://github.com/Reltroner/reltroner-statistics) at `ed3abce95fd5c6f4371bd5e957ff7aa4d680909c`, [PR #11](https://github.com/Reltroner/reltroner-statistics/pull/11).  
> **Critical evidence:** [PR CI #44251870217](https://github.com/Reltroner/reltroner-statistics/actions/runs/44251870217) and [main-push CI #44254064537](https://github.com/Reltroner/reltroner-statistics/actions/runs/44254064537); live publication job `134635454324` **SUCCESS**.  
> **Status at checkpoint:** **MERGED, PRODUCTION DEPLOYED, LIVE_POST_MERGE_ACCEPTANCE: PASS**.  
> **Scope restriction:** Statistics project and its one approved custom domain only; does not change Studio, Remodeling, DNS, nameservers or canon.

## 1. Problem and engineering objective

A Cloudflare Pages deploy can report **`Deployment complete`** while the canonical hostname `statistics.reltroner.com` still serves a previously published `build-info.json`. The original `scripts/verify-deployment.ts` loop effectively ended when it received the first HTTP 200: `attempt < 6 && !live`. If that body carried the *old but otherwise well-formed* Statistics release, the verifier immediately declared a SHA mismatch and exited, rather than waiting for the exact expected build.

The owner requested a deterministic, non-regressive solution, not a weakened assertion, fixed sleep, unbounded retry, cache purge or automatic redeploy. Verification must still compare the application commit **and** semantic digest, rules version, production source SHA and remodeling source SHA, bound all requests, fail closed on persistent problems, and only proceed to strict 16-tool REST/MCP acceptance once the custom domain truly serves the intended release.

## 2. Observed incident sequence

| Evidence | Historical outcome |
| --- | --- |
| [PR #8 production run #44094544189](https://github.com/Reltroner/reltroner-statistics/actions/runs/44094544189) | after `Deployment complete`, one read at roughly +0.33 s returned previous `fc37812…` rather than new `5b54738…`; verification failed |
| [PR #9 production run #44104975078](https://github.com/Reltroner/reltroner-statistics/actions/runs/44104975078) | site SHA verified; subsequent 16-tool verifier failed because SDK-normalized `tools/list` omitted `include_sections.default` (distinct issue, fixed by PR #10) |
| [PR #10 production run #44111759840](https://github.com/Reltroner/reltroner-statistics/actions/runs/44111759840) | Wrangler completed new `92ad608…` publish; custom-domain read +0.78 s later returned previous `1dbca25…`; `STATISTICS_DEPLOYMENT_UNVERIFIED` |
| Subsequent read-only inspections, 2026-11-18 | canonical domain and unique deployment URL later served `92ad608…`, matching digest and source SHAs |
| [PR #11 production run #44254064537](https://github.com/Reltroner/reltroner-statistics/actions/runs/44254064537) | new verifier confirmed the exact unique artifact, two consecutive matching canonical reads and unchanged GitHub main; subsequent live 16-tool acceptance PASS |

The SHA-005 incident report counted **two stale first responses among eight prior main-push publications**. This is a small historical observation, **not** a measured Cloudflare propagation probability or a causal attribution to Cloudflare internals.

**Proven root cause:** the verifier logic failed to retry a valid-but-old HTTP 200. **Plausible but unproven trigger:** short-lived Cloudflare Pages/custom-domain propagation delay. Cache behavior and routing issues were considered; the contemporaneous stale headers were unavailable. The 2026-11-18 read-only probe reported `cf-cache-status: DYNAMIC` with `max-age=0`, weakening but not disproving the cache hypothesis.

A secondary bug was eliminated: comparison using JSON serialization alone could incorrectly pass a malformed expected identity with `null` fields if the observed identity had the same invalid values. Now the expected build identity must be complete and valid before any live request.

## 3. Release evidence stages — never collapse into one boolean

~~~text
Commit to main with verified build
           |
GitHub CI: determinism + Python + pipeline/build + workerd + E2E
           |
Statistics-only guard: credentials, exact Pages project/domain, no DNS writes
           |
Wrangler upload + "Deployment complete"                      UPLOADED
           |
Parse exactly one unique URL from this Wrangler invocation
           |
GET https://<8-hex>.reltroner-statistics.pages.dev/build-info.json
  exact commit / digest / rules / both source SHAs             DEPLOYMENT_ARTIFACT_VALID
           |
Bounded GET on https://statistics.reltroner.com/build-info.json
  if HTTP 200 with old complete identity -> PROPAGATING -> retry
  require 2 consecutive matching observations >=5s apart     CUSTOM_DOMAIN_CONVERGED
           |
Re-read GitHub refs/heads/main == expected deployed SHA       MAIN_EQUALS_EXPECTED
           |
STATISTICS_DEPLOYMENT_VERIFIED (exit 0)
           |
Live verify-remote-mcp.mjs --profile page-aware-v1
  13 legacy + 3 page tools, 18 REST, read-only and source parity
           |
LIVE_POST_MERGE_ACCEPTANCE: PASS
~~~

**Convergence means the verifier's tested origin returned the expected identity twice.** It does not demonstrate every Cloudflare edge worldwide has the new build. A green GitHub build alone and a successful upload alone are each insufficient to declare live acceptance.

## 4. Implementation boundaries and changed files

| File in Statistics repository | Role |
| --- | --- |
| `scripts/lib/statistics-deployment-verification.ts` | typed identity validation, exact origin/deployment URL policies, request transport, bounded convergence state machine, structured diagnostics |
| `scripts/verify-deployment.ts` | CLI wrapper, backward-compatible one-argument call and new protected release flags |
| `scripts/capture-pages-deployment-url.ts` | parse this run's Wrangler stdout and output exactly one unique release URL or fail |
| `.github/workflows/ci.yml` | main-push publication captures URL, validates unique artifact then canonical convergence, finally verifies live PAGE-004 protocol |
| `.github/workflows/release.yml` | explicit owner-authorized release path with same verification sequence |
| `tests/unit/deployment-verification.test.ts` | deterministic virtual-clock replay, positive/negative cases and transport/identity security |
| `tests/unit/publication-workflows.test.ts` | parsed-workflow contracts: sequence, isolation, safe environment-passing and absence of destructive Cloudflare actions |
| `docs/RS-DEPLOY-SHA-005-{INCIDENT,ARCHITECTURE,ACCEPTANCE}.md` | source incident timeline, release state machine, acceptance evidence and on-call runbook |

The fix does not modify `src/`, `functions/`, `public/` or the static browser UI. CI retains the original strict 16-tool `page-aware-v1` production verifier and required SHA equality. No rollback, DNS edit, Cloudflare cache purge, automatic re-publish or configuration mutation was introduced.

## 5. Identity contract and security

The expected artifact's `dist/build-info.json` must contain a complete `reltroner-statistics-build.v1` identity.

| Field | Required property |
| --- | --- |
| `statistics_commit` | valid 40-hex SHA, equals the explicit expected SHA |
| `semantic_digest` | valid 64-hex digest, equals the artifact |
| `rules_version` | nonempty permitted rules version, equal |
| `sources.production` | valid 40-hex source SHA, equal |
| `sources.remodeling` | valid 40-hex source SHA, equal |

Every comparison occurs within **one response body**; no mixing commit from one request with digest from another. Malformed JSON, incomplete identities and unexpected body shapes are not "stale" and do not get silently retried as legitimate propagation.

**Untrusted input controls:** canonical verifier origin must be exactly `https://statistics.reltroner.com` or the allowed bootstrap Pages alias; the unique deployment URL must match `https://<8 lowercase hex>.reltroner-statistics.pages.dev` and originate from this run's Wrangler output. Credentials, ports, alternate hosts, lookalikes, paths, non-HTTPS, arbitrary URLs and redirects are refused. HTTP method is GET only. No URL from a response is followed. The GET request includes `Cache-Control: no-cache` but that is **not proof of bypassing every intermediary cache**.

**Main continuity:** the CLI reads `git ls-remote --exit-code origin refs/heads/main` before and after convergence (20-second bound each). If main advances or is unreadable, the verifier fails with `STALE_DEPLOY_BLOCKED` or `MAIN_REF_UNRESOLVED`, rather than declaring an older SHA the current release.

## 6. Deterministic classification, limits and timeout policy

| Response at canonical origin | Classification | Action |
| --- | --- | --- |
| 200 + valid identity + all fields match | `MATCH` | increment consecutive confirmations; two required |
| 200 + valid identity + at least one field differs | `PROPAGATING` | reset confirmations; retry with bounded backoff |
| Transient HTTP 404/503/522 or transport exception | `HTTP_STATUS` / `NETWORK_ERROR` | retry within deadline |
| Request abort | `REQUEST_TIMEOUT` | retry within deadline |
| Redirect | `REDIRECT_REFUSED` | immediately FAIL |
| Malformed/oversized body | `MALFORMED` | immediately FAIL |
| Immutable unique URL shows wrong complete identity | `DEPLOYMENT_ARTIFACT_MISMATCH` | immediately FAIL |
| Never achieves two confirmations by deadline | `TIMED_OUT` / `UNREACHABLE` | FAIL with observation history |

Default limits (from [source architecture](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-DEPLOY-SHA-005-ARCHITECTURE.md)):

| Policy | Default | Max configured bound |
| --- | --- | --- |
| Request timeout | 10 seconds (clamped to remaining deadline) | 30 s |
| Backoff | 2 → 4 → 8 → 10 s | ≤ 60 s |
| Consecutive canonical confirmations | 2, 5 s apart | 1–5 permitted by internal policy, release flows fixed at 2 |
| Unique artifact phase | 60 seconds | 300 s |
| Custom-domain phase | 120 seconds | 300 s |
| Attempts per target | 30 | 100 |
| Response body | 64 KiB | 1 MiB |
| Read GitHub main | 20 seconds × 2 | fixed |

Default upper bound 220 seconds (60 + 120 + 40); override upper bound 640 seconds, both below a 15-minute release-job timeout. A frozen clock cannot loop forever because the attempt cap still terminates it. The workflows expose **no policy override flags**.

## 7. Diagnostic output contract

The CLI keeps its original leading fields and exit semantics: `status`, `url`, `mismatches` and `live_commit`; `STATISTICS_DEPLOYMENT_VERIFIED` is exit 0 and unverified is exit 1 (usage errors exit 2). Additive fields: `reason`, `failed_target`, `detail`, `expected_sha`, `expected`, `deployment_artifact`, `custom_domain`, `main_ref`, `policy`, `elapsed_ms`, `history[]` and `limitations[]`.

A `history[]` entry includes the target, attempt number, elapsed/duration milliseconds, HTTP status/outcome, observed versus expected commit, mismatched fields and **allowlisted** headers (`etag`, `cf-cache-status`, `age`, `cf-ray`, `cache-control`, `date`, `content-type`, `last-modified`). No raw body, cookies, credentials or extra headers are logged; header values are sanitized. A red step means the release **was not verified**; it does not imply automatic rollback or that the previous release is necessarily still live.

## 8. CI, regressions and non-functional evidence

[Draft PR #11](https://github.com/Reltroner/reltroner-statistics/pull/11) was built from local/GitHub main parity `92ad608…` in the owner's isolated sibling worktree. The owner-reported preflight preserved the primary checkout on `feat/rs-creative-quality-003`, including staged `.vscode/settings.json` and `public/reltroner-statistics-logo.webp`, with SHA-256 equality to backups. The remote documentation author does **not** infer the present-day owner's Windows checkout state from those dated logs.

The final feature head `f32b67c142f10360e02f6ff5654b9681421ae8f6` passed [PR CI #44251870217](https://github.com/Reltroner/reltroner-statistics/actions/runs/44251870217):

| Gate | Result at PR head |
| --- | --- |
| New negative/convergence tests | 33/33 PASS |
| Node unit tests total | 180/180 PASS |
| Protocol profile tests | 9/9 PASS |
| Python analytics | 24 PASS |
| Typecheck | 230 files; zero errors/warnings |
| Pipeline and build | 635 HTML, 642 PDFs, 37,629 internal links |
| Workerd runtime | 18 REST operations, 16 MCP tools, 3 page tools, 634 mirrors |
| Browser E2E | 441 passed, 1 expected skip |
| Determinism and Python CI | Ubuntu and Windows PASS |

**Mutations checked:** old early-exit defect, reduction to one confirmation, omitted semantic digest, reverting either publication workflow, and redirect-following all cause one or more tests to fail. All 50 browser JS/CSS bundles were byte-identical to baseline. The 586 HTML differences seen between independent builds corresponded to embedded `generated_at` values and island identifiers, not an introduced browser change; these observations are tied to that controlled test run.

## 9. Post-merge production acceptance — now verified

PR #11 merged into main at `ed3abce95fd5c6f4371bd5e957ff7aa4d680909c` on 2026-11-18. Its [main-push run #44254064537](https://github.com/Reltroner/reltroner-statistics/actions/runs/44254064537) completed successfully, including the Statistics-only publication job `134635454324`.

| Acceptance evidence from production log | Observed |
| --- | --- |
| Project/custom-domain guard | `ISOLATED_STATISTICS_PAGES_VERIFIED`, project `reltroner-statistics`; DNS and nameserver mutations = 0 |
| Wrangler unique URL | `https://e037afc4.reltroner-statistics.pages.dev` |
| Unique artifact identity | `DEPLOYMENT_ARTIFACT_VALID`, one matching read of `ed3abce…` |
| Canonical domain | `CUSTOM_DOMAIN_CONVERGED`, two matching reads of `ed3abce…` about 5 seconds apart |
| Main ref before/after | `MAIN_EQUALS_EXPECTED`, both equal `ed3abce…` |
| CLI verdict | `STATISTICS_DEPLOYMENT_VERIFIED`, `reason: VERIFIED`, `mismatches: []`, exit 0 |
| Live MCP verification | `RS-AI-API-002` `status: PASS`; `page-aware-v1` 16-tool profile, full new page operations, negative checks |

The observed canonical reads were two `MATCH` responses with `cf-cache-status=DYNAMIC`. The verifier reported elapsed time approximately **6.1 seconds**, before the live protocol check. The source identity matched production SHA `ad895e6d9184f09281a7cc14ccd7867c47acd29e`, remodeling SHA `33ea8fa5472a723d640f1adbea35f686a65b3e27`, rules `P0R-2.0.0` and semantic digest `4119d30b2c2d7ea14b95fe08c2d53365de966acaeb343a2a772e26d42a28e08d`.

This closes **LIVE_POST_MERGE_ACCEPTANCE: PASS** for the tested Statistics deployment/protocol scope. It does **not** close signed-in ChatGPT/Claude/Gemini G8 creative/page fidelity acceptance or verify the separately hosted Studio frontend's source deployment.

## 10. Failure response and operator boundary

If a later publish fails, read the failed job JSON and `reason` / `failed_target` / `history[]` before any action:

1. `EXPECTED_IDENTITY_INVALID`: compare local artifact's `dist/build-info.json` with exact workflow SHA; repair the build, **do not bypass** validation.
2. `DEPLOYMENT_URL_UNAVAILABLE` or `DEPLOYMENT_ARTIFACT_MISMATCH`: check the Wrangler output and unique deployment URL of the **same job**; do not substitute a branch URL.
3. `TIMED_OUT` with valid old build: check unique URL versus canonical identity and Cloudflare Pages deployment/custom-domain state; investigate propagation/caching without guessing.
4. `MALFORMED` / `REDIRECT_REFUSED`: inspect format or unexpected routing; do not follow arbitrary Location hosts.
5. `STALE_DEPLOY_BLOCKED` / `MAIN_REF_UNRESOLVED`: fetch the latest main and use the corresponding CI run; never publish an arbitrary stale SHA as current.
6. If deployment passes but MCP fails: inspect strict `page-aware-v1` test errors; do **not** bypass tool count, read-only metadata, source policy or negative tests.

Any manual rerun, cache rule, rollback, release dispatch or routing change requires explicit owner decision and is **not** part of the verifier.

## 11. Canonical code and provenance register

- [Incident timeline](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-DEPLOY-SHA-005-INCIDENT.md)
- [Verifier architecture](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-DEPLOY-SHA-005-ARCHITECTURE.md)
- [Acceptance and operator runbook](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-DEPLOY-SHA-005-ACCEPTANCE.md)
- [State machine implementation](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/scripts/lib/statistics-deployment-verification.ts)
- [Thin CLI wrapper](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/scripts/verify-deployment.ts)
- [URL capture](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/scripts/capture-pages-deployment-url.ts)
- [Main-push live run](https://github.com/Reltroner/reltroner-statistics/actions/runs/44254064537)

See [PAGE-004 architecture](./2026-11-18-rs-ai-page-004-universal-page-aware-intelligence-architecture.md), [operations runbook](./2026-11-18-rs-page-deployment-operations-runbook.md), and [cross-milestone acceptance ledger](./2026-11-18-page-aware-and-deployment-acceptance-ledger.md). 
