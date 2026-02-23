# Universal Manifest Foundational Reference Crosswalk

Date: 2026-02-13  
Work Order: `WO-reference implementation-universal-manifest-spec-scope-and-done-definition`

This crosswalk maps foundational references to the current spec scope and completion signals.

## A) reference implementation Platform Foundational References

- `/Users/grig/work/repo/reference-platform/.dev/ai/handoffs/2026-02-11-20-45-58Z-universal-manifest-handoff.md`
  - Confirms extraction intent: separate spec repo + concrete spec implementation, not further research.
  - Drives current scope split: “spec repo” vs “reference implementation integration.”

- `/Users/grig/work/repo/reference-platform/.dev/ai/handoffs/2026-02-11-21-52-41Z-handoff-reference-platform-universal-manifest-stubs.md`
  - Captures early transport and storage assumptions for reference implementation stubs.
  - Aligns with current reference implementation endpoint contracts and player caching behavior.

- `/Users/grig/work/repo/reference-platform/docs/decisions/2026-02-11-universal-manifest-integration-decisions.md`
  - Locks critical architectural decisions:
    - separate repo
    - `urn:uuid` issuer IDs
    - cache full manifest while in use, log by ID
    - minimal transport stubs
  - Remains fully aligned with current implementation.

- `/Users/grig/work/repo/reference-platform/docs/decisions/2026-02-12-universal-manifest-queue-decisions.md`
  - Adds bounded retention, optional restore, feature-flagged signature verification, and pinned schema validation.
  - Establishes “adaptability first, integrity upgrade path” behavior.

- `/Users/grig/work/repo/reference-platform/UNIVERSAL-MANIFEST.md`
  - Documents runtime behavior and user-facing implementation guidance in reference implementation.
  - Provides current endpoint and feature-flag contract baseline.

- `/Users/grig/work/repo/reference-platform/.dev/ai/reports/2026-02-12-universal-manifest-status-report.md`
  - Confirms status as “minimal integration + separate spec repo,” not full production standard.
  - Supports current completion estimate and gap list.

## B) Universal Manifest Repo Foundational References

- `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`
  - Defines umbrella vision and multi-surface adoption model.
  - Prevents scope drift toward single-implementation-only implementation.

- `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`
  - Declares explicit current-state and not-yet-finalized areas.
  - Primary source for spec completion maturity.

- `/Users/grig/work/repo/universalmanifest/docs/DEPTH-AND-SCOPE.md`
  - Separates normative spec from examples, integrations, tooling, and research.
  - Used as boundary enforcement for “done done.”

- `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
  - Canonical record of ID strategy and domain split (`universalmanifest.net` + `myum.net`).
  - Aligns with publish/deployment work orders.

- `/Users/grig/work/repo/universalmanifest/spec/v0.1/README.md`
  - Normative v0.1 field and behavior specification.
  - Core input to D1 (contract completeness).

- `/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md`
  - Consumer/issuer conformance behaviors and fixture policy.
  - Core input to D2 (conformance readiness).

- `/Users/grig/work/repo/universalmanifest/spec/v0.1/schema.json`
  - Structural contract used by reference implementation smoke validation.
  - Validates spec-to-implementation alignment.

- `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md`
  - Direction for integrity profile evolution.
  - Evidence that integrity profile is drafted, not finalized.

## C) Indexed External References on Device

- `/Users/grig/.agents/knowledge-sources/INDEX.md`
  - Provides searchable index of local knowledge reservoirs.
  - Confirms where Universal Manifest source archives are indexed and discoverable.

- `/Users/grig/.agents/knowledge-sources/project-indexes/2026-02-08_lan-platform_master-index.md`
  - Includes reference implementation knowledge topology and external reference pointers.
  - Supports audit completeness checks for local sources.

- `/Users/grig/Downloads/INBOX-markdown/universal-manifest/`
  - Contains deep background research and candidate protocol analyses.
  - Treated as design inputs; selected documents are already reflected in synthesis references.

## D) Crosswalk Findings

- Scope boundary is clear and stable: spec and docs are in separate repo; reference implementation consumes by integration contracts.
- “Done done” maturity is strongest in baseline contract + integration stubs.
- Largest remaining closure area is integrity hardening + conformance depth + production publishing guarantees.
- No foundational source reviewed requires a change to `urn:uuid` issuer ID strategy for current phase.
