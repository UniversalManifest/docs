# WO-0028 — Astro content-cache duplicate-id warning cleanup and build hardening

**Status:** COMPLETED
**Created:** 2026-02-22

## Objective

Eliminate recurring Astro duplicate-id warning noise caused by stale `.astro` content cache state and make the default site build path deterministic and clean.

## Scope

In scope:
- codify clean-build behavior in default site build command.
- preserve existing dev ergonomics while ensuring CI/local build parity.
- verify a warning-free clean build path with current docs corpus.

Out of scope:
- changing docs content routes or slugs.
- modifying Starlight content model or Astro internals.

## Deliverables

- `/Users/grig/work/repo/universalmanifest/site/package.json`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0028-astro-content-cache-clean-build-hardening.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/workorders/WO-INDEX.md`

## Acceptance criteria

- [x] `npm run build` in `/Users/grig/work/repo/universalmanifest/site` runs with cache cleanup and no duplicate-id warnings.
- [x] `npm run build:clean` remains valid and non-recursive.
- [x] New WO is indexed in both work-order indexes.

## Execution log

Completed changes:
1. Updated `/Users/grig/work/repo/universalmanifest/site/package.json` so default `build` always performs `clean:astro` before sync and Astro build.
2. Simplified `build:clean` to alias `build` (single deterministic clean-build path).
3. Re-ran build commands to confirm warning-free output and valid script wiring.

Validation commands:
- `cd /Users/grig/work/repo/universalmanifest/site && npm run build` (pass)
- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` (pass)

## Post-Completion Notes

### Regression Investigation (2026-02-23)

**Context:** An independent audit (step2-technical-validation.md) run on 2026-02-22 at 18:45:37 reported 10 duplicate-ID warnings including references to `integrations/lan.md`. This occurred AFTER WO-0028 was marked COMPLETED, suggesting a potential regression.

**Resolution:** No regression occurred. The warnings were valid at the time of the audit, but were subsequently resolved by commit 7f827a1 ("Normalize OMATrust/OMA3 terminology and remove LAN from documentation") at 19:05:58 on the same day. This commit removed the problematic `lan.md` file that was causing one of the duplicate-ID warnings.

**Current Status (verified 2026-02-23):**
- Build output: 0 warnings (verified via `npm run build 2>&1 | grep -ci "warn"`)
- Clean build: 0 duplicate-ID warnings (verified via full `.astro` + `node_modules/.vite` removal)
- Exit code: 0 (build succeeds)
- Pages built: 32
- Pagefind indexed: 31 pages, 1508 words

The original WO-0028 fix (cache cleanup script + build process hardening) remains effective. The temporary warnings seen in the audit were content-related, not cache-related, and were resolved through content cleanup rather than additional cache fixes.

**Verification command:**
```bash
cd /Users/grig/work/repo/universalmanifest/site && rm -rf .astro dist node_modules/.vite && npm run build 2>&1 | grep -ci "warn"
# Output: 0
```
