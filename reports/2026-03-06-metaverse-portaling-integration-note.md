# Metaverse Portaling Integration Note

Date: 2026-03-06  
Project: Universal Manifest (`/Users/grig/work/repo/universalmanifest`)  
Work order: `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0141-metaverse-portaling-integration-and-guidance-refresh.md`

## 1) Direct answer

In the Universal Manifest project, **portaling** means this:

- a subject leaves one platform and enters a different platform,
- the Universal Manifest acts as the portable envelope that travels with the subject,
- the destination platform resolves the subject's allowed pointers and overlays,
- the destination platform enforces the subject's consent and policy state immediately,
- unsupported content degrades gracefully instead of invalidating the whole transfer.

This is already compatible with UM's architecture.
It does not require a new core schema.
It requires explicit guidance.

## 2) What UM already provides for portaling

Portaling is assembled from existing UM primitives and runtime rules:

- **pointer-first content transfer**
  - avatar, inventory, profile, social graph, reputation, and compliance references stay external and are resolved through pointers.
- **subject and trust envelope**
  - the destination platform receives one portable manifest envelope instead of guessing identity from platform-local state.
- **consent and policy continuity**
  - disclosure, voice, recording, social graph, and compliance behaviors are controlled by carried policy state.
- **freshness and trust checks**
  - destination platforms still validate TTL and any required trust posture before projection.
- **unknown-field tolerance**
  - unsupported destination platforms can ignore what they do not understand without breaking the manifest.

## 3) What portaling is not

Portaling does not mean:

- every destination platform must support every asset or behavior,
- UM inlines all avatar or inventory data into the manifest,
- one wallet, runtime, or metaverse engine is mandatory,
- the destination platform can ignore freshness or consent because the user “arrived through a portal”.

UM's correct promise is portability with bounded interpretation, not perfect graphical equivalence.

## 4) Portaling flow in UM terms

Recommended flow:

1. The subject leaves an origin platform with a valid manifest or manifest reference.
2. The destination platform resolves or receives the manifest.
3. The destination validates the UM envelope and freshness requirements.
4. The destination reads the metaverse portability overlays it understands.
5. The destination resolves supported pointers for avatar, inventory, profile, and related content.
6. The destination applies carried consent and policy state before activating features.
7. Unsupported assets or behaviors fall back gracefully while preserving the rest of the transfer.

## 5) Portaling-specific guidance adopted in this pass

The repo now makes five things explicit.

### A. Portaling is a first-class metaverse integration concept

The metaverse lane now says plainly that UM supports movement between different worlds or platforms, not just static “projection”.

### B. Existing metaverse primitives are sufficient

No new required UM members were introduced in this pass.

The lane continues to rely on:

- `metaverse.profile`
- `metaverse.avatar`
- `metaverse.inventory`
- `metaverse.socialGraph`
- `metaverse.reputation`
- `metaverse.complianceProof`
- `crossWorldProfile` shard content
- metaverse consent keys

### C. Graceful degradation is part of the contract story

If a destination platform cannot use a specific avatar format, item type, or social graph feature, that platform should still accept the UM envelope and project the parts it understands.

### D. Portaling does not bypass policy

Arrival in a new world does not grant implicit permission.
Destination platforms still have to honor:

- `metaverse.profilePublic`
- `metaverse.socialGraphShare`
- `metaverse.voiceCapture`
- `metaverse.recording.faceVisible`
- `metaverse.transaction.complianceShare`

### E. Portaling remains non-normative guidance

This is an integration-lane clarification, not a new normative requirement for all UM consumers.

## 6) Repo surfaces updated in this pass

Blueprint and relationship surfaces:

- `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`
- `/Users/grig/work/repo/universalmanifest/docs/MSF-RELATIONSHIP.md`

Integration guidance surfaces:

- `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/metaverse.md`

Proof and teaching surfaces:

- `/Users/grig/work/repo/universalmanifest/docs/journeys/journey-09-metaverse-crossworld-projection.md`
- `/Users/grig/work/repo/universalmanifest/docs/journeys/README.md`
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/integration-lanes/il-03-metaverse-crossworld.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/scripts/sandbox/scenarios/integration-lanes/il-03-metaverse-crossworld-v2.ts`
- `/Users/grig/work/repo/universalmanifest/docs/explainers/metaverse-portaling.md`

## 7) Executive status after integration

The repo already had the mechanics for portaling.
This pass makes the concept explicit and reviewer-friendly.

The practical repo position is now:

- UM supports cross-platform portaling as a metaverse integration pattern,
- that pattern is pointer-first and consent-first,
- the pattern preserves graceful degradation across incompatible destinations,
- no new normative spec layer was required to say this clearly.
