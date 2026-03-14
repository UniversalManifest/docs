# WO-0116 — Expand Resolver Test Suite for Contract Coverage

**Status:** COMPLETED  
**Created:** 2026-03-02  
**Updated:** 2026-03-02  
**Completed:** 2026-03-02  
**Priority:** P0  
**Owner:** Resolver / Quality  
**Source:** Follow-on from deployment/runtime hardening review

## Objective

Add dedicated resolver-focused tests that validate contract behavior directly (beyond smoke/journeys) so regressions in status semantics, header contract, and path decoding are caught pre-deploy.

## Problem Statement

Resolver coverage today is strong at smoke and journey levels, but lacks a standalone contract-grade unit/integration suite in the resolver workspace. This leaves edge behavior vulnerable to unnoticed drift.

## Scope

In scope:

- contract-driven tests for resolver responses and headers
- local integration tests for KV-backed branches
- method/path/error behavior tests

Out of scope:

- changing public resolver contract version
- adding write APIs

## Deliverables

1. Resolver test plan mapped to contract sections:
   - `200`, `304`, `307`, `400`, `404`, `405`, `410`, `500`
   - direct UMID path vs `b64u:` path
   - CORS and exposed-header expectations
2. Executable resolver test suite under `services/myum-resolver/`
3. CI integration for resolver contract tests
4. Documentation update showing how to run resolver tests locally

## Acceptance Criteria

- [x] Test suite asserts full status matrix and required response headers.
- [x] Test suite validates ETag generation + conditional revalidation (`304`).
- [x] Test suite validates redirect semantics (`307` + `Location`).
- [x] Test suite validates malformed path handling and method gating (`405`).
- [x] CI runs resolver contract tests and fails on regression.

## Dependencies

- `services/myum-resolver/src/index.ts`
- `services/myum-resolver/CONTRACT.md`
- `packages/universal-manifest/scripts/smoke-endpoints.mjs`

## Verification Commands (Target)

```bash
cd services/myum-resolver
npm run test
```

```bash
cd packages/universal-manifest
npm run smoke:endpoints:dev
```

## Completion Evidence (2026-03-02)

Delivered artifacts:

- Contract-grade resolver test suite:
  - `services/myum-resolver/scripts/contract-tests.mjs`
- Resolver test command wiring:
  - `services/myum-resolver/package.json`
- Resolver contract/test docs:
  - `services/myum-resolver/README.md`
  - `services/myum-resolver/CONTRACT.md`
- CI integration for resolver contract tests:
  - `.github/workflows/ci.yml` (`resolver-contract` job)

Verification results:

- `cd services/myum-resolver && npm run test:contract` -> PASS
- `cd services/myum-resolver && npm run typecheck` -> PASS
