# Journey 07 — RP1 spatial fabric projection (lane)

## Goal

Demonstrate that RP1/MSF-style spatial-fabric data can be represented as optional pointers and compact shards in Universal Manifest without changing core v0.1 required fields.

## Inputs

- Fixture:
  - `examples/v0.1/stubs/rp1-spatial-fabric-manifest.jsonld`

## Steps

1. Validate the fixture using the standard v0.1 validator path.
2. Confirm required core fields are present and valid (`@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`).
3. Confirm RP1/MSF pointers are modeled as optional pointer entries:
   - `rp1.fabric`
   - `rp1.anchorSet`
   - `rp1.placeGraph`
   - `rp1.attachmentIndex`
   - `rp1.assetProfile`
   - `rp1.sessionContext`
4. Confirm consent keys gate portable spatial behavior:
   - `spatial.locationShare`
   - `spatial.anchorShare`
   - `spatial.crossWorldLinking`
   - `spatial.sessionReplay`
5. Confirm compact shards summarize only the portable subset of state:
   - `spatialAnchors`
   - `placeMembership`
   - `spatialFabricAttachmentPolicy`
   - `spatialAssetProfile`
6. Confirm attachment-policy entries point to the freshness source (`rp1.attachmentIndex`) and declare fail-closed behavior when that evidence is stale.
7. Confirm positive-path freshness metadata on `rp1.attachmentIndex` and `rp1.sessionContext` keeps both pointers fresh relative to manifest issuance.
8. Confirm child-scope composition is summarized through attachment policy rather than embedding the live scope tree.
9. Confirm asset delivery remains pointer-first and external (`gltf`/`glb` profile hints, no embedded 3D payloads).
10. Confirm unknown-field tolerance remains intact (RP1/MSF-specific keys do not break baseline validation).

## Expected outcomes

- Fixture passes baseline v0.1 validation.
- RP1/MSF-specific fields remain additive overlays, not required core contract fields.
- Attachment-routing and session-context safety stay optional pointer metadata, not new core schema requirements.
- Attachment composition is represented as compact portable policy/evidence, not as the live runtime graph.
- Asset profile guidance stays external-pointer-first.
- Consumers that do not understand RP1/MSF keys can still parse and validate manifest core.

## Evidence

- validation output from:
  - `cd packages/universal-manifest && npm test`
  - `cd packages/universal-manifest && npm run journeys`
- fixture path:
  - `examples/v0.1/stubs/rp1-spatial-fabric-manifest.jsonld`

## Normative boundary reminder

This journey is integration evidence. Core normative requirements remain in:
- `spec/v0.1/README.md`
- `spec/v0.1/CONFORMANCE.md`
