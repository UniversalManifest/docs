# Universal Manifest Specification

**W3C-Style Draft Specification (Hybrid Form)**  
**Date:** March 2026

---

## Abstract

This specification defines a JSON-LD-based file format known as the **Universal Manifest**, a portable state capsule. Formulated as a hybrid synthesis of W3C Publication metadata and Web Application parameters, this format provides developers and issuers with a standardized envelope to convey linked-data identity references, role permissions, device registrations, and pointers to canonical data sources. 

The Universal Manifest is specifically designed for local-first environments (e.g., venue edges, public displays) where consumers must tolerate partial connectivity and rely on cached, verifiable state. Using this standard, user agents, smart displays, and network edges can securely interoperate without requiring a continuous cloud connection, facilitating seamless cross-context experiences.

## Status of This Document

*This section describes the status of this document at the time of its publication.*

This document is a draft specification of the Universal Manifest v0.1 format. It borrows structural paradigms from both the **W3C Web Application Manifest** (for lifecycle, parsing, and caching procedures) and the **W3C Web Publication Manifest** (for linked data contexts, identities, and structural facets).

Implementors need to be aware that this specification is not yet fully stable, particularly regarding the signature profile which allows for permissive integrity checks in this version. Implementors who are not taking part in the discussions will find the specification changing out from under them in incompatible ways as the v0.2 iteration is finalized.

Publication as a Working Draft does not imply endorsement by the W3C or its Members. It is inappropriate to cite this document as other than a work in progress.

## Table of Contents

1. [Universal Manifest](#1-universal-manifest)
   1. [Examples](#11-examples)
   2. [JSON-LD Core Members](#12-json-ld-core-members)
   3. [Identities & Lifespans](#13-identities--lifespans)
   4. [Structural State Members](#14-structural-state-members)
   5. [Signature Integrity](#15-signature-integrity)
2. [Entities and Facets](#2-entities-and-facets)
   1. [um:Facet Module](#21-umfacet-module)
   2. [um:Entity Base](#22-umentity-base)
3. [Manifest Lifecycle and Caching](#3-manifest-lifecycle-and-caching)
   1. [Processing the Manifest](#31-processing-the-manifest)
   2. [Caching Formulation](#32-caching-formulation)
4. [Conformance](#4-conformance)
   1. [Consumer Behavior](#41-required-behavior-consumer)
   2. [Issuer Behavior](#42-required-behavior-issuer)
   3. [Standalone Conformance Suite](#43-standalone-conformance-suite)
5. [Extensibility & Profiles](#5-extensibility--profiles)
6. [Security Considerations](#6-security-considerations)
   1. [Signature Limitations](#61-signature-limitations)
   2. [TTL Enforcement](#62-ttl-enforcement)
   3. [Resource Limits](#63-resource-limits)
7. [Privacy Considerations](#7-privacy-considerations)

---

## 1. Universal Manifest

A **Universal Manifest** is a [JSON-LD](https://www.w3.org/TR/json-ld/) document acting as a cross-platform data envelope. It blends the semantic linkability of a Web Publication Manifest with the applied processing lifecycle of a Web App Manifest.

### 1.1 Examples

The following is an example of a minimal Universal Manifest:

```json
{
  "@context": [
    "https://universalmanifest.net/ns/v0.1"
  ],
  "@id": "urn:uuid:123e4567-e89b-12d3-a456-426614174000",
  "@type": ["um:Manifest"],
  "manifestVersion": "0.1",
  "subject": "did:example:123",
  "issuedAt": "2026-03-01T00:00:00Z",
  "expiresAt": "2026-03-02T00:00:00Z"
}
```

### 1.2 JSON-LD Core Members

#### 1.2.1 `@context` member
The `@context` member establishes the semantic definitions of terms used within the manifest. It MUST include the Universal Manifest namespace (e.g., `https://universalmanifest.net/ns/v0.1`).

#### 1.2.2 `@id` member
The `@id` member provides a primary identifier. Issuers SHOULD generate `@id` as an opaque, offline-safe identifier (e.g., `urn:uuid:<uuidv4>`).

#### 1.2.3 `@type` member
The `@type` member indicates the document type classifying the resource. It MUST include the value `um:Manifest`.

### 1.3 Identities & Lifespans

#### 1.3.1 `subject` member
The `subject` member specifies the primary entity (user, app, venue) the manifest describes. It MUST contain a stable identifier URI (e.g., a Decentralized Identifier / DID).

#### 1.3.2 `issuedAt` and `expiresAt` members
The `issuedAt` and `expiresAt` members formulate the bounding constraints (TTL) for the manifest's validity. Both parameters are formatted as ISO 8601 / RFC 3339 date-time strings.

### 1.4 Structural State Members

The manifest structure relies on domain-specific members akin to Web Publication linkages.

#### 1.4.1 `facets` member
The `facets` member organizes extended functional blocks (`um:Facet`), packaging specific verifiable capabilities, metadata subsets, or configuration modules.

#### 1.4.2 `claims`, `consents`, `devices`, and `pointers`
These arrays group specific operational contexts representing permissions, deployed hardware targets, and external data reference pointers connected to the `subject`.

### 1.5 Signature Integrity

#### 1.5.1 `signature` member
The `signature` member encapsulates cryptographic proofs of the manifest payload. In v0.1, its format is intentionally permissive and serves as a placeholder for interoperable profiles (reserved for subsequent iterations).

---

## 2. Entities and Facets

Universal Manifest adopts a compositional pattern allowing nested structures (`facets` mapping to specific `entities`), drawing from semantic web standards for deeply interlinked resources.

### 2.1 um:Facet Module
A facet is a composable part grouped within a manifest's envelope. A facet MUST explicitly declare `@type`: `um:Facet`. It MAY optionally declare a `name` for display purposes, a `ref` routing to its authoritative source, and an `entity` holding the payload parameters (`um:Entity`).

### 2.2 um:Entity Base
The `um:Entity` acts as the base classification for all embedded configurations, representations, or localized states. It MUST be resolvable through an `@id` URI and typed accordingly (`@type` array).

---

## 3. Manifest Lifecycle and Caching

Parallel to the Web Application Manifest lifecycle, the Universal Manifest must be systematically processed, applied, and occasionally evicted from client edges.

### 3.1 Processing the Manifest
When a user agent or smart edge encounters a Universal Manifest, it MUST:
1. Parse the JSON document for semantic syntax errors.
2. Confirm the existence of required properties (`@context`, `@id`, `subject`, `issuedAt`, `expiresAt`).
3. Discard any unknown fields seamlessly to preserve forward compatibility.

### 3.2 Caching Formulation
For constrained devices and public displays:
1. **TTL Ejection**: Caches MUST immediately evict or reject payloads where the system clock surpasses `expiresAt`.
2. **Telemetry Minimization**: Centralized logging platforms SHOULD stream only the `@id` string (and potentially a content hash), bypassing the full JSON payload to conserve bandwidth.
3. **Identifier Rotation**: Identifiers (`@id`) SHOULD be rotated iteratively per-issuance to avert heuristic tracking.

---

## 4. Conformance

### 4.1 Required behavior (consumer)
A consumer platform parsing the manifest MUST validate structural parameters and securely ignore unknown elements without raising fatal invocation errors. Freshness (via `expiresAt` TTL constraints) is an absolute rejection gateway. Implementers MUST verify `issuedAt <= expiresAt`.

### 4.2 Required behavior (issuer)
Issuers generating the manifest MUST assign a globally stable identifier URI for the `subject` (preferably an established DID) and a random URI for the manifest root (`@id`). To shield clients from unbounded trust windows, issuers MUST strictly bound `expiresAt` to a sensible interaction lifetime (e.g., hours or days).

### 4.3 Standalone Conformance Suite
Implementations validate conformance claims natively by testing against the official `conformance/` suite—which includes fixture validation (accepting valid stubs and correctly isolating/flagging malformed artifacts like missing contexts or expired logic trees).

---

## 5. Extensibility & Profiles

Echoing the extensibility models of generic W3C recommendations, proprietary manifest members can be injected via fully qualified URIs inside the linked `@context`. Consumers ignoring unrecognized properties guarantees that domain-specific profiles won't shatter cross-system interoperability.

---

## 6. Security Considerations

**Warning:** Version 0.1 intentionally defers universal cryptographic standardization.

### 6.1 Signature Limitations
Because v0.1 lacks strict prescriptive rules on canonicalization formatting and algorithm bounds, tamper-protection cannot be definitively guaranteed using baseline specifications. Implementers migrating to production applications MUST implement additive signature topologies documented in v0.2.

### 6.2 TTL Enforcement 
Bounding the `expiresAt` timeline dictates the primary line of defense against presentation replay spoofing. 

### 6.3 Resource Limits
Denial-of-Service vectors originating from disproportionately inflated arrays or recursion logic SHOULD be countered with hard limits on payload ingestion:
- Maximum memory serialization threshold: 1 MB
- Maximum recursion/nesting depth: 10 layers
- Array length maximums: 1,000 bounds

---

## 7. Privacy Considerations

- **Opaque Identifiers**: Generating the `@id` via random-distribution UUIDv4 shields session metadata from enumerability.
- **Minimal Disclosure**: Universal Manifest acts as the fundamental passport. Issuers are strongly advised against over-bundling capabilities. Only embed contextually relevant facets.
- **Subject Privacy**: Static DID correlations across disparate endpoints create persistent observation footprints. The use of pairwise / pseudonymous DIDs resolves to significantly improved ecosystem privacy.
