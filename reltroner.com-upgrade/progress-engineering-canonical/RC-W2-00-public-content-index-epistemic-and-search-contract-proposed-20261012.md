# RC-W2-00 — Proposed Canonical Public Content Index, Epistemic Taxonomy and Shared Search Contract

> **Status: CONTRACT DRAFT / W2 SOURCE WORK NOT YET AUTHORIZED**. This starts W2 **architecture/contract preparation**, not implementation or G3/G4 permission. Owner must separately ratify file allowlist, exact branch/SHA, test budget and negative fixtures before an IDE agent changes Studio files.
> **Normative parents:** [Ratified WEB-I04–I07](../00-ratified-frontend-architecture-contract-20261012.md), [WEB-AC05..09](../03-phase1-acceptance-and-invariant-traceability.md), [frontend component design](../06-frontend-component-and-content-architecture.md); W1 `RC-W1-18` residual is not automatically waived.
> **Source baseline:** GitHub Studio main `18b295f96ccb521b228a1855e79448158c09db15` checked 2026-10-12. Read-only examined `lib/utils/content.js`, `types/content.ts`, `components/layout/CommandPalette{,Dialog}.tsx`, `components/worldbuilding/{CollectionPageClient,ContentEntryPage}.tsx`, `lib/constants/collections` and `app/layout.tsx`. Any source implementation uses refreshed SHA and a **new isolated worktree/branch**, preserving primary's 14 untracked author Markdown.

## 1. Existing source facts and design problems

- `getCollectionEntries` derives from Git/Markdown and filters published entries in a known listing path, but published-only semantics of *all* full route, rendered Markdown, sitemap and AI read paths are not yet negative-tested. Treat `getCollectionEntry` and alias route behavior as untrusted until audited.
- `types/content.ts` already defines `ContentEntry` including `published`, `route`, `aliases`, `collection`, title/description/tags/type and file paths; using `any` in rendering/search does not constitute a shared versioned index.
- Global `CommandPaletteDialog.tsx` has `scoreCommandMatch` custom matching; `CollectionPageClient.tsx` has a different local string includes filter over `getSearchValues`. Distinct indexes/scoring can hide or reorder content unpredictably.
- `ContentEntryPage.tsx` places a ReadingPath inside the bounded editorial shell; its breadcrumb target `/#knowledge` currently mismatches `#knowledge-bridge`. Preserve deep routes while separately tracking baseline anchors.

## 2. Index contract (proposed, not a code change)

**Single source of truth:** published Git Markdown source at a frozen Studio commit, with validated frontmatter. **Derived build artifact** `PublicIndexSnapshot` is disposable and regenerable, not a replacement authority.

```ts
type EpistemicType =
  | 'FICTION_CANON'
  | 'FICTION_SPECULATIVE'
  | 'REAL_WORLD_ANALYSIS'
  | 'CREATIVE_FRAMEWORK'
  | 'ENGINEERING_CASE_STUDY'
  | 'CROSS_DOMAIN_ANALOGY';

type PublicIndexEntry = {
  id: string;                // stable collection + slug identity
  collection: string;        // existing route-compatible collection
  slug: string;
  canonicalPath: string;     // /collection/slug, never draft path
  aliases: string[];        // explicit reviewed redirects only
  title: string;
  description: string;
  searchableText: string;    // bounded sanitized human-language excerpt
  tags: string[];
  epistemicType: EpistemicType;
  canonStatus?: 'CANON' | 'SPECULATIVE' | 'NOT_APPLICABLE';
  updatedAt?: string;
  publishedAt?: string;
  revision: string;          // deterministic per public source content
};

type PublicIndexSnapshot = {
  schemaVersion: 1;
  sourceCommit: string;      // exact Git Studio SHA or build provenance
  generatedAt: string;       // metadata only; not part of stable hash
  contentHash: string;       // stable hash over canonical ordered entries
  entries: PublicIndexEntry[];
};
```

**Determinism:** trim/normalize Unicode and whitespace; canonicalize route strings; sort by canonicalPath ascending (stable tie-breaker id); ensure no canonical/alias collision, duplicate id or path, path traversal, HTML/script in snippets or unsafe URI schemes. `revision` derived from source bytes and approved metadata, not mutable wall time. `generatedAt` excluded from `contentHash`; two clean builds at the same source commit produce the same contentHash and ordering. `sourceCommit` provenance must represent **actual candidate source**; do not falsely label uncommitted local changes with remote main SHA.

**Default exclusion:** `published !== true` → EXCLUDE everywhere (deny by default). Ambiguous published status, malformed files, missing classification, missing route mapping or duplicate alias → **CI build FAIL_CLOSED or EXPLICIT_REVIEW_REQUIRED**, never silently promote unpublished entries. In transitional metadata, allow only **explicit owner-reviewed per-entry overrides/migration mapping**; do not globally infer six epistemic classes from route or names. Real-world and fictional statements must stay distinguishable; no real-world claims derived from Asthortera statistical fiction.

**Surfaces using same snapshot/predicate:**
```text
Git published source
   ↓ validate frontmatter + publication + epistemic review
PublicIndexSnapshot v1
   ├── global Ctrl+K (same scoring, shared index revision)
   ├── collection-scoped Archive Explorer (filters are views, not new index)
   ├── related content & Reading Path navigation
   ├── sitemap/static public listing
   └── future W5 read-only retrieval (same publication gate; citation + revision)
```

Individual full entry static route HTML and rich Markdown embed renderer remain a **separate security check** to ensure private draft content cannot bypass the index. No API route exposing file paths or raw unpublished source.

## 3. Shared search semantics

All clients call a single pure search function over `PublicIndexSnapshot`: case/Unicode normalization, exact title and slug boost > title prefix > title term > tag/category > summary full text, stable tie-break by canonicalPath. Same query against Ctrl+K and archive rail, after applying equivalent collection filter, yields the same ordered route IDs. Collection filter must never override explicit “All archives” pathway. Pagination/visible limits must not silently imply 0 results in other collections. Shared empty/error/loading/focus behavior, keyboard Escape/focus-return semantics.

## 4. Adaptive rails scope

On article desktop: left sticky Reading Path to h2/h3 headings; center editorial width limited to roughly 65–76 chars/line; right sticky Archive Explorer (collection selection, search, related content and evidence/canon metadata). On collection index, avoid empty article ToC: collection navigation and index search instead. At narrower widths collapse to distinct accessible drawers or inline controls; preserve skip link, Esc close, focus trap when modal, focus return after close, motion-reduce and no 320px horizontal overflow. No duplicate chatbot that competes with W5 launcher. Existing `ContentEntryPage`/CollectionPageClient should be **refactored minimally**, not forked into parallel implementations.

## 5. W2 candidate sequencing; no current source allowlist

- W2A: read-only exact route/publication inventory; classify malformed frontmatter, alias conflicts, missing taxonomy. Output `public-index-inventory.json` only in external evidence directory; do NOT publish private draft excerpts or copy protected 14 owner files.
- W2B: owner approval for **exact new TS/TSX file list** and minimal bounded migration; source implementation guarded by new branch and explicit tests. Candidate files (not authorized yet): `lib/content/{taxonomy,public-index,search}.ts`, `types/content.ts`, `components/layout/CommandPaletteDialog.tsx`, `components/worldbuilding/{CollectionPageClient,ContentEntryPage}.tsx` and proposed rails. Do not assume a blanket allowlist or rename `content.js` merely for style.
- W2C: unit tests on deterministic index, shared search ranking and negative published-only fixture, then reading rail browser QA mobile/desktop.
- W2D: separate G3 source/PR evidence and W7 negative publication test handoff.

## 6. Minimum acceptance and STOP

Required evidence: same SHA/snapshot hash across search surfaces; distinct six epistemic classes with human-reviewed ambiguous entries; correct canonical/aliases; old permalink stability; unpublished fixture absent from index/search/static/HTML/sitemap/future AI; malformed file causes controlled build failure; 320/375/768/1440 keyboard and desktop/mobility reading rails; no new external service/billing; no primary worktree edits. **No source writes authorized by this draft.**

STOP on any classification ambiguity that cannot be safely mapped, private draft leak, unapproved content-file mutation, changed current Git SHA, third-party provider need, or missing deterministic test fixture. Owner signoff needed before W2 implementation.
