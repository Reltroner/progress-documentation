# Reltroner.com — Canonical Engineering Progress Archive

> Directory: `reltroner.com-upgrade/progress-engineering-canonical/` (note: **canonical**, not the former typo `canocical`).
> Scope: sanitized progress documentation and timestamped evidence. **Current phase: W0 READ-ONLY DISCOVERY IN PROGRESS**, W1–W7 HOLD, Phase 1 not accepted, Phase 2 not active.
> Parent authority: [Architecture Contract](../00-ratified-frontend-architecture-contract-20261012.md) → [W0 Work Order](../02-w0-00-read-only-discovery-work-order-20261012.md) → [Release Governance](../05-source-workspace-and-release-governance.md) → [Acceptance Traceability](../03-phase1-acceptance-and-invariant-traceability.md).
> [Live engineering progress ledger](../01-engineering-progress-ledger.md) is the summary index; dated receipts here preserve evidence and residual risks.

## Current receipts

| Artifact | Scope | Gate |
|---|---|---|
| [RC-W0-00 — Vercel, baseline, browser and source discovery](./RC-W0-00-vercel-and-provider-discovery-receipt-20261012.md) | Git SHAs, local protection, Vercel production/build, CDN 404/freshness and privacy baseline | W0 PARTIAL, with scoped PASS for Git/source inventory |
| [RC-W0-01 — Provider, Vercel usage and 320px responsive UX](./RC-W0-01-provider-and-mobile-ux-evidence-20261012.md) | Cloudflare Workers account, Web3Forms onboarding, Resend profile, Vercel aggregate usage, desktop/mobile UX and outstanding acceptance checks | W0 PARTIAL; no provider activation |

## Publication policy

This directory is the **canonical publication target** for Reltroner.com progress engineering: discoveries, reproducible build/test/CI reviews, risk/gap/decision receipts, later workstream evidence, previews, release/rollback receipts and sanitized handoff records. Once user-authorized and safe, publish directly to `Reltroner/progress-documentation` `main` (with a rechecked HEAD and exact file SHA) rather than requiring a local Markdown download and re-upload.

Every document must identify: observation timestamp, actors and source evidence type, exact relevant source SHA, affected W0/WEB acceptance criteria and WEB invariants, observed outcome, limitations, residual risks, incremental spend impact, authorization boundary, and next gate. Correct historical mistakes through dated addenda or explicit correction notes; never disguise an earlier PARTIAL as PASS. No contact addresses, subscriber records, credentials, authentication material, payment identifiers, unredacted request headers, or confidential texts.

**Important:** a documentation merge to `progress-documentation` cannot authorize mutations to `reltroner-studio`, `reltroner-studio-resource`, Vercel, Cloudflare, Resend, Web3Forms, VPS, LMS, HRM, DNS, paid APIs, or owner-local content. W0 explicitly forbids all those mutations until separately authorized. A successful Vercel build is not UX, privacy, provider quota, security, or Phase 1 completion evidence.

## Status conventions

- `PASS_SCOPED`: specific evidence verified within defined bounds.
- `PARTIAL`: evidence exists but required dimensions remain open.
- `PENDING`: evidence not yet acquired.
- `BLOCKED`: prerequisite conflicts with an engineering invariant or must be resolved by owner decision.
- `UNKNOWN`: account-specific provider entitlement or configuration is not visible.
- `NOT_CONFIGURED`: provider shows onboarding or no operational object, not failure.

See the parent ledger for phase-wide gate status.