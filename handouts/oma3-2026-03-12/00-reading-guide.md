# Universal Manifest -- OMA3 Handout Collection

**Prepared for:** Alfred Tom and OMA3 members
**Date:** 2026-03-12
**Context:** "Architectural overview (data structures, file formats, etc.) to figure out how to fit UM into IWPS."

---

## What These Documents Are

This is a set of nine short documents that explain Universal Manifest from the ground up. Each document covers one topic. You can read them in order for the full picture, or jump to any single document and understand it on its own.

The documents are written for standards body reviewers who want to understand UM's architecture -- what the data structures look like, how they fit together, and where UM complements IWPS.

## Reading Order

| # | Title | What It Covers | Pages |
|---|-------|---------------|-------|
| **01** | [The Problem](01-the-problem.md) | Why portable state is needed | 1 |
| **02** | [The Envelope](02-the-envelope.md) | What a Universal Manifest is (minimal JSON-LD document) | 2 |
| **03** | [Facets and Pointers](03-facets-and-pointers.md) | Modular data compartments and lightweight references | 2 |
| **04** | [Consent](04-consent.md) | Default-deny privacy that travels with the data | 2 |
| **05** | [Signatures](05-signatures.md) | Cryptographic tamper detection (v0.2) | 2 |
| **06** | [The Resolver](06-resolver.md) | How manifests are found (myum.net) | 2 |
| **07** | [IWPS + UM](07-iwps-integration.md) | The complete portaling stack -- the key document for OMA3 | 3 |
| **08** | [Beyond Metaverse](08-what-else.md) | The full application space (15 categories, 163 use cases) | 3 |
| **09** | [What's Next](09-whats-next.md) | Current status, deferred items, collaboration opportunities | 2 |

## If You Have 5 Minutes

Read **01** (the problem) and **07** (IWPS integration). These two documents frame the relationship between UM and IWPS.

## If You Have 20 Minutes

Read **01** through **07** in order. This gives you the complete technical architecture before the integration discussion.

## If You Want More Detail

Each handout references the relevant specification and explainer documents. The full specification lives at:

- **Spec:** `spec/v0.2/README.md`
- **Live site:** https://universalmanifest.net
- **Resolver:** https://myum.net

## Terminology Quick Reference

| Term | Definition |
|------|-----------|
| **UM** | Universal Manifest -- the specification and portable document format |
| **UMID** | Universal Manifest Identifier -- a UUID-based URN for global identification |
| **Facet** | A named, modular data compartment inside a manifest |
| **Pointer** | A URI referencing external authoritative data |
| **TTL** | Time-to-live via `issuedAt` / `expiresAt` timestamps |
| **IWPS** | Inter-World Portaling Standard (OMA3) |
| **JCS** | JSON Canonicalization Scheme (RFC 8785) |
