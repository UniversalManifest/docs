# WO-0082 — Remove or Qualify Implementation-Specific References in Spec Documents

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P0 (Critical)
**Source:** Spec-vs-Implementation Boundary Audit (2026-03-01), Findings 3.1, Recommendations R2-R4, R8, R13, Action Items 2-5, 11, 13
**Tags:** [spec], [implementation]
**Blocks:** Spec document purity; prevents confusion about normative requirements
**Dependencies:** None
**Estimated effort:** 3-5 hours

## Objective

Remove, qualify, or relocate all implementation-specific references from normative and spec-adjacent documents in the `spec/` directory. Spec documents must describe WHAT implementations must do, not HOW a specific TypeScript implementation does it.

## Why this work matters

The boundary audit identified seven specific instances of implementation leakage in spec documents, including device brand names, direct file path references to the TypeScript helper, and SHOULD-language references to implementation-specific guidance documents.

## Scope

### HIGH severity fixes

1. **`/Users/grig/work/repo/universalmanifest/spec/v0.1/README.md` line 49** — Change section header "ID + caching guidance (Shield / public display)" to "ID + caching guidance (constrained devices / public displays)". Remove the NVIDIA Shield brand name.

2. **`/Users/grig/work/repo/universalmanifest/spec/v0.1/README.md` line 78** — Remove or relocate "Reference implementation: `/packages/universal-manifest/src/index.ts`" from the Security Considerations section. Replace with a non-normative note: "See the conformance fixtures for validation examples. A TypeScript reference implementation is available in `packages/universal-manifest/` for those who want one."

3. **`/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md` line 47** — Remove or relocate "Reference implementation: `/packages/universal-manifest/src/index.ts:272-302`" with specific line numbers. Replace with the same non-normative note pattern.

### MEDIUM severity fixes

4. **`/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md` line 61** — Change "Consumers SHOULD follow `integrations/reference-runtime.md` guidance" to "See `integrations/reference-runtime.md` for one reference implementation pattern (non-normative)." Remove the SHOULD keyword from this non-normative reference.

5. **`/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md` lines 131-135** — Qualify the "Reference harness (repo-local)" section. Change from directing to `packages/universal-manifest/ -> npm test` to "TypeScript reference harness (one of many possible implementations): `packages/universal-manifest/ -> npm test`."

6. **`/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md` lines 96-98** — Apply the same qualification to the v0.2 "Reference harness" section.

### LOW severity fixes

7. **`/Users/grig/work/repo/universalmanifest/spec/v0.1/REGISTRY.md` line 14** — Change "Pointer to canonical identity/profile source (often a Solid Pod URL)" to "Pointer to canonical identity/profile source (any stable URL)." Remove the Solid Pod technology reference.

## Acceptance criteria

- [ ] No spec document in `spec/` contains the word "Shield" (referring to NVIDIA Shield).
- [ ] No spec document contains inline file path references to `packages/universal-manifest/src/index.ts` without non-normative qualification.
- [ ] No conformance document uses SHOULD language to reference implementation-specific guidance.
- [ ] All "Reference harness" sections are explicitly qualified as "one reference implementation."
- [ ] No spec document references "Solid Pod" as a specific technology.
- [ ] `rg -n "Shield" /Users/grig/work/repo/universalmanifest/spec/` returns zero matches.
- [ ] `rg -n "index.ts" /Users/grig/work/repo/universalmanifest/spec/` returns zero unqualified matches.

## Validation commands

- `rg -n "Shield" /Users/grig/work/repo/universalmanifest/spec/`
- `rg -n "index.ts" /Users/grig/work/repo/universalmanifest/spec/`
- `rg -n "Solid Pod" /Users/grig/work/repo/universalmanifest/spec/`
- `rg -n "SHOULD.*reference-runtime" /Users/grig/work/repo/universalmanifest/spec/`
