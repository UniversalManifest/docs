# Branding Fix: Schema ID Update and Remaining Work

**Date:** 2026-02-26
**Scope:** Fix legacy `localartist.network` references in schema files and document remaining package/type branding issues

---

## 1. Completed: Schema `$id` Fix

### Fixed Files

**File:** `/Users/grig/work/repo/universalmanifest/spec/v0.1/schema.json`

**Change:**
```diff
-  "$id": "https://localartist.network/ns/universal-manifest/v0.1/schema.json",
+  "$id": "https://universalmanifest.net/ns/universal-manifest/v0.1/schema.json",
```

**Status:** Complete
- v0.1 schema now references correct domain
- v0.2 schema already used `universalmanifest.net` (no change needed)
- Both v0.1 and v0.2 `schema.jsonld` files already used correct domain (no change needed)

### Verification Results

All test suites pass after the fix:

1. **Package tests:** `npm test` - PASS (40/40 fixtures validated)
2. **Journey tests:** `npm run journeys` - PASS (1 preflight + 11 journeys)
3. **Site build:** `npm run build:clean` - SUCCESS (32 pages built, no errors)

---

## 2. Remaining Branding Issues (Phase B Work)

### 2.1 Package Name

**Current:** `@localartistnetwork/universal-manifest`
**Recommended:** `@universalmanifest/core` or `universal-manifest`

**Location:** `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/package.json`

**Impact:** HIGH
- npm publication blocked by legacy naming
- External developers cannot install with current name
- Creates confusion about project ownership/governance

**Blockers for rename:**
- Would break existing imports (though package is currently private, so no external users)
- Requires coordinated update of all import statements
- Needs update to CI/CD configuration
- Should be done as part of pre-publication prep

**Recommendation:** Defer to Phase B (WO-0045) when preparing for npm publication

---

### 2.2 TypeScript Type Names

**Current:** All exported types use `Lan` prefix (legacy from "Local Artist Network")
- `LanEntityV01`
- `LanShardV01`
- `LanSignatureV01`
- `LanSignatureV02`

**Recommended:** Use neutral prefix
- Option A: `UmEntity`, `UmShard`, `UmSignature` (Um = Universal Manifest)
- Option B: `UniversalManifestEntity`, etc. (more verbose but clearer)
- Option C: No prefix, just `Entity`, `Shard`, `Signature` (simplest)

**Location:** `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/src/index.ts`

**Impact:** HIGH
- Creates confusion about project identity
- Would be embarrassing if presented at standards conference
- Breaking change for any existing TypeScript consumers (though none exist yet)

**Affected exports:**
```typescript
export interface LanEntityV01 { ... }
export interface LanShardV01 { ... }
export interface LanSignatureV01 { ... }
export interface LanSignatureV02 { ... }
```

**Usage count:** 9 references total in `index.ts`

**Recommendation:** Rename as part of Phase B (WO-0045), coordinated with package rename

---

### 2.3 No Other Legacy References Found

**Verified clean:**
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/src/` - No `localartist` strings
- `/Users/grig/work/repo/universalmanifest/services/` - No `localartist` strings
- Spec text files - Already use `universalmanifest.net`
- Example fixtures - Already use correct domain
- Documentation site - Already uses correct branding

---

## 3. Gap Analysis Alignment

This work addresses the following items from `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-23-remaining-work-to-final-vision.md`:

### Completed
- **SPEC-001** (CRITICAL): v0.1 `schema.json` `$id` now references `universalmanifest.net` - RESOLVED

### Documented (Phase B)
- **TS-001** (CRITICAL): Package name uses `@localartistnetwork/` prefix - DOCUMENTED
- **TS-008** (HIGH): Type names use `Lan` prefix - DOCUMENTED

---

## 4. Recommended Next Steps

### Immediate (No action needed)
The schema fix is complete and verified. No further action required at this time.

### Phase B (WO-0045: Schema and Naming Normalization)
When ready to prepare for npm publication:

1. **Rename package**
   - Choose neutral name (recommend: `@universalmanifest/core`)
   - Update `package.json`
   - Update all import statements in examples/docs
   - Update CI workflow

2. **Rename TypeScript types**
   - Choose prefix strategy (recommend: `Um` prefix for brevity)
   - Update all type definitions in `src/index.ts`
   - Run full test suite to verify
   - Update any documentation that references types

3. **Update CHANGELOG**
   - Document the breaking changes
   - Provide migration guide for any early adopters

**Estimated effort for Phase B:** 1 day (as per gap analysis)

---

## 5. Breaking Change Impact Assessment

### Current Risk: LOW
- Package is marked `private: true` in package.json
- No external npm installations exist
- No known external TypeScript consumers
- All usage is internal to this repository

### Phase B Risk: MEDIUM
- Type renames will break any TypeScript code using the old names
- Package rename will break any import statements
- However, since package is currently private, external impact is zero
- Internal impact limited to this repository (easily fixed)

### Mitigation Strategy
- Coordinate rename with initial npm publication
- Document breaking changes in CHANGELOG
- Provide clear migration instructions
- Consider deprecation notice if any early adopters exist

---

## 6. Verification Commands

To verify the current state at any time:

```bash
# Check for remaining localartist references
rg "localartist" /Users/grig/work/repo/universalmanifest/spec/
rg "localartist" /Users/grig/work/repo/universalmanifest/packages/universal-manifest/

# Check Lan type prefixes
rg "^export.*Lan" /Users/grig/work/repo/universalmanifest/packages/universal-manifest/src/index.ts
rg "Lan[A-Z]" /Users/grig/work/repo/universalmanifest/packages/universal-manifest/src/index.ts

# Verify tests still pass
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm test
npm run journeys

# Verify site builds
cd /Users/grig/work/repo/universalmanifest/site
npm run build:clean
```

---

**Summary:** Schema `$id` fix is complete and verified. Package and type renaming documented for Phase B coordination with npm publication. All tests pass. No git commit created per instructions.
