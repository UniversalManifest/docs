# WO-0040 — v0.2 signature verification fix

**Status:** COMPLETED
**Created:** 2026-02-23
**Priority:** HIGH
**Source:** Independent audit (2026-02-22 completion audit)

## Objective

Investigate and fix the reported v0.2 signature verification failure in `npm test`, where `examples/v0.2/minimal-signed-manifest.jsonld` was reported as failing signature verification.

## Why this work matters

v0.2 signature verification is the headline feature of the v0.2 spec. A broken signature fixture or verification code path would undermine the entire v0.2 integrity story and cascade failures into journeys J01-J03.

## Scope

In scope:

- Investigate the reported signature verification failure in `npm test`.
- Review uncommitted changes to `examples/v0.2/minimal-signed-manifest.jsonld` and `packages/universal-manifest/src/index.ts`.
- Fix any misalignment between the fixture, canonicalization logic, public key, or algorithm parameters.
- Verify that `npm test` exits with code 0 and journeys improve.

Out of scope:

- Fixing J04 (UMID resolver E2E), which fails due to a `wrangler` CLI compatibility issue unrelated to signature verification.
- Adding new v0.2 fixtures or edge cases (tracked by WO-0036/WO-0037).

## Required deliverables

1. Root-cause analysis of the reported failure.
2. Fix applied (if needed) to fixture or verification code.
3. `npm test` green (exit code 0).
4. Journey results documented.

## Acceptance criteria

- [x] `npm test` exits with code 0.
- [x] `examples/v0.2/minimal-signed-manifest.jsonld` passes v0.2 structural and signature validation.
- [x] All 19 invalid v0.2 fixtures correctly rejected.
- [x] All 21 valid fixtures (v0.1 + v0.2) pass.
- [x] Root cause documented.

## Validation commands

- `cd packages/universal-manifest && npm test`
- `cd packages/universal-manifest && npm run journeys`

## Completion evidence (2026-02-23)

### Root-cause analysis

The independent audit (2026-02-22) reported that `npm test` fails due to v0.2 signature verification failure in `examples/v0.2/minimal-signed-manifest.jsonld`. Investigation found:

1. **No actual content changes exist.** `git diff` for both `examples/v0.2/minimal-signed-manifest.jsonld` and `packages/universal-manifest/src/index.ts` produces empty output -- the working tree matches HEAD exactly. The git status markers (` M`) were likely stale file attribute/timestamp artifacts, not content modifications.

2. **`npm test` passes with exit code 0.** All 40 fixtures validate correctly:
   - 21 valid fixtures pass (including `minimal-signed-manifest.jsonld` with full Ed25519/JCS-RFC8785 signature verification).
   - 19 invalid fixtures are correctly rejected.

3. **The signature verification code path is sound.** The `verifySignatureV02()` function in `packages/universal-manifest/src/index.ts` correctly:
   - Strips the `signature` field from the manifest.
   - Canonicalizes the unsigned payload using JCS (RFC 8785).
   - Decodes the SPKI-DER public key from base64.
   - Verifies the Ed25519 signature using `node:crypto`.

4. **Journeys show 10 pass, 1 fail.** The single failure (J04 -- UMID resolution) is caused by a `wrangler` CLI compatibility issue (`Unknown arguments: local, preview, binding...`), completely unrelated to signature verification. Journeys J01, J02, and J03 (which depend on `npm test`) all pass.

### Conclusion

No code or fixture fix was required. The reported failure could not be reproduced; the v0.2 signature verification pipeline is functioning correctly. The audit observation may have been based on a transient build artifact state or a stale `dist/` directory that has since been rebuilt.

### Test output

```
npm test — exit code 0

OK   examples/v0.2/minimal-signed-manifest.jsonld  (urn:uuid:11111111-1111-4111-8111-111111111111)
OK   examples/v0.2/invalid/invalid-signature-algorithm.jsonld  (expected invalid: structural)
OK   examples/v0.2/invalid/invalid-signature-canonicalization.jsonld  (expected invalid: structural)
OK   examples/v0.2/invalid/invalid-signature-created-format.jsonld  (expected invalid: structural)
OK   examples/v0.2/invalid/invalid-signature-public-key.jsonld  (expected invalid: structural)
OK   examples/v0.2/invalid/invalid-signature.jsonld  (expected invalid: structural)
OK   examples/v0.2/invalid/issued-after-expires-signed.jsonld  (expected invalid: structural)
OK   examples/v0.2/invalid/missing-signature-key-material.jsonld  (expected invalid: structural)
OK   examples/v0.2/invalid/missing-signature.jsonld  (expected invalid: structural)

Summary: 21 valid ok, 0 failed, 19 invalid ok, 0 invalid unexpected-pass
```

```
npm run journeys — 10 pass, 1 fail

J01 Parse and ignore unknown fields: pass
J02 TTL and freshness: pass
J03 Signature verification (v0.2): pass
J04 UMID resolution (myum resolver E2E): fail (wrangler CLI issue, unrelated)
J05 LAN edge to display smoke: pass (skipped — LAN repo not configured)
J06 Public profile projection: pass
J07 RP1 spatial fabric projection lane: pass
J08 Smart-glasses consent enforcement lane: pass
J09 Metaverse cross-world projection lane: pass
J10 Multi-provider personhood coexistence: pass
J11 OMATrust attestation interoperability: pass
```
