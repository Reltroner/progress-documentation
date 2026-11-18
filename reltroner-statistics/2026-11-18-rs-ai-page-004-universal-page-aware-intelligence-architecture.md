# RS-AI-PAGE-004 — Universal Page-Aware Intelligence Architecture

> **Record and evidence checkpoint:** 2026-11-18 (Asia/Jakarta).  
> **Implementation:** [Reltroner Statistics](https://github.com/Reltroner/reltroner-statistics) at main `ed3abce95fd5c6f4371bd5e957ff7aa4d680909c`, incorporating [PR #8](https://github.com/Reltroner/reltroner-statistics/pull/8), [PR #9](https://github.com/Reltroner/reltroner-statistics/pull/9) and [PR #10](https://github.com/Reltroner/reltroner-statistics/pull/10).  
> **Release evidence:** [main-push CI #44254064537](https://github.com/Reltroner/reltroner-statistics/actions/runs/44254064537) completed successfully, including the 16-tool protocol gate.  
> **Record type:** source-grounded engineering chronicle and implementation cross-reference, **not** a dynamic runtime monitor.  
> **Canonical source:** implementation and contracts in [Statistics docs](https://github.com/Reltroner/reltroner-statistics/tree/main/docs); this document is a dated cross-project archive, not a replacement.

## 1. Executive decision, scope and result

The owner ratified **RS-AI-PAGE-004 — Universal Page-Aware Intelligence Architecture** after an AI chat could not open `https://statistics.reltroner.com/statistics/spatial/` through its browser. Prior MCP search and research functions could find related entities but could not reproduce the **specific requested page**, including its displayed data, section structure, source roles and visualization limitations. The resulting design covers **every eligible built Statistics HTML page**, not just the spatial route.

**Intent:** a user pastes an exact Statistics URL into a ChatGPT, Claude or Gemini conversation; an AI client **with an enabled compatible connector** can resolve the exact page through the stateless MCP gateway, read the semantic page and selected sections, and return an evidence-grounded analysis in chat. Browsing, direct REST access and MCP are distinct transport/capability modes: pasting a URL does **not** automatically connect MCP or guarantee that a provider browser can fetch the HTML.

**Verified result on 2026-11-18:** the deployed Statistics release exposes 18 read-only REST operations (15 previous + 3 page operations) and 16 read-only MCP tools (13 previous + 3 page tools). [PR #9](https://github.com/Reltroner/reltroner-statistics/pull/9) was merged at `1dbca25ff3b8e12b1919038967bbfb23f8a4bfce`; [PR #10](https://github.com/Reltroner/reltroner-statistics/pull/10) corrected a release-verifier metadata assumption and merged at `92ad608e1d22193120a2fb9a0b42993271797a84`. The later [PR #11](https://github.com/Reltroner/reltroner-statistics/pull/11) release of `ed3abce…` passed the **live** PAGE-004 protocol checks. This **does not** establish G8 acceptance inside all three native provider sessions.

## 2. Transport and trust architecture

~~~text
Owner supplies a precise https://statistics.reltroner.com/<page> URL
         |
         +--> Provider browser: attempts normal HTML or the public Markdown/JSON mirror
         |      (provider-controlled; may fail; no MCP inference)
         |
         +--> Direct REST-capable client: GET /api/v1/pages/{resolve,context,section}
         |
         +--> Connected MCP client: POST /mcp, stateless Streamable HTTP
                    |
             resolve_statistics_page    (exact registry lookup, no external fetch)
                    |
             read_statistics_page       (semantic page + bounded inline sections)
                    |
             read_statistics_section    (targeted section/table, cursor if required)
                    |
              AI reasoning/answer       (citations, epistemic status, unknowns)
~~~

Production and Remodeling are pinned data sources; **Statistics is the read-only derived observatory**. Neither page reading nor model interpretation writes to Studio, Studio Remodeling, or Asthortera canon. Existing `rs-intelligence.v1` response envelope, permission isolation, and `RS_API_DISABLED` controls on REST/MCP remain intact.

## 3. Static-first build and page-mirror pipeline

1. Run the usual ETL, validated snapshot generation, Astro static build, PDF generation and postbuild verification.
2. Read **the built HTML**, not a fabricated parallel document: `src/engine/page-mirror/html.ts` parses structure, `props.ts` interprets Astro island props, `shapers.ts` provides visualization-specific shapes, and `markdown.ts` emits safe textual representation.
3. `src/engine/page-mirror/index.ts` performs the page census, classifies source/route/family and coverage, applies size limits, validates page JSON contracts and emits the registry and mirrors.
4. `scripts/page-mirrors.ts` and `scripts/postbuild.ts` link the build lifecycle to the mirror generation and parity checks.
5. Cloudflare Pages serves public static mirror files; Pages Functions and the MCP adapter read **only registry-listed same-build artifacts** through `env.ASSETS`. No request-driven crawl, arbitrary file fetch, external URL fetch or dynamic worldbuilding inference occurs.

**Static public artifacts and schemas**

| Artifact | Contract / purpose |
| --- | --- |
| `/ai/pages/index.json` | `rs-page-registry.v1`, snapshot, census, exclusions, route lookup/chunks |
| `/ai/pages/_registry/<route>-<n>.json` | `rs-page-registry-chunk.v1`, bounded dynamic-route registry entries |
| `/ai/pages/<page>.json` | `rs-page-context.v1` for a single eligible page |
| `/ai/pages/<page>.md` | escaped semantic Markdown for that same page |
| `/ai/pages/_root.json` and `_root.md` | home-page mirror; avoids collision with registry index |
| `analytics/schemas/page-context.schema.json` and related registry schemas | derived from `src/contracts/page-schemas.ts` and checked against Zod contracts |

Directory page `/statistics/spatial/` maps to `/ai/pages/statistics/spatial.json` and `.md`; file-style routes retain their extension as part of the mirror path. Public pages advertise alternate JSON/Markdown links without adding browser JavaScript or changing human-facing navigation.

**Coverage is explicit, not an unsupported universal claim:** a page can be `FULL` or `PARTIAL`, and `coverage.not_captured` states what client-only browser behavior could not be reproduced. `NOT_REPRESENTABLE` is reserved in the contract. On the initial PR #9 build there were 608 HTML files, 607 eligible mirrors, 598 FULL and 9 PARTIAL; `/404.html` was excluded (`ERROR_PAGE`). On the later *combined* 2026-11-18 source snapshot, CI verified **635 HTML, 634 mirrors, 625 FULL, 9 PARTIAL**, 642 PDFs and 37,629 internal links. These are distinct dated builds, not contradictory census claims. The registry generated with **each release**, not either historical number, is authoritative.

## 4. Page-context fields and epistemic integrity

A `rs-page-context.v1` mirror carries the exact registered `page_id` and `canonical_path`, canonical URL, headings/title/description/language, site section and page family, static/dynamic classification, declared source links, chart/component metadata, section IDs, tables, links, and `coverage` limitations.

Its `snapshot` identifies the Statistics application commit, production and remodeling source SHAs, semantic digest, rules version, analysis-generation timestamp and `studio_deployment_status`. An analyzed production source commit **does not** prove that `reltroner.com` currently deploys the same Studio revision; `DEPLOYMENT_UNVERIFIED` is a separate source-site verification state, **not** a failed Statistics release.

**Non-negotiable source-status boundaries**

| Classification | Interpretation |
| --- | --- |
| `CANON_OBSERVED` | value directly evidenced from the pinned production canon |
| `CANON_DERIVED` | deterministic calculation from valid production evidence, not new canon |
| `PROPOSED` | remodeling data / proposed content, never silently promoted |
| `SCENARIO` / `HYPOTHESIS` | model or creator assumptions and speculative outputs, not observed canon |
| `INSUFFICIENT_DATA` / null | missing or indeterminate values; must not be replaced by zero or a confident guess |

For `/statistics/spatial/`, land-footprint percentages use **national terrestrial land** as the denominator, while principal-home-habitat percentages use **unique usual residents**. Both spatial tables are `PROPOSED`. Unspecified three-dimensional volumes remain **null**; no km³ or population-capacity figure may be invented. This is a concrete anti-hallucination acceptance check.

The API preserves `source_role` even if the caller chooses `source_policy=production_only`; remodeling rows are withheld, **not relabeled** as production. Unknown sections, unknown entities and unknown pages are never substituted with a plausible neighboring record.

## 5. Exact URL resolution and user view state

`src/domain/page-url.ts` parses the input without fetching it. The accepted remote origin is `https://statistics.reltroner.com` (or a slash-leading site path); only harmless trailing-slash variants may normalize. Lookup is exact against the build registry: no fuzzy route selection, case correction, search substitution or redirect navigation.

| Refusal code | Boundary |
| --- | --- |
| `URL_TOO_LONG` | URL length exceeds 512 characters |
| `INVALID_URL` / `INSECURE_SCHEME` | malformed, relative, scheme-relative or non-HTTPS origin |
| `FOREIGN_ORIGIN` | other domains, IP addresses, punycode/lookalikes or host tricks |
| `CREDENTIALS_NOT_ALLOWED` / `PORT_NOT_ALLOWED` | URL userinfo or unexpected ports |
| `PATH_NOT_CANONICAL` | encoded path, backslash, empty/dot segments or traversal |
| `QUERY_NOT_ALLOWED` | invalid encoding, duplicate names, oversized or excessive parameters |

Supported query/hash state is represented as `view_state` only where it can be mapped to published evidence. Otherwise the response declares `UNSUPPORTED_VIEW_STATE`, `BROWSER_ONLY_STATE`, `VALUE_NOT_PUBLISHED` or `UNKNOWN_PARAMETER`; a fragment referring to an unknown section is disclosed, not silently ignored. Supported historical acceptance examples include `?node`, `?entity`, `?origin`, `?tree`, `#scenario` and `#mode` where a specific page supports them.

**Exact resolution examples:** `/statistics/spatial/` resolves with proposal status; `/statistics/spatial-3d/` returns `PAGE_NOT_FOUND` rather than an invented new page. No HTML/browser inability is disguised as a successful MCP page read.

## 6. REST / MCP contract and compatibility

| New MCP tool | Corresponding REST operation | Key inputs / behavior |
| --- | --- | --- |
| `resolve_statistics_page` | `GET /api/v1/pages/resolve?url=` | exact URL/path, normalized page identity, view state or deterministic refusal |
| `read_statistics_page` | `GET /api/v1/pages/context?path=` | page path; `source_policy=as_published` default, `production_only`; `include_sections=true` default |
| `read_statistics_section` | `GET /api/v1/pages/section?path=&section=` | exact page and section/data ID, `source_policy`, optional `cursor=o:<n>` |

Results use the existing envelope `rs-intelligence.v1` and are byte-identical for the corresponding REST and MCP operations in the tested workerd/runtime cases. The page-read operation inlines at most **48 KiB** of sections; the section-read operation limits blocks to **96 KiB** or tables to **200 rows**. Ready-to-call `follow_up` instructions make large pages navigable without truncation being hidden.

All original **13 MCP tool names, ordering, read-only annotations and compatible input contracts** remain enforced, as do 15 original REST operations. The combined deployment requires precisely **16 MCP tools / 18 REST operations**. [PR #10](https://github.com/Reltroner/reltroner-statistics/pull/10) fixed a verifier mistake: the MCP SDK can omit the Zod default annotation for `include_sections` in `tools/list`. Its verifier now allows the metadata annotation to be absent or true **but checks omitted=true, explicit=true and explicit=false behavior on live MCP/REST**; contradictory types/defaults still fail. This was tested against unchanged production and in the [final main-push live acceptance](https://github.com/Reltroner/reltroner-statistics/actions/runs/44254064537).

Page-scoped evidence IDs such as `page:<page id>#<data id>:<n>` are **not** identical to global `trace_evidence` IDs; existing `CRD-…`, `NAF-…`, `fact:…` and narrative entity IDs retain their own evidence-resolution semantics.

## 7. Security, privacy and resource limits

- **SSRF isolation:** pasted URL parsed as data only; no outbound fetch of caller-supplied addresses; exact origin, path and registry checks. Tests include 4,000 invalid URL inputs.
- **Read-only:** no tools capable of write, delete, execution, arbitrary fetching, repository editing or canon mutation.
- **Fixed budget:** request body 16 KiB, response 256 KiB, existing query-string ceiling 2,048 characters (414), section ID 120 chars, up to 6 URL parameters of 160 chars, fragment 120 chars, mirror ≤ 240 KiB, registry chunks ≤ 200 entries.
- **Public-only data:** mirrors contain public page `<main>` text and published Astro island data, not cookies, sessions, secrets, client state or browser scripts.
- **Prompt injection containment:** text is returned as evidence/data, not instructions for the model; Markdown representation escapes formatting that could change document structure.
- **Kill switch:** `RS_API_DISABLED=true` blocks `/api/v1/*` and `/mcp`. **It does not disable public static mirrors at `/ai/pages/*`.** Removing them requires a subsequent deployment without them; urgent blocking requires a separate owner-authorized Cloudflare rule.
- **Cache & CSP:** public mirrors have a bounded cache policy and public CORS; no new inline script or CSP relaxation. Existing Statistics-only Cloudflare Pages project, custom domain and origin guards remain unchanged.

## 8. Performance and non-functional isolation

At initial PAGE-004 implementation the build added approximately **1,219 files**, **12.6 MB**, and **2–6 seconds** of build time; the 48 JS and 2 CSS client bundles were byte-identical to baseline and existing HTML files were identical after removing the two alternate links. These are **original comparative measurements**, not promises about all future builds.

At 2026-11-18 SHA-005 regression, **50 JS/CSS bundles were byte-identical** to baseline. The combined build rendered **635 pages**, **642 PDFs** and **37,629 internal links**, with **634 mirrors**. Some built HTML files can differ across otherwise identical builds due to embedded `generated_at` timestamps; this does not justify suppressing checks for runtime changes.

## 9. Development and release history

| Stage | Commit / evidence | Outcome |
| --- | --- | --- |
| Owner ratification | Universal Page-Aware Intelligence architecture | Approved design, not automatic canon or release |
| Initial implementation | [PR #9](https://github.com/Reltroner/reltroner-statistics/pull/9), built on earlier main, CI green | 608/607 census, 3 read-only page tools; G8 provider-native acceptance not run |
| Reconciliation with CQ-003 | [combined CI #44101213896](https://github.com/Reltroner/reltroner-statistics/actions/runs/44101213896) | PR #8 exploration/evidence improvements preserved; strictly verified 13+3 tool profile |
| Production integration | [PR #9 merge](https://github.com/Reltroner/reltroner-statistics/commit/1dbca25ff3b8e12b1919038967bbfb23f8a4bfce) | Page-aware features released; deployment verifier initially reported SDK-default mismatch |
| Schema-verifier remediation | [PR #10](https://github.com/Reltroner/reltroner-statistics/pull/10), merged `92ad608…` | SDK-omitted default accepted only with runtime behavior proof; 19 live protocol checks passed in isolated workflow |
| Latest verified publication | [PR #11](https://github.com/Reltroner/reltroner-statistics/pull/11), merged `ed3abce…`; [CI #44254064537](https://github.com/Reltroner/reltroner-statistics/actions/runs/44254064537) | Deployment SHA verification PASS followed by live 16-tool PAGE-004 protocol PASS |

The former **draft** states of PR #8/#9/#10 are historical; each has since been merged. [PR #7](https://github.com/Reltroner/reltroner-statistics/pull/7) remains a separate draft acceptance/evidence workflow at this record date and is **not** silently equated with PAGE-004 provider acceptance.

## 10. Status, limitations and next research

**Live protocol acceptance: PASS** on pinned Statistics SHA `ed3abce95fd5c6f4371bd5e957ff7aa4d680909c`. **G8 provider-native client acceptance: PENDING** for the seven prepared browser-versus-MCP ChatGPT/Claude/Gemini cases; a model-generated self-report is not native tool-call telemetry. Browser access is a provider capability, not guaranteed by MCP availability.

No Studio/Remodeling write-back, worldbuilding canon ratification, H1/H2/H3 ratification or external data acquisition was authorized by this milestone.

**Primary implementation sources:** [PAGE architecture](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-AI-PAGE-004-ARCHITECTURE.md) · [PAGE contracts](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-AI-PAGE-004-CONTRACTS.md) · [PAGE security and client G8](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-AI-PAGE-004-SECURITY-AND-OPERATIONS.md) · [PAGE regression](https://github.com/Reltroner/reltroner-statistics/blob/ed3abce95fd5c6f4371bd5e957ff7aa4d680909c/docs/RS-AI-PAGE-004-REGRESSION-AND-PERFORMANCE.md). See the accompanying [operations runbook](./2026-11-18-rs-page-deployment-operations-runbook.md) and [acceptance ledger](./2026-11-18-page-aware-and-deployment-acceptance-ledger.md).
