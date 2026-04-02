# Decisions (Universal Manifest)

## 2026-04-01 — Payment-handle guidance adopts pointer-first split with additive privacy alignment (WO-0142)

### Decision

- Add non-normative payment-handle naming guidance to `spec/v0.1/REGISTRY.md` for:
  - public-safe initiation pointers,
  - fiat gateway account/order references,
  - crypto settlement references,
  - protected bundle routing.
- Adopt explicit separation between:
  - `payment.public.checkout` (safe initiation surface),
  - `payment.protected.bundle` (sensitive handle route).
- Add consent key `payment.handle.protected` and overlay family `prefs.financial.handle.*` as guidance-only conventions.
- Align protected-handle delivery with WO-0143 privacy outcome using an additive model (`projection-or-encrypted-inline`) without introducing new core conformance requirements.

### Rationale

- `prefs.financial.*` existed but lacked interoperable naming for concrete payment routing.
- Provider-neutral pointer naming avoids lock-in while allowing Stripe, PayPal, and crypto rails to coexist.
- Explicit public-vs-protected split reduces accidental data exposure and gives consumers deterministic initiation behavior.
- Keeping this work non-normative preserves v0.1/v0.2 contract stability.

### Policy impact

- New payment-handle conventions are discoverable via registry guidance and executable fixture/journey proof.
- No core schema or conformance expansion is introduced by this decision.

## 2026-04-01 — Address Bag of Claims vulnerability with tiered trust model and identity binding conventions

### Decision

- Adopt a four-tier trust model for manifest claim verification:
  - Tier 0 (Signature-only): zero friction, self-asserted claims.
  - Tier 1 (Attested/evidence-backed): low friction, attested cross-DID binding or VP evidence.
  - Tier 2 (Cryptographic binding): medium friction, multi-signature or ZK proofs.
  - Tier 3 (Multi-party ceremony): high friction, multi-keyholder co-signing from different locations.
- Ship three non-breaking additions in v0.2:
  - Normative security considerations text documenting the Bag of Claims vulnerability, the tiered trust model, and the privacy-binding tension.
  - An optional `claims[].claimProof` schema field for VP references (Tier 1 foundation).
  - A non-normative `identity.crossDidBinding` claim convention for attested cross-DID binding.
  - A non-normative `um:agentDelegation` pointer convention for delegation transparency.
  - A non-normative `requiredTrustTier` field convention for issuer-declared security requirements per claim/facet.
- Explicitly defer L3 (multi-signature binding) to v0.3 and L4 (ZK identity proofs) to v0.4+.

### Rationale

- The Bag of Claims vulnerability is a structural gap: claims from multiple issuers sit in a manifest with no cryptographic proof of common control. Five attack vectors were identified (credential stacking, cross-DID theft, issuer impersonation, pairwise DID abuse, Sybil amplification), two rated Critical.
- CRO assessment: only L1 (attested binding) is implementable in v0.2. No target credential provider (World ID, Gitcoin Passport, BrightID) issues W3C VCs. DID co-signing is blocked for `did:plc` and `did:chia`.
- Security assessment: L1 alone doesn't address the two Critical vectors. The `claims[].claimProof` field creates the upgrade path at zero current cost.
- The tiered trust model gives relying parties a decision framework instead of a false sense of security, while the `requiredTrustTier` convention allows manifest authors to declare the security level their data requires.
- User friction is the primary adoption concern. Each tier is designed with increasing friction matched to increasing stakes. Users should never face more ceremony than their use case requires.

### Evidence

- CRO Report: `.dev/ai/findings/synthetic-reviews/cro-identity-correlation-implementability.md`
- Security Report: `.dev/ai/findings/synthetic-reviews/security-identity-correlation-privacy-impact.md`
- Thesis: `.dev/ai/knowledge-corpus/thesis-identity-correlation-bag-of-claims.md`
- Proposal: `.dev/ai/proposals/PROPOSAL-v0.2-identity-binding-and-liveness.md`
- Work order: `.dev/ai/workorders/WO-0170-identity-correlation-binding.md`

### Policy impact

- `spec/v0.2/README.md` security considerations must be updated with Bag of Claims disclosure and tiered trust model.
- `spec/v0.2/schema.json` gains an optional `claims[].claimProof` field.
- `docs/security/THREAT-MODEL.md` must be extended with five new attack vectors.
- Follow-on work orders needed for: fixture suite, integration lane updates, site docs, claim registry entry.
- L3/L4 are explicitly deferred — no multi-signature or ZK work should begin until v0.3 planning.
- Pairwise DID privacy is preserved: cross-DID binding is always opt-in, never mandated.

## 2026-03-06 — Execute GPC as runtime-authoritative with optional UM evidence projection

### Decision

- Implement GPC in the TypeScript reference implementation as a hybrid model:
  - runtime observation (`Sec-GPC`, `navigator.globalPrivacyControl`) is authoritative,
  - UM consent/pointer projection is optional descriptive evidence,
  - `/.well-known/gpc.json` is parsed as support metadata, not per-request proof.
- Add a non-normative GPC proof pack and journey row (`J21`) without promoting GPC semantics into v0.1 core conformance requirements.

### Rationale

- This matches the WO-0127 standards review outcome while keeping the base UM contract stable.
- It makes the integration executable and testable immediately.
- It preserves a clean boundary between request-time privacy signaling and transportable manifest evidence.

### Policy impact

- GPC remains non-normative in core UM v0.1/v0.2 spec terms unless promoted later through a separate standards decision.
- Reference implementation proof now includes:
  - runtime GPC normalization,
  - support-resource parsing,
  - evidence projection validation,
  - journey proof for scope-limited supersession behavior.

## 2026-03-05 — Complete Go-Now integration guidance wave for Portable Identity Profile and MUM

### Decision

- Complete and publish both Go-Now execution tracks as non-normative integration hardening outputs:
  - Portable Identity Profile (`PIP-GN-01` through `PIP-GN-06`)
  - Metaverse Universal Manifest (`MUM-GN-01` through `MUM-GN-06`)
- Adopt two new guidance profiles for immediate external implementer use:
  - `docs/guides/PORTABLE-IDENTITY-PROFILE-XR-IMPLEMENTATION-PATH.md`
  - `docs/guides/MUM-SYNCHRONIZATION-PROFILE.md`
- Publish site mirrors and sidebar discoverability for both guides under `/guides/`.

### Rationale

- Both tracks already had executable fixture/journey evidence, but external implementers still needed actionable consumer/issuer sequencing and synchronization conventions.
- Completing GN-05/GN-06 closes documentation-to-governance drift and makes meeting-ready integration claims auditable.
- Keeping these as non-normative profiles preserves core UM contract stability while improving immediate interoperability quality.

### Policy impact

- Integration lanes for Portable Identity Profile and Metaverse now require explicit cross-links to their corresponding implementation/synchronization guides.
- Go-Now closure evidence must include:
  - conformance run artifact,
  - journey run artifact,
  - docs-site build artifact,
  - governance synchronization note.
- Next execution focus shifts from Go-Now to Research-First tracks (`PIP-RS-*`, `MUM-RS-*`) under existing promotion gates.

## 2026-03-02 — Gate G6 governance completion baseline adopted

### Decision

- Adopt explicit governance operational policies required for Gate G6 closure:
  - `docs/governance/BREAKING-CHANGE-POLICY.md`
  - `docs/governance/DEPRECATION-POLICY.md`
  - `docs/governance/INCIDENT-RESPONSE.md`
  - `docs/governance/RELEASE-CADENCE.md`
- Adopt `docs/guides/MIGRATION-V01-V02.md` as the canonical v0.1-to-v0.2 migration playbook.

### Rationale

- Gate G6 requires explicit breaking-change and deprecation policy evidence.
- World-ready checks require documented and tested incident/rollback procedures.
- External adopters need predictable lifecycle and migration contracts before multi-party interoperability claims are credible.

### Policy impact

- Breaking normative changes now require explicit migration and rollback artifacts before merge.
- Version lifecycle states (`draft`, `stable`, `deprecated`, `end-of-life`) are now formal governance vocabulary.
- Incident simulation evidence is now part of release readiness evidence for major governance milestones.

## 2026-02-11 — v0.1 bootstrap decisions

### Separate spec repo

- The Universal Manifest lives as a **fully separate repo** at ``.
- reference implementation consumes it, but it is versioned and maintained independently.

### Manifest ID generation (`@id`)

- v0.1 recommendation: issuers generate `@id` as `urn:uuid:<uuidv4>`.
- Rationale: globally unique, offline-safe, and avoids premature content-addressing commitments.

### Device caching + logging (constrained device / public display)

- Cache the **full manifest JSON** while actively in use.
- Persist only **manifest ID references** (`@id`) in logs/telemetry.
- Future recovery may use those IDs, but recovery workflows are intentionally out of scope for v0.1.

### Security scope (v0.1)

- `signature` is present only as a permissive placeholder.
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

- Capture vision direction that Universal Manifest composition should center on a **Record** primitive:
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

## 2026-02-17 — Journeys → tests as proof of concept (validation direction)

### Decision

- Define canonical **user journeys** for Universal Manifest adoption and map them to an **executable end-to-end test suite** as the primary evidence mechanism for “the concept works”.

### Rationale

- Prevent “done by documentation” without runnable proof.
- Provide a clear, adoptable path for external implementers (Linux Foundation-grade expectations).
- Keep reference implementation as an important consumer without making UM “about reference implementation”.

### Policy impact

- Treat “journeys → tests” as a required output for maturity claims and future “done done” evidence packs.
- Tracked as work order: `docs/workorders/WO-0012-user-journeys-and-e2e-test-suite.md`.

## 2026-02-17 — v0.2 signature profile baseline (interoperability hardening)

### Decision

- Adopt a pragmatic, adoption-first v0.2 integrity baseline:
  - Canonicalization: **JCS (RFC 8785)**
  - Signature: **Ed25519**
  - Signature encoding: **base64url**
- Keep a future **Data Integrity** path as additive (not either-or).

### Rationale

- JCS + Ed25519 is broadly implementable across languages without requiring JSON-LD tooling.
- The signature profile is a major interop-hardening step without forcing identity method standardization.

### Policy impact

- v0.2 artifacts exist in `spec/v0.2/` (schema + context + conformance + profile).
- Fixture verification and harness support for v0.2 must validate the signature profile deterministically.

## 2026-02-17 — TS helper package distribution policy (do not publish yet)

### Decision

- Keep the TypeScript helper package **private/internal** for now:
  - `packages/universal-manifest/` (now `universal-manifest`; formerly `@localartistnetwork/universal-manifest`)

### Rationale

- Avoid “public SDK drift” while the spec is still in v0.x and publishing/governance is stabilizing.
- The primary adoption contract is the published spec artifacts + fixtures, not a single implementation library.

### Policy impact

- No npm or public registry publishing until:
  - v0.2 artifacts are published at stable URLs, and
  - the docs site for `universalmanifest.net` is “implementer-grade”.

## 2026-02-17 — CI verification + endpoint smoke added (repeatable proof)

### Decision

- Add a repo-native CI verification workflow and a small endpoint smoke script.
  - CI workflow: `.github/workflows/verify.yml`
  - Endpoint smoke: `packages/universal-manifest/scripts/smoke-endpoints.mjs`

### Rationale

- Make “proof” repeatable and reviewer-friendly for adopters (Linux Foundation-grade expectation).
- Provide an outside-in contract check for `universalmanifest.net` (docs) and `myum.net` (resolver) without requiring a front-end app.

### Policy impact

- Post-deploy checks for publishing should include endpoint smoke:
  - `packages/universal-manifest` → `npm run smoke:endpoints:prod`

## 2026-02-17 — Repository relocation + GAS split onboarding model

### Decision

- Relocate Universal Manifest from:
  - legacy archived location (historical only)
- To:
  - `<repo-root>`
- Align agent onboarding to the GAS split model:
  - `AGENTS.md` = immutable global rules copy
  - `PROJECT-RULES.md` = project-specific rules and onboarding
- Expand `.dev` structure to GAS-standard working directories.

### Rationale

- Reduce ongoing reference implementation/UM context bleed from shared parent path.
- Make project identity, onboarding, and handoffs clearer for future agents.
- Match current GAS guidance and tooling assumptions.

### Policy impact

- All new path references should use `<repo-root>`.
- Legacy path references are historical only and should be updated when touched.

## 2026-02-18 — Priority: interactive Manifest Workbench on universalmanifest.net

### Decision

- Treat an interactive **Manifest Workbench** as a priority deliverable for adopter trust and usability.
- The workbench must support:
  - import existing manifest
  - structured explore/edit flow
  - create from scratch
  - validate against UM rules
  - export updated/new manifest
- Track implementation as:
  - `docs/workorders/WO-0014-interactive-manifest-workbench.md`

### Rationale

- Standards adoption is blocked if implementers cannot quickly test, edit, and validate manifests in a real tool.
- This is a direct demonstration surface that the contract is practical, not just documented.

### Policy impact

- Workbench is now part of the critical delivery agenda for docs/tooling on `universalmanifest.net`.
- Validation behavior in the workbench must align with spec/conformance docs and not create a second contract.

## 2026-02-18 — Priority: first-time \"What is Universal Manifest\" overview

### Decision

- Add and maintain a first-time reader overview that explains:
  - what Universal Manifest is
  - who it is for
  - how to start using it
- Include visual onboarding (diagram-first support) with maintainable source assets.
- Track implementation as:
  - `docs/workorders/WO-0015-first-time-overview-and-visual-onboarding.md`

### Rationale

- Existing docs are strong for deep implementers but do not yet provide a clear, standalone orientation entry point.
- First-contact clarity is required for external adoption and executive/share-out contexts.

### Policy impact

- Overview content is now a required onboarding artifact, not optional editorial polish.
- Diagram assets must be maintained with source files so visuals stay versionable and auditable.

## 2026-02-18 — Knowledge integration must be tracked via a living ledger

### Decision

- Treat indexed knowledge ingestion as an explicit, ongoing workstream.
- Maintain a living source-to-artifact integration ledger that records:
  - source scanned
  - integration status (`integrated`, `deferred`, `rejected`)
  - evidence path(s)
  - follow-on work order(s), if needed
- Track the workstream as:
  - `docs/workorders/WO-0016-gas-index-scan-and-knowledge-integration-ledger.md`

### Rationale

- Prior audits and crosswalks exist, but they are point-in-time snapshots.
- A maintained ledger is required to ensure high-value indexed sources are systematically applied or explicitly deferred.

### Policy impact

- Future phase transitions should include a knowledge-integration checkpoint.
- Major indexed-source updates should produce a report update under `docs/reports/`.

## 2026-02-18 — Resolve deferred corpus conflicts before IA/journey expansion

### Decision

- Promote all deferred sources in the current external corpus batch into active integration.
- Resolve conflicts before implementation planning, with explicit conflict IDs and decisions.
- Treat conflict decisions as mandatory planning inputs for IA, journeys, and workbench requirements.

Primary conflict register:
- `.dev/ai/ingestion/records/2026-02-18-cross-source-conflicts.md`

### Rationale

- Building IA and user journeys from a partial corpus introduces preventable rework and weakens provenance.
- Conflict resolution must happen before concrete planning so project direction is explicit and auditable.

### Policy impact

- Current batch has no deferred sources remaining.
- Follow-on implementation planning is tracked as:
  - `docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md`

## 2026-02-19 — WO-0017 corpus decisions materialized into IA/journey/workbench planning

### Decision

- Execute first concrete WO-0017 materialization pass from the full-corpus synthesis into:
  - IA delta artifact
  - journey planning overlays and identity-method variants
  - workbench requirement hardening tied to conformance outcomes

### Evidence

- `.dev/ai/specs/2026-02-19-ia-delta-from-full-corpus.md`
- `docs/journeys/README.md`
- `docs/workorders/WO-0014-interactive-manifest-workbench.md`
- `docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md`

### Conflict linkage

- `CON-UM-001`: convergence framing over novelty.
- `CON-UM-002`: composable envelope over monolith.
- `CON-UM-003`: identity-method neutrality in core.
- `CON-UM-004`: implementation and publication sequencing split.
- `CON-UM-005`: metaverse as exemplar, not scope anchor.
- `CON-UM-006`: standards-neutral framing boundaries.

### Policy impact

- `GAP-K2B-001` is closed by IA artifact creation.
- `GAP-K2B-002` is closed for planning-materialization scope.
- `GAP-K2B-003` is now implementation-tracked in WO-0014.

## 2026-02-20 — Directive: codify MUM lineage + metaverse/RP1/smart-glasses integration lanes

### Decision

- Record Universal Manifest lineage to the original **Metaverse Universal Manifest (MUM)** source document:
  - `Metaverse Universal Manifest (MUM) concept source document (Metaverse Standards Forum working group archive)`
- Codify three explicit integration lanes:
  - metaverse applications (cross-world identity, assets, social graph, and preferences)
  - RP1 spatial fabric
  - smart-glasses social layer with granular consent and disclosure controls

### Rationale

- Preserve provenance to the originating concept as part of project source-of-truth documentation.
- Make metaverse scope explicit without collapsing Universal Manifest into a metaverse-only specification.
- Capture high-priority integration directions early so user journeys, IA, and conformance planning can evolve from a stable strategic baseline.

### Policy impact

- Vision and onboarding docs must include the MUM lineage statement and metaverse/RP1/smart-glasses integration targets.
- Integration guidance for these lanes is and belongs under `integrations/` and site `integrations` pages.
- Any normative requirements derived from these lanes require explicit versioned spec and conformance changes.

## 2026-02-20 — Resolver reliability and production route parity hardening

### Decision

- Treat local resolver journey seeding as a preview-KV requirement for deterministic `wrangler dev --local` behavior.
- Bind resolver triggers for both host variants:
  - `myum.net/*`
  - `www.myum.net/*`
- Treat `/getting-started/workbench/` redirect-to-canonical (`308` -> `/workbench/`) as a valid live route outcome when target resolves `200`.

### Rationale

- `J03` failures were caused by local KV writes being made to non-preview storage while local dev served preview bindings.
- Production resolver availability on `www.myum.net` is required to prevent host-variant breakage (`522` observed before trigger update).
- Static-host canonicalization redirects are normal behavior and should not be misclassified as deployment failure when terminal route is healthy.

### Policy impact

- Journey tooling must seed preview KV for local resolver E2E (`packages/universal-manifest/scripts/run-journeys.mjs`).
- Resolver deployment config must carry both route patterns in source (`services/myum-resolver/wrangler.toml`).
- Post-deploy checks should verify both canonical and redirected workbench paths plus `www.myum.net` health.

## 2026-02-20 — DID method selection for initial coverage

### Decision

- Support `did:plc`, `did:web`, and `did:key` as initial DID method coverage for Universal Manifest identity references.

### Rationale

- `did:plc` for AT Protocol / Bluesky ecosystem compatibility.
- `did:web` for web-based DID resolution using existing domain infrastructure.
- `did:key` for self-sovereign, key-based identifiers that work offline without external resolution infrastructure.

### Status

- Active

### Policy impact

- These methods are integration targets; core spec remains identity-method-neutral per CON-UM-003.
- Additional DID methods (e.g., `did:chia`) are supported as extension lanes.

## 2026-02-20 — Proof-of-personhood provider selection

### Decision

- Target World ID, Gitcoin Passport, and BrightID as initial proof-of-personhood providers for the personhood integration lane.

### Rationale

- API-backed, widely recognized, and complementary verification approaches:
  - World ID: biometric (iris-scan) proof of unique personhood.
  - Gitcoin Passport: composite Sybil-resistance score from multiple identity stamps.
  - BrightID: social-graph-based unique-human verification.
- Multi-provider coexistence allows consumers to select trust models appropriate to their context.

### Status

- Active

### Policy impact

- Provider-specific claims, pointer names, and consent keys are explicitly non-normative integration guidance.
- Integration guidance lives under `integrations/proof-of-personhood.md` and corresponding site pages.
- Tracked as part of WO-0024.

## 2026-02-23 — Onboarding validation policy update (WO-0035)

### Decision

- Remove the mandatory human-validation gate for onboarding closure.
- Human-participant reader testing remains available as an optional quality signal.
- `WO-0015` closure is allowed with existing documented implementation and validation evidence.

### Rationale

- The mandatory gate was creating execution deadlock and blocking progress.
- Existing onboarding rewrite work and automated validation already provide sufficient baseline evidence for this phase.
- Human-reader testing can still be run when helpful, but it is no longer a hard release gate.

### Policy impact

- `WO-0015` is no longer blocked on a dated human-participant artifact.
- `WO-0035` is considered complete once policy and status docs are aligned to this decision.
- `WO-0039` closure is no longer gated on Phase 5 human-participant execution.
- Human-test protocol/checklist artifacts remain available for optional validation runs.

## 2026-02-28 — Static diagrams/Excalidraw: ON HOLD

### Decision

- Static diagram work in this repo is placed ON HOLD.
- Infographics creation has been offloaded to the global agent system's infographics kit.
- Excalidraw is not approved for production visuals (previously established).
- Work will be revisited when the user returns with:
  - completed infographics work ready to integrate into the project, or
  - a request to identify knowledge gaps to share with other agents (where Excalidraw may assist).

### Rationale

- Avoiding duplicated effort between this project and the global agent system's infographics tooling.
- Excalidraw retains a potential future role for communicating complex logic flows and infographic layouts, but this is not a current priority.

### Policy impact

- Agents should not start static diagram or Excalidraw work in this repo without explicit instruction from the user.
- The prompt pack pipeline (`docs/design/ANIMATED-SVG-WORKFLOW.md`) remains the default for animated explainer content.

## 2026-02-22 — Integrity and revocation hardening posture (WO-0037)

### Decision

- Execute an aggressive documentation hardening pass for v0.2 contract language:
  - add explicit normative direction for revocation cursor/events as a profile extension lane,
  - codify multi-profile verification behavior (`algorithm` + `canonicalization` pair as profile identifier),
  - expand adversarial fixture expectations in conformance documentation.

### Rationale

- Remaining ambiguity around revocation/integrity extension semantics is a practical source of interop drift.
- Early explicitness in normative language reduces interpretation variance before broader adoption.
- Adversarial fixture coverage is required to turn policy statements into executable safeguards.

### Policy impact

- `spec/v0.2/SIGNATURE-PROFILE.md` and `spec/v0.2/CONFORMANCE.md` must be updated in lockstep.
- Adversarial v0.2 fixture matrix expansion is required in `examples/v0.2/invalid/`.
- Follow-on implementation work may be needed where helper/runtime behavior lags new normative direction.

## 2026-02-28 — Capsule-Pod approved as UM iconic representation

### Decision

- Approve the **Capsule-Pod** (Concept 11 from [01-ICONIC-REPRESENTATION.md](teaching-scripts/01-ICONIC-REPRESENTATION.md)) as the official iconic visual character for Universal Manifest.
- Approve the **variant concept**: each user or entity may have their own personal-style variant while preserving the core shell-gap-payload structure and state color mapping.

### Rationale

- Capsule-Pod scored joint-highest (32/40) across simplicity, distinctiveness, metaphor strength, and animation-friendliness.
- The shell-gap-payload structure directly maps to the manifest's envelope-integrity-data architecture.
- The gap-illumination gesture (green = verified, red = rejected) is the single most teachable animation beat.
- The variant concept enables personalization and community identity without fragmenting visual recognition.

### Evidence

- Design spec: [CAPSULE-POD-DESIGN.md](design/CAPSULE-POD-DESIGN.md)
- Cinematic reference renders: [capsule-pod-reference/](design/capsule-pod-reference/)
- Variant exploration: [Grok render gallery](https://grok.com/imagine/post/06d18c9d-9316-427b-baa6-115d5a5543a8)

### Policy impact

- All future teaching scripts, animations, and visual assets should use the Capsule-Pod as the primary manifest character.
- The visual system vocabulary (Pod = manifest, Shield = verification, Prism = projection) is canonical.
- State color mapping from the design spec must be applied consistently across all render and animation outputs.

## 2026-03-01 — Expanded CI pipeline adopted (ci.yml)

### Decision

- Adopt an expanded CI/CD pipeline ([`.github/workflows/ci.yml`](../.github/workflows/ci.yml)) as the primary CI workflow, replacing the original [`verify.yml`](../.github/workflows/verify.yml) as the authoritative continuous integration configuration.

### Relationship to verify.yml

- The original `verify.yml` workflow provided a single-job pipeline (checkout, install, test) for the TypeScript reference implementation.
- The new `ci.yml` workflow expands this to a multi-job pipeline with the following jobs:
  1. **test** -- runs the TypeScript reference implementation test suite (`packages/universal-manifest`)
  2. **terminology** -- checks terminology consistency across the codebase (`npm run check:terminology`)
  3. **build-site** -- builds the Astro/Starlight documentation site (`site/`) and uploads the built artifact
  4. **link-check** -- checks all internal and external links in the built site (depends on build-site)
  5. **parity-test** -- validates that the Node.js and browser validators produce identical results (depends on test + build-site)
  6. **scenario-smoke-test** -- runs structural smoke tests for sandbox scenarios (depends on build-site)
  7. **smoke-endpoints-prod** -- smoke-tests production endpoints on `universalmanifest.net` and `myum.net` (runs only on main branch merges or manual dispatch; depends on test + terminology + build-site)
- `verify.yml` is retained for backward compatibility but `ci.yml` is now the authoritative CI workflow that covers the full project scope (spec validation, site build, link integrity, cross-runtime parity, and production endpoint health).

### Date and reference

- Date: 2026-02-28
- Work order: [WO-0049](workorders/WO-0049-add-ci-workflow.md)

### Rationale

- The single-job `verify.yml` pipeline only validated the TypeScript reference implementation. It did not cover the documentation site build, link integrity, terminology consistency, cross-runtime parity, or production endpoint health.
- The expanded `ci.yml` pipeline provides comprehensive pre-merge and post-merge validation that covers the full project scope: spec artifacts, documentation, tooling, and live infrastructure.
- Multi-job parallelism improves CI throughput: independent jobs (test, terminology, build-site) run concurrently, while dependent jobs (link-check, parity-test, scenario-smoke-test) wait only for their prerequisites.

### Policy impact

- `ci.yml` is the CI configuration that contributors should reference for understanding what checks run on pull requests and merges.
- `verify.yml` remains in the repository as a simpler, backward-compatible check but is not the primary CI workflow.
- Future CI additions (new test jobs, deployment gates) should be added to `ci.yml`.

## 2026-03-03 — Permissions firewall model adopted as direction for consent evolution (v0.3+)

### Decision

- Adopt the permissions firewall model in [`docs/design/PERMISSIONS-FIREWALL-DESIGN.md`](design/PERMISSIONS-FIREWALL-DESIGN.md) as the architecture direction for consent and permissions evolution for v0.3 and later.
- Keep this direction non-normative until promoted into versioned spec artifacts (`spec/v0.3/`).
- Start immediate backward-compatible groundwork in non-normative surfaces:
  - registry consent-name expansion in `spec/v0.1/REGISTRY.md`
  - integration-lane examples and UX guidance in `integrations/`
  - stub fixture examples under `examples/v0.1/stubs/`

### Rationale

- The current consent model is sufficient for baseline interoperability but not expressive enough for audience-scoped and context-scoped permissions.
- A firewall model preserves the existing "default deny when missing consent" posture while offering clearer rule composition for real integrations.
- Keeping this work non-normative first allows implementation experimentation without destabilizing v0.1 or v0.2 contracts.

### Policy impact

- No normative schema or conformance requirement changes are introduced by this decision.
- Any future normative adoption must be versioned and paired with conformance updates.
- Integration examples may include firewall-style consent metadata as optional, forward-compatible fields.

## 2026-03-06 — Composite-stack and active-runtime architecture direction clarified

### Decision

- Treat Universal Manifest architecture as a **composite stack** with distinct:
  - trust layer,
  - data layer,
  - interaction layer.
- Keep Universal Manifest pointer-first and storage-neutral:
  - the manifest carries portable state and references,
  - large or mutable artifacts stay outside the manifest behind pointers.
- Recognize a **subject-controlled active runtime** (wallet, client, agent, or local-first sync service) as a valid non-normative implementation pattern for:
  - maintaining current state,
  - mediating consent,
  - coordinating push/pull exchange,
  - and operating bridge adapters for closed surfaces when needed.
- Treat closed-surface adapters and automation bridges as integration detail, not normative UM behavior.

### Rationale

- The newly localized architecture corpus converges on the same practical pattern: one portable manifest envelope, multiple underlying trust/data/projection systems, and a subject-side runtime that coordinates exchange.
- Current project docs implied this pattern but did not state it strongly enough at the source-of-truth level.
- Making the architecture direction explicit improves consistency across vision docs and integration lanes without forcing a protocol lock-in.

### Policy impact

- `docs/PROJECT-VISION.md` and `integrations/reference-runtime.md` should explicitly use the composite-stack and active-runtime framing.
- Integration lanes may reference this direction, but no new conformance obligation is created by this decision.
- Follow-on lane-specific updates should handle protocol volatility and unresolved research gaps separately from this architecture clarification.

## 2026-03-06 — Volatile protocol selection, proximity presentation, and federation strategy remain Research-First topics

### Decision

- Keep current architecture guidance and lane caveats, but do not promote any single protocol family, proximity transport, or federation substrate into stronger UM guidance without explicit promotion evidence.
- Treat the following as distinct Research-First work items:
  - protocol recommendation governance and standards currency,
  - proximity-triggered credential presentation boundaries,
  - federation and bridge strategy criteria for open and closed surfaces.
- Do not add new core-schema obligations for any of these topics at this stage.

### Rationale

- The localized source wave strengthened the architecture direction, but it did not produce a stable single answer for volatile credential stacks, proximity transport patterns, or federation substrate choice.
- Current official standards checkpoints show a mixed landscape: some foundations are stable, while several transport, selective-disclosure, browser/OS mediation, and substrate choices remain active decision surfaces.
- Moving these topics into explicit Research-First work prevents accidental lock-in through documentation drift.

### Policy impact

- Current integration lanes may continue to name protocol families only as bounded examples.
- Follow-on work should land as separate decision packages before any stronger recommendations appear in UM guidance.
- The next registered Research-First work orders are:
  - `docs/workorders/WO-0133-protocol-recommendation-governance-and-standards-currency-matrix.md`
  - `docs/workorders/WO-0134-proximity-credential-and-presentation-profile-assessment.md`
  - `docs/workorders/WO-0135-federation-and-bridge-strategy-decision-package.md`

## 2026-03-06 — Time-sensitive protocol-family status should live in a dated currency matrix

### Decision

- Keep narrative standards-positioning docs focused on relationship and scope.
- Track volatile protocol-family maturity and recommendation strength in a dated currency matrix instead of freezing those judgments inline across multiple docs.
- Allow only bounded examples in narrative or integration docs unless a protocol family has been promoted by the matrix process.

### Rationale

- The same protocol family can be stable enough to reference architecturally while still being too volatile to recommend operationally.
- A dated matrix reduces drift, centralizes review cadence, and keeps adopter-facing docs from quietly becoming stale.
- This model strengthens governance without changing UM conformance behavior.

### Policy impact

- `docs/STANDARDS-POSITIONING.md` and its site mirror should point readers to the dated currency matrix for live status context.
- Future protocol-family promotions or demotions should update the matrix first, then propagate only the approved wording into narrative docs.

## 2026-03-06 — Federation and bridge strategy is role-based; no single substrate is normative for UM

### Decision

- Keep the subject-controlled runtime as the canonical private-state authority for current consent, pointer routing, freshness decisions, and disclosure mediation.
- Evaluate external substrates by bounded role, not by brand alone:
  - canonical private state substrate,
  - public projection broker,
  - trust federation gatekeeper,
  - relay/sync coordinator,
  - edge availability custodian,
  - closed-surface bridge adapter.
- Do not present Solid, DWN, AT Protocol, OpenID Federation, or any other single substrate as “the UM federation layer”.
- Keep closed-surface bridge adapters non-normative implementation detail.

### Rationale

- The project’s architecture direction was already correct but lacked a final decision package that separated storage, projection, trust, sync, and bridge roles cleanly enough.
- The current standards landscape is mixed: different substrates are strong in different roles, and forcing them into one winner would create premature lock-in.
- A role-based frame preserves the composite-stack model while making source-of-truth, refresh, and failure behavior explicit.

### Policy impact

- Shared runtime and synchronization guidance should absorb the new role taxonomy first.
- Substrate-specific docs may reference only the role they actually fill, with explicit scope limits.
- No new conformance obligation is created by this decision.

## 2026-03-06 — OMB Wiki is discovery-only for spatial-fabric detail; RP1/MSF requires primary-source refresh before stronger guidance

### Decision

- Treat `omb.wiki` as a discovery and synthesis map for spatial-fabric material, not as the source of record.
- Keep the current UM RP1/MSF architectural boundary:
  - no new required core fields,
  - optional pointers and facets for ecosystem-specific semantics,
  - consent-gated cross-world behavior,
  - runtime-managed live spatial/presence state.
- Require a primary-source refresh before promoting newly surfaced spatial-fabric details into stronger RP1/MSF guidance.

### Rationale

- The OMB audit surfaced useful topology, attachment, service-decomposition, tooling, and asset-profile detail that was not yet reflected in the repo’s localized RP1 source set.
- That new detail reveals a source-completeness and integration-depth gap, not a core schema gap.
- The wiki is visibly still mixed-purpose and incomplete, so promoting its content directly would weaken authority discipline.

### Policy impact

- Follow-on spatial-fabric work should localize additional primary sources first, then refresh RP1/MSF guidance and proof artifacts from those sources.
- The existing RP1/MSF pointer/facet/consent overlay model remains valid.
- No normative UM change is created by this decision.

## 2026-03-06 — RP1/MSF scope composition and asset delivery remain non-normative integration guidance

### Decision

- Keep RP1/MSF scope composition represented through optional pointers and compact facets only.
- Use parent/root scope, child scope, and attachment-point summaries as the portable model instead of promoting live scope-tree semantics into the UM core.
- Keep 3D asset delivery external and pointer-first, with lightweight asset-profile hints only.
- Treat runtime session/view/tool state as non-portable unless deliberately exposed through a revocable pointer.

### Rationale

- Primary/open-source Manifolder sources make scope composition concrete: linked MSF resources create child-scope mounts, with runtime-managed cycles, caches, and view state.
- RP1 source captures already showed resource-driven linkage and internal primary/secondary object handling, but not a reason to encode that internal model into the standard.
- Khronos glTF confirms that runtime 3D asset delivery is a separate concern from identity or consent envelopes.

### Policy impact

- The RP1/MSF lane may use non-normative examples such as `rp1.attachmentIndex`, `rp1.assetProfile`, `spatialFabricAttachmentPolicy`, and `spatialAssetProfile`.
- Future hardening work should focus on adversarial attachment/freshness proof rather than schema expansion.
- No normative UM change is created by this decision.

## 2026-03-06 — RP1/MSF stale attachment indexes and revoked session context must fail closed

### Decision

- Keep RP1/MSF freshness and revocation handling in non-normative integration guidance and executable proof, not in the v0.1 core contract.
- Allow optional pointer-level freshness/status metadata such as `observedAt`, `expiresAt`, and `status` on RP1/MSF examples.
- If `rp1.attachmentIndex` evidence is stale or uncertain, block child-scope traversal.
- If `rp1.sessionContext` is expired or revoked, block replay/reuse.

### Rationale

- Pointer-first spatial integration is only safe if portable evidence cannot silently outlive the runtime authority that issued it.
- The risk is not missing schema coverage; the risk is stale or replayed attachment/session state being treated as current.
- Fail-closed runtime behavior preserves the existing UM boundary while giving adopters a concrete safety model they can implement immediately.

### Policy impact

- RP1/MSF guidance may include optional freshness/status metadata on pointers as portable audit evidence.
- New adversarial fixtures and journeys should prove blocked traversal/replay behavior without promoting those fields into core conformance obligations.
- No normative UM change is created by this decision.
