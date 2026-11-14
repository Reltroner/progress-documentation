# Reltroner Statistics — Engineering and Production Archive

**Project:** [Reltroner Statistics](https://github.com/Reltroner/reltroner-statistics)  
**Published website:** [statistics.reltroner.com](https://statistics.reltroner.com)  
**Archive date:** **2026-11-14** (Asia/Jakarta)  
**Implementation commit accepted in this record:** `042aa46354b9253feb2c0d55e4c0ce1adbd3e7a6`  
**Record category:** Comprehensive chronological engineering archive, deployment operations and CI evidence.

## Archive contents

| Document | Contents |
| --- | --- |
| **[End-to-end engineering and production chronicle](./2026-11-14-end-to-end-engineering-and-production-chronicle.md)** | Initial requirements; production/remodeling source-of-truth; ETL, graph, Creative Intelligence and Decision Intelligence; AI-agent interruption/recovery; supervised ML sufficiency gates; RC-DEPLOY-01/02/03; incident lessons; final acceptance and residual risks |
| **[Operations and recovery runbook](./2026-11-14-operations-and-recovery-runbook.md)** | Windows PowerShell 5.1 safe synchronization; full CI commands; Cloudflare Pages/GitHub Actions GUI procedures; DNS/project isolation; deployment and live identity verification; common errors; rollback and credential rotation |
| **[Conversation and evidence ledger](./2026-11-14-conversation-and-evidence-ledger.md)** | Substantive owner requests and assistant actions reconstructed in chronological order, commit and PR IDs, screenshots/terminal outputs, workflow links, tested results, rejected approaches, final status and unresolved acceptance gates |

## Verified outcome at archival close

| Acceptance property | Recorded status |
| --- | --- |
| Statistics Engineering + Decision Intelligence CI | **Passed** |
| RC-DEPLOY-01 — Production readiness / release isolation and visual QA | **Passed** |
| RC-DEPLOY-02 — Local/GitHub parity contract and exact custom-domain release guard | **Passed** |
| Windows PowerShell 5.1 native Git stderr regression | **Fixed and passed CI** |
| RC-DEPLOY-03 — Dedicated Pages project and `statistics.reltroner.com` | **Live production deployment verified** |
| Local `main` / fetched GitHub `main` commit identity | **Verified** |
| Live website `build-info.json` / Statistics GitHub commit identity | **Verified** |
| One complete **new commit → CI → automatic publish** cycle | **Not yet independently demonstrated**; proposed RC-DEPLOY-04 |

Final version-identity evidence was supplied by the owner:

~~~text
LOCAL_MAIN_1_TO_1_GITHUB: VERIFIED (042aa46354b9253feb2c0d55e4c0ce1adbd3e7a6)
STATISTICS_PUBLIC_SHA_PARITY: VERIFIED (042aa46354b9253feb2c0d55e4c0ce1adbd3e7a6)
~~~

The final manual release was [GitHub Actions run #43587678915](https://github.com/Reltroner/reltroner-statistics/actions/runs/43587678915). Build, project/domain preflight, Pages publication and live build verification all passed.

## Architectural boundaries

The project **does not write** to `Reltroner/reltroner-studio` or `Reltroner/reltroner-studio-remodeling`. Source repository content, verified Studio live deployment and the Statistics production website are distinct states. Remodeling suggestions are not automatically production canon.

Only the **`reltroner-statistics`** Cloudflare Pages project and its single authorized custom hostname `statistics.reltroner.com` were involved. Protected DNS/nameservers and deployments for `reltroner.com`, `www.reltroner.com`, `lms.reltroner.com` and `hrm.reltroner.com` were not authorized for modification.

**Security:** No Cloudflare raw API token, secret value or account-specific private identifier is stored in this archive. Refer to GitHub Actions encrypted secrets by name only.

## Source-of-truth and historical interpretation

This is a dated engineering **archive**, not a live runtime monitor, an automatically updated canonical source contract or a full verbatim chat transcript. Evidence is attributed to linked GitHub PRs/CI runs or to clearly labeled owner-provided console and GUI observations. Dynamic source/digest values, CI counts, Cloudflare state and production commit versions may change on later releases.

Current operational implementation contracts remain in the [Statistics repository](https://github.com/Reltroner/reltroner-statistics/tree/main/docs), particularly [RC-DEPLOY-01](https://github.com/Reltroner/reltroner-statistics/blob/main/docs/RC-DEPLOY-01.md) and [RC-DEPLOY-02](https://github.com/Reltroner/reltroner-statistics/blob/main/docs/RC-DEPLOY-02.md). The latter explicitly supersedes the initial no-custom-domain bootstrap rule by authorizing exactly `statistics.reltroner.com`.
