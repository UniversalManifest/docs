# WO-0142 — Payment Handles and Fiat/Crypto Gateway Integration

## Scope and dependency posture

- Work order: `docs/workorders/WO-0142-payment-handles-and-fiat-crypto-gateway-integration.md`
- Dependency outcome consumed: `WO-0143` additive privacy decision (projection remains normative, encrypted inline facets are optional guidance).
- Boundary: non-normative naming guidance and executable fixture/journey proof only; no core schema mandate changes.

## Problem decomposition

UM already had `prefs.financial.*` as a broad family, but no interoperable naming for concrete payment-handle routing across fiat gateways and crypto settlement rails. This created drift risk:

- different issuers using incompatible ad hoc pointer names,
- consumers unable to distinguish public-safe checkout links from protected handle data,
- no consistent bridge between projection and encrypted-inline handling for sensitive payment references.

## Decisions for WO-0142 implementation

1. Keep payment integration pointer-first and provider-neutral.
2. Separate public-safe initiation from protected handle routing.
3. Align protected delivery with WO-0143 additive privacy model (`projection-or-encrypted-inline`).
4. Keep all additions non-normative in v0.1 registry guidance.

## Registry additions (non-normative)

Pointer family:

- `payment.public.checkout`
- `payment.gateway.stripe.accountRef`
- `payment.gateway.paypal.merchantRef`
- `payment.gateway.crypto.settlementRef`
- `payment.protected.bundle`

Consent key:

- `payment.handle.protected`

Overlay family:

- `prefs.financial.handle.*`

## Fixture and journey evidence

Fixture:

- `examples/v0.1/stubs/metaverse-mum-payment-handles-manifest.jsonld`

Journey:

- `docs/journeys/J23-mum-payment-handles-and-gateway-flow.md`
- executable row `J23` in `packages/universal-manifest/scripts/run-journeys.mjs`

What the proof demonstrates:

- consumer can read `payment.public.checkout` as initiation URL,
- protected handles remain behind `payment.protected.bundle`,
- consent gate (`payment.handle.protected`) is explicit,
- encrypted-envelope metadata exists for protected path without forcing one cryptosystem into core conformance.

## Out-of-scope items intentionally not implemented

- direct processor SDK integration (Stripe/PayPal API calls),
- mandatory algorithm requirements for payment-handle encryption,
- blockchain-specific normative lock-in.
