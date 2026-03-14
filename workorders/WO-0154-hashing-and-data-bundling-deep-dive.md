# WO-0154: Hashing, Caching, and Data Bundling Deep Dive

**Status:** COMPLETED
**Priority:** P1
**Created:** 2026-03-12
**Completed:** 2026-03-12

## Objective

Create a comprehensive deep-dive explainer covering how Universal Manifest handles content hashing, HTTP caching, data bundling, and the pointer-first architecture -- synthesizing internal implementation decisions with external standards research.

## Deliverables

1. `docs/explainers/hashing-and-data-bundling-deep-dive.md` -- 9-section deep dive following the pattern of `docs/explainers/facet-encryption-deep-dive.md`
2. L3-11 video brief added to `docs/scripts/production-queue.md`
3. WO-INDEX.md updated with this work order

## Scope

### Covered
- SHA-256 ETag generation and conditional revalidation (304 Not Modified)
- Ed25519 + JCS signing architecture and coverage map
- Pointer-first architecture as the primary optimization
- HTTP caching strategy (max-age=60, two TTL layers)
- Why CIDs are deferred (UMID as stable identity vs content hash)
- Pointer integrity gap and digestMultibase proposal
- CBOR-LD as future binary encoding profile
- Merkle history and bitstring status lists as future considerations
- Comparison to VCs, IPFS, DIDComm, Solid, DNS, Certificate Transparency

### Not covered
- Facet encryption (WO-0153)
- Resolver operational details (covered in resolver deep dive)
- Implementation code or TypeScript specifics

## Research Inputs

- Internal: resolver source code, ENVELOPE-TOPOLOGY.md, SIGNATURE-PROFILE.md, resolver-deep-dive.md
- External: CIDs/Multihash, CBOR-LD, COSE, W3C VC Data Integrity, SRI/Hashlink, HTTP caching RFCs, Merkle DAGs, Certificate Transparency

## Evidence

- Deep dive document created at `docs/explainers/hashing-and-data-bundling-deep-dive.md`
- L3-11 video brief integrated into production queue
