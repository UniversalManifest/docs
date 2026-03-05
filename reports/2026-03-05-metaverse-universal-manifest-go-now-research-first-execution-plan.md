# Metaverse Universal Manifest (MUM) — Comprehensive Go-Now / Research-First Execution Plan

Date: 2026-03-05  
Project: Universal Manifest (`/Users/grig/work/repo/universalmanifest`)  
Source baseline: `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-05-metaverse-universal-manifest-gap-and-implementation-report.md`  
Primary use-case input: `/Users/grig/Desktop/Use Case_ Metaverse Universal Manifest - v1.0.md`

## 1) Purpose and outcome

This plan converts the MUM v1.0 use-case requirements into an executable program that can start immediately while preserving rigorous promotion gates for high-risk areas.

Outcomes required:

- prove that core MUM scenarios are implementable now,
- close interoperability and security profile gaps in controlled waves,
- produce adopter-ready documentation and executable evidence,
- keep normative boundaries explicit while hardening integration quality.

## 1.1) Execution status snapshot (2026-03-05)

- `MUM-GN-01`: `IN_PROGRESS`
  - evidence: `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`
  - evidence: `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/metaverse.md`
- `MUM-GN-02`: `IN_PROGRESS`
  - evidence: `/Users/grig/work/repo/universalmanifest/spec/v0.1/REGISTRY.md`
  - evidence: `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-05-mum-registry-pack-consistency-scan.txt`
- `MUM-GN-03`: `DONE`
  - evidence: `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-05-metaverse-mum-fixture-pack-scenario-mapping-note.md`
  - evidence: `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-05-gn03-conformance-npm-test.txt`
- `MUM-GN-04`: `DONE`
  - evidence: `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-05-metaverse-mum-journey-suite-mapping-note.md`
  - evidence: `/Users/grig/work/repo/universalmanifest/docs/journeys/_artifacts/2026-03-05T15-18-11-406Z-journey-report.json`
- `MUM-GN-05` to `MUM-GN-06`: `NOT_STARTED`

## 2) Program constraints and operating rules

1. UM core remains method-agnostic and language-neutral.
2. Normative changes require `spec/` + conformance fixture impact + evidence.
3. Integration and profile guidance should land first when uncertainty is high.
4. Every promoted requirement must have at least one executable evidence path.
5. Security-sensitive claims cannot be treated as complete without threat-model alignment.
6. Status/governance docs must remain synchronized after each merged wave.

## 3) Current baseline: strong vs uncertain

## 3.1 Strong enough to execute now

- MUM lineage and metaverse integration lane documentation already exists.
- Pointer-first composition pattern supports avatar/inventory/social references.
- Consent-gated behavior and unknown-field tolerance are established.
- TTL freshness enforcement and v0.2 signature verification are available.
- Initial metaverse journey already proves cross-world optional overlay behavior.

Baseline references:

- `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`
- `/Users/grig/work/repo/universalmanifest/docs/journeys/journey-09-metaverse-crossworld-projection.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md`
- `/Users/grig/work/repo/universalmanifest/docs/security/THREAT-MODEL.md`

## 3.2 Requires research/planning before broad claims

- selective disclosure/compliance proof profile,
- anti-cloning and holder-binding semantics,
- platform attestation + secure enclave interoperability profile,
- synchronization conflict resolution conventions,
- formal social/reputation portability schema semantics.

## 4) Two-track structure

This program runs as two synchronized tracks:

- Track A: `Go-Now` (implementation-first, based on current UM capabilities).
- Track B: `Research-First` (spikes that must pass promotion gates before wider adoption claims).

All Track B outputs flow through a decision board with three possible outcomes:

- `promote to guidance`,
- `promote to normative candidate`,
- `defer with explicit rationale`.

## 5) Track A — Go-Now execution workstreams

## A1) Workstream MUM-GN-01 — MUM integration lane hardening (v2)

Goal:

- Expand metaverse integration documentation to fully cover all MUM v1.0 scenario families, especially preference/security/transaction flows.

Deliverables:

- update:
  - `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`
- mirror update:
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/metaverse.md`

Scope:

- scenario 1: onboarding + identity/asset projection,
- scenario 2: consent propagation,
- scenario 3: secure transaction/compliance references,
- scenario 4: social graph/reputation continuity,
- scenario 5: language/financial/logistics/voice/security/credential preferences.

Acceptance criteria:

- all five scenarios documented with boundary-safe UM mappings,
- explicit guidance on what is optional vs required core contract,
- at least one full end-to-end example per scenario.

## A2) Workstream MUM-GN-02 — MUM registry pack (non-normative)

Goal:

- Reduce integration drift by publishing a stable MUM key family recommendation set.

Deliverables:

- extend:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/REGISTRY.md`
- add MUM key families for:
  - profile/avatar/inventory/social/reputation,
  - language/translation preferences,
  - currency/payment preferences,
  - logistics address reference pointers,
  - voice and capture consent classes,
  - context-specific authentication policy hints,
  - loyalty/discount/membership credential pointers.

Acceptance criteria:

- namespaced, collision-safe key proposals,
- marked non-normative,
- used consistently by fixtures and integration docs.

## A3) Workstream MUM-GN-03 — MUM fixture pack expansion

Goal:

- Convert use-case scenarios into executable fixture evidence.

Deliverables:

- add fixtures under:
  - `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.2/`

Candidate fixture set:

- `metaverse-mum-onboarding-projection-manifest.jsonld`
- `metaverse-mum-consent-propagation-manifest.jsonld`
- `metaverse-mum-compliance-transaction-manifest.jsonld`
- `metaverse-mum-social-reputation-portability-manifest.jsonld`
- `metaverse-mum-preferences-bundle-manifest.jsonld`
- `metaverse-mum-cache-freshness-and-change-log-manifest.jsonld`

Acceptance criteria:

- valid fixtures pass validator;
- intentionally invalid cases fail for expected reasons;
- fixture semantics documented in journey and/or integration docs.

## A4) Workstream MUM-GN-04 — Journey suite expansion for MUM

Goal:

- Prove operational behavior, not just documentation claims.

Deliverables:

- new/expanded journey docs under:
  - `/Users/grig/work/repo/universalmanifest/docs/journeys/`
- runner updates in:
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`

Candidate journey additions:

- MUM onboarding projection end-to-end,
- cross-platform consent update propagation,
- secure transaction using compliance proof pointer,
- social graph portability under restricted consent,
- preference bundle projection and policy gating,
- stale-cache detection and refresh behavior.

Acceptance criteria:

- each journey has clear pass/fail criteria,
- at least one evidence artifact generated per new journey group,
- journey IDs are included in automated journey report outputs.

## A5) Workstream MUM-GN-05 — Synchronization profile (guidance-first)

Goal:

- Provide a practical, non-normative sync model for versioning/staleness/change-log behavior.

Deliverables:

- new guidance document:
  - `/Users/grig/work/repo/universalmanifest/docs/guides/MUM-SYNCHRONIZATION-PROFILE.md`
- site mirror publication under guides.

Scope:

- authoritative source pointer conventions,
- cache staleness checks,
- update sequencing and retry guidance,
- append-only change-log pointer pattern,
- conflict handling guidance (best-effort deterministic behavior).

Acceptance criteria:

- implementable by third parties without UM core changes,
- cross-linked from metaverse integration lane and quick references.

## A6) Workstream MUM-GN-06 — Governance and publication synchronization

Goal:

- Keep governance artifacts consistent with new MUM execution scope.

Deliverables:

- update:
  - `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
  - `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
  - `/Users/grig/work/repo/universalmanifest/docs/CRITICAL-PATH.md` (if milestone impact exists)

Acceptance criteria:

- all MUM workstreams are decision-traceable,
- no status drift between docs and merged implementation state.

## 6) Track B — Research-First execution workstreams

Each research stream must produce:

- research brief,
- evaluated options + tradeoffs,
- recommended option,
- implementation impact,
- promotion recommendation (`guidance`, `normative candidate`, `defer`).

## B1) Workstream MUM-RS-01 — Selective disclosure and compliance proof profile

Question:

- Which proof profile can satisfy metaverse compliance checks with minimal disclosure and realistic verifier support?

Research tasks:

1. Compare SD-JWT VC, BBS+, and adjacent practical options.
2. Define UM claim-to-proof binding model (embedded vs pointer + binding metadata).
3. Define replay and proof substitution mitigation rules.

Output artifact:

- `/Users/grig/work/repo/universalmanifest/docs/research/MUM-SELECTIVE-DISCLOSURE-AND-COMPLIANCE-PROFILE-RESEARCH.md`

Promotion gate:

- at least two independent runtime verifier paths must be feasible.

## B2) Workstream MUM-RS-02 — Anti-cloning and holder-binding profile

Question:

- How should UM-based flows reduce manifest theft/misuse without breaking portability?

Research tasks:

1. Evaluate holder-binding patterns and practical enforcement models.
2. Define risk-based policy levels for clone resistance.
3. Define fallback behavior for low-capability platforms.

Output artifact:

- `/Users/grig/work/repo/universalmanifest/docs/research/MUM-ANTI-CLONING-HOLDER-BINDING-RESEARCH.md`

Promotion gate:

- option must remain optional/additive and not break UM baseline interoperability.

## B3) Workstream MUM-RS-03 — Platform attestation and secure enclave profile

Question:

- What minimum attestation semantics are needed for high-trust metaverse transactions and credential requests?

Research tasks:

1. Define abstract attestation evidence model (transport-neutral).
2. Define requester trust levels and policy outcomes.
3. Define optional secure enclave metadata expectations.

Output artifact:

- `/Users/grig/work/repo/universalmanifest/docs/research/MUM-ATTESTATION-AND-SECURE-ENCLAVE-PROFILE-RESEARCH.md`

Promotion gate:

- equivalent semantics must map to at least two platform/runtime families.

## B4) Workstream MUM-RS-04 — Synchronization conflict-resolution protocol

Question:

- How should concurrent updates and stale merges be handled across independent platforms?

Research tasks:

1. Evaluate version vectors, monotonic timestamps, and change-log merge approaches.
2. Define deterministic conflict-resolution guidance for profile classes.
3. Define auditability requirements for merge outcomes.

Output artifact:

- `/Users/grig/work/repo/universalmanifest/docs/research/MUM-SYNC-CONFLICT-RESOLUTION-RESEARCH.md`

Promotion gate:

- must show deterministic behavior across at least two implementation styles.

## B5) Workstream MUM-RS-05 — Social/reputation portability profile

Question:

- What minimum schema and provenance metadata is needed for portable social/reputation continuity?

Research tasks:

1. Define social graph pointer and relationship model conventions.
2. Define provenance and attestation signals for reputation claims.
3. Define privacy-safe disclosure patterns.

Output artifact:

- `/Users/grig/work/repo/universalmanifest/docs/research/MUM-SOCIAL-REPUTATION-PORTABILITY-RESEARCH.md`

Promotion gate:

- schema must stay optional and compatible with unknown-field tolerance.

## 7) Timeline and sequencing

## Wave 0 (Week 1) — Bootstrap and immediate execution

Deliverables:

- start A1/A2/A3 and A6,
- create B1 and B2 research briefs,
- publish this plan and MUM gap baseline.

Exit criteria:

- metaverse lane hardening draft exists,
- first fixture set exists,
- initial research briefs have source inventory and decision questions.

## Wave 1 (Weeks 2-3) — Go-Now completion and first research decisions

Deliverables:

- complete A1-A5,
- complete B1 and B4 recommendation outputs,
- generate journey evidence artifacts for new MUM scenario coverage.

Exit criteria:

- go-now deliverables published,
- at least one research output promoted to implementable guidance.

## Wave 2 (Weeks 4-6) — Promotion cycle

Deliverables:

- implement promoted B-stream outputs into guidance/fixtures/journeys,
- complete B2/B3/B5,
- prepare normative candidate pack where justified.

Exit criteria:

- each research stream has final decision status,
- clear list of additive vs normative-candidate changes.

## 8) Promotion decision framework

Every research output must end with:

- `Decision`: integrate now / defer / reject,
- `Integration level`: guidance-only / conformance-candidate / normative-candidate,
- `Risk class`: low / medium / high,
- `Migration impact`: none / additive / breaking,
- `Evidence readiness`: fixture-ready? journey-ready? independent implementation feasible?

Promotion prerequisites:

1. security posture documented,
2. executable evidence path identified,
3. no contradiction with UM core neutrality.

## 9) Verification and evidence requirements

For each merged implementation unit:

1. Build and test:
   - `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
   - `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test`
2. Journey evidence when applicable:
   - `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`
3. Drift and publication checks:
   - docs link hygiene,
   - route integrity for updated site pages,
   - decision/status synchronization checks.

Evidence artifacts must be stored under:

- `/Users/grig/work/repo/universalmanifest/docs/reports/`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/` (operational support artifacts)

## 10) Governance update policy

For each completed workstream:

1. update `docs/DECISIONS.md`,
2. update `docs/STATE-OF-THE-PROJECT.md` when status/scope changes,
3. keep integration docs and site mirrors synchronized,
4. maintain explicit normative vs non-normative boundaries.

## 11) Risk register

Risk: metaverse-specific assumptions leak into core UM required fields.  
Mitigation: keep all MUM semantics in optional shards/pointers/consents.

Risk: privacy/security claims exceed implemented controls.  
Mitigation: no claims without fixture/journey evidence and threat-model alignment.

Risk: synchronization behavior fragments across implementers.  
Mitigation: publish sync guidance early and test through journey fixtures.

Risk: too many key names without governance discipline.  
Mitigation: centralized registry pack with naming conventions and review gates.

Risk: standards-positioning ambiguity.  
Mitigation: produce explicit crosswalk report as part of Wave 1/2 outputs.

## 12) Immediate action list (first five steps)

1. Harden metaverse integration lane to include all five MUM scenarios.
2. Publish initial MUM registry key pack additions (non-normative).
3. Add first MUM fixture bundle mapped to scenario coverage.
4. Create B1/B2 research briefs and source map.
5. Log program decision and synchronize project status docs.

## 13) Definition of program success

Program succeeds when all are true:

1. MUM scenarios are implementable through published, test-backed UM artifacts.
2. Each high-uncertainty gap has a documented research decision.
3. Promoted research outcomes are converted into executable fixtures/journeys.
4. Core UM neutrality is preserved.
5. Governance and status artifacts remain synchronized.

## 14) Final recommendation

Start Track A immediately and run Track B in parallel with strict promotion gates. This achieves immediate practical interoperability while preventing premature standardization of unresolved security/privacy design choices.

## 15) New concept weaving protocol (for incoming metaverse specifications)

Use this exact sequence for each new concept bundle:

1. Capture the incoming concept text and assign a stable ID (`MUM-SPEC-###`).
2. Decompose into atomic requirements with success criteria and omission risk.
3. Classify each requirement: `covered`, `partial`, or `gap`.
4. Attach one concrete UM application example per requirement.
5. Route each item:
   - `covered` -> evidence update,
   - `partial` -> Track A (`MUM-GN-*`),
   - `gap` -> Track B (`MUM-RS-*`) with promotion gate.
6. Record decision metadata:
   - dependencies,
   - owner,
   - evidence gate,
   - merge readiness.
7. Do not merge requirement-level changes without:
   - executable evidence path,
   - docs/spec boundary check,
   - governance/status synchronization.

Operational artifact for this protocol:

- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-05-metaverse-universal-manifest-spec-integration-log.md`
