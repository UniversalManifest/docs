# WO-0107 — Commit Interactive Sandbox Work and Uncommitted Design Artifacts

**Status:** COMPLETED
**Created:** 2026-03-01
**Priority:** P0 (Critical)
**Source:** Documentation Freshness Audit (2026-03-01), Section 6 Priority 1 (items 1-4)
**Tags:** [implementation], [structural]
**Blocks:** All status tracking depends on committed state; largest body of untracked work
**Dependencies:** None
**Estimated effort:** 1-2 hours

## Objective

Commit all currently uncommitted work that has been built, verified, and is ready for inclusion in the repository. This is the single largest body of untracked work in the project.

## Why this work matters

The freshness audit found that the entire interactive sandbox (V1: WO-0060-0068, plus V2: WO-0069-0080) is built, verified, and browser-tested but is entirely uncommitted. Additionally, several design documents and a new fixture are uncommitted. Until this work is committed, it cannot be referenced in any status document, tracked in CI, or relied upon by other work orders.

## Scope

### Work to commit

**Interactive Sandbox V1 (WO-0060-0068):**
- `site/src/components/sandbox/` — 18 Astro components
- `site/src/pages/sandbox/` — Sandbox pages
- `site/src/scripts/sandbox/` — Sandbox engine, validator, scenarios
- `site/src/styles/sandbox/` — Sandbox styles
- `site/public/sandbox/` — 25 SVG illustrations, fixtures
- `site/scripts/parity-test.mjs`, `sync-sandbox-fixtures.mjs`, `test-scenarios-smoke.mjs`, `test-validator-parity.mjs`

**Interactive Sandbox V2 (WO-0069-0080):**
- V2 components (HierarchyExplorer, DetailsCard, EntityColumn, ProtocolLens, SubjectPanel, SandboxLayoutV2, SandboxEngineV2)
- 25 V2 scenario files

**Design documents:**
- `docs/design/CAPSULE-POD-DESIGN.md`
- `docs/design/capsule-pod-reference/` (9 cinematic renders)
- `docs/design/PERMISSIONS-FIREWALL-DESIGN.md`
- `docs/design/sandbox-ui-mockup.excalidraw`

**Updated docs (uncommitted diffs):**
- `docs/STATE-OF-THE-PROJECT.md`
- `docs/DECISIONS.md`
- `docs/diagrams/README.md`

**New fixture:**
- `examples/v0.1/stubs/cross-system-projection-manifest.jsonld`
- `site/public/harness/fixtures/v0.1/stubs/cross-system-projection-manifest.jsonld`

**Site configuration:**
- `site/astro.config.mjs` (uncommitted changes)
- `site/package.json` (uncommitted changes)
- `.github/workflows/ci.yml` (uncommitted changes)

### Commit strategy

Organize into logical commits:
1. Design documents (CAPSULE-POD, permissions firewall, sandbox mockup)
2. Interactive Sandbox V1 (components, pages, scripts, styles, illustrations)
3. Interactive Sandbox V2 (V2 components and scenarios)
4. Documentation updates (STATE-OF-THE-PROJECT, DECISIONS, diagrams/README)
5. New fixture and configuration changes

## Acceptance criteria

- [x] All uncommitted sandbox code is committed.
- [x] All uncommitted design documents are committed.
- [x] All uncommitted documentation diffs are committed.
- [x] New fixture is committed.
- [x] `git status` shows a clean working tree (or only intentionally-deferred items).
- [x] `cd site && npm run build:clean` succeeds after commit.

## Validation commands

- `git status` (should show clean or minimal working tree)
- `cd site && npm run build:clean`
- `cd  && npm test`
