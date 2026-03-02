# WO-0079 -- Remaining Scenario Migration to V2 Format (TV, IL, EC, AD)

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-02-28
**Priority:** P5 (Phase 5 -- Polish + Migration)
**Source:** Sandbox V2 UI Redesign Proposal, Phase 5
**Tags:** [site], [sandbox], [scenarios]
**Blocks:** None
**Dependencies:** WO-0077 (scenario detail page rewrite), WO-0078 (GS migration)
**Estimated effort:** 2 days
**Proposal:** `.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md`

## Objective

Migrate all remaining sandbox scenarios from V1 to V2 format across four categories: Trust & Verification (TV), Integration Lanes (IL), Edge Cases (EC), and Advanced (AD).

## Why this work matters

After the Getting Started scenarios were migrated (WO-0078), the remaining 21 scenarios still ran in V1 backward-compatible mode (single entity, no subject, step-list fallback). Migrating them to V2 ensures the full sandbox experience is consistent across all scenarios.

## Scope

### Files created (21 V2 scenario files)

**Trust & Verification (5 scenarios):**
- `site/src/scripts/sandbox/scenarios/trust-verification/tv-01-signed-manifest-v2.ts`
- `site/src/scripts/sandbox/scenarios/trust-verification/tv-02-tamper-detection-v2.ts`
- `site/src/scripts/sandbox/scenarios/trust-verification/tv-03-expired-manifest-v2.ts`
- `site/src/scripts/sandbox/scenarios/trust-verification/tv-04-missing-fields-v2.ts`
- `site/src/scripts/sandbox/scenarios/trust-verification/tv-05-invalid-algorithm-v2.ts`

**Integration Lanes (8 scenarios):**
- `site/src/scripts/sandbox/scenarios/integration-lanes/il-01-social-profile-v2.ts`
- `site/src/scripts/sandbox/scenarios/integration-lanes/il-02-smart-glasses-v2.ts`
- `site/src/scripts/sandbox/scenarios/integration-lanes/il-03-metaverse-v2.ts`
- `site/src/scripts/sandbox/scenarios/integration-lanes/il-04-rp1-spatial-v2.ts`
- `site/src/scripts/sandbox/scenarios/integration-lanes/il-05-omatrust-v2.ts`
- `site/src/scripts/sandbox/scenarios/integration-lanes/il-06-chia-vc-v2.ts`
- `site/src/scripts/sandbox/scenarios/integration-lanes/il-07-personhood-v2.ts`
- `site/src/scripts/sandbox/scenarios/integration-lanes/il-08-venue-edge-v2.ts`

**Edge Cases (4 scenarios):**
- `site/src/scripts/sandbox/scenarios/edge-cases/ec-01-temporal-misuse-v2.ts`
- `site/src/scripts/sandbox/scenarios/edge-cases/ec-02-missing-signature-v2.ts`
- `site/src/scripts/sandbox/scenarios/edge-cases/ec-03-clock-skew-v2.ts`
- `site/src/scripts/sandbox/scenarios/edge-cases/ec-04-shard-type-v2.ts`

**Advanced (4 scenarios):**
- `site/src/scripts/sandbox/scenarios/advanced/ad-01-cross-system-v2.ts`
- `site/src/scripts/sandbox/scenarios/advanced/ad-02-pointers-v2.ts`
- `site/src/scripts/sandbox/scenarios/advanced/ad-03-revocation-v2.ts`
- `site/src/scripts/sandbox/scenarios/advanced/ad-04-full-v02-v2.ts`

### Scenario registry

- `site/src/scripts/sandbox/scenarios/index.ts` -- Updated with V2 registration support for all migrated scenarios

## Acceptance criteria

- [x] All 21 remaining scenarios have V2 versions with two-entity definitions.
- [x] Each V2 scenario includes entity A/B metadata, subject, session states, and protocol interactions.
- [x] All scenarios load and run in the V2 layout without JavaScript errors.
- [x] Scenario registry includes all V2 entries.
