# WO-0039 Completion Report — Onboarding Language Hardening

**Date:** 2026-02-23
**Work Order:** WO-0039
**Status:** Phases 1-4 complete, Phase 5 blocked on human participation
**Completion Agent:** Claude (Sonnet 4.5)

## Executive summary

WO-0039 addressed plain-language clarity issues in first-read onboarding documentation and implemented automated guardrails to prevent regression. Phases 1-4 are complete with all verification tests passing. Phase 5 (human reader validation) requires human participation and remains incomplete.

## Completed phases

### Phase 1 — Inventory and source map

**Deliverable:** Source map report
**Location:** `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-22-wo-0039-onboarding-language-source-map-and-rewrite-plan.md`

Completed full inventory of all wording sources that affect onboarding narrative, including:
- First-read documentation pages (4 files)
- Example manifests and test fixtures
- Backend service documentation
- Tooling scripts and error messages
- Template files and stub content

### Phase 2 — Onboarding rewrite

**Files modified:** 4 first-read documentation pages

All first-read pages were rewritten to use plain language with inline definitions for technical terms:

1. `/Users/grig/work/repo/universalmanifest/site/src/content/docs/index.md`
2. `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md`
3. `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/concepts.md`
4. `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/quick-start.md`

Key improvements:
- Removed undefined jargon (e.g., "integration pair", "brittle mappings")
- Replaced with clear explanations (e.g., "each pair of systems", "custom data format for every pair of systems")
- Added inline definitions for all restricted terms within 2 lines of first use
- Maintained technical accuracy while improving readability

### Phase 3 — Propagation fixes (docs + backend/tooling)

**Files updated:** 67 files across docs, examples, and backend services

Updated all identified source files that could reintroduce stale wording:

**Documentation updates:**
- Site navigation and configuration files
- Integration guides (OMA Trust, Chia VC, social, metaverse, spatial)
- Specification and conformance pages (v0.1, v0.2)
- Publishing and deployment guides
- Proof and governance documentation

**Example manifest updates:**
- Valid examples (v0.1, v0.2)
- Invalid examples (structural and validation failures)
- Stub manifests for all integration scenarios

**Backend and tooling updates:**
- Service documentation (myum-resolver)
- Journey runner scripts
- Validation scripts
- Test harness files

See source map report for complete file list with change rationale.

### Phase 4 — Guardrail automation

**Deliverable:** Automated terminology guard script
**Location:** `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/check-terminology.mjs`
**Command:** `npm run check:terminology`

Implemented automated terminology/readability guard with:

**Features:**
- Scans first-read documentation for banned and restricted terms
- BANNED patterns: Must never appear (e.g., "integration pair", "CEO-directed", "MUM")
- RESTRICTED patterns: Must have inline definition within 2 lines (e.g., "facets", "UMID", "TTL", "pointers")
- Definition detection using multiple heuristics:
  - Parenthetical definitions: "UMID (Universal Manifest Identifier)"
  - Colon definitions: "UMID: the Universal..."
  - Sentence patterns: "is a", "is the", "called", "means", "refers to"
  - Emphasis patterns: bold/italic with explanatory text
- Exit code 0 on success, 1 on violations
- Clear violation reporting with file paths and line numbers

**Wired to npm script:**
```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm run check:terminology
```

**Policy documentation:**
- Pattern maintenance documented in script header
- Add new patterns to BANNED_PATTERNS or RESTRICTED_PATTERNS arrays
- Use regex word boundaries for whole-word matching

## Terminology violations fixed (2026-02-23)

Initial run of guard script found 6 restricted-term violations. All were fixed by adding inline definitions:

### 1. "Harness" violation
**File:** `/Users/grig/work/repo/universalmanifest/site/src/content/docs/index.md:41`
**Fix:** Added inline definition "(browser-based tools for creating, editing, and validating manifests)"
**Context:** Tools section describing Manifest Workbench and Verification Harness

### 2. "facets" and "TTL" violations
**File:** `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md:63`
**Fix:** Added inline definitions "TTL (time-to-live validity window)" and "facets (named data sections)"
**Context:** "How to start" section listing core concepts

### 3. "facets" violation in code block
**File:** `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/concepts.md:71`
**Fix:** Added inline definition in example introduction "Below is a manifest with two facets (named data sections):" and added comment in code block
**Context:** Section 4 example showing facets structure

### 4. "pointers" violation in code block
**File:** `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/concepts.md:98`
**Fix:** Modified section header definition and added comment in code block "Below shows pointers (URL references to authoritative sources):"
**Context:** Section 5 example showing pointers structure

### 5. "UMID" violation
**File:** `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/concepts.md:33`
**Fix:** Added inline definition in Example line "In the manifest above, the UMID (the unique `@id` identifier) is..."
**Context:** Section 1 example explaining UMID field

## Verification results

All verification tests pass:

### 1. Terminology guard
```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm run check:terminology
```
**Result:** ✓ No violations found. All terminology checks passed. (Exit code 0)

### 2. Test suite
```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm test
```
**Result:**
- 21 valid examples OK
- 19 invalid examples OK (expected invalid, correctly rejected)
- 0 failures

### 3. Journeys
```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm run journeys
```
**Result:**
- Preflight: 1 pass, 0 fail
- Journeys: 11 pass, 0 fail
- Report: `/Users/grig/work/repo/universalmanifest/docs/journeys/_artifacts/2026-02-23T03-12-36-425Z-journey-report.json`

### 4. Site build
```bash
cd /Users/grig/work/repo/universalmanifest/site
npm run build:clean
```
**Result:**
- Built 32 pages successfully
- Pagefind indexed 31 pages, 1610 words
- Sitemap created
- No build errors

### 5. Production endpoints
```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm run smoke:endpoints:prod
```
**Result:** PASS
- Docs endpoints: /, /conformance/resolver/, /harness/index.html, ns schema.jsonld, /404.html (all OK)
- Resolver endpoints: /health, /.well-known/myum-resolver.json, resolve umid, resolve b64u:umid (all OK)

## Acceptance criteria status

| Criterion | Status | Evidence |
|-----------|--------|----------|
| First-read sections no longer assume unexplained jargon | ✓ Complete | All first-read pages rewritten with inline definitions |
| Terms like "integration pair" removed or defined | ✓ Complete | Removed from all first-read content, replaced with plain language |
| Source-map report identifies injection points | ✓ Complete | Source map report covers 67 files across all surfaces |
| No stale phrasing remains after rewrite | ✓ Complete | All 67 identified files updated per source map |
| Automated guard passes and fails correctly | ✓ Complete | Guard script implemented, tested, and passing |
| Human-reader evidence published | ✗ Blocked | Requires human participation (Phase 5) |
| WO-0015 and WO-0035 references updated | ✓ Complete | References aligned with rewritten baseline |

## Files modified

### First-read documentation (Phase 2)
1. `/Users/grig/work/repo/universalmanifest/site/src/content/docs/index.md`
2. `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md`
3. `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/concepts.md`
4. `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/quick-start.md`

### Terminology violation fixes (2026-02-23)
5. `/Users/grig/work/repo/universalmanifest/site/src/content/docs/index.md` (Harness definition)
6. `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/universal-manifest-overview.md` (facets, TTL definitions)
7. `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/concepts.md` (UMID, facets, pointers definitions)

### Propagation fixes (Phase 3)
See source map report for complete list of 67 files updated across:
- Site documentation and navigation
- Example manifests (valid and invalid)
- Integration guides
- Specification and conformance pages
- Backend service documentation
- Journey and validation scripts
- Test fixtures and harness files

### Guardrail automation (Phase 4)
8. `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/check-terminology.mjs` (new file)
9. `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/package.json` (added check:terminology script)

## Remaining work

### Phase 5 — Human validation and closure evidence

**Status:** Blocked on human participation

**Required:**
1. Execute human-reader check on rewritten onboarding pages
2. Publish dated evidence artifact showing comprehension outcomes
3. Link evidence artifact in WO-0039

**Recommendation:** Recruit 2-3 readers unfamiliar with Universal Manifest to read first-read pages and answer comprehension questions. Document results in timestamped evidence artifact.

## Related work orders

- **WO-0015**: First-time overview and visual onboarding (references updated to rewritten baseline)
- **WO-0035**: Human reader testing policy and onboarding evidence alignment (references updated)

## References

- **Source map report:** `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-22-wo-0039-onboarding-language-source-map-and-rewrite-plan.md`
- **Work order:** `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0039-onboarding-plain-language-rewrite-and-source-propagation-hardening.md`
- **Terminology guard script:** `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/check-terminology.mjs`
- **Latest journey report:** `/Users/grig/work/repo/universalmanifest/docs/journeys/_artifacts/2026-02-23T03-12-36-425Z-journey-report.json`

## Conclusion

WO-0039 Phases 1-4 are complete with all automated verification tests passing. The first-read onboarding documentation now uses plain language with inline definitions for all technical terms, and an automated terminology guard prevents regression. Phase 5 (human reader validation) requires human participation and is the only remaining acceptance criterion.

The project now has a hardened onboarding experience with automated quality gates that will maintain plain-language standards over time.

---

**Completion timestamp:** 2026-02-23T03:12:00Z
**Verification status:** All automated tests pass
**Next action:** Execute Phase 5 human reader validation when human participants are available
