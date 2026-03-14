# WO-0089 — Fix Legacy Naming and Branding Leaks

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P2 (Nice-to-have)
**Source:** Spec-vs-Implementation Boundary Audit (2026-03-01), Findings 3.5, Action Items 16-18
**Tags:** [docs], [implementation]
**Blocks:** None (polish)
**Dependencies:** None
**Estimated effort:** 1-2 hours

## Resolution

1. **`docs/TS-HELPER-PACKAGE.md`**: Updated package name to `universal-manifest` with explicit legacy note for `@localartistnetwork/universal-manifest`.
2. **`site/src/content/docs/governance/decisions.md`**: Replaced "Shield" with "constrained device" in the device caching decision header.
3. **`docs/UNIVERSAL-MANIFEST-BRIEFING.md`**: Replaced "NVIDIA Shield TV Pro enrolled to venue edge" with "Public display device enrolled to venue edge"; replaced "NVIDIA Shield TV Pro as a public display" with "a public display device (e.g., an Android TV)"; replaced "NVIDIA Shield" with "public display device" in fixture list description.
4. **`docs/DECISIONS.md`**: Updated "NVIDIA Shield / public display" header to "constrained device / public display" and noted legacy package name.
5. **`docs/STATE-OF-THE-PROJECT.md`**: Replaced "Shield caching" with "device caching" in integration notes.
6. **`docs/DEPTH-AND-SCOPE.md`**: Replaced "Shield storage/transport" with "device storage/transport".

## Objective

Clean up legacy naming artifacts and implementation-specific branding references that remain in documentation and governance pages.

## Why this work matters

Legacy naming creates confusion about the project's current identity and scope. Brand names for specific devices (NVIDIA Shield) appearing in spec-adjacent text suggest implementation specificity that does not belong at the spec level.

## Scope

### Files to modify

1. **`docs/TS-HELPER-PACKAGE.md`** (line 14)
   - Update the legacy `@localartistnetwork/universal-manifest` package name to the current package name (or add a note that this is the legacy name and the current name is X).

2. **`site/src/content/docs/governance/decisions.md`** (line 18)
   - Remove or qualify "Device caching + logging (public display / Shield)" — replace "Shield" with "constrained device" or "public display device."

3. **`docs/UNIVERSAL-MANIFEST-BRIEFING.md`** (line 234)
   - Review the fixture example mentioning "NVIDIA Shield TV Pro enrolled to venue edge" — consider replacing with a generic device description like "public display device enrolled to venue edge."

## Acceptance criteria

- [ ] No document outside of `integrations/reference-runtime.md` and fixture files uses the "Shield" device brand name without context.
- [ ] The legacy `@localartistnetwork` package scope is either updated or explicitly noted as legacy.
- [ ] `rg -n "Shield" site/src/content/docs/` returns zero unqualified results.

## Validation commands

- `rg -n "@localartistnetwork" docs/`
- `rg -n "Shield" site/src/content/docs/`
- `rg -n "NVIDIA" docs/` (should return only integration/fixture references)
