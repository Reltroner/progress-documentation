# ADR-LMS-TRUST-001 — Internal Workload & Delegated Principal Cryptographic Profile

> **Prepared and owner-ratified:** 2026-10-10 (Asia/Jakarta); **status:** **OWNER RATIFIED — NONPRODUCTION PHASE 3B DESIGN ONLY**.  
> **Scope:** non-production design decision and requirements only; **no source candidate SHA change**, no signing keys generated/deployed, no Keycloak/VPS/Redis/DB change.  
> **Gate:** B3-AC07 / R-03. Binding parents: frozen Phase 0C physical placement and Phase 1 logical/API contracts, FZ-10, FZ-11. Not a waiver of B3-AC25/28.

## 1. Provenance, threat boundary and non-evidence

Candidate cryptographic parameters: [LMS-BE `contracts/identity/crypto-profile-proposal.json` at BE SHA 0fc17da](https://github.com/Reltroner/LMS-BE/blob/0fc17dabc1af845053ac525986f40fb260f73e4c/contracts/identity/crypto-profile-proposal.json), [identity trust schema](https://github.com/Reltroner/LMS-BE/blob/0fc17dabc1af845053ac525986f40fb260f73e4c/contracts/identity/trust-contract.json), [real sodium Ed25519 test-only verification](https://github.com/Reltroner/LMS-BE/blob/0fc17dabc1af845053ac525986f40fb260f73e4c/contracts/tests/validate-trust-crypto.php), [BE green CI](https://github.com/Reltroner/LMS-BE/actions/runs/37960568787).

This decision covers **service-to-service caller authentication and bounded signed end-user principal delegation**, NOT Keycloak browser access-token verification, NOT a replacement for TLS/private network, and NOT production deployment. Current 10 synthetic sodium tests prove only the bounded fixture behavior; no production key custody, dual-assertion HTTP verifier, cache-failure, or replay-store durability has been exercised.

## 2. Ratified design parameters and bounded deployment exclusions

**Owner-ratified contract:** Adopt **EdDSA / Ed25519 JWS Compact** exclusively for the new LMS internal workload and scoped delegation assertions, with explicit call-site allowlisting and an atomic fail-closed replay store. **Do not authorize it for live usage until the downstream runtime gates in §5 pass.** Algorithm choice is independent of Keycloak's configured/JWKS-verified OIDC access-token algorithms; the OIDC algorithm allowlist remains a separate Phase 4 observed-configuration decision.

| Dimension | Owner-ratified Phase 3B nonproduction design parameter | Fail-closed requirement |
|---|---|---|
| Serialization/signing | JWS Compact, protected `alg=EdDSA`, public `kty=OKP`, `crv=Ed25519` (RFC 7515/8037) | No `none`, HS/RS algorithm substitution, untrusted remote `jku`/`x5u`, ambiguous `kid` |
| Workload + delegation | Two independently validated **logical** controls: a known signed caller-service identity and signed scoped end-user delegation when an end-user exists | Reject an unsigned/missing workload proof OR unsigned/missing delegation on user-bound calls; avoid treating synthetic combined fixtures as a real dual-assertion runtime proof |
| Identity binding | Pinned `iss=lms-internal-trust`, `aud=lms-internal-services`, caller and recipient service IDs, operation ID, principal subject/capability intersection, request_id | Reject mismatched recipient, wrong caller-to-`kid` registration, cross-API operations, privilege elevation, reused user headers |
| Timestamp | Max token lifetime `exp-iat <= 60s`; `iat`, `nbf`, `exp` required; clock skew **5s** maximum | `nbf` too far ahead, expired token, `iat` in future beyond skew, missing claims all denied; bound actual validity to max 60s |
| Replay | Unpredictable `jti` (>=128 bits entropy), unique by issuer + caller + recipient + `jti`; perform atomic one-use reservation BEFORE side effects | Repeated `jti` denied; atomic set-if-not-exists with TTL at least remaining `exp` + allowed skew; missing store or indeterminate result denies |
| Store failure/restart | Redis for **ephemeral anti-replay safety only** (`SET NX PX` equivalent), NOT canonical business-state or durable booking authority | Never fail open; a lost/unknown replay keyspace requires a gated recovery quarantine **at least 65s after verified recovery** so all previously issued <=60s tokens are expired including skew; operator must detect keyspace-loss, otherwise runtime gate remains BLOCKED |
| Key distribution | Per-caller issuer/service-specific pinned Ed25519 public-key registry installed by controlled release, with exact `kid`, service identity and fingerprint; private signing keys stored out of Git and separated per workload | Unknown/retired `kid`, wrong owner, fingerprint change without approved release, insecure private-key exposure all deny; never auto-fetch key from token-header URLs |
| Routine rotation | **180s** maximum overlap with explicit current+previous allowed keys; old key removed after overlap and all <=60s assertions have expired | Compromised key revoked immediately (no overlap); rollback needs deliberate trust-registry update and security review |
| Audience and endpoint | Private service ingress only, exact caller/recipient/operation allowlist; external browser bearer tokens cannot be reused as workload tokens | `lms-api` access token alone is never an internal caller proof; no public internal service hostnames |
| Audit / hygiene | Record `kid`, caller, recipient, operation, request ID, decision and reason code; never log tokens, private keys, unredacted user PII or secrets | Fail closed on unexpected signature/claims/replay; no secret-bearing CI fixtures |

**Header versus payload:** `kid` in the JWS protected header is authoritative for key lookup; if the existing schema's `kid` claim is retained, verify exact equality of protected-header `kid` and signed-payload `kid`. Before Phase 4 runtime implementation, specify unique assertion type/domain separation to prevent workload/delegation token confusion and write dedicated positive/negative tests. Do not silently reinterpret the existing schema without a versioned, reviewed amendment.

**Redis recovery limitation:** Redis is replaceable state under the frozen architecture; relying on ephemeral Redis alone without observable reset detection, quarantine and fault-injection evidence is **not** acceptable anti-replay proof. If the proposed quarantine/detection model cannot be reliably implemented in Phase 4, stop and return a revised owner-reviewed ADR with another architecture-compliant replay strategy; do not invent a fifth canonical domain DB or turn Redis into business truth.

## 3. Decision alternatives considered

- **Ed25519 with pinned per-service public keys (recommended for 3B nonproduction contract):** asymmetric scoped verification, small signatures, test-only sodium proof already in candidate; still requires distribution, rotation, replay, operational validation.
- **HMAC shared secret:** simpler, but verification holders can forge any caller using that shared key; increases cross-service impersonation and rotation blast radius. **Not recommended** for delegated principal proof.
- **mTLS without signed delegation:** transport proof does not bind the original user/operation/capability and cannot replace the already frozen dual-control intent. Can be an additional layer after measurement; not a substitute.
- **Direct Keycloak token forwarding:** confuses public audience and internal recipient constraints, enables scope confusion and bypasses exact caller binding. **Rejected** as default.

## 4. Recorded owner ratification — no fabricated cryptographic signature

| Decision | State |
|---|---|
| Adopt Ed25519/EdDSA and JWS profile | **APPROVED — NONPRODUCTION DESIGN ONLY** |
| Approve max TTL 60s, skew 5s, overlap 180s | **APPROVED — NONPRODUCTION DESIGN ONLY** |
| Approve per-service pinned public-key distribution/rotation/revocation | **APPROVED — NONPRODUCTION DESIGN ONLY** |
| Approve Redis NX replay store with fail-closed unknown-state and >=65s recovery quarantine, subject to executable Phase 4 safety proof | **APPROVED — NONPRODUCTION DESIGN ONLY** |
| Source candidate merged to `main` | **NO** |
| Production trust authority provisioned | **NO** |

**Actual owner ratification (2026-10-10 Asia/Jakarta):** “aku menyetujui menyetujui ratifikasi ADR-LMS-TRUST-001 dengan seluruh parameter pada tabel di atas, khusus untuk desain nonproduction Phase 3B.” The current decision accepts **this ADR's parameter set**, tied to BE reviewed source `0fc17dabc1af845053ac525986f40fb260f73e4c`, **as a design authority only**. It does not claim the owner has signed a JWS or approved any actual runtime key. The same instruction selected markdown-only/manual branch governance in [BRANCH-GOV-001](./branch-gov-001-main-branch-contractual-protection-20261010.md), not GitHub settings. BE/FE source PRs remain unmerged, and final Phase 3 exit and source merge still need separate approval.

## 5. Downstream mandatory safety checks (not Phase 3 synthetic PASS)

Before **any** runtime accept/use, require: actual isolated Ed25519 signer/verifier integration with separate workload/delegation credential validation; signer-key custody and public-key registry/fingerprint review; 401/403 wrong key/aud/sub/recipient/operation/capability; bounded 60s freshness under clock skew; same-jti concurrent replay; Redis loss during flight and cache loss detection/quarantine; rotation, emergency revoke and rollback with previous-key expiry; Keycloak access JWT/JWKS real validation independently; CI and HRM/realm nonregression. Evidence must pin test runtime and code SHAs. All need a **distinct Phase 4+ owner-authorized work order**.

**Owner ratification obtained:** the missing **owner cryptographic decision** for B3-AC07/R-03 is now evidenced, but the immutable 3B-07R audit remains the historical classification until an explicit revalidation reconciles the BE source contract's earlier pending-ADR markers and records a new 28-gate delta. **No synthetic crypto fixture is production/runtime verification**; B3-AC25 and B3-AC28 remain open.
