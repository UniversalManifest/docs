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

## 2026-02-12 — Public domain split for standards vs resolver

### Standards + docs host

- Canonical public standards/docs domain is **`universalmanifest.net`**.
- This site hosts learning material and versioned spec artifacts intended for external adoption.

### UMID resolver host

- Canonical resolver domain is **`myum.net`**, with lookup pattern: `https://myum.net/{UMID}`.
- This domain is for manifest resolution/retrieval behavior, not spec governance docs.

### Compatibility policy

- Existing `localartist.network` namespace references in v0.1 are treated as compatibility aliases.
- New publishing guidance uses `universalmanifest.net` as canonical for spec artifacts.
- Previously published URLs must remain resolvable (no breaking URL churn).

## 2026-02-13 — Official done-done framework adopted

### Decision

- Adopt a formal, gate-based done-done framework as the official release readiness authority:
  - `docs/DONE-DONE-DEFINITION.md`
  - `docs/DONE-DONE-CHECKLIST.md`
  - `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`

### Rationale

- Prevent ambiguous completion claims.
- Require auditable evidence for release readiness.
- Separate “early-adopter ready” from “world-ready” using explicit maturity targets.

### Policy impact

- Future release claims MUST include a completed evidence pack.
- “Done done” claims without gate evidence are invalid.

## 2026-02-13 — Record-primitive vision direction captured

### Decision

- Capture CEO direction that Universal Manifest composition should center on a **Record** primitive:
  - records can be leaf or nested/container
  - records can be exchanged via push and pull/request
  - records may declare their own schema/standards context
  - records/attributes require permission states with field-level policy control

### Rationale

- Supports multi-domain extensibility without forcing a single rigid schema too early.
- Aligns with local-first and cross-system interoperability goals.

### Policy impact

- Treat this as vision-level guidance until translated into normative spec artifacts.
- Any normative adoption of record semantics/permissions must flow through versioned spec + conformance updates.
