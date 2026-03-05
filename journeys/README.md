# Universal Manifest — User Journeys (canonical) + executable proof suite

These journeys are the project’s **“show it works”** layer.

Each journey has:

- a human-readable definition (this folder)
- a corresponding executable row in the journey report (`J01` through `J14`)

Run the proof suite:

- `cd packages/universal-manifest && npm run journeys`
- Optional reference-implementation smoke (J05) can be enabled in journey-runner config.

Outputs:

- A JSON report is written under `docs/journeys/_artifacts/`.
- The report includes explicit rows for every documented journey ID (`J01` through `J14`).

## Executable mapping (J01-J14)

- `J01` Parse and ignore unknown fields -> `journeyParseAndIgnoreUnknownFields` (shared `npm test` conformance run)
- `J02` TTL and freshness -> `journeyTtlAndFreshness` (shared `npm test` conformance run)
- `J03` Signature verification (v0.2) -> `journeySignatureVerificationV02` (shared `npm test` conformance run)
- `J04` UMID resolution -> `journeyMyumResolver`
- `J05` UM edge to display smoke (optional) -> optional reference-implementation smoke journey
- `J06` Public profile projection -> `journeyPublicProfileProjection`
- `J07` RP1 spatial fabric projection -> `journeyRp1SpatialFabricProjection`
- `J08` Smart-glasses consent enforcement -> `journeySmartGlassesConsentEnforcement`
- `J09` Metaverse cross-world projection -> `journeyMetaverseCrossworldProjection`
- `J10` Multi-provider personhood coexistence -> `journeyMultiProviderPersonhood`
- `J11` OMATrust attestation interoperability -> `journeyOmaTrustInteroperability`
- `J12` Portable Identity Profile XR projection and consent behavior -> `journeyPortableIdentityProfileProjection`
- `J13` Portable Identity Profile pairwise subject privacy -> `journeyPortableIdentityPairwisePrivacy`
- `J14` Portable Identity Profile revocation-aware policy checks -> `journeyPortableIdentityRevocationAwarePolicy`

Execution source:

- `packages/universal-manifest/scripts/run-journeys.mjs`

## Journey list

1. `journey-01-parse-and-ignore-unknown-fields.md`
2. `journey-02-ttl-and-freshness.md`
3. `journey-03-signature-verification-v0-2.md`
4. `journey-04-umid-resolution-myum.md`
5. `journey-05-um-edge-to-display-smoke.md`
6. `journey-06-public-profile-projection.md`
7. `journey-07-rp1-spatial-fabric-projection.md`
8. `journey-08-smart-glasses-consent-enforcement.md`
9. `journey-09-metaverse-crossworld-projection.md`
10. `J10-multi-provider-personhood-coexistence.md`
11. `J11-omatrust-attestation-interoperability.md`
12. `J12-portable-identity-profile-projection-and-consent.md`
13. `J13-portable-identity-profile-pairwise-privacy.md`
14. `J14-portable-identity-profile-revocation-aware-policy.md`

## Cross-Domain Overlay Lanes (WO-0017)

Planning authority:
- `.dev/ai/specs/2026-02-19-ia-delta-from-full-corpus.md`
- `docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md`

Required overlay lanes for journey expansion:
- Venue/local-first display lane (baseline operational lane).
- Creator/public profile projection lane (adopter-facing lane).
- Metaverse portability lane as exemplar (not scope anchor).
- RP1 spatial-fabric lane as interoperability overlay.
- Smart-glasses consent lane as policy overlay.

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

- `docs/DONE-DONE-DEFINITION.md`
- `docs/DONE-DONE-CHECKLIST.md`
- `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`
