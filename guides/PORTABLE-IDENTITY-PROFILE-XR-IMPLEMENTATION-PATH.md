---
work_order: WO-0125
program_track: PIP-GN-05
updated: "2026-03-05"
spec_versions_covered:
  - "0.1"
  - "0.2"
---

# Portable Identity Profile XR Implementation Path (Guidance-First)

This guide is an adopter-ready addendum for teams implementing Portable Identity Profile behavior in XR surfaces.

It is intentionally implementation-oriented and language-neutral.

## 1) Normative boundary

Normative requirements remain in:

- `spec/v0.1/CONFORMANCE.md`
- `spec/v0.2/CONFORMANCE.md`
- `spec/v0.2/SIGNATURE-PROFILE.md`

Everything in this guide is non-normative integration guidance.

## 2) Inputs you should have before implementation

- A manifest parser that enforces required UM fields and TTL.
- Signature verification support for v0.2 (`Ed25519` + `JCS-RFC8785`) where policy requires it.
- Consent-evaluation logic that defaults to deny when consent keys are missing.
- Pointer resolver client for profile/avatar/wearable/proof endpoints.

Recommended fixtures:

- `examples/v0.1/stubs/portable-identity-profile-xr-minimal-manifest.jsonld`
- `examples/v0.1/stubs/portable-identity-profile-xr-avatar-pointers-manifest.jsonld`
- `examples/v0.1/stubs/portable-identity-profile-xr-consent-matrix-manifest.jsonld`
- `examples/v0.1/stubs/portable-identity-profile-xr-pairwise-subject-variant-a.jsonld`
- `examples/v0.1/stubs/portable-identity-profile-xr-pairwise-subject-variant-b.jsonld`
- `examples/v0.2/portable-identity-profile-xr-revocation-metadata-v02.jsonld`

## 3) Consumer algorithm order (recommended)

1. Parse and validate baseline UM fields.
2. Enforce freshness (`expiresAt`) before any projection.
3. If trust-sensitive, enforce v0.2 signature policy.
4. Read only supported portable profile overlays.
5. Evaluate required consents for each planned action.
6. Apply default deny when consent keys are absent.
7. Resolve profile/avatar/wearable pointers only after consent pass.
8. Apply pairwise subject handling rules (no cross-surface subject correlation by default).
9. Apply revocation/freshness posture if using extended trust tier.
10. Emit audit event with decision reason.

Language-neutral pseudocode:

```text
manifest = parse(input)
requireBaseline(manifest)
requireFresh(manifest, now)

if policy.requiresSignature:
  verifyV02Signature(manifest)

for action in requestedActions:
  requiredConsents = policy.consentsFor(action)
  if not allAllowedOrScoped(manifest.consents, requiredConsents):
    deny(action, "consent")
    continue

  if policy.requiresExtendedRevocation:
    requireRevocationFreshness(manifest.signature)

  projectSupportedOverlayFields(manifest, action)
  logDecision(action, "allow")
```

## 4) Issuer checklist (recommended)

Issuer flow should satisfy baseline UM validity, then add Portable Identity Profile overlays.

Checklist:

- [ ] Set valid required UM fields and version.
- [ ] Use short TTL aligned to XR session risk.
- [ ] Use pairwise/pseudonymous subject strategy where privacy requires it.
- [ ] Store large assets externally and reference via pointers.
- [ ] Emit explicit consent values for sensitive actions.
- [ ] Include signature metadata for trust-sensitive issuance.
- [ ] Include `statusRef` and `revocationCursor` when extended revocation policy is expected.

## 5) Consent enforcement examples

Example A: conversational AR/MR interaction

- Required consent keys:
  - `portableIdentity.voiceCapture`
  - `portableIdentity.translationEnabled`
- If voice capture is missing, treat as denied.

Example B: immersive retail checkout

- Required consent keys:
  - `portableIdentity.profilePublic`
  - `portableIdentity.recording.faceVisible`
- If profile publicity is denied, project minimal anonymous storefront mode.

Example C: analytics-sharing request

- Required consent key:
  - `portableIdentity.analyticsShare`
- If denied, continue session without telemetry export.

## 6) Revocation policy tiers

Two policy tiers keep rollout practical.

`baseline` tier:

- TTL enforced.
- Signature verification optional by relying-party policy.
- No mandatory `statusRef` network check.

`extended` tier:

- TTL enforced.
- Signature verification required.
- `statusRef` checked.
- `revocationCursor` freshness checked against policy window.

## 7) Offline-mode risk handling

Recommended offline behavior:

- Never use expired manifests offline.
- For `baseline` tier, allow short grace cache only within policy-defined local window.
- For `extended` tier, degrade to read-only/non-sensitive actions when revocation status cannot be refreshed.
- Re-resolve authoritative manifest and re-evaluate consent immediately on reconnect.

## 8) Copy/paste verification flow

Run from repo root:

```bash
cd packages/universal-manifest
npm test
npm run journeys
```

Expected journey coverage for this guide:

- `J12` projection + consent
- `J13` pairwise privacy
- `J14` revocation-aware policy

## 9) Operational evidence map

Guide inputs and supporting evidence:

- Integration lane: `integrations/portable-identity-profile-xr.md`
- Registry families: `spec/v0.1/REGISTRY.md`
- Journey docs:
  - `docs/journeys/J12-portable-identity-profile-projection-and-consent.md`
  - `docs/journeys/J13-portable-identity-profile-pairwise-privacy.md`
  - `docs/journeys/J14-portable-identity-profile-revocation-aware-policy.md`
- Mapping report: `docs/reports/2026-03-05-portable-identity-profile-implementation-path-mapping-note.md`

## 10) Next links

- `docs/guides/IMPLEMENTATION-GUIDE.md`
- `docs/guides/QUICK-REFERENCE.md`
- `docs/reports/2026-03-05-portable-identity-profile-go-now-research-first-execution-plan.md`
