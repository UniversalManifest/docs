# WO-0083 — Restructure Root README Quick Start to Lead with the Specification

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P0 (Critical)
**Source:** Spec-vs-Implementation Boundary Audit (2026-03-01), Recommendation R6, Action Item 4
**Tags:** [docs], [onboarding]
**Blocks:** First-contact perception of UM
**Dependencies:** WO-0081 (banner should be in place first)
**Estimated effort:** 1-2 hours

## Objective

Restructure the root `README.md` Quick Start section so it leads with the specification and fixtures, not with `cd packages/universal-manifest && npm test`.

## Why this work matters

The root README is the first thing a newcomer sees on GitHub. Currently, its Quick Start section immediately sends the reader to `cd packages/universal-manifest && npm test`, framing UM as "a TypeScript project you install" rather than "a specification you read and implement."

## Scope

### File to modify

**`/Users/grig/work/repo/universalmanifest/README.md`** (lines 17-23, Quick Start section)

### New Quick Start structure

Replace the current Quick Start with:

1. **Read the v0.1 specification** — link to `spec/v0.1/README.md`
2. **Review example manifests** — link to `examples/v0.1/` fixtures
3. **Read the conformance requirements** — link to `spec/v0.1/CONFORMANCE.md`
4. **Browse the interactive sandbox** — link to `universalmanifest.net/sandbox/`
5. *(Optional)* **Try the TypeScript reference implementation** — `cd packages/universal-manifest && npm test` (qualified as "if using TypeScript/JavaScript")

### Also update

- **`/Users/grig/work/repo/universalmanifest/PROJECT-RULES.md`** (lines 43-48) — The "Build, Test, and Development Commands" section lists only npm/TS commands. Add a note that these are specific to the TypeScript reference implementation, and that the spec itself is language-neutral.

## Acceptance criteria

- [ ] Root README Quick Start leads with reading the spec, not running npm commands.
- [ ] The TypeScript helper is positioned as step 4 or 5, not step 1.
- [ ] The TypeScript step is explicitly qualified as optional and language-specific.
- [ ] PROJECT-RULES.md notes that commands are for the TypeScript reference implementation.
- [ ] A first-time reader following the Quick Start would read the spec before encountering any TypeScript code.

## Validation commands

- Manual review of `/Users/grig/work/repo/universalmanifest/README.md` Quick Start section ordering.
- `rg -n "npm test" /Users/grig/work/repo/universalmanifest/README.md` (should appear only in the optional TypeScript section).
