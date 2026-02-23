# WO-0037 — Integrity profile, revocation, and adversarial conformance hardening

**Status:** NOT_STARTED
**Created:** 2026-02-22
**Priority:** MEDIUM
**Source:** `/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md`

## Objective

Define and implement next-layer contract hardening for integrity profile evolution, revocation semantics direction, and adversarial conformance coverage.

## Why this work matters

The current state explicitly calls out three open hardening areas:

- additional integrity profile direction beyond the v0.2 baseline,
- revocation cursor/events direction,
- deeper adversarial/misuse conformance coverage.

This WO converts those items into a concrete hardening track.

## Scope

In scope:

- Document forward direction for additional integrity-profile support without destabilizing current baseline.
- Define revocation cursor/event model direction and boundary (normative vs non-normative).
- Add adversarial fixture cases and corresponding validation expectations.
- Record resulting governance decisions in canonical decision docs.

Out of scope:

- New deployment architecture work.
- Broad onboarding/readability edits unrelated to integrity/revocation/conformance hardening.

## Required deliverables

1. Decision updates in:
   - `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
2. Contract/conformance updates in:
   - `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`
   - `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md`
3. Adversarial fixtures in:
   - `/Users/grig/work/repo/universalmanifest/examples/v0.2/`
4. Hardening evidence report in:
   - `/Users/grig/work/repo/universalmanifest/docs/reports/`

## Acceptance criteria

- [ ] Integrity-profile extension direction is explicitly documented and does not contradict existing v0.2 baseline.
- [ ] Revocation cursor/event direction is documented with scope boundary.
- [ ] Adversarial fixture set is expanded and validated in test workflow.
- [ ] State and decision docs remain mutually consistent after updates.

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test`
- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
- `rg -n 'integrity|revocation|cursor|adversarial|misuse' /Users/grig/work/repo/universalmanifest/docs/DECISIONS.md /Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md /Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`

