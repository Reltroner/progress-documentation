---
title: "Phase 2 Chunk 2.2 — End-to-End Production Domain, DNS, and TLS Baseline"
description: "Complete engineering record of the Reltroner ERP production domain migration, Cloudflare authoritative DNS cutover, Vercel corporate-site restoration, Cloudflare Worker custom-domain activation, Hostinger email preservation, and HRM subdomain recovery."
project: "Reltroner ERP"
phase: 2
chunk: "2.2"
status: "complete"
completed_at: "2026-08-06"
timezone: "Asia/Jakarta"
document_type: "engineering-evidence"
---

# Phase 2 Chunk 2.2 — End-to-End Production Domain, DNS, and TLS Baseline

## 1. Document Purpose

This document records the complete execution of **Phase 2 Chunk 2.2 — Production Domain, DNS, and TLS Baseline** for Reltroner ERP.

It captures:

- The initial domain and DNS state.
- The intended production-domain architecture.
- The migration of authoritative DNS to the correct Cloudflare zone.
- The restoration of the Reltroner corporate website on Vercel.
- The preservation of Hostinger Email DNS.
- The activation of `erp.reltroner.com` as a Cloudflare Worker Custom Domain.
- The DNS regression affecting `hrm.reltroner.com`.
- The investigation and recovery of the HRM application.
- Validation gates, failures, corrections, and final evidence.
- The final engineering status and transition to Phase 2 Chunk 2.3.

This is an implementation and operational evidence document. It is not an architecture-decision record, product roadmap, or release note.

---

## 2. Chunk Identity

| Field | Value |
|---|---|
| Project | Reltroner ERP |
| Phase | Phase 2 — Production Infrastructure Foundation |
| Chunk | 2.2 — Production Domain, DNS, and TLS Baseline |
| Execution window | 2026-08-05 to 2026-08-06 |
| Primary DNS provider | Cloudflare |
| Domain registrar | Hostinger |
| Corporate website platform | Vercel |
| Tenant ERP frontend platform | Cloudflare Workers |
| Email provider | Hostinger Email |
| HRM application origin | Hostinger Shared Hosting |
| Final status | **COMPLETE** |

---

## 3. Relevant Production Architecture

The production-domain architecture established by this chunk is:

```text
reltroner.com
└── Vercel
    └── 307 redirect to https://www.reltroner.com

www.reltroner.com
└── Vercel
    └── Reltroner Studio production website

erp.reltroner.com
└── Cloudflare Worker Custom Domain
    └── Worker: erp-reltroner-fe

hrm.reltroner.com
└── Cloudflare authoritative DNS
    └── DNS-only A record
        └── Hostinger origin: 145.79.28.61
            └── Laravel HRM application

Email @reltroner.com
└── Hostinger Email
    ├── MX
    ├── SPF
    ├── DKIM
    └── DMARC

admin.erp.reltroner.com
└── Deferred to Phase 2 Chunk 2.4

api.reltroner.com
└── Deferred to Phase 2 Chunk 2.5
```

---

## 4. Initial State

Before this chunk was completed, the domain environment had several operational problems.

### 4.1 Production endpoint status

| Endpoint | Initial condition |
|---|---|
| `reltroner.com` | Publicly reachable, but routing was inconsistent and later exposed the Hostinger default page |
| `www.reltroner.com` | Vercel reported invalid configuration |
| `erp.reltroner.com` | No production DNS record or custom domain |
| `admin.erp.reltroner.com` | Not configured |
| `api.reltroner.com` | Not configured |
| `hrm.reltroner.com` | Initially working under the previous DNS environment, but omitted from the new Cloudflare zone |
| `sso.skill-wanderer.com` | Existing externally managed Keycloak endpoint remained operational |

### 4.2 Initial authoritative nameservers

The domain was initially delegated to a different Cloudflare zone:

```text
eloise.ns.cloudflare.com
louis.ns.cloudflare.com
```

The intended Cloudflare zone in the active account was assigned:

```text
millie.ns.cloudflare.com
nicolas.ns.cloudflare.com
```

### 4.3 Incorrect initial website assumption

The Hostinger hosting-plan address was:

```text
145.79.28.61
```

This IP was initially treated as the corporate website origin. That assumption was incorrect for `reltroner.com`, because the corporate website was intended to remain on Vercel.

An early zone draft therefore incorrectly used:

```text
A @ → 145.79.28.61
CNAME www → reltroner.com
```

This produced the Hostinger default website instead of Reltroner Studio.

### 4.4 Vercel project state

The Vercel project was:

```text
Team:    Reltroner
Project: reltroner-studio
```

The project domains were configured as:

```text
reltroner.com
→ 307 Temporary Redirect
→ www.reltroner.com

www.reltroner.com
→ Production

reltroner-studio.vercel.app
→ Production
→ Valid Configuration
```

However, both custom domains were reported as invalid because public DNS did not match the required Vercel records.

---

## 5. Target DNS Ownership Model

The selected ownership model was:

```text
Vercel
→ Provides the required DNS target for the corporate website.
→ Owns application deployment and apex-to-www redirect behavior.

Cloudflare
→ Acts as authoritative DNS for reltroner.com.
→ Stores website, email, application, and Worker DNS.
→ Provides the Worker Custom Domain for erp.reltroner.com.

Hostinger
→ Remains the registrar.
→ Remains the email provider.
→ Hosts the HRM application and future Laravel backend.
→ Is used to change registrar-level nameservers.
```

Vercel DNS nameservers were explicitly not adopted.

The following Vercel nameservers were not used:

```text
ns1.vercel-dns.com
ns2.vercel-dns.com
```

This avoided moving email and Worker-domain management away from Cloudflare.

---

## 6. Vercel DNS Requirements

The exact Vercel target shown by the project dashboard was:

```text
7aa147f8fdf28e8b.vercel-dns-017.com
```

Vercel required the following external-DNS records:

```text
CNAME @
→ 7aa147f8fdf28e8b.vercel-dns-017.com
Proxy: Disabled

CNAME www
→ 7aa147f8fdf28e8b.vercel-dns-017.com
Proxy: Disabled
```

The Vercel project behavior remained:

```text
reltroner.com
→ 307 Temporary Redirect
→ www.reltroner.com

www.reltroner.com
→ Production
→ No redirect
```

---

## 7. Cloudflare Zone Preparation

The new Cloudflare zone was prepared before nameserver cutover.

### 7.1 Corporate website records

The incorrect Hostinger apex record was removed:

```text
A @ → 145.79.28.61
```

The final corporate website records were configured as:

```text
CNAME @
→ 7aa147f8fdf28e8b.vercel-dns-017.com
Proxy status: DNS only
TTL: Auto

CNAME www
→ 7aa147f8fdf28e8b.vercel-dns-017.com
Proxy status: DNS only
TTL: Auto
```

The records were intentionally set to **DNS only** because Vercel detected and warned against an additional reverse proxy in front of the Vercel edge.

### 7.2 Hostinger Email records

The following email records were preserved:

```text
MX @
→ mx1.hostinger.com
Priority: 5

MX @
→ mx2.hostinger.com
Priority: 10

TXT @
→ v=spf1 include:_spf.mail.hostinger.com ~all

TXT _dmarc
→ v=DMARC1; p=none

CNAME hostingermail-a._domainkey
→ hostingermail-a.dkim.mail.hostinger.com

CNAME hostingermail-b._domainkey
→ hostingermail-b.dkim.mail.hostinger.com

CNAME hostingermail-c._domainkey
→ hostingermail-c.dkim.mail.hostinger.com

TXT @
→ google-site-verification=...
```

All email-related records remained DNS-only.

### 7.3 DNSSEC state

No active DS record was detected through public resolvers.

DNSSEC was intentionally left disabled during migration and stabilization.

---

## 8. First Nameserver Cutover and Rollback

### 8.1 First cutover

The nameservers were changed from:

```text
eloise.ns.cloudflare.com
louis.ns.cloudflare.com
```

to:

```text
millie.ns.cloudflare.com
nicolas.ns.cloudflare.com
```

### 8.2 Failure symptoms

The first cutover exposed several problems:

- `reltroner.com` produced certificate errors.
- `www.reltroner.com` produced certificate name or chain errors.
- The browser displayed the Hostinger default page.
- The corporate website was not served by Vercel.

### 8.3 Root cause

The new zone still directed the website to the Hostinger hosting-plan IP:

```text
145.79.28.61
```

That address was not the intended corporate-site origin.

### 8.4 Controlled rollback

The registrar nameservers were restored to:

```text
eloise.ns.cloudflare.com
louis.ns.cloudflare.com
```

The rollback restored DNS authority and basic HTTP reachability, but it did not prove that the correct application content had returned.

The earlier statement:

```text
ROLLBACK VALIDATION: PASSED
```

was later reclassified as incomplete because it only established DNS/HTTP reachability and MX continuity, not correct website rendering.

### 8.5 Corrective decision

The corporate website target was locked to Vercel.

The Hostinger IP was permanently excluded from the `reltroner.com` and `www.reltroner.com` records.

---

## 9. New-Zone Pre-Cutover Validation

A dedicated PowerShell validator was used to query the new assigned nameservers directly:

```text
millie.ns.cloudflare.com
nicolas.ns.cloudflare.com
```

The validator checked:

- Flattened apex responses.
- Absence of the old Hostinger website IP.
- Exact Vercel CNAME for `www`.
- Hostinger MX records.
- SPF.
- DMARC.
- DKIM selectors A, B, and C.

### 9.1 Successful output

Both nameservers returned:

```text
Apex flattened addresses:
216.198.79.1
64.29.17.1

WWW:
7aa147f8fdf28e8b.vercel-dns-017.com

MX:
mx1.hostinger.com
mx2.hostinger.com

SPF:   PASSED
DMARC: PASSED
DKIM:  PASSED
```

The gate output was:

```text
NEW ZONE PRECUTOVER VALIDATION: PASSED
```

### 9.2 Parser failure encountered

An earlier validator attempt failed before execution because of a PowerShell interpolation problem:

```powershell
"$Nameserver: $ExpectedMx"
```

PowerShell interpreted the colon as part of the variable reference.

The corrected form was:

```powershell
"${Nameserver}: $ExpectedMx"
```

The manually printed success message from the failed attempt was rejected as invalid evidence because the validator block never executed.

---

## 10. Final Nameserver Cutover

After the pre-cutover gate passed, the nameservers were updated in the Hostinger registrar GUI:

```text
Old:
eloise.ns.cloudflare.com
louis.ns.cloudflare.com

New:
millie.ns.cloudflare.com
nicolas.ns.cloudflare.com
```

The Cloudflare zone subsequently changed to active.

### 10.1 Recursive DNS propagation behavior

During propagation, public resolvers returned mixed states:

- Old nameservers on one query.
- New nameservers on another query.
- Temporary absence of `www` CNAME responses.
- Different flattened Vercel IP values.
- Occasional Cloudflare edge IP responses during cache transition.

This was treated as recursive-cache convergence rather than authoritative-zone failure because both assigned authoritative nameservers had already passed direct validation.

### 10.2 Post-cutover validator correction

The first post-cutover validator stopped too early because it validated nameserver propagation but immediately required the new `www` answer from recursive resolvers.

A second validator was created to:

1. Validate the authoritative nameservers.
2. Poll `1.1.1.1` and `8.8.8.8`.
3. Wait for NS, `www`, apex, and MX convergence.
4. Validate apex redirect behavior.
5. Validate `www` HTTPS.
6. Reject the Hostinger default page.

### 10.3 Final corporate cutover result

The final validation produced:

```text
Authoritative check: PASSED
PUBLIC DNS RECORD PROPAGATION: PASSED

Apex status:   307
Apex location: https://www.reltroner.com/
WWW status:    200
HTTPS ready:   True
```

The accepted gate was:

```text
PHASE 2 CHUNK 2.2: CORPORATE DNS CUTOVER VALIDATED
```

### 10.4 Corporate cutover evidence

```text
C:\Projects\erp-reltroner\_audit\phase-2\
└── chunk-2.2-cutover-validation-v2-20260805-231755\
    ├── phase-2-chunk-2.2-cutover-validation-v2.md
    └── phase-2-chunk-2.2-cutover-validation-v2.json
```

A shared status file was also written:

```text
C:\Projects\erp-reltroner\_audit\phase-2\
└── phase-2-chunk-2.2-status.json
```

---

## 11. Tenant ERP Worker Custom Domain

After corporate DNS was validated, the tenant ERP frontend domain was attached to the Cloudflare Worker.

### 11.1 Cloudflare configuration

The following Custom Domain was added:

```text
Worker:      erp-reltroner-fe
Environment: Production
Zone:        reltroner.com
Domain:      erp.reltroner.com
```

The domain was added through:

```text
Cloudflare
→ Workers & Pages
→ erp-reltroner-fe
→ Domains
→ Add Domain
```

No manual A or CNAME record was created for `erp.reltroner.com`.

Cloudflare created and managed the Worker DNS route and certificate.

### 11.2 Worker validation

The validation result was:

```text
Resolver 1.1.1.1: Resolved
Resolver 8.8.8.8: Resolved

HTTPS status:       200
Final URL:          https://erp.reltroner.com/
Server:             cloudflare
CF-Ray:             present
TLS:                available
TLS protocol:       TLS 1.3
TLS days remaining: 89
```

The resulting gate was:

```text
PHASE 2 CHUNK 2.2:
COMPLETE WITH ADMIN AND BACKEND DOMAINS DEFERRED
```

### 11.3 Worker-domain evidence

```text
C:\Projects\erp-reltroner\_audit\phase-2\
└── chunk-2.2-tenant-worker-domain-20260805-233402\
    ├── phase-2-chunk-2.2-tenant-worker-domain-validation.md
    └── phase-2-chunk-2.2-tenant-worker-domain-validation.json
```

Additional status files:

```text
C:\Projects\erp-reltroner\_audit\phase-2\
├── phase-2-chunk-2.2-status.json
└── phase-2-status.json
```

### 11.4 Expected Worker DNS behavior

The Worker domain resolved to Cloudflare edge addresses, for example:

```text
104.21.23.103
172.67.210.125
2606:4700:3034::6815:1767
2606:4700:3034::ac43:d27d
```

No public CNAME was required.

This was expected because Cloudflare manages the hostname, route, edge proxy, and TLS certificate internally for a Worker Custom Domain.

---

## 12. HRM DNS Regression

After the authoritative DNS migration, the existing HRM application became unavailable:

```text
https://hrm.reltroner.com
→ DNS_PROBE_FINISHED_NXDOMAIN
```

### 12.1 Root cause

The previous Hostinger DNS zone contained:

```text
A hrm
AAAA hrm
```

However, Hostinger showed those records as inactive because the active authoritative nameservers had moved to Cloudflare.

The `hrm` records were not included in the new Cloudflare zone during the initial migration.

### 12.2 Chunk status response

Phase 2 Chunk 2.2 was temporarily reopened:

```text
Phase 2 Chunk 2.2:
REOPENED — HRM DNS regression
```

Corporate Vercel domains, email DNS, and the tenant ERP Worker remained validated.

---

## 13. Initial HRM Recovery Attempt

The inactive Hostinger DNS records showed:

```text
A hrm
→ 2.57.91.91

AAAA hrm
→ 2a02:4780:5c:2146:0:e07:6065:6
```

These records were copied into Cloudflare as DNS-only records.

### 13.1 DNS result

Both authoritative nameservers correctly returned:

```text
A:
2.57.91.91

AAAA:
2a02:4780:5c:2146:0:e07:6065:6
```

### 13.2 Application and TLS result

The DNS restoration removed NXDOMAIN, but application validation failed.

HTTP to `2.57.91.91` returned:

```text
HTTP 200
Server: hcdn
Page: Parked Domain name on Hostinger DNS system
```

HTTPS failed during the TLS handshake:

```text
SEC_E_INTERNAL_ERROR
Authentication failed because the remote party sent a TLS alert: InternalError
```

The IPv6 test could not be completed from the local network because there was no reachable IPv6 route.

### 13.3 Interpretation

The address `2.57.91.91` was a Hostinger parked-domain or edge endpoint, not the correct application origin for the HRM Laravel application.

The existence of an active SSL entry in hPanel did not prove that the public DNS target was reaching the virtual host serving that certificate.

---

## 14. HRM Origin Investigation

### 14.1 Hostinger hosting-plan details

The Hostinger plan showed:

```text
Website IP address: 145.79.28.61
Server name:         server2046
Server location:     Asia (Malaysia)
Backup location:     Singapore
```

### 14.2 Subdomain configuration

Hostinger showed the active subdomain mapping:

```text
Subdomain:
hrm.reltroner.com

Document root:
/home/u235364453/domains/reltroner.com/public_html/hrm/public
```

This confirmed that the HRM Laravel public directory was still registered.

### 14.3 Parked-domain configuration

The Hostinger parked-domain list was empty.

Therefore, `hrm.reltroner.com` was not intentionally configured as a parked alias.

### 14.4 SSL inventory

The hPanel SSL page showed:

```text
hrm.reltroner.com
Lifetime SSL
Status: Active
```

The root-domain Hostinger SSL entry showed a failed state, but that was not relevant because the root domain was intentionally served by Vercel.

---

## 15. Direct HRM Origin Validation

The actual Hostinger plan IP was tested directly with the HRM hostname using `curl --resolve`.

### 15.1 HTTP validation

Request:

```text
hrm.reltroner.com:80
→ 145.79.28.61
```

Response:

```text
HTTP/1.1 301 Moved Permanently
Server: LiteSpeed
Location: https://hrm.reltroner.com/
platform: hostinger
panel: hpanel
```

### 15.2 HTTPS validation

Request:

```text
hrm.reltroner.com:443
→ 145.79.28.61
```

Response:

```text
HTTP/1.1 302 Found
X-Powered-By: PHP/8.4.19
Server: LiteSpeed
Location: https://hrm.reltroner.com/login
Vary: X-Inertia
```

The application also returned Laravel session and XSRF cookies.

This established that:

- The correct origin was `145.79.28.61`.
- Hostinger virtual-host mapping was correct.
- TLS worked on the correct origin.
- Laravel routing worked.
- The HRM application was present and running.

---

## 16. Final HRM DNS Correction

The Cloudflare record was corrected to:

```text
Type:         A
Name:         hrm
Content:      145.79.28.61
Proxy status: DNS only
TTL:          Auto
```

The unverified AAAA record was removed.

### 16.1 Why DNS-only was retained

The HRM domain remained DNS-only to preserve direct Hostinger origin behavior while avoiding an additional proxy-related variable during recovery.

Cloudflare proxying can be evaluated later through a separate hardening task after testing:

- Authentication.
- Session persistence.
- CSRF behavior.
- Inertia requests.
- File uploads.
- Payroll workflows.
- Email callbacks.
- Any application-specific IP or proxy assumptions.

### 16.2 Public DNS result

Both recursive resolvers returned:

```text
1.1.1.1
→ 145.79.28.61

8.8.8.8
→ 145.79.28.61
```

### 16.3 Public HTTP and HTTPS result

Public HTTP:

```text
http://hrm.reltroner.com/
→ 301
→ https://hrm.reltroner.com/
```

Public HTTPS:

```text
https://hrm.reltroner.com/
→ 302
→ https://hrm.reltroner.com/login
```

### 16.4 Browser validation

The authenticated HRM dashboard loaded successfully at:

```text
https://hrm.reltroner.com/dashboard
```

Visible application modules included:

- Dashboard.
- Tasks.
- Employees.
- Departments.
- Roles.
- Presences.
- Payrolls.
- Leave Requests.
- Logout.

This validated surface-level application availability after DNS restoration.

---

## 17. Final DNS Record Set Relevant to This Chunk

### 17.1 Vercel corporate website

```text
CNAME @
→ 7aa147f8fdf28e8b.vercel-dns-017.com
DNS only
TTL Auto

CNAME www
→ 7aa147f8fdf28e8b.vercel-dns-017.com
DNS only
TTL Auto
```

### 17.2 Tenant ERP Worker

```text
Worker erp.reltroner.com
→ erp-reltroner-fe
Proxied and managed by Cloudflare
TTL Auto
```

### 17.3 HRM application

```text
A hrm
→ 145.79.28.61
DNS only
TTL Auto
```

No AAAA record was retained for HRM.

### 17.4 Hostinger Email

```text
MX @
→ mx1.hostinger.com
Priority 5

MX @
→ mx2.hostinger.com
Priority 10

TXT @
→ v=spf1 include:_spf.mail.hostinger.com ~all

TXT _dmarc
→ v=DMARC1; p=none

CNAME hostingermail-a._domainkey
→ hostingermail-a.dkim.mail.hostinger.com

CNAME hostingermail-b._domainkey
→ hostingermail-b.dkim.mail.hostinger.com

CNAME hostingermail-c._domainkey
→ hostingermail-c.dkim.mail.hostinger.com
```

---

## 18. Final Validation Matrix

| Capability | Final result | Evidence |
|---|---:|---|
| Cloudflare zone active | Passed | Zone active after registrar cutover |
| Public nameservers | Passed | `millie` and `nicolas` through `1.1.1.1` and `8.8.8.8` |
| Vercel apex DNS | Passed | Exact Vercel target through Cloudflare CNAME flattening |
| Vercel `www` DNS | Passed | Exact project CNAME |
| Apex redirect | Passed | HTTP 307 to `https://www.reltroner.com/` |
| Corporate website HTTPS | Passed | HTTP 200 |
| Hostinger default page absent | Passed | Content check |
| Hostinger MX continuity | Passed | Both MX records resolved |
| SPF | Passed | Hostinger SPF present |
| DKIM | Passed | Selectors A, B, and C present |
| DMARC | Passed | `p=none` record present |
| ERP Worker DNS | Passed | Resolved through both public resolvers |
| ERP Worker HTTPS | Passed | HTTP 200 |
| ERP Worker TLS | Passed | TLS 1.3, 89 days remaining at validation |
| Cloudflare edge evidence | Passed | `Server: cloudflare`, CF-Ray present |
| HRM hostname DNS | Passed | A record to `145.79.28.61` |
| HRM HTTP redirect | Passed | 301 to HTTPS |
| HRM HTTPS | Passed | 302 to login |
| HRM virtual host | Passed | LiteSpeed/Hostinger response |
| HRM Laravel runtime | Passed | PHP 8.4, Laravel cookies, Inertia response |
| HRM dashboard rendering | Passed | Browser screenshot |
| Admin ERP domain | Deferred | Phase 2 Chunk 2.4 |
| Backend API domain | Deferred | Phase 2 Chunk 2.5 |

---

## 19. Failure Register and Resolutions

| Failure | Root cause | Resolution |
|---|---|---|
| Corporate site displayed Hostinger default page | Apex was incorrectly pointed to Hostinger plan IP | Replaced apex and `www` with exact Vercel project CNAME |
| Vercel reported invalid configuration | Public DNS did not match project requirements | Installed exact Vercel CNAME records in Cloudflare |
| Vercel reported proxy detected | Old live zone or proxied answers remained in recursive caches | Kept new records DNS-only and completed nameserver/cache convergence |
| First cutover produced certificate errors | Wrong corporate origin and incomplete zone | Rolled back, corrected zone, revalidated, and repeated controlled cutover |
| PowerShell pre-cutover validator failed to parse | Colon immediately followed an interpolated variable | Used `${Nameserver}` syntax |
| Post-cutover validator failed on `www` | It checked recursive records before cache convergence | Replaced it with an authoritative-first polling validator |
| `hrm.reltroner.com` returned NXDOMAIN | HRM record was omitted from the new Cloudflare zone | Recreated HRM DNS in Cloudflare |
| HRM returned Hostinger parked page | Imported Hostinger DNS IP was not the HRM application origin | Identified and tested the hosting-plan IP |
| HRM TLS failed on initial recovery IP | Wrong endpoint did not serve the HRM SNI/certificate | Repointed A record to `145.79.28.61` |
| HRM IPv6 could not be validated | Local IPv6 path unavailable and origin behavior unconfirmed | Removed AAAA record pending future validation |

---

## 20. Operational Lessons

### 20.1 Registrar, DNS provider, and hosting provider are separate responsibilities

A domain registered at Hostinger can use Cloudflare authoritative DNS while still using Hostinger Email and Hostinger application hosting.

### 20.2 A hosting-plan IP is not automatically the correct target for every hostname

The Hostinger plan IP was correct for HRM but incorrect for the Vercel corporate website.

Each hostname must be mapped to its actual platform owner.

### 20.3 Direct authoritative validation is required before nameserver cutover

Querying `millie` and `nicolas` directly allowed the new zone to be validated before it became public.

### 20.4 Recursive propagation must not be confused with authoritative failure

Resolvers can temporarily return mixed NS, CNAME, and flattened-IP responses after delegation changes.

### 20.5 HTTP reachability is not sufficient acceptance evidence

A `200` response can still be a default or parked page.

Validation must include content and application behavior.

### 20.6 SSL inventory is not the same as TLS delivery

A certificate can appear active in a hosting dashboard while the public DNS target reaches a different edge or virtual host.

### 20.7 Legacy subdomains must be explicitly inventoried during authoritative-DNS migration

The HRM outage occurred because its records were not included in the new zone migration.

Future migrations must compare the complete old-zone record inventory against the new zone before cutover.

### 20.8 Manually printed success messages are not evidence

A validator must complete without parser or runtime failure before its success message is accepted.

---

## 21. Deferred Work

The following domain work remains outside this chunk.

### Phase 2 Chunk 2.4

```text
admin.erp.reltroner.com
→ Admin frontend Cloudflare Worker
```

### Phase 2 Chunk 2.5

```text
api.reltroner.com
→ Laravel backend on Hostinger
```

### Future HRM hardening

Potential future work:

- Evaluate Cloudflare proxy compatibility.
- Validate `Full (strict)` origin mode.
- Test authentication from a clean browser session.
- Test all critical CRUD workflows.
- Test payroll and presence workflows.
- Test uploads and storage.
- Test background tasks and scheduled jobs.
- Test outbound email.
- Reassess IPv6 and restore AAAA only with evidence.
- Add uptime monitoring and expiry alerts.

---

## 22. Evidence Inventory

### Corporate DNS cutover

```text
C:\Projects\erp-reltroner\_audit\phase-2\
└── chunk-2.2-cutover-validation-v2-20260805-231755\
    ├── phase-2-chunk-2.2-cutover-validation-v2.md
    └── phase-2-chunk-2.2-cutover-validation-v2.json
```

### Tenant Worker domain

```text
C:\Projects\erp-reltroner\_audit\phase-2\
└── chunk-2.2-tenant-worker-domain-20260805-233402\
    ├── phase-2-chunk-2.2-tenant-worker-domain-validation.md
    └── phase-2-chunk-2.2-tenant-worker-domain-validation.json
```

### Shared status

```text
C:\Projects\erp-reltroner\_audit\phase-2\
├── phase-2-chunk-2.2-status.json
└── phase-2-status.json
```

### HRM recovery evidence

The recovery was validated through:

- Cloudflare DNS-record inspection.
- Hostinger plan details.
- Hostinger subdomain document-root inspection.
- Hostinger SSL inventory.
- Hostinger parked-domain inspection.
- Direct HTTP and HTTPS origin tests with `curl --resolve`.
- Public DNS queries against `1.1.1.1` and `8.8.8.8`.
- Public HTTP and HTTPS tests.
- Browser rendering of the authenticated HRM dashboard.

A dedicated HRM validation run can be retained under:

```text
C:\Projects\erp-reltroner\_audit\phase-2\
└── chunk-2.2-hrm-reactivation-<timestamp>\
```

---

## 23. Final Production Domain Baseline

```text
AUTHORITATIVE DNS

reltroner.com
→ millie.ns.cloudflare.com
→ nicolas.ns.cloudflare.com


CORPORATE WEBSITE

reltroner.com
→ Vercel
→ 307 to www.reltroner.com

www.reltroner.com
→ Vercel Production
→ HTTP 200


TENANT ERP

erp.reltroner.com
→ Cloudflare Worker Custom Domain
→ erp-reltroner-fe
→ HTTP 200
→ TLS 1.3


HRM

hrm.reltroner.com
→ Cloudflare DNS only
→ 145.79.28.61
→ Hostinger LiteSpeed
→ Laravel HRM
→ HTTPS
→ /login or authenticated /dashboard


EMAIL

@reltroner.com
→ Hostinger Email
→ MX/SPF/DKIM/DMARC preserved


DEFERRED

admin.erp.reltroner.com
→ Phase 2 Chunk 2.4

api.reltroner.com
→ Phase 2 Chunk 2.5
```

---

## 24. Final Engineering Status

```text
Phase 2 Chunk 2.1:
COMPLETE_WITH_FINDINGS

Phase 2 Chunk 2.2:
COMPLETE

Corporate Vercel domains:
VALIDATED

Hostinger email DNS:
VALIDATED

Tenant ERP Worker custom domain:
VALIDATED

HRM DNS regression:
RESOLVED

HRM origin, TLS, and application surface:
VALIDATED

Phase 2 completed chunks:
2 / 8

Phase 2 operational progress:
25%

Phase 2 gate:
NOT YET — six chunks remain

Official Reltroner ERP v1 release credit:
8%

Evidence-backed implementation maturity:
20.55%

Next engineering target:
Phase 2 Chunk 2.3 — Tenant Frontend Cloudflare Worker Foundation
```

---

## 25. Completion Statement

Phase 2 Chunk 2.2 established a validated production-domain foundation across multiple providers without changing the locked Reltroner ERP architecture.

The completed outcome is:

- Cloudflare is the authoritative DNS provider.
- Vercel serves the corporate website.
- Hostinger continues to provide email and the HRM application origin.
- Cloudflare Workers serves the tenant ERP frontend.
- DNS, TLS, redirect, email, Worker routing, and legacy HRM availability are all evidence-backed.
- Admin and backend production domains remain explicitly deferred to their assigned chunks.

```text
PHASE 2 CHUNK 2.2: COMPLETE
NEXT: PHASE 2 CHUNK 2.3
```
