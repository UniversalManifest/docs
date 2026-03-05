---
work_order: WO-0126
program_track: MUM-GN-05
updated: "2026-03-05"
spec_versions_covered:
  - "0.1"
  - "0.2"
---

# MUM Synchronization Profile (Guidance-First)

This guide defines a practical, non-normative synchronization profile for metaverse portability implementations using Universal Manifest.

It is designed to be implementable now without changing UM core requirements.

## 1) Normative boundary

Normative requirements remain in:

- `spec/v0.1/CONFORMANCE.md`
- `spec/v0.2/CONFORMANCE.md`
- `spec/v0.2/SIGNATURE-PROFILE.md`

This guide provides operational conventions only.

## 2) Synchronization goals

- keep platform-local caches fresh,
- make consent and preference changes converge quickly,
- provide deterministic conflict behavior,
- maintain auditable update history.

## 3) Recommended synchronization pointers

Use optional pointers to make sync sources explicit.

- `metaverse.sync.authoritativeSource`
- `metaverse.sync.changeLog`
- `metaverse.sync.snapshot`

Recommended usage:

- `authoritativeSource`: canonical manifest endpoint for refresh checks.
- `changeLog`: append-only event feed endpoint.
- `snapshot`: optional compact state snapshot for fast bootstrap.

## 4) Staleness checks (consumer side)

Recommended check order:

1. Validate baseline UM fields.
2. Enforce TTL (`now <= expiresAt`).
3. If signature is present and policy requires it, verify signature profile.
4. If extended policy is enabled, verify `statusRef` and freshness of `revocationCursor`.
5. Compare cached metadata to authoritative source metadata.
6. Refresh when cache is stale or uncertain.

Staleness trigger examples:

- cache `expiresAt` is near threshold,
- authoritative `issuedAt` is newer,
- authoritative revocation cursor is newer,
- local consent state conflicts with latest authoritative consent state.

## 5) Update sequencing and retry guidance

Recommended deterministic sequence:

1. fetch metadata from `authoritativeSource`,
2. decide if refresh required,
3. fetch full manifest,
4. validate + verify,
5. apply conflict-resolution policy,
6. persist applied version + audit event.

Retry guidance:

- exponential backoff with jitter for transient network errors,
- hard stop on validation/signature failure,
- degrade gracefully to minimal mode when source unavailable.

Language-neutral pseudocode:

```text
meta = fetchMeta(authoritativeSource)
if not needsRefresh(cache, meta):
  return cache

candidate = fetchManifest(authoritativeSource)
requireBaseline(candidate)
requireFresh(candidate, now)
if policy.requiresSignature:
  verifyV02Signature(candidate)

merged = resolveConflicts(cache, candidate, policy)
persist(merged)
logSyncEvent(cache.id, merged.id, "applied")
```

## 6) Append-only change-log pattern

If `metaverse.sync.changeLog` is present, treat it as append-only.

Recommended event shape:

- `eventId`
- `manifestId`
- `subject`
- `changedAt`
- `changeType` (`consent`, `preference`, `pointer`, `claim`, `policy`)
- `fields`
- `source`

Rules:

- never mutate historical events,
- always include monotonic ordering material (`changedAt` and/or sequence cursor),
- keep local replay idempotent.

## 7) Conflict handling (best-effort deterministic)

Recommended precedence:

1. Core required UM fields: authoritative source wins.
2. Consent keys: deny wins on conflict unless newer authoritative allow is verified and policy permits.
3. Preferences: newest authoritative value wins.
4. Claims: newest verified issuer-trusted claim wins.
5. Pointers: newest authoritative pointer wins.

If timestamps are equal and values differ:

- keep previous active value,
- log a `conflict_unresolved_equal_timestamp` event,
- request manual or policy-specific reconciliation.

## 8) Offline behavior

Recommended offline policy:

- continue only with unexpired cached manifest,
- restrict sensitive operations when extended trust checks are unavailable,
- queue local non-authoritative preferences separately and reconcile on reconnect,
- never overwrite authoritative consent with unverified offline state.

## 9) Verification flow

Run from repo root:

```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm test
npm run journeys
```

Journey coverage most relevant to synchronization profile:

- `J16` consent propagation
- `J19` preferences bundle projection
- `J20` freshness and change-log behavior

## 10) Operational evidence map

Key implementation references:

- `integrations/metaverse.md`
- `docs/journeys/J16-mum-consent-propagation-flow.md`
- `docs/journeys/J19-mum-preferences-bundle-projection-flow.md`
- `docs/journeys/J20-mum-freshness-and-change-log-flow.md`
- `docs/reports/2026-03-05-mum-synchronization-profile-mapping-note.md`

## 11) Next links

- `docs/guides/IMPLEMENTATION-GUIDE.md`
- `docs/guides/QUICK-REFERENCE.md`
- `docs/reports/2026-03-05-metaverse-universal-manifest-go-now-research-first-execution-plan.md`
