# Fixture Source of Truth and Published Mirror Policy

This document defines where Universal Manifest fixtures are authored, where browser-facing copies are published, and how those published copies are generated.

It exists so fixture truth does not drift across multiple trees while the site still keeps browser-accessible copies for public tools.

## 1. Authoritative authored source

The authored source of truth for Universal Manifest fixture data is:

- `examples/`

Rules:

- Add, revise, or retire fixture content in `examples/`, not in site-published copies.
- Treat `examples/` as the human-reviewed and repo-authored fixture corpus.
- When a public tool needs browser-accessible fixture files, publish them as generated mirrors of authored sources rather than treating the public trees as editable origin data.

## 2. Published mirror surfaces

The site publishes fixture mirrors for browser-facing tools under:

- `site/public/harness/fixtures/`
- `site/public/sandbox/fixtures/`

These trees are publish surfaces, not authored sources.

Rules:

- Do not manually edit published fixture mirrors.
- Regenerate published mirrors through the sync scripts.
- If a published mirror looks wrong, fix the authored source or the sync logic rather than patching the public copy directly.

## 3. Mirror model by surface

### 3.1 Harness mirror

`site/public/harness/fixtures/` is a generated tool-facing mirror for the harness surface.

Current published posture:

- mirror all of `examples/v0.1/`
- mirror the signed v0.2 minimal manifest
- mirror `examples/v0.2/invalid/`

This is intentionally a curated subset rather than a full copy of every authored example.

### 3.2 Sandbox mirror

`site/public/sandbox/fixtures/` is a generated tool-facing mirror for the sandbox surface.

Current published posture:

- mirror all of `examples/v0.1/`
- mirror all of `examples/v0.2/`, including nested fixture families

This keeps the sandbox browser-readable while preserving `examples/` as the authored origin.

## 4. Generation and sync rules

The mirror relationship is implemented through shared sync logic in:

- `site/scripts/fixture-mirrors.mjs`
- `site/scripts/sync-harness-fixtures.mjs`
- `site/scripts/sync-sandbox-fixtures.mjs`

Operational rules:

1. Mirror configuration should be defined centrally rather than duplicated across scripts.
2. Sync runs should delete and regenerate the published mirror roots so stale files do not accumulate silently.
3. Local development and builds should refresh fixture mirrors before serving or publishing browser-facing tool surfaces.

## 5. Agent/discovery implications

Machine-readable discovery should distinguish authored truth from published mirrors.

The public fixture catalog at `site/public/agent/fixture-catalog.json` should expose:

- the published public path
- the authored source path
- whether the file is a published mirror

That keeps browser and agent consumers pointed at the public file while still making the authored origin explicit.

## 6. Authoring rules for future work

Use these rules when adding or changing fixture content:

1. Create or modify fixtures in `examples/`.
2. Update sync logic only when the published mirror set itself should change.
3. Never introduce a second authored fixture tree under `site/public/`.
4. If a tool needs only a subset of fixtures, document that curation explicitly instead of implying the public tree is canonical.
5. Preserve recursive sync behavior for nested fixture families so new authored subtrees are not silently omitted from published mirrors.

## 7. Related documents

- `docs/COMPREHENSIVE-PROJECT-PROPERTIES-AND-SURFACES-MAP.md`
- `docs/PROJECT-VISION.md`
- `docs/PUBLISHING-AND-VERSIONING.md`
- `docs/workorders/WO-0186-fixture-mirror-source-of-truth-consolidation.md`
- `docs/reports/2026-04-13-fixture-mirror-source-of-truth-consolidation.md`
