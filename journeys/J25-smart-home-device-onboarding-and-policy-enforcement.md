# J25 — Smart-Home Device Onboarding and Policy Enforcement

## Goal

Prove that a smart-home consumer can read household policy, inventory the onboarding manifest, and enforce default-deny telemetry, remote-access, and location behavior while recognizing the lane's scoped exceptions and fail-closed freshness posture.

## Why this matters

The smart-home lane is only useful if devices can safely join a household without bespoke vendor logic. This journey makes the proof story explicit: baseline privacy policy, device inventory, audience-scoped demand-response and owner-remote exceptions, and fail-closed policy metadata are all checked as executable evidence.

## Inputs

- Baseline household policy fixture:
  - `examples/integrations/smart-home/baseline-household-policy-manifest.jsonld`
- Near-real multi-device onboarding fixture:
  - `examples/integrations/smart-home/near-real-multi-device-onboarding-manifest.jsonld`

## Expected behavior

1. Both fixtures preserve a valid v0.1 UM envelope.
2. Baseline household policy is explicit default-deny for usage data, remote access, and location.
3. Baseline `homePolicy` and `deviceIdentity` facets capture the minimum consumer state needed for onboarding.
4. The near-real manifest carries a three-device inventory plus explicit device-identity and automation overlays.
5. Demand-response telemetry sharing is restricted to the named energy-provider audience and scoped to aggregated telemetry fields.
6. Remote access is restricted to the named owner relay; all other origins remain blocked.
7. Location sharing remains denied even when other exceptions are present.
8. The policy-enforcement profile encodes daily refresh, fail-closed stale-manifest handling, and location stripping for outbound telemetry.

## Executable mapping

- Journey runner row: `J25`
- Implementation: `packages/universal-manifest/scripts/run-journeys.mjs`

## Evidence

Successful execution appears in the generated journey report under `docs/journeys/_artifacts/`.
