# WO-0216: Establish Integration-Lane Fixture Baseline

**Status:** NOT_STARTED
**Priority:** HIGH (P1)
**Depends on:** none directly; coordinate with WO-0213 if integration-lane doc edits land first
**Unblocks:** WO-0017 lane-coverage closure, WO-0219 cross-reference consolidation
**Derived from:** 2026-04-26 resolver runtime drift scan, finding 2 (HIGH)

## Objective

Of 15 documented integration lanes, only GPC has substantive fixture coverage (10 files). The other 14 lanes (smart-glasses, metaverse, RP1, OMATrust, education, healthcare, smart-home, proof-of-personhood, portable-identity-profile-xr, did-vc, data-firewall-ux, runtime-profile, social, and the remaining lane) are documented as guidance only with no runnable proof. Adopters have nothing to validate against. Establish a v0.1-conformant fixture baseline for each lane and tie at least one executable journey to each.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/integrations/` (all `*.md`)
- `/Users/grig/work/repo/universalmanifest/examples/integrations/` (current GPC-only baseline)
- `/Users/grig/work/repo/universalmanifest/spec/v0.1/schema.json`
- `/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md`
- `/Users/grig/work/repo/universalmanifest/spec/v0.2/schema.json`
- `/Users/grig/work/repo/universalmanifest/docs/journeys/` (J10–J23 for journey patterns)
- `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-04-26-resolver-runtime-drift-scan.md`

## Work to perform

1. **Enumerate the 15 lanes** — confirm the canonical list from `integrations/*.md` directory. Note any naming inconsistencies for later WO-0219 consolidation but do not fix them here.
2. **Per lane, design a minimum fixture set** — at least one valid baseline and one near-real example that exercises the lane's distinguishing field combinations. Use v0.1 schema as the conformance target; v0.2 is layered on later.
3. **Validate each fixture** — `npm test` in `packages/universal-manifest/` must pass with the new fixtures included.
4. **Map to journeys** — for each lane, either point at an existing journey (J10–J23 list) that already exercises it, or scope a new journey ID. Do not implement new journeys in this WO; flag follow-on WO drafts.
5. **Update each `integrations/{lane}.md`** with a "Proof coverage" table linking the new fixtures and the responsible journey ID.
6. **Sequence** — this is multi-week. Acceptable to ship in batches by lane group: glasses/metaverse/social first, then xr/runtime, then did-vc/personhood, then healthcare/education/smart-home, then OMATrust/firewall/RP1.

## Files to modify / create

- `examples/integrations/{lane}/` (14 new directories with fixtures)
- `integrations/{lane}.md` (add "Proof coverage" table)
- Possibly `docs/STUB-MANIFESTS.md` (the human index for fixtures)
- New WO drafts for journey work (do not lift into formal WO files unless the user approves; queue them as follow-on candidates)

## Constraints

- **v0.1 first** — establish baseline against the v0.1 contract. v0.2 layered fixtures are out of scope for this WO unless a lane is explicitly v0.2-only.
- **No shortcut "stub" fixtures** — each fixture must validate, must illustrate the lane's distinguishing pattern, and must be cite-able by an adopter.
- Do not commit, push, stage, or branch. Sibling commit agent owns git mutations.
- Run `git status --short` first; respect their diff.
- Do not change schema, conformance, or signing logic. Fixture-only WO.

## Acceptance criteria

- 14 new lane fixture directories under `examples/integrations/`, each with at least one valid + one near-real fixture.
- All fixtures pass `npm test` (validation matrix expanded; baseline 49 valid + 26 invalid grows accordingly).
- Each `integrations/{lane}.md` has a Proof Coverage table.
- A follow-on WO draft list identifies any new journeys needed.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0216-result.md` (use the date the WO actually completes; this is a multi-batch WO, so multiple result files per batch are acceptable, e.g. `-batch-1.md`, `-batch-2.md`).
Blocked: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0216-BLOCKED.md`

Reports must include: lane coverage matrix (before/after), fixtures added, npm test pass evidence, follow-on journey WO drafts.
