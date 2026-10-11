# RC-W0-00 — Read-Only Baseline, Cost & UX Discovery Work Order

> Status: **OWNER AUTHORIZED FOR READ-ONLY DISCOVERY ONLY** (ratification + start earliest workstream, 2026-10-12).
> Authority: [Ratified website contract](./00-ratified-frontend-architecture-contract-20261012.md), [ledger](./01-engineering-progress-ledger.md), [source governance](./05-source-workspace-and-release-governance.md).
> Explicit NOT authorized: source edits, new worktree/branch in the owner's computer, Git stage/commit/merge/push, Vercel/Cloudflare/Resend/Web3Forms paid activation, API key creation, DNS/TLS/caches purge, VPS/Keycloak/PostgreSQL/Redis operations, model inference probes using paid entitlements or production deployments.
> Check a fresh repo HEAD before treating any dated SHA as a write baseline.

## 1. Purpose, actors and execution

Goal: establish **observable baseline** and a testable smallest W1 implementation proposal without disrupting existing local content creation. Human operator handles private GUI evidence (redacted); ChatGPT handles architecture, source comparison and gate review; IDE AI agent **not needed for W0**. Production dashboards are inspection-only. No screenshot of API keys, authentication tokens, recipient email addresses, confidential messages or payment identifiers.

Execution order for each checkpoint: TUJUAN → FAKTA → GAP → RISIKO → SOLUSI → TOOLS/OWNER → OTORISASI → BUKTI.

## 2. W0 discovery checklist and acceptance IDs

| ID | Actor / mode | Required observable evidence | Stop if |
|---|---|---|---|
| W0-AC01 | GitHub connector read-only | Exact HEAD SHA for docs/studio/resource, repository ownership, branch default and current relevant source paths | Mismatch with alleged authority or missing repo |
| W0-AC02 | Owner PowerShell read-only | Studio primary local git status, branch, HEAD, remote and worktree list; report protected file list, no modifications | Unexpected tracked modifications, origin mismatch, local SHA drift not resolved |
| W0-AC03 | GitHub review | Route/layout/collection and markdown frontmatter catalog, legacy .js/.jsx boundary, search/TOC behavior | Unknown source trust or draft-publication gap |
| W0-AC04 | Browser/network read-only | Broken-image URLs and statuses, response headers, browser errors, jsDelivr @main caching and existing delivery settings | Cannot separate CDN origin from Vercel caches |
| W0-AC05 | Owner Vercel GUI read-only | Hobby plan, metered/budget enforcement, build/deploy quota, production vs preview domain and latest source, commercial-use applicability | Any non-zero unpredictable spending path |
| W0-AC06 | Owner Cloudflare GUI read-only | Existing zone/Pages/Workers and Workers AI Free availability/limits, payment state, Turnstile eligibility | Provider requires paid upgrade/automatic overages |
| W0-AC07 | Owner Resend GUI read-only | Existing verified sending domain, free contacts/emails, sender/setup requirements, API usage policy, suppression/unsubscribe | New payment obligation, missing privacy control |
| W0-AC08 | Owner Web3Forms GUI read-only | Free access key eligibility, quotas, spam policy, verified recipient, fallback address plan | Contact would be falsely 'success' |
| W0-AC09 | Browser/source audit read-only | Existing GA, RouteAnalytics, iframe/video/remote assets and cookie behavior; draft truthful notice | Privacy claim contradicted by active behavior |
| W0-AC10 | UX inspection | Home creator/reader comprehension, archive navigation, contact and subscribe journey, desktop/mobile screenshots | Unresolved mandatory user journey |
| W0-AC11 | Owner/architect | Domain cost matrix, public/privacy security threat model, rollout plan and exact W1 path allowlist | Model/use violates LMS or budget |
| W0-AC12 | Owner | W0 gap closure receipt: PASS_SCOPED/PARTIAL/BLOCKED by ID, accepted deferrals and explicitly separate W1 authorization | Missing hard requirement is silently deferred |

A PASS of W0 means **discovery completed with evidence and recorded residuals**. It does not assert a fixed site, working newsletter/chatbot, source implementation or production readiness.

## 3. Initial findings, source-only (not final W0 gate)

- Source HEAD inspected: Reltroner/reltroner-studio main 18b295f96ccb521b228a1855e79448158c09db15; resource HEAD 6c6fb38f8ff3376c0789c15bcfe4d0cafc4d057e. Current mutable refs must be re-read.
- Existing app/layout.tsx imports CommandPalette and GoogleAnalytics; GoogleAnalytics.jsx embeds a production GA tracking ID. Privacy banner language cannot assert no tracking without further review.
- lib/assets/cdn.js currently pins @main. next.config.mjs remote pattern similarly mentions @main. ArchiveCardMedia.jsx uses unoptimized true for jsDelivr; Vercel CDN purge must not be assumed to clear jsDelivr.
- app/contact/page.jsx uses existing Formspree + reCAPTCHA component, **not Web3Forms yet**.
- ContentEntryPage.tsx contains ReadingPath already, while editorial shell limits article width; sidebars can be relocated/refactored rather than recreated from zero.
- getCollectionEntries publicly filters published; getCollectionEntry has a distinct lookup path and uses remark-html sanitize:false. Perform actual negative tests later; do not assert a disclosure without evidence.
- Screenshot evidence shows Vercel Hobby, valid domain mapping and historical dashboard metrics; these do not establish live balance or commercial plan compliance.

## 4. Windows PowerShell 5.1 — safe local W0 command batch (copy/paste only in primary checkout)

This is READ-ONLY, with no git fetch/pull/reset/clean/checkout or writes. It does not print .env or Markdown contents.

~~~powershell
$ErrorActionPreference = 'Stop'
$Repo = 'C:\Projects\reltroner-studio'
if (-not (Test-Path -LiteralPath $Repo -PathType Container)) { throw 'Studio repo not found; stop.' }
Write-Host '=== W0 LOCAL NON-MUTATING INVENTORY ==='
Get-Date -Format o
git -C $Repo remote get-url origin
git -C $Repo branch --show-current
git -C $Repo rev-parse HEAD
git -C $Repo status --porcelain=v1 --untracked-files=all
git -C $Repo worktree list --porcelain
Write-Host '=== END W0 ==='
~~~

Verify origin is Reltroner/reltroner-studio, preserve all untracked files. The 2026-10-12 owner status listed 14 untracked Markdown files; do not stage or infer their absence from remote GitHub. If local output changed, record it as a new snapshot and STOP any later worktree mutation.

### 4.1 Protected owner-reported files at entry

~~~
content/music/astrostelia-the-astronomers-horizon.md
content/music/astrostelia-the-waltz-of-falling-stars.md
content/music/cenrestier-the-eternal-citadel.md
content/music/cenrestier-where-the-fortresses-stand.md
content/music/depcutland-the-grand-library.md
content/music/reltronland-the-pursuit.md
content/music/stelpadland-across-the-quiet-lake.md
content/music/stelpadland-adventure-awaits.md
content/music/stelpadland-keep-moving-forward.md
content/music/stelpadland-snowfall-in-stelpadland.md
content/music/stelpadland-the-open-trail.md
content/music/stelpadland-the-wild-and-the-warm.md
content/places/reltronland-map-scale-architecture.md
content/places/skytropolis.md
~~~

## 5. Browser and provider GUI protocol

- Developer Tools → Network → Disable cache only as a **local test mode**; inspect exact failing image Request URL, status, content-type, response headers and console. Repeat normally cached; compare source bytes or ETag where present. No purge command.
- Vercel: observe project Plan/Billing/Budgets, Deployments source SHA, Domains/root redirect, Cache dashboard and Speed Insights availability **without clicking enable, purge, deploy or rollback**.
- Cloudflare: observe zone settings, Workers/AI Free available quota, billing mode and any present Turnstile settings; **do not toggle**.
- Resend: observe account Free entitlement, verified domain status, sending reputation/deliverability prerequisites, Contacts and unsubscribe; **do not generate/paste API key**.
- Web3Forms: observe free tier and recipient validation; **do not submit live public test unless a later test work order authorizes it**.
- Record redacted outcomes: AVAILABLE_FREE, REQUIRES_PAYMENT, UNKNOWN, NOT_CONFIGURED or BLOCKED. Do not invent balances.

## 6. Exit artifact and STOP policy

Publish a W0 receipt in the ledger with each AC ID and evidence class; crosslink to the 18 WEB invariants and cost gates. Gate to W1 only after owner accepts the W0 result and a new exact-SHA nonproduction PR scope. Unresolved financial exposure, unpublished-content leak, unprotected local authoring or provider account mismatch = STOP. No automatic upgrades, no broad IDE-agent prompts.
