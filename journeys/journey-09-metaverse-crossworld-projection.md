# Journey 09 — Metaverse cross-world projection (non-normative lane)

## Goal

Show that metaverse identity/profile/avatar/social pointers can be projected from a UM manifest as optional overlays while preserving core-contract neutrality.

## Inputs

- `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/metaverse-crossworld-profile-manifest.jsonld`

## Steps

1. Validate fixture with baseline v0.1 validation.
2. Confirm cross-world pointers are modeled in optional `pointers` entries.
3. Confirm metaverse consents gate profile/social/voice publication behavior.
4. Confirm unknown-field tolerance remains intact for world-specific shard payloads.

## Expected outcomes

- Fixture passes baseline structural validation.
- World-specific semantics remain in optional shards/pointers.
- Core required UM fields are unchanged.

## Evidence

- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test`
- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`
