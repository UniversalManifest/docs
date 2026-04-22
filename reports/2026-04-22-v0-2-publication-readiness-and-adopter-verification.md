# 2026-04-22 v0.2 Publication Readiness and Adopter Verification

## Purpose

This report closes `WO-0189` by turning “v0.2 remains draft” into an explicit publication-readiness checklist with evidence-backed blockers.

The goal is not to declare v0.2 final. The goal is to define exactly what must be true before a stronger publication claim would be honest.

## Publication-Readiness Criteria

| Criterion | Current status | Evidence |
| --- | --- | --- |
| Baseline integrity profile is explicit and stable | `satisfied` | `spec/v0.2/SIGNATURE-PROFILE.md`; `docs/reports/2026-04-22-additional-integrity-profile-decision-package.md` |
| Revocation/status boundary is explicit | `satisfied` | `docs/reports/2026-04-22-revocation-cursor-and-status-contract.md`; `spec/v0.2/CONFORMANCE.md` |
| v0.2 conformance package includes explicit TTL/security invalid coverage | `satisfied` | `docs/reports/2026-04-22-conformance-suite-ttl-replay-and-security-expansion.md`; `conformance/v0.2/expected.json` |
| Reference validation of the v0.2 fixture corpus is clean enough for publication claims | `not satisfied` | `npm --prefix /Users/grig/work/repo/universalmanifest/packages/universal-manifest run validate:examples` still reports v0.2 failures in valid signed fixtures and one semantic invalid case |
| Broader adopter verification exists beyond the reference implementation | `not satisfied` | no independent adopter conformance report or external implementation evidence is recorded in the current repo |
| Publication claim and evidence posture are explicit | `partially satisfied` | v0.2 is clearly marked draft in `spec/v0.2/README.md`, but no stronger readiness declaration or explicit “ready/not-ready” package existed before this report |

## Current Evidence That Does Exist

The repo already has meaningful v0.2 readiness inputs:

- explicit JCS + Ed25519 signature profile
- explicit defer decision for additional integrity profiles
- explicit optional-boundary decision for revocation/status signaling
- expanded TTL/security invalid-fixture coverage
- implementation-neutral conformance packaging
- published namespace artifacts under `/ns/universal-manifest/v0.2/...`

These are enough to describe the readiness posture precisely, but not enough to claim broader publication readiness yet.

## Evidence-Based Blockers

### 1. The current v0.2 reference-validation picture is not clean

Fresh validation evidence from this execution wave:

- `npm --prefix /Users/grig/work/repo/universalmanifest/packages/universal-manifest run validate:examples`

That run still reports v0.2 failures in fixtures that should be strong publication signals, including:

- `examples/v0.2/minimal-signed-manifest.jsonld`
- `examples/v0.2/manifest-with-revocation-metadata.jsonld`
- multiple identity-binding v0.2 fixtures

It also still reports a semantic invalid-lane problem:

- `examples/v0.2/invalid/forged-issuer-claim.jsonld`
  - `Unknown __validate mode: semantic`

Until the v0.2 reference-validation story is clean enough to distinguish expected draft limitations from actual fixture or validator defects, publication readiness remains blocked.

### 2. Independent adopter evidence is still missing

The repo has reference-implementation and conformance packaging material, but it does not yet contain a recorded independent adopter result that shows another implementation successfully consuming the v0.2 contract.

That does not block draft publication, but it does block a stronger claim that v0.2 is broadly adopter-ready.

### 3. Publication posture needs a stronger evidence package than “draft artifacts exist”

Before this report, the repo correctly said that v0.2 remains draft, but it did not package the readiness criteria and blocker list into one explicit artifact.

This report fixes that documentation gap, but the blocker list itself remains real.

## Readiness Conclusion

The honest current claim is:

- v0.2 has meaningful draft artifacts
- the baseline integrity/revocation/conformance decisions are now materially clearer
- v0.2 is **not yet ready for a stronger publication claim** beyond draft availability

## What Must Be True Before A Stronger v0.2 Claim

At minimum:

1. The reference-validation story for the v0.2 fixture set must be clean enough to trust as publication evidence.
2. At least one independent adopter or non-reference implementation should produce a recorded conformance result.
3. The publication claim should be restated from “draft artifacts exist” to an explicit readiness posture once the above evidence exists.

## Outcome

`WO-0189` is now complete.

The repo now has:

- explicit v0.2 publication-readiness criteria
- explicit adopter-verification needs
- an evidence-based blocker list instead of a vague “still draft” note
