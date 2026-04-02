# WO-0142 — Payment Handles and Fiat/Crypto Gateway Integration

**Status:** COMPLETED  
**Created:** 2026-03-07  
**Updated:** 2026-04-01  
**Priority:** P1  
**Owner:** Universal Manifest Integration  

## Objective

Conduct a deep analysis and create explicit, well-thought-out standard pointers or overlays for payment handles (including crypto wallets, fiat gateways like Stripe, PayPal, etc.) to ensure Universal Manifest can seamlessly handle incoming payments or monetization across interoperable experiences.

## Problem Statement

While Universal Manifest v0.1 supports financial preferences via the `prefs.financial.*` overlay family, it lacks explicit, well-known naming conventions for concrete payment handles. A simple "quick fix" adding generic strings is insufficient. A universal, highly interoperable approach is needed so platforms know exactly how to hook up major payment gateways securely without friction.

## Scope

In scope:
- Deep analysis of major fiat payment gateways (Stripe, PayPal, etc.) and crypto wallet handling.
- Development of a universal, non-opinionated schema for declaring these capabilities in a manifest.
- Proposal for explicit `REGISTRY.md` pointers, facets, or claims.
- Consideration of standardizing receiver formats without leaking sensitive financial info.

Out of scope:
- Implementing the actual payment processors inside the core repo.
- Restricting payment methods to a single blockchain or single fiat provider.

## Deliverables

- [x] Analysis report on payment gateway integration options.
  - `docs/reports/2026-04-01-wo-0142-payment-handles-and-fiat-crypto-gateway-integration.md`
- [x] Proposed standard additions to `REGISTRY.md` or a dedicated extension profile.
  - `spec/v0.1/REGISTRY.md`
  - `docs/DECISIONS.md`
- [x] Fixtures and journey tests proving how an XR consumer would read the payment handle and initiate a transaction.
  - `examples/v0.1/stubs/metaverse-mum-payment-handles-manifest.jsonld`
  - `docs/journeys/J23-mum-payment-handles-and-gateway-flow.md`
  - `docs/journeys/README.md`
  - `packages/universal-manifest/scripts/run-journeys.mjs`

## Dependencies

- WO-0143 completed outcome consumed:
  - additive privacy model (projection remains normative, encrypted inline facets allowed as optional guidance profile).
  - authority: `docs/workorders/WO-0143-private-encrypted-inline-facets-vs-projection-model-analysis.md`
  - ADR: `docs/reports/2026-04-01-wo-0143-private-encrypted-inline-facets-vs-projection-adr.md`

## Execution Notes

- Must ensure the solution is thoroughly considered ("well thought out") and universally applicable, rather than just appending quick strings to the registry.

## Completion Notes

- Payment-handle naming now includes explicit public-vs-protected routing and provider-neutral fiat/crypto pointer conventions.
- Protected-handle delivery is aligned with WO-0143 additive privacy direction (`projection-or-encrypted-inline`) while remaining non-normative.
- Verification evidence captured via:
  - `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm test`
  - `cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest && npm run journeys`
