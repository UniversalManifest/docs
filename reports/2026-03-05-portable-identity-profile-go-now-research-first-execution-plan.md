# Portable Identity Profile — Comprehensive Go-Now / Research-First Execution Plan

Date: 2026-03-05  
Project: Universal Manifest (`/Users/grig/work/repo/universalmanifest`)  
Source baseline: `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-05-portable-identity-profile-gap-and-implementation-report.md`

## 1) Purpose and outcome

This plan converts the Portable Identity Profile gap analysis into an execution program that can be run immediately. It defines:

- what can be implemented now without waiting for new research,
- what requires research/planning before implementation,
- exact deliverables, verification, and evidence expectations,
- decision gates to move work from research into implementation.

This is not a concept note. It is a work-execution blueprint.

## 2) Planning constraints and operating rules

1. Universal Manifest remains spec-first and language-neutral.
2. Normative changes must go through `spec/` + `conformance/` + evidence.
3. Non-normative integration guidance should land first when uncertainty is high.
4. Work must satisfy existing Done-Done gate expectations:
   - `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-DEFINITION.md`
   - `/Users/grig/work/repo/universalmanifest/docs/DONE-DONE-CHECKLIST.md`
5. No execution outside approved sequence without user confirmation (current project policy).

## 3) What is already strong vs what is still uncertain

## 3.1 Strong enough to execute now

- Consent-first behavior and default-deny patterns.
- Pointer-first architecture for large XR assets.
- v0.2 signing and verification baseline.
- Revocation-aware extension path (`statusRef`, `revocationCursor`).
- Existing metaverse, smart-glasses, personhood, and Chia integration lanes.

Primary references:
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`
- `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`
- `/Users/grig/work/repo/universalmanifest/integrations/smart-glasses.md`
- `/Users/grig/work/repo/universalmanifest/integrations/data-firewall-ux.md`

## 3.2 Needs research/planning first

- Encrypted private-fragment profile.
- Selective disclosure / ZK proof profile.
- Wallet recovery profile.
- Protocol binding profile for OIDC4VP/OIDC4VCI/DIDComm.
- XR avatar translation profile standardization.

Primary references:
- `/Users/grig/work/repo/universalmanifest/docs/security/THREAT-MODEL.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md`
- `/Users/grig/work/repo/universalmanifest/docs/STANDARDS-POSITIONING.md`

## 3.3 Research depth status

Research exists, but unevenly:

- Deepest and most execution-ready: proof-of-personhood provider intake and integration artifacts.
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-22-world-id-proof-of-personhood.md`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-23-gitcoin-passport-verification.md`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-24-brightid-verification.md`
- Moderate: reference-platform architecture context (DIDComm, VRM, encryption patterns).
  - `/Users/grig/work/repo/universalmanifest/research/reference-platform/profile-architecture.md`
  - `/Users/grig/work/repo/universalmanifest/research/reference-platform/appendices-and-standards-mapping.md`
- Weaker: several external corpus items are still import-note level, not full design-ready synthesis.
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-01-composite-universal-manifest.md`
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/knowledge-corpus/imports/external-06-candidate-projects-protocols.md`

Execution implication:
- We should not block all progress.
- We should start Go-Now implementation while running targeted research spikes in parallel.

## 4) Program structure

This program has two synchronized tracks.

- Track A: `Go-Now` (implementation-first, no additional foundational research required).
- Track B: `Research-First` (spikes required before normative or high-risk implementation).

Both tracks feed a shared integration decision board:

- `Promote to integration guidance`
- `Promote to normative candidate`
- `Hold as optional lane`

## 5) Track A — Go-Now execution (implementation-first)

## A1) Workstream PIP-GN-01 — Portable Identity Profile XR Integration Lane v1

Goal:
- Publish a comprehensive non-normative lane for Portable Identity Profile in XR that combines existing patterns into one coherent contract for adopters.

Deliverables:
- New integration doc:
  - `/Users/grig/work/repo/universalmanifest/integrations/portable-identity-profile-xr.md`
- Site page mirror:
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/portable-identity-profile-xr.md`
- Link from docs index and integrations navigation.

Scope:
- Required baseline fields and flow.
- Suggested shard names for profile, avatar, capabilities, device-state, policy.
- Suggested pointer names for avatar, wearables, policy, proof endpoints.
- Suggested consent keys for capture, disclosure, voice, analytics.
- Clear normative boundary statement.

Acceptance criteria:
- Document is complete and follows integration template quality bars.
- Unknown-field tolerance and default-deny semantics are explicit.
- At least 3 end-to-end use cases are included.

Verification:
- Site build passes.
- Link hygiene passes for new routes.

## A2) Workstream PIP-GN-02 — Portable Identity Profile fixture pack (v0.1 + v0.2 overlays)

Goal:
- Add executable fixture evidence for Portable Identity Profile patterns that are already implementable.

Deliverables:
- New fixtures under:
  - `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.2/`
- Suggested fixture set:
  - `portable-identity-profile-xr-minimal-manifest.jsonld`
  - `portable-identity-profile-xr-avatar-pointers-manifest.jsonld`
  - `portable-identity-profile-xr-consent-matrix-manifest.jsonld`
  - `portable-identity-profile-xr-pairwise-subject-variant-a.jsonld`
  - `portable-identity-profile-xr-pairwise-subject-variant-b.jsonld`
  - `portable-identity-profile-xr-revocation-metadata-v02.jsonld`

Acceptance criteria:
- All new valid fixtures pass validator.
- Any intentionally invalid fixtures fail as expected.
- Fixture names and semantics are documented.

Verification commands:
- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test`

## A3) Workstream PIP-GN-03 — Journey expansion for Portable Identity Profile

Goal:
- Prove real Portable Identity Profile behavior through executable journeys, not doc-only claims.

Deliverables:
- New journey docs in:
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/`
- New or extended runner mappings in:
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`
- Candidate journey additions:
  - Portable Identity Profile XR onboarding projection.
  - Avatar + wearable pointer projection with consent gating.
  - Pairwise DID privacy behavior.
  - Revocation-aware XR policy decision flow.

Acceptance criteria:
- Journey docs exist with clear pass/fail logic.
- Runner outputs include new journey IDs.
- Journey report artifact generated with pass evidence.

Verification commands:
- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`

## A4) Workstream PIP-GN-04 — Registry expansion (non-normative, controlled)

Goal:
- Reduce integration friction by adding stable candidate key names for Portable Identity Profile XR while retaining forward compatibility.

Deliverables:
- Extend:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/REGISTRY.md`
- Add keys for:
  - avatar and wearables pointers,
  - translation/profile metadata shards,
  - XR privacy/consent key families.

Acceptance criteria:
- New names are namespaced and collision-safe.
- Registry changes are explicitly labeled non-normative.
- Integration lane and fixtures use same names consistently.

Verification:
- Consistency scan of key names across integrations/fixtures via `rg`.

## A5) Workstream PIP-GN-05 — Implementation guide addendum (adopter-ready)

Goal:
- Make this actionable for external teams now.

Deliverables:
- New guide addendum:
  - `/Users/grig/work/repo/universalmanifest/docs/guides/PORTABLE-IDENTITY-PROFILE-XR-IMPLEMENTATION-PATH.md`
- Site publication page mirror.

Scope:
- Consumer algorithm order.
- Issuer checklist.
- Consent enforcement examples.
- Revocation policy tiers (`baseline` vs `extended`).
- Risk handling for offline mode.

Acceptance criteria:
- Guide includes copy/paste validation flow.
- Cross-links to fixtures and journeys.
- No TypeScript lock-in language in normative explanation.

## A6) Workstream PIP-GN-06 — Decision and status synchronization

Goal:
- Keep governance and project-state coherence.

Deliverables:
- Add decision record entries in:
  - `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
- Update status docs:
  - `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
  - `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md` (if phase impact exists)

Acceptance criteria:
- All go-now scope changes are traceable to decisions.
- No status drift after merge.

## 6) Track B — Research-First execution (spikes with explicit promotion gates)

Each research workstream must produce:
- research brief,
- decision options,
- recommended option with tradeoffs,
- implementation impact diff,
- promotion recommendation (`do not integrate`, `non-normative lane`, `normative candidate`).

## B1) Workstream PIP-RS-01 — Encrypted private-fragment profile

Question:
- How should UM support private fragments in an interoperable way without violating local-first and language-neutral constraints?

Research tasks:
1. Evaluate payload packaging models:
   - encrypted shard payload,
   - encrypted pointer payload,
   - detached protected object with UM metadata references.
2. Evaluate key-distribution patterns:
   - wallet-mediated decryption grants,
   - recipient key wrapping,
   - hybrid envelope approach.
3. Evaluate canonicalization/signature interactions for signed manifests with encrypted parts.

Output artifact:
- `/Users/grig/work/repo/universalmanifest/docs/research/PORTABLE-IDENTITY-PROFILE-ENCRYPTED-FRAGMENTS-RESEARCH.md`

Promotion gate:
- Promote only if at least two implementation patterns are shown feasible across independent runtimes.

## B2) Workstream PIP-RS-02 — Selective disclosure / ZK proof profile

Question:
- Which proof-carrying approach is practical for UM in near term (SD-JWT VC, BBS+, other)?

Research tasks:
1. Compare verifier complexity, ecosystem maturity, and runtime footprint.
2. Define how UM references proofs (embedded vs pointer vs claim binding).
3. Define failure semantics and privacy guarantees.

Output artifact:
- `/Users/grig/work/repo/universalmanifest/docs/research/PORTABLE-IDENTITY-PROFILE-SELECTIVE-DISCLOSURE-RESEARCH.md`

Promotion gate:
- Promote only if the selected option has:
  - stable verifier libraries in at least two languages,
  - clear replay and binding mitigations,
  - conformance-fixture feasibility.

## B3) Workstream PIP-RS-03 — Wallet recovery profile

Question:
- What can be standardized in UM for recovery without overreaching into wallet internals?

Research tasks:
1. Identify minimal interoperable recovery metadata (policy pointer, method class, recovery state version).
2. Model security pitfalls (recovery takeover, social-engineering, stale recovery delegates).
3. Define whether recovery belongs as integration guidance only or candidate profile.

Output artifact:
- `/Users/grig/work/repo/universalmanifest/docs/research/PORTABLE-IDENTITY-PROFILE-RECOVERY-PROFILE-RESEARCH.md`

Promotion gate:
- Promote only if minimum metadata can be defined without mandating wallet vendor internals.

## B4) Workstream PIP-RS-04 — Wallet protocol binding profile (OIDC4VP/OIDC4VCI/DIDComm)

Question:
- How should UM payload exchange be profiled over wallet transports while keeping UM transport-neutral?

Research tasks:
1. Define protocol-agnostic exchange state model (request, authorize, present, verify, log).
2. Map OIDC4VP/OIDC4VCI and DIDComm bindings to same abstract state machine.
3. Define cross-protocol error taxonomy and evidence model.

Output artifact:
- `/Users/grig/work/repo/universalmanifest/docs/research/PORTABLE-IDENTITY-PROFILE-WALLET-PROTOCOL-BINDINGS-RESEARCH.md`

Promotion gate:
- Promote only if binding model demonstrates equivalent semantics across at least two transport families.

## B5) Workstream PIP-RS-05 — Avatar translation profile (XR interoperability deep dive)

Question:
- What is the minimum translation metadata needed for cross-engine avatar portability?

Research tasks:
1. Compare candidate format anchors (for example VRM/GLTF families and related metadata conventions).
2. Define translation shard schema candidates:
   - skeleton profile id,
   - morph target set declarations,
   - scale and locomotion hints,
   - fallback behavior.
3. Validate against at least two distinct XR runtime assumptions.

Output artifact:
- `/Users/grig/work/repo/universalmanifest/docs/research/PORTABLE-IDENTITY-PROFILE-AVATAR-TRANSLATION-RESEARCH.md`

Promotion gate:
- Promote only if schema can be represented as optional shard extensions without core-field bloat.

## 7) Integrated timeline and sequencing

This plan runs in three waves.

## Wave 0 (Week 1) — Program bootstrap

Deliverables:
- Confirm execution owners and priority order.
- Create work artifacts and decision board.
- Start A1/A2/A6 immediately.
- Start B1/B2 discovery in parallel.

Exit criteria:
- Integration lane draft exists.
- Initial fixtures committed.
- Research briefs for B1/B2 created with explicit questions and source lists.

## Wave 1 (Weeks 2-3) — Go-Now completion + first research decisions

Deliverables:
- Complete A1-A5.
- Run full verification and publish evidence artifacts.
- Complete B1/B2/B4 research outputs with recommendation verdicts.

Exit criteria:
- Go-Now deliverables merged and published.
- At least one research stream promoted to implementation-ready guidance or explicitly deferred.

## Wave 2 (Weeks 4-6) — Promotion cycle

Deliverables:
- Convert promoted research streams into:
  - integration guidance updates,
  - fixture/journey expansions,
  - optional normative proposal drafts (if justified).
- Complete B3/B5.

Exit criteria:
- Final decision pack produced for each research stream.
- Clear list of normative-candidate changes (if any) with migration impact.

## 8) Decision framework for promotion

Every research output must include a final decision block:

- `Decision`: integrate now / defer / reject.
- `Integration level`: guidance-only / conformance candidate / normative candidate.
- `Risk class`: low / medium / high.
- `Migration impact`: none / additive / breaking.
- `Evidence readiness`: fixtures possible now? journeys possible now? independent implementation evidence?

Promotion prerequisites:

1. Security posture documented.
2. At least one executable evidence path identified.
3. No contradiction with method-agnostic UM core.

## 9) Verification and evidence package requirements

For every merged implementation unit:

1. Build and test:
   - `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
   - `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test`
2. Journey evidence when applicable:
   - `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`
3. Drift governance checks:
   - strict K2B validator
   - production route checks
   - docs link-hygiene scan

Evidence artifacts must be stored under:
- `/Users/grig/work/repo/universalmanifest/docs/reports/`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/` (operational trace/evidence support)

## 10) Governance and documentation update policy

For each approved workstream completion:

1. Update decision log (`docs/DECISIONS.md`).
2. Update project status (`docs/STATE-OF-THE-PROJECT.md`) when scope/status changes.
3. Update work-order index if formal WOs are created.
4. Ensure spec-vs-implementation language boundary remains intact.

## 11) Risk register and mitigation

Risk: scope sprawl from over-normativizing early.
- Mitigation: guidance-first pattern, promotion gates, additive-first changes.

Risk: protocol lock-in from wallet-specific assumptions.
- Mitigation: abstract state model first, protocol bindings second.

Risk: privacy claims exceeding implemented guarantees.
- Mitigation: explicit verification posture labels and threat-model updates before claims.

Risk: fixture proliferation without conformance relevance.
- Mitigation: every fixture mapped to specific requirement and journey.

Risk: status drift between docs and runtime reality.
- Mitigation: keep Phase 9 drift checks mandatory after each wave.

## 12) Immediate action list (first 5 execution steps)

1. Create integration lane skeleton for `portable-identity-profile-xr`.
2. Create initial fixture pack (minimal, pointer, consent, pairwise variants).
3. Create research brief files for B1 and B2 and load existing source references.
4. Add decision record entry that establishes this two-track program.
5. Run baseline verification and record evidence artifact for Wave 0 start.

## 13) Definition of "program success"

The program succeeds when all are true:

1. Portable Identity Profile is implementable today through documented, tested Go-Now artifacts.
2. Each high-uncertainty gap has a completed research decision with clear promotion outcome.
3. At least one promoted research area is converted into executable fixture/journey evidence.
4. No core-spec neutrality regressions are introduced.
5. Status and governance artifacts remain synchronized and auditable.

## 14) Final recommendation

Start immediately with Track A while launching Track B spikes in parallel. Do not wait for perfect research before shipping integration guidance and executable examples. Use promotion gates to prevent speculative requirements from entering normative contract text prematurely.

## 15) New concept weaving protocol (for upcoming specifications)

Use this exact sequence whenever new concept specifications are introduced:

1. Capture the incoming spec as immutable input text and assign a stable ID (`PIP-SPEC-###`).
2. Break the spec into atomic requirements, each with:
   - requirement statement,
   - success criteria,
   - risk if omitted.
3. Classify each requirement:
   - `covered` (existing UM behavior already satisfies it),
   - `partial` (satisfiable with guidance/fixtures/journeys),
   - `gap` (requires new research/profile/spec work).
4. For every requirement, attach one concrete application example in UM terms:
   - manifest fields/shards/pointers,
   - consent/policy behavior,
   - verification expectations.
5. Route each requirement to a workstream:
   - `covered` -> evidence update only,
   - `partial` -> Track A (`PIP-GN-*`),
   - `gap` -> Track B (`PIP-RS-*`), then promotion gate.
6. Produce an integration decision entry with:
   - chosen path,
   - dependencies,
   - implementation owner,
   - merge gate/evidence requirements.
7. Do not merge requirement-level changes unless all three are complete:
   - fixture or runnable evidence path,
   - docs/spec boundary check,
   - governance/status sync (`DECISIONS.md`, `STATE-OF-THE-PROJECT.md` as applicable).

Operational artifact for this process:
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-05-portable-identity-profile-spec-integration-log.md`
