# J24 — Data Firewall UX Decision Flow and Audit Minimization

## Goal

Prove that a firewall-style UM consumer can evaluate default-deny consent rules, honor higher-priority audience/context/scope-specific overrides, surface the matched rule metadata in the decision panel, and keep audit retention keyed to identifiers rather than full payload storage.

## Why this matters

The data-firewall-ux lane is only credible if its rules are more than descriptive prose. This journey turns the lane's decision contract into executable evidence: specific-over-broad precedence, deny-by-default posture, per-rule expiry metadata, explicit reason text, and privacy-preserving audit retention all have to line up in real fixtures.

## Inputs

- Baseline rule-set fixture:
  - `examples/integrations/data-firewall-ux/baseline-default-deny-rule-set-manifest.jsonld`
- Audience-scoped override fixture:
  - `examples/integrations/data-firewall-ux/near-real-audience-scoped-rule-overrides-manifest.jsonld`

## Expected behavior

1. Both fixtures preserve a valid v0.1 UM envelope.
2. Baseline policy is explicit default-deny with deterministic precedence and deny-wins tie-breaking.
3. Baseline rule-set entries align with the three default-deny consent records and their `ruleId` values.
4. Audience-scoped profile sharing is only exposed through the high-priority clinic rule for `emergency` / `clinical` contexts.
5. Lower-priority fallback deny rules remain present so the decision panel can explain "no specific allow rule matched."
6. Telemetry sharing stays restricted to the named analytics service, with per-rule `expiresAt` metadata that remains independent of manifest TTL.
7. Location sharing remains denied because no allow rule exists for it.
8. Decision-panel and audit-view descriptors preserve matched-rule, reason-text, and ID-keyed audit-retention contracts.

## Executable mapping

- Journey runner row: `J24`
- Implementation: `packages/universal-manifest/scripts/run-journeys.mjs`

## Evidence

Successful execution appears in the generated journey report under `docs/journeys/_artifacts/`.
