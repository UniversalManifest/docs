# Journey 01 — Parse a manifest and ignore unknown fields safely

Goal: prove the baseline consumer behavior that prevents fragmentation.

## Steps

1. Load a valid v0.1 fixture with extra unknown fields:
   - `examples/v0.1/unknown-fields-manifest.jsonld`
2. Validate required v0.1 structure and semantics.
3. Ensure validation succeeds even with unknown properties present.

## Expected outcome

- Consumer accepts the manifest as v0.1 and does not crash on unknown fields.

## Executable proof

- `cd packages/universal-manifest && npm test`

