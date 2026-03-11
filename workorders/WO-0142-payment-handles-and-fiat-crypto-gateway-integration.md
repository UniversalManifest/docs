# WO-0142 — Payment Handles and Fiat/Crypto Gateway Integration

**Status:** NOT_STARTED  
**Created:** 2026-03-07  
**Updated:** 2026-03-07  
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

- Analysis report on payment gateway integration options.
- Proposed standard additions to `REGISTRY.md` or a dedicated extension profile.
- Fixtures and journey tests proving how an XR consumer would read the payment handle and initiate a transaction.

## Dependencies

- None.

## Execution Notes

- Must ensure the solution is thoroughly considered ("well thought out") and universally applicable, rather than just appending quick strings to the registry.
