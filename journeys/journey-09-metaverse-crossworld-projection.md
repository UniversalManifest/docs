# Journey 09 — Metaverse portaling and cross-world projection (lane)

## Goal

Show that a subject can move between different metaverse platforms using one UM envelope, with identity, avatar, inventory, and policy data projected as optional overlays while preserving core-contract neutrality.

## Inputs

- `examples/v0.1/stubs/metaverse-crossworld-profile-manifest.jsonld`

## Steps

1. Validate fixture with baseline v0.1 validation.
2. Confirm cross-world pointers are modeled in optional `pointers` entries.
3. Confirm metaverse consents gate profile/social/voice publication behavior at destination entry.
4. Confirm unsupported or world-specific shard payloads do not invalidate the whole transfer.
5. Confirm unknown-field tolerance remains intact for world-specific shard payloads.

## Expected outcomes

- Fixture passes baseline structural validation.
- World-specific semantics remain in optional shards/pointers.
- Portaling uses pointer-first projection and policy continuity rather than a monolithic payload copy.
- Core required UM fields are unchanged.

## Evidence

- `cd packages/universal-manifest && npm test`
- `cd packages/universal-manifest && npm run journeys`
