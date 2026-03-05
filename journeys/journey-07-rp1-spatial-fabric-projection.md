# Journey 07 — RP1 spatial fabric projection (lane)

## Goal

Demonstrate that RP1-style spatial-fabric data can be represented as optional pointers/shards in Universal Manifest without changing core v0.1 required fields.

## Inputs

- Fixture:
  - `examples/v0.1/stubs/rp1-spatial-fabric-manifest.jsonld`

## Steps

1. Validate fixture using the standard v0.1 validator path.
2. Confirm required core fields are present and valid (`@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`).
3. Confirm RP1 pointers are modeled as optional pointer entries:
   - `rp1.fabric`
   - `rp1.anchorSet`
   - `rp1.placeGraph`
4. Confirm consent keys gate spatial behaviors:
   - `spatial.locationShare`
   - `spatial.crossWorldLinking`
5. Confirm unknown-field tolerance remains intact (RP1-specific keys do not break baseline validation).

## Expected outcomes

- Fixture passes baseline v0.1 validation.
- RP1-specific fields are additive overlays, not required core contract fields.
- Consumers that do not understand RP1 keys can still parse and validate manifest core.

## Evidence

- validation output from:
  - `cd packages/universal-manifest && npm test`
- fixture path:
  - `examples/v0.1/stubs/rp1-spatial-fabric-manifest.jsonld`

## Normative boundary reminder

This journey is integration evidence. Core normative requirements remain in:
- `spec/v0.1/README.md`
- `spec/v0.1/CONFORMANCE.md`
