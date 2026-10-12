# RC-W0-08 — Direct Authoritative DNS Timeouts, Cloudflare Records Absent, Resend W6 Handoff

> **Timestamp:** 2026-10-12T17:49:18.9739190+07:00 (owner PowerShell 5.1); owner GUI conclusion received immediately afterward.
> **Mode:** read-only discovery; **W0 IN PROGRESS**; owner W0-AC12 / G1 signoff NOT GRANTED.
> **Evidence:** OWNER_WINDOWS_POWERSHELL_OUTPUT + OWNER_CLOUDFLARE_DNS_GUI_CONCLUSION; not a reviewer-executed DNS packet trace. The earlier 1.1.1.1 / 8.8.8.8 recursive results are recorded in [RC-W0-07](./RC-W0-07-resend-dns-nxdomain-and-incognito-ga-consent-20261012.md).
> **Relevant source baseline rechecked:** Studio GitHub `main` = `18b295f96ccb521b228a1855e79448158c09db15`; Resource GitHub `main` = `6c6fb38f8ff3376c0789c15bcfe4d0cafc4d057e`.
> **Governance:** [W0](../02-w0-00-read-only-discovery-work-order-20261012.md), [WEB-I12/WEB-I14](../00-ratified-frontend-architecture-contract-20261012.md), [WEB-AC16/17/25](../03-phase1-acceptance-and-invariant-traceability.md), [Source/Release](../05-source-workspace-and-release-governance.md).
> **Sensitive data:** Do not record Resend full DKIM TXT value, provider credentials, billing IDs, browser cookies or owner contact emails.

## 1. Exact observed DNS result, not over-interpreted

Owner PowerShell 5.1 called `Resolve-DnsName -DnsOnly -Server` directly for two DNS hostnames advertised by previous public NS lookup:
- `nicolas.ns.cloudflare.com`
- `millie.ns.cloudflare.com`

At **both** server names:
- `SOA reltroner.com`: `LOOKUP_FAILED: This operation returned because the timeout period expired`.
- `TXT resend._domainkey.resend.reltroner.com`: **timeout**.
- `TXT send.resend.reltroner.com`: **timeout**.
- `MX send.resend.reltroner.com`: **timeout**.
- `CNAME send.resend.reltroner.com`: **timeout**.

**Inference limit:** Ten timeout reports, including apex SOA, mean no usable direct authoritative answers were obtained. These are **NOT** authoritative NXDOMAIN, NODATA, SERVFAIL or proof Cloudflare's servers were down. Local upstream networking/UDP-53 filtering, DNS transport, resolution of `-Server` target, and routing could explain the pattern; no network packet/transport diagnosis was executed. Therefore `AUTHORITATIVE_DNS_PROBE_INCONCLUSIVE_TIMEOUT`.

Owner separately inspected **Cloudflare → reltroner.com zone → DNS → Records** using a Resend-related filter and reports exactly `CLOUDFLARE_RESEND_RECORDS_ABSENT`. This is **OWNER_GUI_REPORTED**, not an API export of every zone record. It strongly supports missing records in the **inspected active zone**; ensure correct zone, dashboard account and exact FQDN construction before later editing. The prior public recursive resolvers `1.1.1.1` and `8.8.8.8` also failed to find the three expected Resend records. Together with Resend's **domain Failed, DKIM Failed, SPF Failed, MX Failed**, the operational diagnosis is **`RESEND_SENDER_BLOCKED / REQUIRED_DNS_RECORDS_NOT_PRESENT_IN_INSPECTED_CLOUDFLARE_ZONE`**.

Do not conflate the Resend UI's **Hostinger** provider label with DNS public delegated nameservers; earlier public NS lookup reported `nicolas.ns.cloudflare.com` and `millie.ns.cloudflare.com`. This establishes **potential stale provider selection**, not evidence Hostinger currently serves the authoritative records.

## 2. W6 handoff and source-of-authority guardrails

**Required W6 remediation (NOT authorized or performed in W0):**
1. Confirm live Resend domain **`resend.reltroner.com`** and exact DNS record **Type / Hostname / Value / Priority / TTL** for DKIM TXT, feedback MX and SPF TXT without publishing long cryptographic TXT records. Beware absolute vs zone-relative hostname duplication: e.g., `resend._domainkey.resend` can be displayed relative to `reltroner.com`, and UI normalization must be verified before writing.
2. Reconfirm Cloudflare account/zone is currently delegated, examine any conflicting existing records (TXT/SPF/MX, DMARC, delegated subzone); classify blast radius to current production mail and web. Do not delete or overwrite existing DNS records as cleanup.
3. Create a **separately owner-approved**, narrowly scoped DNS write plan. Prefer exact explicit records and documented backout before the change; no auto-configure/restart blindly.
4. After future changes, allow propagation; validate authoritative vs two recursive public resolvers, Resend **Verified** state, actual approved minimal email/lifecycle tests, and quota/suppression/opt-out end-to-end. Do not interpret a DNS Verified badge as proof emails are delivered.
5. Keep W6 **BLOCKED** until provider verification, functional lifecycle and cost/privacy gates are evidenced. Do not enable Phase 2 outreach.

No further repeated DNS timeout probing is necessary for W0 closure; the discrepancy is documented as a known tool/transport limitation. If a future operator has different network paths, direct authoritative queries may be performed as part of a new narrowly scoped diagnostic, not a prerequisite to entering W1.

## 3. Other inherited W0 blockers are not fixed by DNS diagnosis

- **W4 / WEB-I13 / WEB-AC19:** owner reports a fresh Incognito session with `_ga` and GA `collect` but no visible consent UI. Studio production GitHub `GoogleAnalytics.jsx`, `RouteAnalytics.jsx`, `lib/gtag.js` lack in-component consent gating. Remediation/accurate notice remains mandatory; specific legal violation is not asserted.
- **W3 / WEB-I08 / WEB-AC10–12:** `/images/background.webp` production 404.
- **W1 / WEB-I03 / WEB-AC01–04:** hero lacks approved creator/reader first-contact paths.
- **W2/W6/W7 mobile:** reCAPTCHA visually clipped at 320px, native automated narrow viewport and 200% zoom cases not fully executed.
- **W5 / WEB-I10/14 / WEB-AC13–15/25:** Cloudflare account Workers Free Active; no per-model Workers AI inference entitlement or cost-qualified model selected. Never treat catalogue as inference authorization.
- **W0-AC05:** Vercel Hobby and snapshot quotas observed, but future commercial terms/usage and preview automatic deploy/cost still need G2/G4 checks. Avoid new preview without exact scope/owner approval.

## 4. Status and non-authorization statement

| Area | Disposition |
|---|---|
| Direct `-Server` authoritative queries | **INCONCLUSIVE_TIMEOUT** |
| Cloudflare DNS Records inspection | **OWNER_GUI_REPORTED_ABSENT** |
| Recursive DNS (prior RC-W0-07) | **TWO_RESOLVER_MISSING_HOSTS** |
| Resend Domain readiness | **BLOCKED** — three DNS failures |
| W0-AC07 discovery | **PASS_SCOPED_DIAGNOSTIC_WITH_RESIDUAL**; not provider acceptance |
| W0-AC12 final closure | **PENDING explicit owner signoff** |
| W1–W7 engineering | **HOLD** (each needs own authorization) |
| Source/provider/production mutations | **NONE** |

**Decision:** stop repeated low-value W0 authoritative queries; archive limitations; move to a **proposed W0 closing risk/deferral review** for owner signoff, not to immediate W6 edits or W1 code work.
