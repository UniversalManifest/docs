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
7. `journey-07-rp1-spatial-fabric-projection.md`

## Cross-Domain Overlay Lanes (WO-0017)

Planning authority:
- `/Users/grig/work/repo/universalmanifest/.dev/ai/specs/2026-02-19-ia-delta-from-full-corpus.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md`

Required overlay lanes for journey expansion:
- Venue/local-first display lane (baseline operational lane).
- Creator/public profile projection lane (adopter-facing lane).
- Metaverse portability lane as non-normative exemplar (not scope anchor).
- RP1 spatial-fabric lane as non-normative interoperability overlay.

## Identity-Method Variant Lanes (CON-UM-003)

Journey assertions must pass with the same core manifest envelope while varying identity/anchor methods.

Variant minimums:
- `variant-a`: detached key material path.
- `variant-b`: resolver-anchored identity pointer path.

Core rule:
- Core journey pass/fail criteria remain method-agnostic; variant-specific checks are additive.

## Sequencing Rubric (CON-UM-004)

Prioritize journey implementation order by:
1. interoperability evidence quality,
2. conformance test leverage,
3. adopter utility across more than one domain.

## Why this exists

The Universal Manifest project does not consider “docs exist” as proof.

Maturity claims require runnable evidence (see):

- `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-DEFINITION.md`
- `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-CHECKLIST.md`
- `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`
