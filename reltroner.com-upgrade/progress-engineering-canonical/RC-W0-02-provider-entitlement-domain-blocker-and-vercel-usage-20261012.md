# RC-W0-02 — Provider Entitlement, Resend Domain Blocker & Vercel Usage Evidence

> Observed: 2026-10-12 Asia/Jakarta (owner-provided screenshots and UI text).
> State: W0 read-only, **PARTIAL**. This is an evidence receipt, not implementation or vendor activation permission.
> Canonical: [Progress archive](./README.md) | [W0 work order](../02-w0-00-read-only-discovery-work-order-20261012.md) | [Engineering ledger](../01-engineering-progress-ledger.md).
> Source authority when inspected: documentation main `9733c5cc64adcc8b729f0795789a244633219a76`; Studio GitHub main `18b295f96ccb521b228a1855e79448158c09db15`; Studio resource main `6c6fb38f8ff3376c0789c15bcfe4d0cafc4d057e`.
> Evidence class: OWNER-SUPPLIED UI SNAPSHOT/TEXT, GIT-VERIFIED source references, and published vendor plan descriptions. No API secrets, payments, identifiable subscriber addresses or account IDs included.

## W0-AC08 — Web3Forms (PARTIAL; Free public plan verified, form NOT_CONFIGURED)

Official public pricing and authenticated onboarding show **Personal Free forever** with `250 monthly submissions`, `unlimited forms`, `unlimited domains`, `advanced spam protection`, `hCaptcha integration`, and a custom redirect page. The same screenshot lists reCAPTCHA and Cloudflare Turnstile under **Pro**, so do **not** design the zero-spend contact path assuming those are bundled in Personal Free. These are plan-level assertions, not per-account verified access-key readiness or delivered-message acceptance.

Authenticated UI still shows `Choose Your Plan` / `Create Your First Form`; no submitted form creation or access key in evidence. `Continue with Free Plan` / `Create Form` are provisioning actions and are **NOT** authorized during W0. Confirm free account selection, future recipient verification, spam/rejection/timeout behavior and usable fallback without showing the recipient address before implementation. Contact emails must never imply an accepted form response guarantees inbox delivery.

## W0-AC07 — Resend (PARTIAL billing, **BLOCKED sending domain**)

Resend Settings → Billing shows two subscriptions **Transactional: 3,000 emails at $0/month** and **Marketing: 1,000 contacts at $0/month**, with **no payment methods** listed. This demonstrates account plan capacity at the moment of observation; it does not establish exact daily limits, overage enforcement, automatic sends, unsubscribe behavior, or any delivery success.

Domains lists exactly one configured sender `resend.reltroner.com`, status **Failed**. **Sending-domain readiness is BLOCKED.** Do not send production email, present subscription/welcome workflow as functional, modify DNS, add new domains, generate API keys or press Verify as part of W0. Determine exact per-record failure first (DKIM, SPF, MX, propagation, ownership or other cause) from Resend Domains → domain details read-only, then compare to authoritative DNS read-only. Resend's updated domain verification UI may show per-record failure/timeline; do not infer which record failed until viewed.

Resend Metrics (last 15 days) shows **0 emails** and `0%` displayed deliverability/bounce/complaint. Because there were no observed sends, these percent values are **not an empirical deliverability assessment**. Audience shows **2 contacts, 2 subscribed, 0 unsubscribed**. These may be test contacts; no personal addresses are retained. Existing contacts are not proof of verified opt-in, delivery, or correct unsubscribe/re-subscribe semantics. Marketing sends/opt-in remain W6 gated.

## W0-AC06 — Cloudflare Workers AI (PARTIAL; model-list only)

The authenticated account can open Workers AI Overview/Usage and Models catalogue; the owner interface displays **243 model entries** across Cloudflare-hosted and third-party providers, including generative text and nontext models. The model listing is **discovery**, not evidence of free entitlement, per-model zero cost or access to third-party models. Account-specific Workers AI Free usage/neurons, payment/overage mode, exact allowed text-generation model and limits remain UNKNOWN.

Existing Workers & Pages workload shares an account with ERP/LMS; no Worker, inference, DNS, Turnstile, route or provider setting can be created/changed during W0. For the Navigator workstream W5, require a dedicated bounded no-spend model entitlement, deny-by-default model allowlist, per-user rate limiting, privacy guard, published-only retrieval and fail-closed quota behavior. Avoid assuming all 243 models are free.

## W0-AC05 — Vercel (PARTIAL; extra project dashboard evidence)

The owner browser is at `/reltroner/reltroner-studio/usage`, but graphs show aggregate `Total` and selectable `Projects` views; screenshots do **not yet prove** per-project attribution despite the project URL.

For an approximately last-30-days screenshot:
- Fast Data Transfer `2.63 GB / 100 GB` (incoming ~141.98 MB / outgoing ~2.48 GB).
- Fast Origin Transfer `5.52 GB / 10 GB` (incoming ~3.96 MB / outgoing ~5.51 GB).
- CDN Requests `134,236 / 1,000,000`; CDN Request CPU duration `47s / 1h`.
- ISR Reads `712,452 / 1,000,000`; ISR Writes `0 / 200,000`.
- Function Invocations `164 / 1,000,000`, displayed `156 Success` and `8 User Error` (**cause unknown; not automatically a production crash**).
- Build Time `4h / 100h`; 34 builds `Completed`, 0 `Errored` in displayed period; `Build CPU Minutes` ~7h14m; billed `Build Minutes` 0s.
- The 30-day rolling window is a snapshot, not projected monthly capacity. Do not use this as proof of a hard stop for commercial operations.

~71.25% ISR reads and ~55.2% Fast Origin Transfer versus displayed quota are monitoring risks, particularly if deployments or bot traffic rise. Project allocation, budget/overage policy, commercial Hobby eligibility and separate merge-vs-production release authority remain unresolved. No plan upgrade, deployment, provider activation, billing change or release is authorized.

## W0-AC10 / Browser QA method decision (PROPOSED, not automatic run approval)

The owner prefers using a Gemini IDE AI agent for a consolidated device/browser QA in local `npm run dev` instead of many manual screenshots. This is a useful **future local engineering method**, but W0 ratified work order forbids workspace writes and using an IDE agent to mutate the repository. Next.js `next dev` can write generated `.next` artifacts and compile code, and the current primary Windows checkout is **11 commits behind** production with 14 protected untracked Markdown files. Therefore W0 acceptance must not represent that dev run as production-parity QA. An [IDE browser-QA protocol](./RC-W0-AC10-gemini-ide-browser-qa-protocol-20261012.md) is archived as a bounded proposal: source-only audit and existing public-site UI review can be read-only now; local `npm run dev` should be performed in the **later owner-authorized isolated exact-SHA worktree**, or after explicit, recorded W0 exception to permit only generated dev-cache files. No auto-installation, source edits, tests/outputs in the protected primary checkout, localhost form submission or paid-provider probes.

## Gate disposition

| Acceptance | Status | Outstanding |
|---|---|---|
| W0-AC05 | PARTIAL | Project-attributed usage, release controls, Hobby commercial eligibility |
| W0-AC06 | PARTIAL/UNKNOWN_AI_ENTITLEMENT | AI Free/account/model quota, payment hard stop and Turnstile |
| W0-AC07 | PARTIAL with **BLOCKED_DOMAIN_FAILED** | Resend per-record DNS cause; sending verification; consent/unsubscribe |
| W0-AC08 | PARTIAL / NOT_CONFIGURED | Form account setup, recipient validation, spam/rejection tests |
| W0-AC10 | PARTIAL | Representative keyboard, scroll, focus, zoom, 320px/desktop, source-parity QA |
| W0-AC11 | PARTIAL | Provider cost matrix and fail-closed risks |
| W0-AC12 | PENDING | Owner W0 conclusion and separate code workstream authorization |

### Next consolidated evidence batch

1. Resend domain **details/status diagnostics only**, including redacted per-record failures, no DNS mutation.
2. Workers AI **usage/quota/billing model limits** and account payment status, no inference runs.
3. Vercel `Projects` breakdown for ISR Reads, Fast Origin Transfer and the 8 user-error events via available metrics/log detail, no deploy.
4. Browser QA via read-only production screenshots and agent source inspection now; deferred localhost dev within isolated exact-SHA worktree or by a separate explicitly authorized W0 generated-cache exception.

**No provider action or source implementation has been performed by this evidence receipt. Phase 1 NOT ACCEPTED; Phase 2 NOT ACTIVE.**
