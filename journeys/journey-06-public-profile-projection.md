# Journey 06 — Public profile projection (cross-implementation adopter proof)

## Goal

Prove that Universal Manifest is not coupled to a single implementation.

An adopter should be able to take a manifest and derive a safe, public-facing profile projection (a future social media profile, ActivityPub actor page, or a static “creator card”).

## Input fixture

- `examples/v0.1/stubs/social-profile-manifest.jsonld`

## Steps (conceptual)

1. Parse the manifest and verify it is structurally valid for v0.1 (required fields exist).
2. Locate a shard intended for public profile projection (e.g., `shards[].name = "publicProfile"`).
3. Derive a small “public profile” object that a consumer could render.
4. Confirm that the projection can be built without requiring implementation-specific fields.

## Success criteria

- The projection contains:
  - stable references (`@id` / `subject`)
  - a renderable `name`
  - at least one interop pointer (e.g., ActivityPub actor URL)
- The journey runs as part of `npm run journeys` in:
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest`
