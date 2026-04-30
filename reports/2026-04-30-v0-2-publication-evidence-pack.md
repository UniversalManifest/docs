# Universal Manifest v0.2 Publication Evidence Pack

## 1) Release identity

- Version: Universal Manifest `v0.2`
- Target maturity: Early-adopter ready (`v0.x`)
- Release date: 2026-04-30
- Owner: Universal Manifest maintainers
- Reviewers: WO-0231 implementation worker closeout audit
- Publication URL: `https://universalmanifest.net/spec/v0.2/`
- Latest-spec URL: `https://universalmanifest.net/spec/latest/`
- GitHub release URL: `https://github.com/grigb/universal-manifest/releases/tag/spec-v0.2`
- Release execution evidence: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0220-release-executed-result.md`

## 2) Gate status summary

- G1 Contract completeness: PASS
- G2 Conformance testability: PASS
- G3 Integrity and trust profile: PASS
- G4 Interoperability proof: PASS
- G5 Publishing and discoverability: PASS
- G6 Governance and change control: PASS
- G7 Operational realism: PASS

## 3) Evidence by gate

### G1 Contract completeness evidence

- Artifact paths:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.json`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.jsonld`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md`
  - `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
  - `/Users/grig/work/repo/universalmanifest/docs/W3C-STYLE-SPEC.html`
- Result-report evidence:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0221-result.md`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0223-result.md`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0225-result.md`
- Review notes:
  - The published spec route is `https://universalmanifest.net/spec/v0.2/`; `/spec/latest/` is the current latest published route.
  - The v0.2 schema and context are pinned by hash in the release execution result: `schema.json` is `fe79ddb4b6cef525c658196d11ed9da22884e836bbb87c989154d9c77e544011`; `schema.jsonld` is `005bd972d7cb7c6b5725670b06606d31d3394132391d771d89ba510aa4b3bc30`.
  - Verification re-ran the local hash parity check against `/Users/grig/work/repo/universalmanifest/spec/v0.2/` and `/Users/grig/work/repo/universalmanifest/site/public/ns/universal-manifest/v0.2/`; both hashes matched the pinned release values.
- Residual risk:
  - None blocking for v0.2 early-adopter publication. Future identity-binding and profile-expansion questions are listed in section 4.

### G2 Conformance testability evidence

- Artifact paths:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.2/`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.2/invalid/`
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/conformance/v0.2.md`
  - `/Users/grig/work/repo/universalmanifest/site/public/conformance/badges/v0.2-baseline.svg`
  - `/Users/grig/work/repo/universalmanifest/site/public/conformance/badges/v0.2-extended.svg`
- Result-report evidence:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0224-result.md`
- Commands run:
  - `npm test` from `/Users/grig/work/repo/universalmanifest/packages/universal-manifest`
- Output summary:
  - TypeScript build passed.
  - Example validation passed with 49 valid fixtures accepted, 26 invalid fixtures rejected as expected, 26 integration-lane fixtures accepted as non-normative integration evidence, and 11 GPC proof checks passed.
- Residual risk:
  - Broader adversarial conformance expansion remains future work, but the v0.2 baseline and invalid-fixture suite pass for this release.

### G3 Integrity and trust profile evidence

- Artifact paths:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.2/minimal-signed-manifest.jsonld`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.2/manifest-with-facets-signed.jsonld`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.2/manifest-with-pointers-signed.jsonld`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.2/invalid/invalid-signature.jsonld`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.2/invalid/invalid-signature-algorithm.jsonld`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.2/invalid/invalid-signature-canonicalization.jsonld`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.2/invalid/invalid-signature-public-key.jsonld`
- Result-report evidence:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0224-result.md`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0230-result.md`
- Commands run:
  - `npm test` from `/Users/grig/work/repo/universalmanifest/packages/universal-manifest`
- Output summary:
  - The v0.2 signed manifest fixtures and invalid signature fixtures participated in the passing validation run.
  - The v0.2 baseline is JCS + Ed25519. Data Integrity / RDF profile expansion is explicitly deferred by `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md` and Phase 19.
- Residual risk:
  - Data Integrity / RDF profiles, additional integrity-profile registry entries, and broader identity-binding tiers remain Phase 19 follow-ons, not v0.2 blockers.

### G4 Interoperability proof evidence

- Artifact paths:
  - `/Users/grig/work/repo/universalmanifest/integrations/reference-runtime.md`
  - `/Users/grig/work/repo/universalmanifest/integrations/social.md`
  - `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`
  - `/Users/grig/work/repo/universalmanifest/integrations/runtime-profile.md`
  - `/Users/grig/work/repo/universalmanifest/integrations/data-firewall-ux.md`
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/README.md`
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/implementations/index.md`
- Result-report evidence:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0224-result.md`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0230-result.md`
- Commands run:
  - `npm run journeys` from `/Users/grig/work/repo/universalmanifest/packages/universal-manifest`
  - `npm run smoke:endpoints:prod` from `/Users/grig/work/repo/universalmanifest/packages/universal-manifest`
  - `npm run smoke:endpoints:prod:contract` from `/Users/grig/work/repo/universalmanifest/packages/universal-manifest`
- Output summary:
  - Journey proof passed: preflight 1 pass, journeys 27 pass, 0 fail.
  - Production endpoint smoke passed against `https://universalmanifest.net` and `https://myum.net`.
  - Production contract smoke passed; redirect, revoked, and corrupt-record prod-only fixtures were skipped because the required optional environment UMIDs were not set.
- Residual risk:
  - Independent external adopter feedback remains a Phase 19 follow-on. That is not a blocker for v0.2 early-adopter publication closeout.

### G5 Publishing and discoverability evidence

- Artifact paths:
  - `/Users/grig/work/repo/universalmanifest/docs/PUBLISHING-AND-VERSIONING.md`
  - `/Users/grig/work/repo/universalmanifest/docs/RELEASING.md`
  - `/Users/grig/work/repo/universalmanifest/docs/README.md`
  - `/Users/grig/work/repo/universalmanifest/site/public/.well-known/universal-manifest.json`
  - `/Users/grig/work/repo/universalmanifest/site/public/llms.txt`
  - `/Users/grig/work/repo/universalmanifest/site/public/agent/fixture-catalog.json`
  - `/Users/grig/work/repo/universalmanifest/site/public/agent/sandbox-scenarios.json`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/publishing/changelog.md`
  - `/Users/grig/work/repo/universalmanifest/docs/announcement/2026-04-30-v0-2-published.md`
- URLs:
  - `https://universalmanifest.net/spec/v0.2/`
  - `https://universalmanifest.net/spec/latest/`
  - `https://universalmanifest.net/.well-known/universal-manifest.json`
  - `https://universalmanifest.net/llms.txt`
  - `https://github.com/grigb/universal-manifest/releases/tag/spec-v0.2`
- Result-report evidence:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0220-release-executed-result.md`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0222-result.md`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0226-result.md`
- Commands run:
  - `npm run build` from `/Users/grig/work/repo/universalmanifest/site`
  - `gh release view spec-v0.2 --repo grigb/universal-manifest --json tagName,isDraft,isPrerelease,publishedAt,url,targetCommitish`
  - `jq` checks against `/Users/grig/work/repo/universalmanifest/site/public/.well-known/universal-manifest.json`, `/Users/grig/work/repo/universalmanifest/site/public/agent/fixture-catalog.json`, and `/Users/grig/work/repo/universalmanifest/site/public/agent/sandbox-scenarios.json`
  - Built-output link and placeholder checks against `/Users/grig/work/repo/universalmanifest/site/dist/spec/latest/index.html`, `/Users/grig/work/repo/universalmanifest/site/dist/spec/v0.2/index.html`, and `/Users/grig/work/repo/universalmanifest/site/dist/publishing/changelog/index.html`
- Output summary:
  - Site build passed and emitted `/spec/latest/index.html`, `/spec/v0.2/index.html`, `/publishing/changelog/index.html`, and `/governance/spec-improvement-queue/index.html`.
  - Existing route-conflict warnings remain for `/about/one-pager`, `/about/why-um`, `/proof/harness`, and `/use-cases`; they did not block the build.
  - GitHub release lookup returned `tagName: spec-v0.2`, `isDraft: false`, `isPrerelease: false`, `publishedAt: 2026-04-30T21:54:06Z`, `targetCommitish: main`, and URL `https://github.com/grigb/universal-manifest/releases/tag/spec-v0.2`.
  - JSON publication metadata checks passed: the well-known descriptor declares `currentSpecVersion: "v0.2"`, `project.versions.stable: "v0.2"`, `project.versions.previous: "v0.1"`, `project.versions.draft: null`, and `lastUpdated: "2026-04-30"`; both agent catalogs declare `currentSpecVersion: "v0.2"` and `generatedAt: "2026-04-30T00:00:00.000Z"`.
  - Built-output link checks passed for v0.2 spec, migration guide, conformance, reference implementation, governance queue, and GitHub release links.
  - Placeholder checks passed: no `MIGRATION_GUIDE_HREF`, `RFC_HREF`, `BREAKING_CHANGE_HREF`, `Latest Draft Specification`, or `This document is a draft` remained in the built latest/v0.2 spec pages.
- Residual risk:
  - `npm run smoke:publication` does not exist because `WO-0227` is obsolete after the 2026-04-28 revert. The substitute checks above are the closest available publication verification path.

### G6 Governance and change control evidence

- Artifact paths:
  - `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
  - `/Users/grig/work/repo/universalmanifest/docs/governance/BREAKING-CHANGE-POLICY.md`
  - `/Users/grig/work/repo/universalmanifest/docs/governance/DEPRECATION-POLICY.md`
  - `/Users/grig/work/repo/universalmanifest/docs/governance/INCIDENT-RESPONSE.md`
  - `/Users/grig/work/repo/universalmanifest/docs/governance/RELEASE-CADENCE.md`
  - `/Users/grig/work/repo/universalmanifest/docs/governance/SPEC-IMPROVEMENT-QUEUE.md`
  - `/Users/grig/work/repo/universalmanifest/docs/guides/MIGRATION-V01-V02.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/governance/spec-improvement-queue.md`
- Result-report evidence:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0223-result.md`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0225-result.md`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0230-result.md`
- Decision references:
  - The published spec links to breaking-change, deprecation, incident-response, release-cadence, and spec-improvement queue paths.
  - Phase 19 is routed through `/Users/grig/work/repo/universalmanifest/docs/governance/SPEC-IMPROVEMENT-QUEUE.md` before new normative text changes.
- Residual risk:
  - WO-0225 documented source-to-site governance mirror drift as intentional summary drift. Full source policies remain the source of truth.

### G7 Operational realism evidence

- Artifact paths:
  - `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
  - `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md`
  - `/Users/grig/work/repo/universalmanifest/docs/DEPTH-AND-SCOPE.md`
  - `/Users/grig/work/repo/universalmanifest/integrations/reference-runtime.md`
  - `/Users/grig/work/repo/universalmanifest/integrations/runtime-profile.md`
  - `/Users/grig/work/repo/universalmanifest/site/public/.well-known/universal-manifest.json`
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/smoke-endpoints.mjs`
- Result-report evidence:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0229-result.md`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-30-wo-0230-result.md`
- Operational validation notes:
  - Production smoke passed against docs and resolver surfaces.
  - Production contract smoke passed for direct UMID resolution, 304 revalidation, 400, 404, 405, and OPTIONS behavior.
  - Phase 9 remains manual-only after revert commit `e493b3e`; this is explicitly reflected in `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md` and `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md`.
- Residual risk:
  - Synthetic monitoring remains obsolete/reverted with `WO-0228`. That is not a release blocker because budget-zero/manual operational posture is the current authority-doc state.

## 4) Deferred items

- Item: `WO-0243` post-publication external-human reader validation activation.
- Why deferred: External-human validation was intentionally deferred until after v0.2 publication.
- Impact if unresolved: The project keeps internal and executable evidence, but lacks a new post-publication external-reader evidence pack.
- Owner: Future Phase 19 owner.
- Target closure date: Not assigned.

- Item: `WO-0244` adopter-feedback loop activation against published v0.2.
- Why deferred: Real adopter feedback starts after the published spec is stable.
- Impact if unresolved: Feedback/SLA machinery remains available but not yet exercised against post-publication reports.
- Owner: Future Phase 19 owner.
- Target closure date: Not assigned.

- Item: `WO-0245` Tier 2 cryptographic identity-binding research package.
- Why deferred: Cryptographic binding promotion requires more evidence than v0.2 publication closeout.
- Impact if unresolved: v0.2 remains at the published Tier 1 baseline while stronger binding remains future scope.
- Owner: Future Phase 19 owner.
- Target closure date: Not assigned.

- Item: `WO-0246` Tier 3 multi-party ceremony research package.
- Why deferred: Multi-party ceremony support is explicitly future candidate work.
- Impact if unresolved: v0.2 remains simpler and does not standardize ceremony behavior.
- Owner: Future Phase 19 owner.
- Target closure date: Not assigned.

- Item: `WO-0247` Data Integrity / RDF profile decision package.
- Why deferred: `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md` leaves RDF graph-signing semantics as future work.
- Impact if unresolved: v0.2 continues to use the JCS + Ed25519 interop baseline only.
- Owner: Future Phase 19 owner.
- Target closure date: Not assigned.

- Item: `WO-0248` additional integrity-profile registry decision package.
- Why deferred: Additional profiles beyond JCS + Ed25519 were not needed for v0.2 publication.
- Impact if unresolved: No alternate canonicalization, post-quantum, or multi-proof profile discovery is standardized yet.
- Owner: Future Phase 19 owner.
- Target closure date: Not assigned.

- Item: `WO-0249` revocation-as-normative decision package.
- Why deferred: Revocation/status metadata remains optional extension-lane behavior for v0.2.
- Impact if unresolved: Future versions still need to decide whether `statusRef` or `revocationCursor` become conformance requirements.
- Owner: Future Phase 19 owner.
- Target closure date: Not assigned.

- Item: `WO-0250` encrypted inline facet promotion decision.
- Why deferred: Encrypted inline facets remain guidance-only optional privacy work.
- Impact if unresolved: v0.2 does not require encrypted-facet lifecycle conformance.
- Owner: Future Phase 19 owner.
- Target closure date: Not assigned.

- Item: `WO-0251` broader cross-DID binding tier scope decision.
- Why deferred: Cross-DID binding expansion is beyond the v0.2 Tier 1 baseline.
- Impact if unresolved: Broader cross-DID scope waits for the Tier 2/Tier 3 research track.
- Owner: Future Phase 19 owner.
- Target closure date: Not assigned.

## 5) Blocking risks

- Risk: None identified for v0.2 early-adopter publication closeout.
- Severity: None.
- Owner: Universal Manifest maintainers.
- Mitigation status: Publication-wave residuals are explicitly deferred through Phase 19 stubs in `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md` and `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`.

## 6) Final release decision

- Decision: APPROVED
- Reasoning: v0.2 publication is already executed, the public surfaces build, production docs/resolver smoke checks pass, artifact hashes match the pinned release values, machine-readable discovery declares v0.2 current, conformance validation passes, journey proof passes, and residual items are explicitly deferred into Phase 19.
- Effective date: 2026-04-30

## 7) Sign-off

- Approver name: WO-0231 implementation worker
- Approver role: Publication closeout audit worker
- Date: 2026-04-30
- Signature/approval note: Approved for v0.2 early-adopter publication closeout based on the evidence paths, result reports, command outputs, and URLs listed in this pack.
