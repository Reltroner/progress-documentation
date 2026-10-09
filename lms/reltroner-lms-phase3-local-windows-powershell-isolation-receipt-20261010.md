# Reltroner LMS — Phase 3 Local Windows PowerShell 5.1 Verification and Contentlayer Isolation Receipt

> **Evidence received:** 2026-10-10 Asia/Jakarta. Original visible PowerShell log contains application log timestamps **2026-10-09 18:23–18:34** and the supplied console transcript was presented to the owner/assistant on 2026-10-10. Exact start/end wall-clock times of every command are not independently established.  
> **Status:** **BACKEND LOCAL PASS; FRONTEND CATALOG/VALIDATORS PASS; FRONTEND STATIC EXPORT + PRIVACY PASS UNDER IGNORED-STAGING LF NORMALIZATION; UNMODIFIED WINDOWS `npm run build` STILL NOT VERIFIED GREEN**.  
> **Security/architecture boundary:** No source commit, no change to application `main`, no permissions settings, no production deployment, no Phase 4 work order, no live Keycloak/DB/Redis testing. Existing Phase 3 scope remains FROZEN.

## 1. Inherited immutable SHA, CI and governance anchors

- LMS-BE local `main` and GitHub source merge SHA: `a2672d0085fe84b55520f8f52f41a8c7fc8568a0`; [owner-authorized PR #11](https://github.com/Reltroner/LMS-BE/pull/11), [postmerge `push:main` CI GREEN 7/7](https://github.com/Reltroner/LMS-BE/actions/runs/37970800113).
- LMS-FE isolated **detached worktree**, original `main` merge SHA: `cc3d9c132d293058c0ff37c93ef4b3ab5547ad34`; [owner-authorized PR #3](https://github.com/Reltroner/LMS-FE/pull/3), [postmerge `push:main` CI GREEN 2/2](https://github.com/Reltroner/LMS-FE/actions/runs/37970833082).
- Local backend path: `C:\Projects\lms-reltroner-backend`; original frontend path **preserved**: `C:\Projects\lms-reltroner-studio`; isolated FE test path: `C:\Projects\lms-reltroner-studio-phase3b-main-verify-20261010`.
- Historical source merge/tree identity and CI were recorded before local testing in [source-main integration receipt](./reltroner-lms-phase3b-main-merge-and-postmerge-ci-20261010.md). This local record appends new evidence; **it does not overwrite historical observations**.

## 2. Local baseline `v1`: environment prerequisite only

First PowerShell 5.1 validation script:
- `git fetch` + `git pull --ff-only` on clean LMS-BE/main succeeded; local BE SHA matched the pinned merge SHA.
- FE/main fetched; a separate, detached verification worktree was created at the exact FE merge SHA, leaving the dirty original FE workspace untouched.
- Early **environment blocker**: PHP `sodium` extension absent from CLI module list. No BE or FE tests executed in this first attempt.

Operator inspected PHP CLI 8.4.4 (ZTS, Windows), found `C:\Program Files\php-8.4.4\ext\php_sodium.dll` and `libsodium.dll`, backed up `php.ini`, enabled `extension=sodium`, and verified `php --ri sodium` reports **`sodium support => enabled`** and `php -m` lists `sodium`.

## 3. Local `v2`: substantive test receipt

On the exact pinned merged SHAs, after sodium was enabled:

| Stage | Observed evidence | Classification |
|---|---|---|
| BE local SHA/pull | `a2672d...`; `Already up to date.` | PASS |
| FE isolated detached SHA | `cc3d9c...`; original FE workspace untouched | PASS |
| PHP/Node prerequisite inventory | modules and version prerequisites verified | PASS |
| PHP syntax `contracts/tests/*.php` | 7 files `No syntax errors detected` | PASS |
| BE 6 contract harnesses | **22+22+42+23+136+10 = 255 PASS, 0 FAIL**; synthetic/model/fixture scope only | PASS_SCOPED |
| Laravel gateway | **20 tests, 140 assertions** | PASS |
| Laravel learning | **16 tests, 117 assertions** | PASS |
| Laravel mentorship | **16 tests, 117 assertions** | PASS |
| Laravel knowledge | **16 tests, 117 assertions** | PASS |
| Laravel assistant | **16 tests, 117 assertions** | PASS |
| Laravel audit | **16 tests, 117 assertions** | PASS |
| Six Laravel service total | **100 tests, 725 assertions; composer validate/install and PHPUnit suites success** | PASS |
| FE `npm ci` | 690 npm packages installed; deprecation warnings do not equal test failures | PASS |
| FE Node `node --test tests/catalog-contract.test.mjs` | **9 PASS, 0 FAIL**, including no-leak/deny fixtures | PASS |
| FE manifest | **3 published lessons**, 31 registered source MDX, content-only SHA256 `1dfecfddc97ce1676a719b1538e2d12d17a40c77f51370951dcf69e634b86e43` | PASS |
| FE TypeScript, ESLint, content/resource/orphan validations | all individually reported passed in `npm run build` execution | PASS |
| FE ordinary, unmodified Windows `npm run build` | Contentlayer frontmatter YAML parser rejected all 3 staged published MDX, `Generated 0 documents`, Next failed static export with misleading missing `generateStaticParams()` message | **FAIL / unresolved standalone platform path** |
| Runtime service-to-service Keycloak/PostgreSQL/Redis and production | not run, out of Phase3 scope | NOT_CERTIFIED |

**Important expected negative-test log noise:** Laravel `testing.ERROR: SENSITIVE_INTERNAL_MESSAGE_SHOULD_NEVER_LEAK` and stack traces were written by deliberate `InternalFailureBoundaryTest` exceptions. The corresponding tests **PASS** (verify external Problem Details/500 behavior). These logs alone are **not PHPUnit failures** and do not certify production log-redaction configuration.

## 4. Controlled A/B experiment: Contentlayer under Windows CRLF vs LF staging

A separate [conversation-provided PowerShell isolation script](#source-of-evidence), run against FE **detached worktree only**, verified `HEAD=cc3d9c...`, and checked git worktree clean plus `.public-content` ignored by Git.

**Read-only measurements of tracked source, with no source edits:**

| Original MDX lesson | CRLF sequences | LF-only sequences |
|---|---:|---:|
| `01-http-overview.mdx` | 39 | 0 |
| `02-http-methods.mdx` | 31 | 0 |
| `03-rest-introduction.mdx` | 31 | 0 |

The scripted procedure:
1. Ran the same production `node scripts/prepare-public-content.mjs`, staging **3 of 31** source MDX via the publication-only allowlist.
2. Converted **only the three ignored `.public-content` staged copies**, replacing CRLF/CR with LF, with UTF-8 no BOM. Changed staged files **3/3**; did not edit tracked `content/` originals.
3. Invoked `contentlayer build`: **`Generated 3 documents in .contentlayer`**, whereas baseline reported 0. **Caveat:** Contentlayer/Clipanion also printed `TypeError: The "code" argument must be of type number. Received an instance of Object` / `ERR_INVALID_ARG_TYPE` after generation. The PowerShell helper did not throw at this step and proceeded to Next.js; therefore the external process appears to have returned zero to the exit-code guard on that run **despite emitting an internal CLI exception**. This is a real unresolved tooling defect, not a clean Contentlayer CLI.
4. Invoked `next build --webpack` **without re-staging**: **compiled successfully, TypeScript PASS, page data collection PASS, `25/25` static pages generated**. Six route variants for three published lessons and course aliases were represented.
5. Invoked `node scripts/phase3b-catalog.mjs --verify-out`: publication-only artifact and privacy scan **PASS**, manifest SHA256 remained `1dfecfddc97ce1676a719b1538e2d12d17a40c77f51370951dcf69e634b86e43`.
6. Script ended `LOCAL FRONTEND STAGING + STATIC EXPORT: PASS`, reasserted the exact Git SHA and clean tracked/untracked worktree, original FE workspace preserved.

**Inference bounded by experiment:** The CRLF-to-LF staging change is strong causal evidence for the Contentlayer frontmatter YAML parse discrepancy on this Windows CLI setup, because the same unchanged Git source generated 0 published Contentlayer docs before normalization and 3 afterwards. It is **not** proof that all Contentlayer/Clipanion exceptions are solved, that the normal `npm run build` is already fixed, or that the environment behaves the same across other Windows machines.

The Next.js error `Page ".../lessons/[lesson]" is missing "generateStaticParams()"` was misleading at the baseline: the committed route module actually **exports `generateStaticParams()`**, and static page generation succeeded after Contentlayer produced 3 real documents. Thus a primary route-implementation defect was **not demonstrated**.

## 5. Exact acceptance classification and next independent remediation gate

**Observed:** Backend local contract/testing PASS; frontend 9 catalog checks PASS; frontend static build and publication privacy **PASS under explicit ignored staging LF normalization**. Both original merged source SHAs remain unchanged, tracked git worktrees clean, six-services and source-main CI remain green.

**Still not proven:** ordinary Windows `npm run build` on an unchanged CRLF checkout; clean Contentlayer CLI completion free of `ERR_INVALID_ARG_TYPE`; a source-controlled Windows portability regression guard. Do not convert the workaround proof into an unconditional `STANDARD_WINDOWS_BUILD_PASS` claim.

**Recommended tightly scoped FOLLOW-UP, not authorized in this receipt:**
- If desired, introduce an **explicit new FE-only portability-hardening work order/PR**. Prefer LF-normalizing only **publication-allowlisted, ignored `.public-content` staging** within `scripts/prepare-public-content.mjs`, not rewriting source MDX or touching the dirty original workspace. Add both CRLF and LF fixture coverage, preserve fail-closed deny-list and manifest SHA guarantees, and run ordinary `npm run build` on Windows + GitHub CI on Linux before any new merge.
- Diagnose Contentlayer/Clipanion `ERR_INVALID_ARG_TYPE` as an independent CLI/tooling defect; do **not** just suppress stderr or blindly treat exit code zero as proof. Require explicit 3-document count and output privacy validation.
- Execute any further source change **only after a distinct user instruction**. No Phase4 provisioning, production release, GitHub branch setting change, or automatic local-workspace reset/stash follows from this log.

## 6. Transferable summary

`PHASE3 OWNER ACCEPTED 28/28 SCOPED → BE/FE MAIN MERGED + PUSH MAIN CI GREEN → LOCAL SODIUM ENV REMEDIATED → BE CONTRACT 255/255 + 6 LARAVEL 100 TESTS/725 ASSERTIONS PASS → FE 9/9 CATALOG/PRIVACY PASS → WINDOWS NORMAL npm run build FAIL (CRLF MDX → 0 DOCS → MISLEADING STATIC PARAM ERROR) → IGNORED STAGING LF A/B: CONTENTLAYER 3 DOCS + NEXT STATIC 25/25 + PUBLIC ARTIFACT SCAN PASS → CONTENTLAYER CLI POST-GENERATION ERR_INVALID_ARG_TYPE REMAINS → NO SOURCE EDIT / PRODUCTION CHANGE / PHASE4 AUTH`.

## Source of evidence

- Original operator-shared Windows PowerShell 5.1 console transcripts, including version 1 initial sodium blocker, version 2 complete BE/FE attempts, and follow-up isolation transcript. These raw transcripts were **not committed** to avoid unintentionally archiving local paths and verbose synthetic exception stack traces into the public repository. Instead, this record contains the minimal security-conscious independently auditable aggregate.
- Pre-existing source contract [Phase 3 source-main integration receipt](./reltroner-lms-phase3b-main-merge-and-postmerge-ci-20261010.md).
- Frozen [Phase3B exit acceptance](./reltroner-lms-phase3b-11-final-owner-exit-acceptance-20261010.md).
