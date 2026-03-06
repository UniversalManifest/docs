# J22 — RP1 Attachment Freshness and Session-Context Safety

## Goal

Prove that RP1/MSF consumers fail closed when portable attachment-routing evidence is stale and when an optional session-context pointer is expired or revoked.

## Why this matters

The RP1/MSF lane is intentionally pointer-first and non-normative. That only remains safe if consumers do not keep traversing child scopes or replaying session context after freshness or status evidence says they should stop.

## Inputs

- Stale attachment fixture:
  - `examples/v0.1/stubs/rp1-spatial-fabric-stale-attachment-manifest.jsonld`
- Revoked session fixture:
  - `examples/v0.1/stubs/rp1-spatial-fabric-revoked-session-manifest.jsonld`

## Expected behavior

1. The stale attachment fixture still preserves the normal UM envelope and RP1 optional-pointer structure.
2. `rp1.attachmentIndex` carries explicit freshness metadata (`observedAt`, `expiresAt`, `status`).
3. When that attachment index is already stale at manifest issuance time, child-scope traversal is blocked.
4. The attachment-policy example makes the fail-closed behavior explicit with `onFreshnessFailure = deny-child-scope-traversal`.
5. The revoked-session fixture keeps session context optional and pointer-based rather than promoting it into core UM fields.
6. `rp1.sessionContext` carries explicit status/freshness metadata.
7. When the session context is revoked or already expired, reuse is blocked.
8. `spatial.sessionReplay = denied` remains aligned with the blocked replay decision.

## Executable mapping

- Journey runner row: `J22`
- Implementation: `packages/universal-manifest/scripts/run-journeys.mjs`

## Evidence

Successful execution appears in the generated journey report under `docs/journeys/_artifacts/`.
