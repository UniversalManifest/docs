# WO-0224: Conformance-Suite + Badge + Adopter-Onboarding Cross-Link Wiring

**Status:** NOT_STARTED
**Priority:** P1 (publication completeness; not a hard dependency for smoke)
**Depends on:** WO-0221
**Unblocks:** none
**Derived from:** 2026-04-26 v0.2 publication push plan, item 6; WO-0053 (standalone conformance), WO-0055 (adopter onboarding)

## Objective

Make the standalone conformance suite (WO-0053) and the conformance badges discoverable from the published spec. Cross-link adopter onboarding (WO-0055) so a reader who lands on `/spec/v0.2/` can reach badge mechanism, adopter checklist, and reference-implementation repo within two clicks.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/conformance/README.md`
- `/Users/grig/work/repo/universalmanifest/conformance/badges/v0.2-baseline.svg`
- `/Users/grig/work/repo/universalmanifest/conformance/badges/v0.2-extended.svg`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/conformance/standalone-suite.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/conformance/v0.2.md`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/implementations/` (does it exist?)
- `/Users/grig/work/repo/universalmanifest/docs/guides/IMPLEMENTATION-GUIDE.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0053-standalone-conformance-test-suite.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0055-adopter-onboarding-document-package.md`

## Work to perform

1. **Cite the conformance suite from the spec body.** In the spec's Conformance section (find the appropriate `<h2>` in W3C-STYLE-SPEC.html), add an explicit pointer: "Implementations claiming v0.2 conformance MUST pass the standalone conformance suite at /conformance/standalone-suite/."
2. **Surface the badges.** Either (a) add inline `<img>` references in `site/src/content/docs/conformance/v0.2.md`, or (b) publish the badges as static assets with documented URLs. Preferred: do both — embed in v0.2.md AND ensure `https://universalmanifest.net/conformance/badges/v0.2-baseline.svg` resolves.
3. **Wire adopter onboarding.** Link `docs/guides/IMPLEMENTATION-GUIDE.md` (or its content-collection mirror) from the spec page Status-of-This-Document section under a "For implementers" pointer.
4. **Cross-link the reference implementation.** The external repo `https://github.com/grigb/um-typescript` should be linked from the spec page and from `site/src/content/docs/implementations/`.
5. **Verify** `https://universalmanifest.net/conformance/v0.2/` (the conformance landing) is reachable from the spec body.

## Files to modify

- `docs/W3C-STYLE-SPEC.html` (add Conformance + adopter pointers in the Status block and Conformance section)
- `site/src/content/docs/conformance/v0.2.md` (embed badge images, add a "Claim a badge" subsection that explains the mechanism)
- `site/src/content/docs/implementations/index.md` (or similar — link reference implementation)
- `site/src/data/home-cluster.ts` (only if the home cluster has an adopter slot that should include the conformance link)

## Constraints

- **Do not modify spec normative requirements.** Add pointers only.
- **Badges are illustrative, not certifying.** The README MUST NOT imply Universal Manifest issues centralized certification — language should match `WO-0053`'s posture.
- **No new top-nav entries.** All links live within existing surfaces.

## Acceptance criteria

- The published spec page links to `/conformance/standalone-suite/` and `/conformance/v0.2/` from the Status-of-This-Document section.
- Both v0.2 badges are reachable as static assets from `https://universalmanifest.net/conformance/badges/`.
- `site/src/content/docs/conformance/v0.2.md` shows the badges and explains the claim mechanism.
- The reference implementation repo URL appears in the spec page or its directly-linked implementations index.
- `npm run build` passes.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0224-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0224-BLOCKED.md`
