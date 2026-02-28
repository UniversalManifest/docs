# WO-0057 — Spec-vs-Implementation Documentation Clarity

**Status:** NOT_STARTED
**Created:** 2026-02-27
**Priority:** HIGH
**Blocks:** Gate G4 (Interoperability proof — prevents "UM = TypeScript" perception)
**Dependencies:** WO-0054 (Reference Implementation Repository — must exist to point to)
**Estimated effort:** 1 week

## Objective

Audit and update all documentation to clearly and consistently distinguish the Universal Manifest specification from any particular implementation. Ensure the TypeScript helper is positioned as ONE implementation (the reference implementation), not THE implementation. Add explicit calls-to-action for external implementations throughout the documentation.

## Why this work matters

Universal Manifest is a specification, not an implementation. However, because the spec repo also contains a TypeScript helper (`packages/universal-manifest/`), documentation can inadvertently suggest that UM "is" the TypeScript package. This perception is fatal for Gate G4:

- External adopters may believe they need to use TypeScript.
- External adopters may believe the TypeScript helper IS the spec and that they need to replicate its internals.
- The project may appear to be a single-implementation project rather than an open specification.

Clear spec-vs-implementation messaging is a prerequisite for credible multi-party adoption.

## Scope

In scope:

- Audit all documentation (spec, docs site, integrations, README files) for spec-vs-implementation confusion.
- Add explicit "UM is a specification" messaging to key entry points.
- Reposition the TypeScript helper as "one reference implementation" throughout.
- Add calls-to-action for external implementations (e.g., "Build your own implementation in any language").
- Update the docs site navigation to separate spec content from implementation content.
- Ensure code examples in docs are marked as "reference implementation" not "the way to do it."

Out of scope:

- Removing the TypeScript helper from the spec repo (future WO, after WO-0054 is complete).
- Rewriting the TypeScript helper.
- Changing normative spec text semantics.

## Execution phases

### Phase 1 — Documentation audit

- [ ] Scan all documentation for spec-vs-implementation confusion patterns:
  - References to `packages/universal-manifest/` as if it were the spec.
  - Language like "UM uses Ed25519" (spec says; implementation demonstrates).
  - Missing "this is one implementation" qualifiers on code examples.
  - Absence of "you can implement this in any language" messaging.
  - Integration docs that assume TypeScript/Node.js.
- [ ] Produce an audit report listing every instance with file path, line number, and proposed fix.
- [ ] Key files to audit:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/README.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/README.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/` (all pages)
  - `/Users/grig/work/repo/universalmanifest/integrations/` (all files)
  - `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
  - `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md`
  - `/Users/grig/work/repo/universalmanifest/README.md`

### Phase 2 — Key entry-point messaging updates

- [ ] Add "UM is a specification" banner or callout to:
  - Docs site landing page (`site/src/content/docs/index.md`)
  - Spec README files (`spec/v0.1/README.md`, `spec/v0.2/README.md`)
  - Root `README.md`
- [ ] Standard language template:
  ```
  Universal Manifest is an open specification for portable state capsules.
  It is not tied to any particular programming language, framework, or runtime.
  The TypeScript helper in this repository is a reference implementation;
  you can build a conformant implementation in any language.
  ```
- [ ] Add "Build Your Own Implementation" call-to-action:
  - Link to implementation guide (WO-0055).
  - Link to conformance suite (WO-0053).
  - Link to reference implementation (WO-0054) as a starting template.

### Phase 3 — Code example qualification

- [ ] Add headers/notes to all code examples in docs:
  - "This example uses the TypeScript reference implementation. The same operations can be performed in any language that implements the UM spec."
- [ ] Where possible, add pseudocode or multi-language examples alongside TypeScript.
- [ ] Ensure conformance docs reference the conformance suite (language-agnostic) rather than the TypeScript validator directly.

### Phase 4 — Navigation and information architecture updates

- [ ] Review docs site sidebar for spec-vs-implementation separation:
  - "Specification" section: spec versions, conformance, signature profile.
  - "Implementations" section: reference implementation, adopter registry, conformance suite.
  - "Guides" section: implementation guide, quick-start, migration.
- [ ] Ensure the TypeScript helper page (`getting-started/typescript-helper.md`) clearly states it is ONE implementation.
- [ ] Add a "Known Implementations" page linking to:
  - Reference implementation (WO-0054).
  - Adopter registry (WO-0056).

### Phase 5 — Integration docs updates

- [ ] Review each integration page in `integrations/` and `site/src/content/docs/integrations/`:
  - Ensure guidance is spec-level (what any implementation should do), not TypeScript-specific.
  - Add notes when TypeScript-specific examples are used.
  - Include language like "Any conformant UM implementation can be used for this integration."

## Key file paths (created/modified)

Modified files (partial list; full list from audit):
- `/Users/grig/work/repo/universalmanifest/README.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.1/README.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/README.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/index.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/` (multiple pages)
- `/Users/grig/work/repo/universalmanifest/integrations/` (multiple files)
- `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`

New files:
- `/Users/grig/work/repo/universalmanifest/docs/reports/YYYY-MM-DD-wo-0057-spec-impl-audit-report.md` (audit report)
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/implementations/` (new docs section, if navigation restructure is warranted)

## Acceptance criteria

- [ ] Audit report exists listing all spec-vs-implementation confusion instances found and fixed.
- [ ] Every key entry point (docs landing, spec READMEs, root README) includes "UM is a specification" messaging.
- [ ] The TypeScript helper is described as "a reference implementation" (not "the implementation") in every context where it appears.
- [ ] At least 3 calls-to-action for external implementations exist in prominent documentation locations.
- [ ] Code examples in docs include qualification notes about being reference-implementation examples.
- [ ] Integration docs do not assume TypeScript/Node.js as the only option.
- [ ] A new reader encountering UM for the first time would understand within the first 30 seconds that UM is a specification they can implement in any language.
- [ ] `rg -i "the implementation" /Users/grig/work/repo/universalmanifest/site/src/content/docs/ /Users/grig/work/repo/universalmanifest/spec/` returns zero results that position the TS helper as "the" (only) implementation.

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` (site builds cleanly)
- `rg -n "the implementation" /Users/grig/work/repo/universalmanifest/site/src/content/docs/ /Users/grig/work/repo/universalmanifest/spec/` (check for problematic phrasing)
- `rg -n "packages/universal-manifest" /Users/grig/work/repo/universalmanifest/site/src/content/docs/` (verify all references are qualified)
- Manual review of docs site entry points for correct messaging.

## Dependencies and sequencing notes

- Depends on WO-0054 (reference implementation must exist in a separate repo before docs can point to it as a separate entity).
- Can begin Phase 1 (audit) in parallel with WO-0054 development.
- Coordinate with WO-0055 (implementation guide) to ensure consistent messaging.
- Coordinate with WO-0058 (migration guide) to ensure migration docs are spec-level, not implementation-level.
