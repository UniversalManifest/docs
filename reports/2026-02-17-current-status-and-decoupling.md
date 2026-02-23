# Universal Manifest — Current Status and Decoupling Snapshot

**Date:** 2026-02-17  
**Project:** Universal Manifest  
**Canonical repository path:** `/Users/grig/work/repo/universalmanifest`  
**Previous path (legacy):** `/Users/grig/work/repo/universalmanifest (legacy path archived)`

## Executive status

Universal Manifest is in a strong pre-production state:

- v0.1 contract, fixtures, and baseline conformance are implemented.
- v0.2 draft signature profile (JCS + Ed25519) is implemented with draft artifacts and fixtures.
- Proof surfaces exist and pass locally (tests, journeys, endpoint smoke, harness autorun).
- Public docs IA and tone have been polished for adopter-first usage.

The main remaining blocker for "published and live" status is production deployment and DNS actions (Cloudflare Pages + Worker + domain bindings), tracked in WO-0003.

## Work-order status summary

- Completed: `WO-0001`, `WO-0002`, `WO-0004` through `WO-0013`
- Blocked: `WO-0003` (`docs/workorders/WO-0003-publishing-and-release.md`)
  - Blocked by external deployment actions and production validation on real domains.

## Verification status (latest local run)

- Site build: `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` → PASS
- Package validation: `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test` → PASS
- Journeys proof: `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys` → PASS
- Endpoint smoke (dev): `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run smoke:endpoints:dev` → PASS
- Harness autorun: `http://127.0.0.1:4300/harness/index.html?autorun=1` → PASS

Latest journey artifact:

- `/Users/grig/work/repo/universalmanifest/docs/journeys/_artifacts/2026-02-17T23-21-42-271Z-journey-report.json`

## Decoupling status

Decoupling from reference implementation is now explicit and operational:

- Repo moved out of `/Users/grig/work/repo/` into `/Users/grig/work/repo/universalmanifest`.
- Agent infrastructure aligned to GAS split model:
  - `AGENTS.md` = immutable global rules copy
  - `PROJECT-RULES.md` = Universal Manifest-specific onboarding and project rules
- `.dev` tree expanded to include GAS-expected working directories for handoffs, workorders, reports, and inbox capture.

## Immediate next actions

1. Execute production deployment runbooks and unblock `WO-0003`.
2. Run production smoke on real domains and capture evidence pack artifacts.
3. Maintain adopter-first docs while hardening v0.2 and resolver contract edge-case tests.
