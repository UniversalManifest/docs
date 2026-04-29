# WO-0242: Integration Lane Dedicated Journey Coverage

**Status:** COMPLETED 2026-04-29
**Priority:** MEDIUM (P2)
**Depends on:** WO-0219
**Unblocks:** Full published status for lanes currently marked In Progress because dedicated journey coverage is missing
**Derived from:** WO-0219 residual risk report

## Objective

Add dedicated executable journey coverage for integration lanes that currently have lane docs and fixtures but no dedicated lane journey:

- `data-firewall-ux`
- `smart-home`
- `healthcare-patient-consent`
- `education-credentials`

The goal is not to expand the normative spec. The goal is to make each lane's proof story explicit and executable so the integration catalog can distinguish published lanes from incomplete proof lanes.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-28-23-54-48Z-T4-wo-0219-result.md`
- `/Users/grig/work/repo/universalmanifest/integrations/smart-home.md`
- `/Users/grig/work/repo/universalmanifest/integrations/healthcare-patient-consent.md`
- `/Users/grig/work/repo/universalmanifest/integrations/education-credentials.md`
- `/Users/grig/work/repo/universalmanifest/integrations/data-firewall-ux.md`
- `/Users/grig/work/repo/universalmanifest/examples/integrations/data-firewall-ux/`
- `/Users/grig/work/repo/universalmanifest/examples/integrations/smart-home/`
- `/Users/grig/work/repo/universalmanifest/examples/integrations/healthcare-patient-consent/`
- `/Users/grig/work/repo/universalmanifest/examples/integrations/education-credentials/`
- `/Users/grig/work/repo/universalmanifest/docs/journeys/README.md`
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/run-journeys.mjs`

## Work to perform

1. Add four dedicated journey docs, one per lane, following the existing `docs/journeys/J##-*.md` pattern.
2. Extend the executable journey runner so each new journey is exercised by `npm run journeys` from `packages/universal-manifest`.
3. Use existing WO-0216 fixtures for each lane; do not invent new manifest fields unless the lane docs already define them.
4. Update each lane's `Implementation notes` block to point at its dedicated journey.
5. Update the integration catalog status for the three lanes if the route, fixture, and journey coverage are now complete.

## Files to modify

- `docs/journeys/`
- `docs/journeys/README.md`
- `packages/universal-manifest/scripts/run-journeys.mjs`
- `integrations/data-firewall-ux.md`
- `integrations/smart-home.md`
- `integrations/healthcare-patient-consent.md`
- `integrations/education-credentials.md`
- `site/src/content/docs/integrations/index.md`

## Constraints

- Do not change normative spec text.
- Do not add new fixture files unless an existing fixture is insufficient and the reason is documented.
- Do not create or modify CI workflows, schedules, releases, tags, commits, or deployment infrastructure.
- Keep the journey checks deterministic and local.

## Acceptance criteria

- Four new dedicated journey docs exist and are linked from `docs/journeys/README.md`.
- `npm run journeys` passes from `/Users/grig/work/repo/universalmanifest/packages/universal-manifest`.
- Each affected lane's `Implementation notes` block points at its dedicated journey.
- The integration catalog accurately reflects the resulting status of `data-firewall-ux`, `smart-home`, `healthcare-patient-consent`, and `education-credentials`.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0242-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0242-BLOCKED.md`
