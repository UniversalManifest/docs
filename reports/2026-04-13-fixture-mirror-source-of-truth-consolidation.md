# 2026-04-13 Fixture Mirror Source-of-Truth Consolidation

## Purpose

This report closes `WO-0186` by making fixture authorship and public mirror behavior explicit.

The project already depended on public browser-facing fixture trees for the harness and sandbox, but the authored-versus-generated boundary was not stated clearly enough in the canonical docs. That gap made it too easy to treat published copies as if they were a second source tree.

## What changed

### 1. Added a canonical fixture policy

Created:

- `docs/FIXTURE-SOURCE-OF-TRUTH-AND-PUBLISHED-MIRROR-POLICY.md`

That document now defines:

- `examples/` as the authored source of truth
- `site/public/harness/fixtures/` and `site/public/sandbox/fixtures/` as generated publish mirrors
- the current curated harness mirror versus broader sandbox mirror model
- the authoring and regeneration rules for future fixture work

### 2. Closed the documentation gap around mirror generation

The paired implementation slice centralizes the mirror model in:

- `site/scripts/fixture-mirrors.mjs`
- `site/scripts/sync-harness-fixtures.mjs`
- `site/scripts/sync-sandbox-fixtures.mjs`
- `site/scripts/sync-agent-discovery.mjs`

Those implementation files now reflect one shared mirror definition instead of repeating fixture-root assumptions in multiple places.

### 3. Made authored origin visible to machine consumers

The fixture catalog generation now exposes authored provenance alongside published paths so browser and agent consumers can tell the difference between:

- the public file they can fetch
- the authored fixture path that remains canonical in the repo

## Result

The authoritative posture is now:

- author fixtures in `examples/`
- publish browser-accessible copies as generated mirrors
- regenerate mirror trees through sync scripts instead of editing public copies
- keep machine-readable catalogs explicit about authored origin versus published mirror

That materially reduces drift risk without removing the browser-accessible fixture surfaces that the harness and sandbox still need.

## Verification

Docs-side verification completed for this closeout:

- status-layer coherence was checked across `WO-0186`, `WO-INDEX`, `CRITICAL-PATH`, and `STATE-OF-THE-PROJECT`
- the new canonical policy doc was added to the docs index so it is discoverable as a first-class project rule
- changed markdown links and file references were validated against on-disk targets

Implementation proof was reviewed from the current root-repo working state:

- `site/scripts/fixture-mirrors.mjs` defines shared mirror roots and mirror-set configuration
- `site/scripts/sync-harness-fixtures.mjs` and `site/scripts/sync-sandbox-fixtures.mjs` consume that shared definition
- `site/scripts/sync-agent-discovery.mjs` now emits `authoredSourcePath` and `publishedMirror`

This work order is a source-of-truth and documentation closure paired to that implementation slice; it does not itself modify the root-repo implementation files.
