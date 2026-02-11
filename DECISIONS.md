# Decisions (Universal Manifest)

## 2026-02-11 — v0.1 bootstrap decisions

### Separate spec repo

- The Universal Manifest lives as a **fully separate repo** at `/Users/grig/work/lan/universal-manifest/`.
- LAN consumes it, but it is versioned and maintained independently.

### Manifest ID generation (`@id`)

- v0.1 recommendation: issuers generate `@id` as `urn:uuid:<uuidv4>`.
- Rationale: globally unique, offline-safe, and avoids premature content-addressing commitments.

### Device caching + logging (NVIDIA Shield / public display)

- Cache the **full manifest JSON** while actively in use.
- Persist only **manifest ID references** (`@id`) in logs/telemetry.
- Future recovery may use those IDs, but recovery workflows are intentionally out of scope for v0.1.

### Security scope (v0.1)

- `signature` is present only as a permissive placeholder envelope.
- Cryptographic signing/verification formats are intentionally deferred until canonicalization rules and integration needs are confirmed.

