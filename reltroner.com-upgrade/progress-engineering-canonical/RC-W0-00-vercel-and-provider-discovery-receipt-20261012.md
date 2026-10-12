# RC-W0-00 — Interim Evidence Receipt (2026-10-12)

**Status:** READ-ONLY W0 IN PROGRESS. This receipt has been published to the canonical GitHub documentation archive. Its publication is documentation-only and does not authorize application implementation, provider configuration or deployment.

## Authority / immutable source snapshots
- Ratification repository: `Reltroner/progress-documentation`, `main` = `f60c0d5dfbc356f5f5250769457040d383a0fbe5` (GitHub verified during this review).
- Studio source: `Reltroner/reltroner-studio`, `main` = `18b295f96ccb521b228a1855e79448158c09db15`.
- Resource source: `Reltroner/reltroner-studio-resource`, `main` = `6c6fb38f8ff3376c0789c15bcfe4d0cafc4d057e`.
- Windows primary checkout `main` = `d6969ddfbc5e7d98d49b1523259785125159e722`, 11 commits behind remote, same ancestry, 14 protected Markdown untracked, no tracked modifications (OWNER-REPORTED terminal output; GitHub compare corroborates ancestry).

## Vercel observations (OWNER-SUPPLIED GUI / LOGS)
- Hobby Active; no payment card added; AI Gateway $0 and auto-reload off; **no team budget** configured; do not equate 'no team budget' with a $0 hard cap.
- Current Production: Ready, `main`, commit `18b295f`, `www.reltroner.com`; this identifies deployment provenance only.
- Vercel production build log: Next.js 16.2.6 / Turbopack / Node 22.x; 2 vCPU and 8 GB; compilation 9.5s; TypeScript 5.9s; 440/440 static pages in 4.1 minutes with one worker; build completed around 5 minutes; `next-sitemap` generated 1 sitemap index and 1 sitemap; deployment completed; build cache ~159.64 MB uploaded. No failed build step in provided log.
- Build & Deployment PDF (5 pages): Root `./`; Ignored Build Step Automatic; 'Skip deployments when there are no changes to root directory or dependencies' Disabled; Deployment Checks: No checks configured; Rolling Releases Disabled; deployment retention 30 days shown for cancelled, errored, pre-production, production; Pro-only on-demand concurrency choices displayed; no proof of paid options enabled.
- Environment screen: Production tracks `main`, Preview tracks unassigned branches, Development via CLI. Git integration connected; no deploy hooks. Deployment protection screenshot indicates Legacy Standard Protection, but exact access to all preview routes and CI integrations not proven.
- Risk: pushing/merging to production-tracked `main` can trigger deployment. Separate owner gate for release (WEB-I18) needs a verified, explicit technical policy before the first implementation PR merge.
- Billing: Vercel Hobby eligibility for *commercial* use remains unresolved; actual current usage is not a blanket guarantee of future quotas or compliance. Project-specific resource usage not yet separately measured.

## CDN / browser evidence (OWNER-SUPPLIED SCREENSHOTS and GitHub source)
- `/images/background.webp` served Vercel HTTP 404, content-type HTML; static source `components/layout/ShellBackdrop.tsx` directly references URL and neither inspected Studio public tree nor resource repo contains that filename. This is a confirmed missing-asset reference at inspected SHA, not an instruction to purge caches.
- Three jsDelivr image requests served HTTP 200 with correct image media types. Cache headers: `public, max-age=604800, s-maxage=43200`, `Age=61`, `CF-Cache-Status=HIT`, `X-Jsdelivr-Version=main`; same-name update freshness is NOT verified. Current code resolves resource URLs via `@main`, not immutable commit SHA.
- Public Chrome Network screenshot shows Google Analytics script and `collect` events; privacy/consent behavior requires a further complete audit.

## W0 acceptance classification (evidence-specific, not final gate)
| AC | State | Key residual |
|---|---|---|
| W0-AC01 | PASS_SCOPED | Recheck mutable refs before future writes. |
| W0-AC02 | PASS_SCOPED_LOCAL_INVENTORY | Primary checkout behind; never mutate primary working tree; 14 untracked protected. |
| W0-AC03 | PARTIAL | More frontmatter/publication audit, actual negative route fixtures required at later scoped tests. |
| W0-AC04 | PARTIAL | Browser error inventory and same-name publish freshness untested. |
| W0-AC05 | PARTIAL | Build and deployment settings mapped; actual project resource quota, commercial-use compatibility, release gating unresolved. |
| W0-AC06 | PENDING | Cloudflare Free/Workers AI billing and entitlements account evidence missing. |
| W0-AC07 | PENDING | Resend domain, plan, quotas and unsubscribe controls missing. |
| W0-AC08 | PENDING | Web3Forms account/recipient/limits missing. |
| W0-AC09 | PARTIAL | Analytics observed; full cookies/iframe/tracker inventory missing. |
| W0-AC10 | PARTIAL | Home shown on mobile; creator vs reader journey not accepted; desktop route walkthrough missing. |
| W0-AC11 | PARTIAL | Domain cost boundary, threat and rollout proposals known; vendor placement not frozen. |
| W0-AC12 | PENDING | Final owner W0 gap acceptance and W1 bounded authorization separately required. |

## No-spend provider decision state (external documentation vs account-specific verification)
| Service | Official public free provision (not entitlement proof) | Account-specific decision |
|---|---|---|
| Vercel Hobby | Personal non-commercial use; finite usage; possible pause on over-limit. | PARTIAL; commercial context / traffic and W1 release plan pending. |
| Cloudflare Workers AI | Free: public docs show 10,000 neurons/day; selected models restricted to Paid; daily limit failures when exhausted. | UNKNOWN; inspect exact account plan/billing/model access. |
| Cloudflare Workers Free | Candidate bounded server endpoint only. | UNKNOWN; verify account and request limits. |
| Resend Free | Public pricing: 3,000 transactional emails/mo and 100/day, but separate contacts/marketing lifecycle is not inferred from those figures. | UNKNOWN; inspect domain verification, contacts, suppression, billing/overage and free marketing entitlements. |
| Web3Forms Free | Candidate ratified contact provider. | UNKNOWN; verify free quota, anti-spam, recipient ownership and fallback before activation. |

## Nonnegotiable stop conditions
No source edits, isolated branch/worktree creation, Git stage/commit/push/merge, secrets creation, provider activations, billing changes, DNS changes, Vercel deployments, cache purges, Cloudflare Workers AI inference or VPS/LMS service modifications in W0. No *absolute* zero-risk or debt-free certification is possible: evidence and reversible design instead.

## Next batched operator package
1. Run `RC-W0-00-local-readonly-discovery.ps1` **only** in PowerShell 5.1, examine aggregate nonsecret output; report untracked mismatch immediately. This script does not fetch or synchronize local checkout.
2. Capture **read-only** Cloudflare Workers/Workers AI/zone/Turnstile/plan/billing screenshots and quotas in one pass.
3. Capture **read-only** Resend free plan, verified sending domain state, contacts/unsubscribe/suppression and overage state in one pass; never show keys or personal subscriber records.
4. Capture **read-only** Web3Forms free plan, recipient verification state, quotas, abuse protection and fallback readiness; no live form submissions.
5. Capture **read-only** Vercel project-filtered usage (ISR, build minutes, storage and transfers); no configuration changes.
6. Capture UX snapshots on mobile and desktop for home, archive, entry, contact, and subscribe existence (or absence); note if data is unpublished and refrain from uploading private content.

## Owner gate
W0 is not complete. The next source implementation (W1) remains NOT AUTHORIZED. A final W0 acceptance and a separately scoped G2 PR/preview authorization are needed. This receipt is published to the canonical documentation archive; see [subsequent provider and UX evidence](./RC-W0-01-provider-and-mobile-ux-evidence-20261012.md). The W0 gate is still open and future source changes require separate owner approval.

## Dated correction — 2026-10-12 local-only background asset

The initial statement that the production asset was missing from the remote Git tree remains accurate, but later PowerShell read-only evidence confirmed `public/images/background.webp` **exists locally**. The Studio repository `.gitignore` excludes `public/images/`. Therefore the likely deployment issue is an ignored local-only file, not proof that the owner never had the image, and not evidence of a jsDelivr cache bug. No application source was changed. Extended details and additional provider evidence are in [RC-W0-01](./RC-W0-01-provider-and-mobile-ux-evidence-20261012.md).
