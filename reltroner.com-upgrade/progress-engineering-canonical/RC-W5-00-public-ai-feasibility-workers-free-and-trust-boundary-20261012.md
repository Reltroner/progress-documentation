# RC-W5-00 — Read-Only Reltroner Navigator AI Feasibility: Cloudflare Free Quota and Trust Boundary

> **Classification:** `W5_PUBLIC_RESEARCH=COMPLETE_SCOPED`, **`ACCOUNT_ENTITLEMENT=UNKNOWN`**, **`AI_INFERENCE_RUNTIME=NOT_TESTED`**, **`W5_SOURCE_AND_PROVIDER_ACTIVATION=NOT_AUTHORIZED`**. Reviewed 2026-10-12. No authenticated Cloudflare account API/provider calls or deployments were made.
> **Binding:** [WEB-I09/10/14](../00-ratified-frontend-architecture-contract-20261012.md), [WEB-AC13/14/15/25](../03-phase1-acceptance-and-invariant-traceability.md), [zero-spend contract](../04-zero-incremental-spend-and-provider-boundaries.md), W2 [single public index proposal](./RC-W2-00-public-content-index-epistemic-and-search-contract-proposed-20261012.md).
> **Snapshot:** W0 owner screenshots report Workers Free active, Free zone active, and no attached card at observation; do not equate Workers Free with access to any arbitrary Workers AI model.

## 1. Official pricing/status research — public provider, not owner-specific proof

Cloudflare's official [Workers AI pricing, updated Oct 1, 2026](https://developers.cloudflare.com/workers-ai/platform/pricing/) states an included **10,000 neurons/day** for Workers Free/Paid, with free plan requests exceeding limit failing rather than charging unless upgraded. Workers Paid bills usage above free allocation; do not activate Paid. Some named resource-intensive models **require a paid billing method**, as also documented in [July 28 model entitlement change](https://developers.cloudflare.com/changelog/post/2026-07-28-models-require-workers-paid/). Examples still described as available to Workers Free on that change page: `@cf/zai-org/glm-4.7-flash`, `@cf/google/gemma-4-26b-a4b-it`, `@cf/nvidia/nemotron-3-120b-a12b`. These examples **are not an owner-account entitlement certificate** or automatic model-quality approval.

Official [Workers Free limits](https://developers.cloudflare.com/workers/platform/limits/) currently include **100,000 requests/day**, separate from inference neurons; model-specific request limits, token cost and total-neuron billing still matter. [Workers AI inference limits](https://developers.cloudflare.com/workers-ai/platform/limits/) additionally document per-model/task restrictions. Wranglers' local AI inference tests can count against provider limits; therefore no “free local provider test” without separate owner consumption approval.

**Feasibility disposition:** A no-cash, bounded generative AI is plausible, **NOT YET VERIFIED**. Keep W5 model/account/latency/quality and no-overage behavior `CONDITIONAL`; never transform the ratified real-generative-AI feature into an FAQ-only chat and claim full acceptance.

## 2. Proposed architecture

- Global branded **Reltroner Navigator** launcher on public pages, accessible, bottom right, nonblocking of contact/privacy/reading rails. Plain-language welcome, reset, quick navigation and failure states.
- A deterministic **public-only W2 index** supplies retrieval snippets with source paths and exact revisions. Server owns model prompt assembly, truncation and quotas; browser does not supply trusted document metadata. No retrieval of unpublished Markdown or source file paths; no direct GitHub private refs.
- Narrow API boundary on approved Free Cloudflare Worker as a **candidate**, with token-free browser frontend requests subject to per-IP/session rate limits, bot/abuse controls, byte/input caps, output-token caps, concurrency cap, quota budget reserve (manual or hard-stop), response citations and safe error states.
- System separates `FICTION_CANON`, `FICTION_SPECULATIVE`, `REAL_WORLD_ANALYSIS`, `CREATIVE_FRAMEWORK`, `ENGINEERING_CASE_STUDY`, `CROSS_DOMAIN_ANALOGY`. Unsupported claims return uncertainty. Canon changes, arbitrary HTTP/shell/tool, Keycloak, SQL, LMS/HRM/VPS are **not accessible**.
- User-facing fallback if Free inference unavailable: clearly labeled **“AI temporarily unavailable; browse verified public resources”**. The fallback maintains usability but **does not itself satisfy WEB-AC14**.
- Privacy notice must describe inference processor, submitted prompt/cookies/retention/logging if applicable. Do not claim zero data transfer if provider receives prompts.

## 3. Required account-read-only and scoped future proof

Before owner authorizes any inference:
1. Owner/approved operator inspects **Cloudflare → Workers & Pages → Workers AI / AI Gateway billing** read-only for actual Free plan, model access, usage/counters, hard overage behavior, payment method/credit state; redact account identifiers and secrets.
2. Choose one **free-eligible** model based on current actual catalog; check supported input/output size, language quality, model availability and costs per 1,000 inference requests at realistic prompt+context size. Calculation must include reserve for bursts and a hard global daily limit that is stricter than provider quota.
3. Independently authorize a **small finite real inference pilot** with maximum number of tests and usage cap if Free entitlement is verified; account request is not yet approved by this documentation. Negative tests: quota/429, paid-only/403, provider capacity, oversize input, prompt-injection attempts, draft search, false citations, cross-domain fiction/real-world confusion.
4. If no free eligible quality model / robust hard-stop is available, record `W5=BLOCKED_COST_QUALITY` and request an explicit owner scope decision. **No paid upgrade and no fake generative claim.**

## 4. Engineering and W7 gates

W5A account entitlement read-only → W5B W2 publication/index + permission boundary tests → W5C distinct owner-authorized minimal backend/TSX allowlist and finite provider pilot → W5D true generative positive+abuse acceptance → W7 privacy/analytics/runtime/SEO and monitored quota release.

Current `W5_FEASIBILITY=PUBLIC_DOCS_PLAUSIBLE_ACCOUNT_UNVERIFIED`, not complete, not activated. The SaaS subscription and website global Phase 1 exit are unaffected.
