# Crucial Details — Universal Manifest

## Terminology collision

- “Manifest” is used in reference implementation signage for **playback bundles** (`um:ManifestBundle`).
- This repo uses “Universal Manifest” to mean a **state capsule** (identity refs, claims/consents/devices/pointers).

## Local-first constraints

- Consumers (e.g., public displays) should **cache only what they need**:
  - store full manifests while in active use
  - store **manifest IDs/references** for logging (possible future recovery)

