# J21 — GPC Runtime Signal and Evidence Projection Flow

## Goal

Prove that a consumer can normalize an observed GPC runtime signal, parse a `/.well-known/gpc.json` support resource, and express optional UM evidence projection without treating document state as the authoritative request-time input.

## Why this matters

The GPC integration decision for Universal Manifest is hybrid:

- runtime signal is authoritative for request-time behavior,
- UM projection is descriptive evidence for portability and audit,
- support-resource metadata is informative but not per-request proof.

This journey proves that reference behavior directly.

## Inputs

- Runtime signal fixtures under `examples/integrations/gpc/runtime/`
- Support-resource fixtures under `examples/integrations/gpc/support-resource/`
- Evidence projection manifest:
  - `examples/v0.1/stubs/gpc-evidence-projection-manifest.jsonld`

## Expected behavior

1. `Sec-GPC: 1` normalizes to `active`.
2. Duplicate header handling remains deterministic.
3. Explicit intermediary provenance is preserved.
4. No-signal case normalizes to `unknown`.
5. `/.well-known/gpc.json` requires `application/json` and a JSON object body.
6. Unknown support-resource members are tolerated.
7. Invalid `lastUpdate` is ignored rather than promoted to authoritative state.
8. Optional UM consent projection mirrors the normalized runtime evidence.
9. An active GPC signal constrains conflicting permissive local in-scope behavior.

## Executable mapping

- Journey runner row: `J21`
- Implementation: `packages/universal-manifest/scripts/run-journeys.mjs`

## Evidence

Successful execution appears in the generated journey report under `docs/journeys/_artifacts/`.
