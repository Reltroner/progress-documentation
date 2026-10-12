# RC-W3-00 — Proposed Immutable Image Delivery, Same-Name Refresh and Fallback Contract

> **Status:** existing source inspected, target algorithm/design documented, **W3 implementation NOT AUTHORIZED / production asset repair NOT EXECUTED**.
> Baseline: [RC-WEB-ARCH-001 WEB-I08](../00-ratified-frontend-architecture-contract-20261012.md), [RC-WEB-AC10–12](../03-phase1-acceptance-and-invariant-traceability.md), [W0 asset facts](./RC-W0-09-final-discovery-disposition-and-proposed-w1-entry-20261012.md).
> Latest observed main source refs 2026-10-12: Studio `18b295f96ccb521b228a1855e79448158c09db15`, `reltroner-studio-resource` `6c6fb38f8ff3376c0789c15bcfe4d0cafc4d057e`. Do not assume those SHAs remain current after this observation.

## 1. Known facts and defect

`lib/assets/cdn.js` currently declares `CDN_VERSION = "main"` and resolves `/images/foo.webp` to `https://cdn.jsdelivr.net/gh/Reltroner/reltroner-studio-resource@main/landing-page-resource/images/foo.webp`. A mutable `@main` URL is insufficient as deterministic evidence that new bytes under the *same filename* reach clients across jsDelivr/Next/Vercel caches. Prior W0 production observed `/images/background.webp` HTTP **404** and a locally ignored asset. It is an existing bug, not fixed by W1.

## 2. Required deterministic asset contract (proposed)

A controlled resource-build input records the exact **full commit SHA** and approved file path. A generated stable manifest maps logical paths (e.g. `/images/foo.webp`) to revisioned immutable URL and optional source content hash, dimensions, alt/fallback class and source provenance.

```ts
type AssetManifestEntry = {
  logicalPath: string;             // /images/foo.webp, filename preserved in Markdown
  sourceRepo: 'Reltroner/reltroner-studio-resource';
  sourceCommit: string;            // FULL immutable resource Git SHA
  sourcePath: string;              // /landing-page-resource/images/foo.webp
  immutableUrl: string;            // jsDelivr /gh/Reltroner/reltroner-studio-resource@<sha>/...
  sha256?: string;                 // validated source bytes if available
  mediaType: string;
  altPolicy: 'AUTHOR_PROVIDED' | 'DECORATIVE' | 'FALLBACK_REQUIRED';
  width?: number; height?: number;
};
type AssetManifest = { schemaVersion: 1; resourceCommit: string; entries: AssetManifestEntry[] };
```

No names/paths are silently changed; manifest generation rejects missing asset, wrong MIME, unsupported schemes/path traversal and duplicate mapping. Existing `next.config.mjs` must be inspected for remote-pattern allowlisting of **SHA-addressed** URLs (not only `@main`); changes require distinct owner-approved exact path allowlist. Do **not** publish tokens.

## 3. Actual same-name freshness acceptance

```text
resource commit R0: /images/same.webp hash H0 → immutable URL @R0
resource commit R1: /images/same.webp hash H1 (H1 != H0), SAME filename
  → controlled trigger observes R1
  → new manifest references @R1
  → new Studio production release references @R1 (separately authorized)
  → URL changed / observed displayed image bytes correspond H1
  → old @R0 keeps H0 for rollback
```

Do not label this automated unless the whole **commit-event → controlled manifest/Studio version → allowed deployment** chain is implemented, reliable, authenticated and verified after an actual controlled push. jsDelivr purge alone is not the accepted freshness mechanism. Record exact resource SHA, website deployment SHA, URL, response MIME/cache headers and screenshot pixels before/after. Never trigger a paid CI/build or auto-deploy just to demonstrate the concept.

## 4. Trigger options — discovery first, do not choose blindly

- **GitHub Actions** resource push → immutable manifest update → approved Studio change → website build. Requires checking actual Actions budget and usage hard stops; prior account observations of an Actions `$0` budget with Stop Usage mean a trigger might be disabled despite public free minutes. Check repository Actions permissions, Vercel Git integration and free quota **read-only** first.
- **Vercel Deploy Hook** or provider event: could create an immediate deployment and must NOT be invoked without G4/G6 owner release authorization, cost and secret model.
- **Manual manifest update** can be a temporary bounded authoring workflow, but **does not satisfy** the ratified *automatic same-filename refresh* unless the owner explicitly amends the required outcome. An unproved cron/cache purge is not an acceptable substitute.

## 5. Negative/fault acceptance

- Missing/404 `background.webp` and unknown asset: meaningful bounded placeholder or decorative fallback, no broken huge layout or inaccessible navigation.
- CDN 404, timeout, wrong content-type, empty response, stale prior bytes: visible fallback, telemetry does not leak request identifiers, no infinite retry.
- Same-name image bytes update: manifests and page URL change by SHA and load H1; old URL shows H0 deterministically.
- CSS responsive at 320/375/768/1440, alt semantics for decorative vs meaningful, image dimensions prevent CLS, correct priority for LCP and lazy for offscreen.
- Security: reject untrusted external URLs and oversized/media-format surprises; no arbitrary remote fetch proxy.
- Unit tests for manifest mapping, collision, invalid source and missing files, plus local fixture image comparisons; integration verification on owner-approved preview/prod only.

## 6. W3 gated stages

**W3A read-only:** inventory actual `/images/` references, resource repo path/case, current Vercel and jsDelivr behavior, `next.config.mjs` patterns, production 404 class, GitHub Actions budget/trigger feasibility.

**W3B separate owner signoff:** exact source/resource repository allowlist and cheapest viable trigger consistent with hard `Rp0`. If no available reliable free trigger, `W3_AUTOMATION=BLOCKED` pending a specific decision, not silently downgraded.

**W3C:** scoped isolated TypeScript manifest/fallback implementation, fault tests and owner-approved controlled same-name asset fixture (never mutate author protected content).

**W3D:** separate G3 source PR, G4 preview and G6 production acceptance.

Current `W3_IMAGE_DEFECT=OPEN`, `W3_IMMUTABLE_REFRESH=NOT_IMPLEMENTED`, `WEB-AC10..12=PENDING`. No source commits, provider hooks, CDN purge or deployments permitted from this document.
