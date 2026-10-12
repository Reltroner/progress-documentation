# RC-W0-09 — Final Discovery Disposition & **Proposed** G1/W1 Entry

> **2026-10-12 G1 DECISION UPDATE (addendum, historical proposal preserved):** The owner subsequently **approved G1 W0 discovery closure with residual risks retained**; this proposal's original `G1=PENDING_OWNER` language is now **historical pre-decision state**, not the current status. See [RC-W0-10 owner G1 ratification](./RC-W0-10-owner-g1-ratification-and-discovery-closure-20261012.md). `G2=NOT_AUTHORIZED`; see the separate [RC-W1-01 proposed G2 work order](./RC-W1-01-proposed-g2-first-contact-creator-reader-ia-work-order-20261012.md). No WEB-AC was waived.

> **Document class:** OWNER-REVIEW PROPOSAL, **NOT OWNER-RATIFIED G1** and **NOT W1 implementation authorization**.
> As-of: 2026-10-12 Asia/Jakarta, after [RC-W0-08](./RC-W0-08-authoritative-dns-timeouts-and-cloudflare-zone-absence-20261012.md).
> **Document evidence:** summarized reviewed receipts RC-W0-00…08 and the [W0 acceptance work order](../02-w0-00-read-only-discovery-work-order-20261012.md).
> **Immutable source snapshot reviewed for planning:** Studio `18b295f96ccb521b228a1855e79448158c09db15`; resource `6c6fb38f8ff3376c0789c15bcfe4d0cafc4d057e`; documentation initial snapshot for this review `03db213d1112fd0f630567f482aa39acdd01fc50`. These are dated values; check fresh before any future implementation.
> **No authority to modify:** `reltroner-studio`, resource repository, 14 protected local untracked Markdown, Vercel, Cloudflare, DNS, Resend, Web3Forms, API keys, billing, production, LMS, HRM.
> **Decision requested from owner:** Does G1 accept **completed W0 discovery with explicitly accepted downstream blockers**, leaving each actual issue to W1–W7? If not, record which exact W0 residual needs one more read-only evidence check.

## 1. Final W0-AC01…W0-AC12 evidence matrix (no invented global PASS)

| W0 AC | Reviewed evidence and limitations | Final discovery reviewer disposition | Residual workstream / guard |
|---|---|---|---|
| AC01 GitHub | Docs/Studio/resource repos and GitHub SHAs verified from connector, source and contract paths known | **PASS_SCOPED** dated snapshots | Recheck exact remote main SHA before G2 |
| AC02 primary checkout | Owner local git main HEAD `d6969dd`, zero tracked edits, 14 protected untracked files, one worktree; later IDE reported same state | **PASS_SCOPED_OWNER_REPORTED** | Fresh read-only preflight; no primary checkout writes, clean/reset/add-all |
| AC03 routes/content | Next route/build tree, `lib/utils/content.js`, markdown source, existing reading/search behavior inspected; published-only entry path not negative-tested | **PARTIAL** | W1 taxonomy IA design, W2/public-index; W4/W7 draft leak negative suite |
| AC04 image/CDN | Production `/images/background.webp` 404, local ignored asset; jsDelivr mutable `@main` and image caching observed; no same-name refresh automation proof | **PARTIAL / KNOWN_DEFECT** | W3 immutable SHA resolver, fallback and fault injection |
| AC05 Vercel | Hobby active, production mapped `main`, build succeeded 440/440 static pages; 30-day team/URL-scoped totals + Studio project 12h observability; commercial-use allowance and precise preview/overage posture not finally certified | **PARTIAL** | G2/G4 cost/preview gating; no paid plan, no unapproved preview |
| AC06 Cloudflare | Workers Free Active, zone Free Plan Active, no card on file, no invoices in owner screenshot; AI inference meter UI not exposed and model entitlement unverified | **PASS_SCOPED_PLAN / PARTIAL_AI** | W5 only: per-model cost/limit/fail-closed and privacy before inference, no paid trial |
| AC07 Resend | Free entitlement screenshots, sender `resend.reltroner.com` Failed; DKIM TXT, sending TXT SPF, MX Failed; recursive two-resolver absence, Cloudflare active zone owner GUI no matching records; direct authoritative requests **timeout including SOA**, not NXDOMAIN | **BLOCKED_SENDER / DIAGNOSIS_SCOPED** | W6: separate owner DNS write authorization and end-to-end lifecycle, no test send in W0 |
| AC08 Web3Forms | Account onboarding & Personal Free quota 250/month shown; no form created/recipient verified, no live submit | **PARTIAL / NOT_CONFIGURED** | W6: correct recipient, basic anti-spam and fallback, provider accepted != delivered |
| AC09 privacy | GA tag GET 200 + analytics collect POST 204 + _ga cookies; owner fresh Incognito reports `_ga`/collect with no visible consent UI; components initialize without an in-component gate; reCAPTCHA iframe on contact | **PARTIAL / P1 CONTRACT GAP DISCOVERED** | W4 mandatory WEB-I13/WEB-AC19 action: accurate notice and pre-consent control or removal; no specific legal adjudication |
| AC10 UX | Desktop/tablet/502px Gemini QA scoped positives; true 320px operator DevTools screenshots including clipped captcha candidate; native agent 320/375 full keyboard and 200% zoom unavailable; creator/reader hero absent | **PARTIAL / GAPS MAPPED** | W1 creator/reader; W2 rail/focus, W6 contact widget, W7 native mobile/zoom |
| AC11 risk+cost+W1 | Ratified provider boundary, no-spend and threat model documented; cross-provider cost unknowns remain; **this receipt adds a proposed exact minimal W1 file allowlist** rather than claiming tested operation | **PARTIAL / REVIEW_PROPOSAL_READY** | Final W1 G2 must gate cost, source, privacy, publication, rollback/preview; no extra charges |
| AC12 owner W0 closure | No explicit owner G1 acceptance after this consolidated review yet | **PENDING_OWNER** | Require the exact owner decision and accepted deferrals below |

**Meaning:** W0 source/provider/UX diagnosis is sufficiently mature for owner **G1 review**, but non-PASS individual ACs and provider blockers remain recorded. Do **not** label all twelve PASS. Documentation-only publication does not grant next-stage authorization.

## 2. Hard inherited issue owners and W1 non-dependencies

| Priority | Issue / live production observation | Owner scope | Must be fixed before |
|---|---|---|---|
| P1 | Creator vs Reader primary hero CTA paths absent; first-contact IA must reflect real offerings | **W1**, WEB-I03, WEB-AC01–04 | W1 completion and Phase 1 website DoD |
| P1 privacy | Fresh-session GA tracking without visible consent gate, source consistent with unconditional GA initialization | **W4**, WEB-I13, WEB-AC19 | W4 exit and website production DoD; no claims of no tracking before fix |
| P1 provider blocker | Resend `resend.reltroner.com` failed; required DNS records absent in owner Cloudflare zone view | **W6**, WEB-I12, WEB-AC16/17/25 | Newsletter production enablement and website DoD; no DNS edits under W1 |
| P1 future trust | Public source publication/draft negative tests and unsafe HTML sanitization are unverified | **W4/W7**, WEB-I05/I13, WEB-AC06/20 | Public index/AI exposure and website DoD |
| P2 | `/images/background.webp` HTTP 404 and ignored production asset | **W3**, WEB-I08, WEB-AC10–12 | W3 exit and website DoD |
| P2 candidate | 320px Google reCAPTCHA right clipping (visual), keyboard reachability not proven | **W2/W6/W7**, WEB-I07/I11, WEB-AC09/18/22 | Contact and accessibility exit |
| Quota risk | AI per-model Free status not shown; Workers Free is not a universal AI inference entitlement | **W5**, WEB-I10/I14, WEB-AC13–15/25 | Any real AI inference or public API enablement |
| Cost risk | Vercel Hobby future commercial suitability, preview build limits and provider hard-stop unresolved | **G2/G4/W7**, WEB-I14/I18, WEB-AC25/26 | Paid/commercial marketing activation, previews/production release |

**Dependency rule:** W1 IA source PR can be designed as a self-contained nonproduction text/layout change, independent from fixing DNS/GA. It may not worsen, remove concealment of, or falsely claim resolution for W4/W6 blockers. Published-route side effects and production default-branch auto-deploy remain separate G5/G6 matters.

## 3. Proposed smallest W1-G2 source slice (NOT AUTHORIZED)

**Proposed work order:** `RC-W1-01 — First-Contact Creator/Reader Information Architecture Slice`.

**Target user outcome:** On `/`, first-time readers understand the two strategic entry paths (creator seeks framework/proof, reader seeks spoiler-safe Asthortera) with real destinations and honest availability. A secondary collaborator/engineering route must remain discoverable; current ecosystem app links must not disappear silently.

**Proposed source:** `Reltroner/reltroner-studio`, **base commit only after freshly verifying current GitHub main SHA**; currently reviewed snapshot `18b295f96ccb521b228a1855e79448158c09db15`.

**Smallest candidate allowlist (3 existing TSX files, exact paths):**
1. `app/page.tsx`
2. `components/ecosystem/EcosystemHero.tsx`
3. `components/ecosystem/UseCasePathways.tsx`

These were independently fetched at the reviewed Studio SHA and are **existing** files. The hero currently has `Explore Ecosystem`, `Browse Knowledge Base`, `Open LMS`; the pathway list currently has `For learners`, `For builders`, `For HR/admins`, `For lore readers`, `For partners/recruiters`. No first-contact Creator/Reader pair is established on hero. New content labels/copy/route destinations must refer to real published routes and must be checked in read-only discovery before implementing. If correct IA requires changes outside three paths, **STOP and request separate G2 scope**, not broad edits.

**Explicit exclusions:** `app/layout.tsx`, `components/GoogleAnalytics.jsx`, `components/RouteAnalytics.jsx`, `lib/gtag.js`, `app/contact/page.jsx`, DNS/Resend/Cloudflare/Web3Forms, `content/**`, `public/images/**`, all `package*.json`, `.env*`, `next.config.mjs`, release config, other services, user drafts and resource repo. No new dependencies, no implicit broad taxonomy migration or parallel W2 search rewrite.

**Execution environment after separate G1 + G2 owner approvals only:** use independent isolated Windows worktree at exact verified Git SHA on unique `phase1/w1-creator-reader-ia-...` branch; primary working tree protected. No automatic `git fetch`, new worktree, branch creation, `npm run dev`, `npm install`, formatting/build/preview or push during W0. All new UI/logic must remain TS/TSX TypeScript-first.

**Proposed evidence/acceptance for the eventual W1 PR:**
- Direct distinct prominent Creator/Reader CTAs at responsive desktop+mobile, no invented offering/paid promises, durable keyboard focus, safe external link handling.
- Two real routes with published content, no draft/sitemap surprise, spoiler-safe Reader entry, creator proof reachable.
- Third collaborator/engineering lens remains findable.
- AppDock/LMS/HRM current link behavior regression sampled; do not rewrite SSO or linked services.
- Exact changed file allowlist and `git diff --check`, `npm run typecheck` or `npm run lint` as scripts exist, `npm run content:validate`, `npm run build` only in explicitly approved isolated worktree; build can consume resources and does NOT prove production privacy/safety.
- Before any Vercel Preview: verify project Git integration/pull request automatic deployment cost behavior, ensure no unapproved billing and get G4 owner approval. Main merge must be treated as **potential automatic production deployment**, requiring separately satisfied G5/G6 owner releases.
- Rollback concept = preserve exact accepted base SHA and independent branch/PR; actual revert/redeploy needs explicit owner plan and cannot guarantee zero incident.

**Do not create a GitHub issue/branch/PR or change Studio source from this proposal.**

## 4. Contractual W0 decision for owner (G1) — not implicit

The owner may choose one of these explicit dispositions:

**Option A — Approve G1 W0 discovery completion with recorded downstream blockers:** Accept the evidence matrix and **defer IMPLEMENTATION of** W3 broken image, W4 privacy consent, W5 AI Free model verification, W6 Resend DNS/Web3Forms lifecycle, and W2/W7 mobile/zoom suites to their ratified workstreams. This is NOT a waiver of any `WEB-AC01..27`; Phase 1 DoD still needs mandatory pass evidence. Any genuinely missing W0 observation needed for safe G2 must remain a G2 STOP.

**Option B — Keep G1 W0 open with named extra read-only requirement:** Identify the specific issue and the exact missing W0 evidence, not a general request to repeat all vendor dashboards. No source work.

**If Option A:** G1 acceptance must be separately followed by a **distinct, scoped G2 owner decision** on `RC-W1-01` exact SHA, three-file allowlist, isolated worktree and local test permissions. A G1 declaration alone is NOT a W1 code authorization; G2 is NOT a merge or deploy approval.

### Suggested explicit owner decision text (not executed)

```text
Saya [menyetujui / menunda] G1 penutupan discovery W0 berdasarkan RC-W0-09.
Jika menyetujui, saya menerima residual berlabel PARTIAL/BLOCKED
sebagai kewajiban W2–W7 yang TIDAK dihapus dari WEB-AC01..27.
Saya belum memberikan G2 izin perubahan source W1, izin DNS,
provider setup, preview, merge, atau production deployment.
```

**Current recorded state:** `G1=PENDING_OWNER`, `G2=NOT_AUTHORIZED`, `W1–W7=HOLD`, `Phase 1=NOT ACCEPTED`, `Phase 2=NOT ACTIVE`.

## 5. Financial and security boundary at W1 entry

- **Rp0 additional cash remains binding**. Vercel Hobby source/preview usage and any account commercial restrictions cannot be assumed solved; no plan upgrade.
- All production GA third-party analytics remain a **known P1 non-remediated risk**, even if W1 UI changes are eventually previewed. W1 must not hide/understate it.
- No unsanitized HTML publication/public search or public AI inference expansion in the three-file slice.
- Web3Forms and Resend are distinct provider journeys; a contact form must never auto-enroll a mailing list.
- Protected owner `content/music` (12) + `content/places` (2) are never touched; fresh local file/status inventory required before creating authorized worktree.
- Separate privacy/security/rate-limit approval required before any provider keys or AI runtime.

**Final recommendation:** present this document for G1 explicit signoff; do not start implementation or DNS edit while G1/G2 remains unapproved. If W0 closes, maintain downstream remediation as mandatory exit-gated debt rather than pretending the site is already production-ready.
