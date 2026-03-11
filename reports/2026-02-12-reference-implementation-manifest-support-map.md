# reference implementation Manifest Support Map (UM ↔ reference implementation integration contract)

Date: 2026-02-17  
Work Order: `docs/workorders/WO-0010-build-out-reference-implementation-support.md`

This report maps:

- Universal Manifest fixtures and conformance expectations
- to reference implementation integration responsibilities and endpoint contracts

## 1) Core responsibilities by reference implementation role

Edge (issuer):

- issues manifests (rotating `@id`)
- serves `current` and `by-id` retrieval
- emits update signals (push ID, pull manifest)

Display (consumer):

- fetches by ID and caches full manifest while in use
- logs by manifest ID reference
- enforces TTL (reject expired for use)

Admin:

- views current manifest ID and recent logs
- supports enrollment and debugging flows

## 2) Fixture mapping

v0.1 near-real fixtures:

- `examples/v0.1/stubs/venue-edge-manifest.jsonld`
  - role: edge identity and policy capsule
- `examples/v0.1/stubs/display-device-manifest.jsonld`
  - role: display device enrollment / trust stub
- `examples/v0.1/stubs/creator-public-capsule-manifest.jsonld`
  - role: creator capsule pointer / projection driver
- `examples/v0.1/stubs/display-envelope-manifest.jsonld`
  - role: reference implementation display manifest used in smoke tests and contract alignment

v0.2 integrity fixture (draft profile):

- `examples/v0.2/minimal-signed-manifest.jsonld`
  - role: signature verification baseline (JCS + Ed25519)

## 3) Endpoint mapping (reference implementation)

Descriptor:

- `GET /.well-known/um/edge.json`

Manifest retrieval:

- `GET /api/v1/universal-manifests/current?displayId={displayId}`
- `GET /api/v1/universal-manifests/by-id?id={manifestId}&displayId={displayId?}`

Manifest issuance:

- `POST /api/v1/universal-manifests/issue`

Resolver alignment:

- reference implementation local: `POST /api/v1/universal-manifests/resolve`
- Canonical: `GET https://myum.net/{UMID}` (skeleton in `services/myum-resolver/`)

Logging:

- `POST /api/v1/universal-manifests/logs` (ID-reference only)
- `GET /api/v1/universal-manifests/logs?...` (debugging)

## 4) Test hooks and evidence

UM proof suite (UM-first):

- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest` → `npm run journeys`

reference implementation smoke test (reference implementation repo; validates issuance, retrieval, socket, logging semantics):

- `/Users/grig/work/repo/reference-platform` → `SMOKE_PORT=3119 npm run smoke:universal-manifest`

## 5) Boundary enforcement (prevent reference implementation pollution)

Rules:

- implementation-specific endpoints belong in `integrations/` docs, not in `spec/`.
- The UM spec must remain adopter-neutral; reference implementation is a consumer with guidance.
- If reference implementation introduces a reusable standardized facet name, register it in `spec/v0.1/REGISTRY.md`.
