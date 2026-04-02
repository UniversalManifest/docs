# Journey 23 -- MUM payment handles and fiat/crypto gateway flow

## Goal

Prove an XR consumer can read a public-safe payment initiation pointer while protected gateway handles remain behind an explicit protected-handle path.

## Inputs

- Fixture: `examples/v0.1/stubs/metaverse-mum-payment-handles-manifest.jsonld`

## Steps

1. Validate required manifest envelope fields.
2. Verify payment pointer family coverage:
   - `payment.public.checkout`
   - `payment.gateway.stripe.accountRef`
   - `payment.gateway.paypal.merchantRef`
   - `payment.gateway.crypto.settlementRef`
   - `payment.protected.bundle`
3. Verify `payment.handle.protected` consent is explicitly set.
4. Verify `paymentHandles` facet maps public checkout and protected bundle aliases.
5. Verify `paymentHandleEnvelope` captures encrypted-envelope metadata for protected delivery.
6. Treat `payment.public.checkout` as the initiation URL and keep protected handles pointer-first.

## Expected outcomes

- Consumer can initiate a payment from a public-safe checkout pointer.
- Protected payment handles are not embedded as raw secrets and remain pointer-gated.
- Delivery model is explicit (`projection-or-encrypted-inline`) and aligned with additive privacy guidance.

## Evidence

- `cd packages/universal-manifest && npm test`
- `cd packages/universal-manifest && npm run journeys`
