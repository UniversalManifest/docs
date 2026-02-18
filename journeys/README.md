# Universal Manifest — User Journeys (canonical) + executable proof suite

These journeys are the project’s **“show it works”** layer.

Each journey has:

- a human-readable definition (this folder)
- a corresponding executable test step (see `packages/universal-manifest/`)

Run the proof suite:

- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`

Outputs:

- A JSON report is written under `docs/journeys/_artifacts/`.

## Journey list

1. `journey-01-parse-and-ignore-unknown-fields.md`
2. `journey-02-ttl-and-freshness.md`
3. `journey-03-signature-verification-v0-2.md`
4. `journey-04-umid-resolution-myum.md`
5. `journey-05-lan-edge-to-display-smoke.md`
6. `journey-06-public-profile-projection.md`

## Why this exists

The Universal Manifest project does not consider “docs exist” as proof.

Maturity claims require runnable evidence (see):

- `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-DEFINITION.md`
- `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-CHECKLIST.md`
- `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`
