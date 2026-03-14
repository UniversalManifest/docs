# Facet Privacy — Public, Encrypted, and Selective Disclosure

**Summary:** Universal Manifest v0.1/v0.2 deliberately ships without built-in encryption, keeping the base specification flexible. All facets are plaintext today, with privacy enforced through consent toggles (default-deny) and the projection model (consumer-specific derived manifests). For stronger cryptographic privacy, three encryption methods are recommended as opt-in layers above the base protocol: JWE per-facet encryption for confidentiality at rest, BBS+ selective disclosure for unlinkable presentation privacy, and SD-JWT for JWT ecosystem interoperability. Per-facet encryption in a portable, self-contained document is something no other standard offers at the envelope level.

---

## 1. How Facets Work Today (Public Facets)

Facets are named, typed data compartments within the Universal Manifest JSON-LD envelope. Each facet represents a distinct category of information -- `publicProfile`, `deviceIdentity`, `venuePolicy`, `crossWorldProfile`, `gameProfile` -- and can contain structured data, claims, or references to external resources.

In v0.1 and v0.2, all facets are plaintext. When a consumer resolves a manifest, every facet is readable as standard JSON. There is no encryption, no obfuscation, and no binary encoding. This is a deliberate design choice: the base specification prioritizes interoperability and simplicity over built-in confidentiality.

Privacy today is enforced through two mechanisms:

**Consent toggles** govern what downstream systems are allowed to do with the data. The `consents` array uses a default-deny model: if a consent is not explicitly granted, it is denied. A facet might be readable, but the consent rules say "you may not display this publicly" or "you may not feed this to analytics." Consent is structural and portable -- it travels inside the manifest, so every consumer in the chain has the same rules.

**Pointers** reference external data without embedding it. Instead of copying a large avatar asset or a full social graph into the manifest, a pointer provides a URI to the authoritative source. This means the manifest stays lightweight, and the external resource can enforce its own access controls independently.

**Forward compatibility** is built in: consumers that encounter unknown facets preserve them without rejection. This means new facet types -- including encrypted ones -- can be introduced without breaking existing consumers.

---

## 2. Three Approaches to Facet Privacy

The Universal Manifest specification recognizes that no single privacy mechanism fits all use cases. The design principle is explicit: "UM needs multiple, flexible ways of handling private data to remain truly universal." Three approaches exist, each with different trade-offs.

### Approach A: Projection Model (Current Normative Approach)

**How it works:** The manifest issuer creates consumer-specific derived manifests called projections. Instead of sharing the full manifest with every consumer, the issuer generates a tailored version that contains only the facets and claims appropriate for that recipient. Each projection is independently signed, creating a complete and verifiable manifest in its own right.

**Pros:**
- Simple to implement -- it is just creating different JSON documents
- Each projection is independently signed and self-contained
- Reduced payload size -- consumers only receive what they need
- No encryption complexity -- privacy is achieved through omission
- Proven in existing journeys (Journey 06, J12, J21)

**Cons:**
- Lifecycle management -- every projection must be updated when the source manifest changes
- Stale projections -- a consumer may hold a projection that no longer matches the canonical manifest
- Operational burden -- the issuer must track which consumers have which projections
- Authority questions -- who decides what goes into each projection?
- Revocation complexity -- revoking a specific projection requires tracking its distribution

**Status:** NORMATIVE. This is the established approach, proven in multiple journey scenarios.

### Approach B: Consent-Gated Access Control

**How it works:** All facets remain plaintext within the manifest, but consent toggles gate what consumers are allowed to do with the data. The manifest carries an array of consent rules, each with a name and a value indicating the permission state.

**Three states:**
- **allowed** -- the consumer may use this data for the specified purpose
- **denied** -- the consumer must not use this data for the specified purpose
- **not-set** (absent from the array) -- treated as denied (default-deny principle)

**Extended model capabilities:**
- Audience matching -- consent rules can specify which consumer types they apply to
- Context scoping -- different consent values for different usage contexts
- Per-rule TTL -- individual consent rules can have their own expiration

**Pros:**
- Simple to implement and understand
- No encryption complexity
- Default-deny provides strong baseline protection
- Consent travels with the data, enforceable at every point in the chain
- The Little Snitch firewall model provides intuitive UX for managing consent

**Cons:**
- Relies on consumer honesty -- a determined attacker who obtains the manifest JSON can read all facets regardless of consent toggles
- No cryptographic enforcement -- consent is a policy signal, not a technical barrier
- Insufficient for high-sensitivity data where the transport channel itself may be untrusted

**Status:** NORMATIVE. This is the established consent architecture.

### Approach C: Encrypted Inline Facets (Proposed)

**How it works:** Individual facets are encrypted within the manifest document itself. The manifest envelope -- UMID, subject, TTL, consents -- stays in cleartext so that any consumer can identify the manifest, check its validity, and read its consent rules. But specific facets are replaced with encrypted blobs that only authorized recipients can decrypt.

Each encrypted facet is a JWE (JSON Web Encryption) object embedded as the facet's value. The facet key (name) remains visible, but the facet content is opaque ciphertext. A consumer that lacks the decryption key sees the facet exists but cannot read its contents.

**Pros:**
- Cryptographic enforcement -- privacy is not just policy, it is mathematically enforced
- Self-contained -- encrypted data, key metadata, and consent rules all travel together
- Selective access -- different recipients decrypt different facets from the same manifest
- No separate access control infrastructure required

**Cons:**
- Key management complexity -- distributing, rotating, and revoking keys
- Payload size increase -- encrypted facets are larger due to base64 encoding and JWE headers
- Signature interaction -- how does JCS canonicalization work when parts of the JSON are encrypted?
- Key distribution -- how do recipients obtain the decryption keys?
- Implementation complexity -- every consumer needs encryption library support

**Status:** Proposed. WO-0143 (NOT_STARTED) will produce the architectural decision. This deep dive informs that decision.

---

## 3. The Three Encryption Methods

For Approach C (encrypted inline facets), three encryption methods are recommended as opt-in layers above the base protocol. Each serves a different purpose and fits different scenarios.

### Method 1: JWE Per-Facet Encryption (Recommended Primary)

**Mechanism:** Each sensitive facet is encrypted as a JWE object conforming to RFC 7516 (JSON Web Encryption). The cleartext facet value is encrypted using a Content Encryption Key (CEK), and the CEK is wrapped for each intended recipient using their public key.

**Algorithm selection:**
- **Key wrapping:** ECDH-ES+A256KW -- Elliptic Curve Diffie-Hellman Ephemeral Static with AES-256 Key Wrap. This generates an ephemeral key pair for each encryption operation, derives a shared secret with the recipient's public key, and wraps the CEK.
- **Content encryption:** A256GCM -- AES-256 in Galois/Counter Mode. Authenticated encryption that provides both confidentiality and integrity.
- **Key exchange curve:** X25519 -- compatible with the Ed25519 keys already established for UM v0.2 signing via birational mapping (Ed25519 signing keys can be converted to X25519 key agreement keys).

**Multi-recipient support:** JWE JSON Serialization (as opposed to JWE Compact Serialization) supports multiple recipients. The same CEK encrypts the facet content once, and the CEK is separately wrapped for each recipient's public key. This means:
- The ciphertext is generated once (efficient)
- Each recipient gets their own wrapped copy of the CEK in the `recipients` array
- Adding or removing a recipient only requires adding or removing a key wrap, not re-encrypting the data

**Example structure (conceptual):**
```json
{
  "@context": "https://universalmanifest.net/context/v0.2",
  "umid": "urn:uuid:...",
  "subject": "did:example:alice",
  "facets": {
    "publicProfile": {
      "@type": "PublicProfile",
      "displayName": "Alice"
    },
    "medicalHistory": {
      "protected": "eyJhbGciOiJFQ0RILUVTK0EyNTZLVyIsImVuYyI6IkEyNTZHQ00ifQ",
      "recipients": [
        { "header": { "kid": "did:example:doctor#key-agree-1" }, "encrypted_key": "..." },
        { "header": { "kid": "did:example:insurer#key-agree-1" }, "encrypted_key": "..." }
      ],
      "iv": "...",
      "ciphertext": "...",
      "tag": "..."
    }
  }
}
```

In this example, `publicProfile` is plaintext and readable by anyone. `medicalHistory` is a JWE object -- only the doctor and the insurer can decrypt it.

**Why JWE is the right primary choice:**
- IETF standard (RFC 7516) with broad library support in every major language
- DIDComm v2 uses JWE for encrypted messaging, validating this exact pattern
- ECIES (Elliptic Curve Integrated Encryption Scheme) is mechanically what JWE ECDH-ES does -- there is no need for a separate standard
- Envelope encryption (DEK/KEK pattern) is what JWE does internally -- the CEK is the DEK, the key wrapping is the KEK layer
- HPKE (RFC 9180) is a modern alternative but is not yet integrated into the JOSE family; JWE provides equivalent security with better ecosystem support today

**Key rotation:** To rotate a recipient's key, re-wrap the CEK for the new key version. The ciphertext does not change. This is the envelope encryption advantage -- key rotation is a metadata operation, not a data re-encryption operation.

**Status:** Recommended by external standards research. Aligns with UM's internal "layer encryption above the base protocol" guidance.

### Method 2: BBS+ Selective Disclosure (For Presentation Privacy)

**Mechanism:** BBS+ is a multi-message signature scheme operating on BLS12-381 elliptic curves. The issuer signs a set of messages (claims) together. The holder can then create a derived proof that reveals only selected messages while proving the original issuer's signature remains valid -- without revealing the unrevealed messages or allowing the verifier to correlate presentations.

**How it works with JSON-LD:**
1. The JSON-LD manifest is canonicalized using RDF canonicalization (RDFC-1.0)
2. The canonical form is serialized as N-Quads (one statement per line)
3. Each N-Quad statement becomes a separate BBS message
4. The issuer signs all messages together with BBS+
5. At presentation time, the holder selects which N-Quads to reveal
6. The holder generates a zero-knowledge proof that the revealed N-Quads belong to a validly signed set
7. The verifier checks the proof without seeing the hidden N-Quads

**Pros:**
- True unlinkability -- each derived proof is cryptographically unique; the verifier cannot correlate two presentations of the same manifest
- Selective disclosure without revealing structure -- the verifier learns nothing about which claims were hidden or how many exist
- JSON-LD native -- the RDF canonicalization path means BBS+ works naturally with JSON-LD documents
- W3C Candidate Recommendation -- active standardization with strong community momentum

**Cons:**
- Requires BLS12-381 curves -- these are not Ed25519 and cannot share key material with UM's existing v0.2 signing profile
- Computationally heavier -- BLS pairing operations are significantly more expensive than Ed25519 signatures
- Larger proof sizes -- BBS+ proofs are larger than Ed25519 signatures
- Not yet a final W3C Recommendation -- the specification may change before finalization
- Library maturity varies -- fewer production-grade implementations compared to JWE

**When to use:** When the holder needs to prove specific facts about themselves without revealing the full manifest and without allowing the verifier to track presentations across sessions. This is the gold standard for privacy-preserving credential presentation.

**Status:** Research-first track in UM (PIP-RS-02). W3C Candidate Recommendation. Explicitly marked as uncertain/research in UM's internal roadmap.

### Method 3: SD-JWT Selective Disclosure (For JWT-Compatible Systems)

**Mechanism:** SD-JWT (Selective Disclosure for JWTs, RFC 9901) works by replacing claim values with salted hashes (digests) in the signed JWT. The original claim values, along with their salts, are provided as separate Disclosure objects. The holder selects which Disclosures to present alongside the JWT, revealing only the chosen claims.

**How it works:**
1. The issuer creates a JWT with some claims replaced by `_sd` digest arrays
2. For each hidden claim, a Disclosure is created: `base64url(json([salt, claim_name, claim_value]))`
3. The SHA-256 hash of the Disclosure is included in the `_sd` array
4. The issuer signs the JWT with standard JWS
5. At presentation, the holder sends the JWT plus selected Disclosures
6. The verifier hashes each Disclosure and checks it matches an entry in `_sd`

**Pros:**
- Full IETF standard (RFC 9901) -- finalized, stable, not going to change
- Simple mechanism -- SHA-256 hashing and standard JWS; no exotic cryptography
- EU Digital Identity Wallet (EUDIW) is adopting SD-JWT, creating a large compliance-driven ecosystem
- Broad tooling support -- JWT libraries are ubiquitous

**Cons:**
- JWT-native, not JSON-LD-native -- UM uses JSON-LD as its base format; SD-JWT would require a translation layer or a parallel JWT-based profile
- Linkable -- the same JWT is presented each time; verifiers can correlate presentations (unlike BBS+)
- Reveals claim structure -- the `_sd` array reveals how many hidden claims exist, even if their values are hidden
- No unlinkability -- the holder cannot prevent two verifiers from comparing notes

**When to use:** When interoperating with JWT-based ecosystems such as OIDC providers, EU eIDAS infrastructure, or enterprise systems that already process JWTs. SD-JWT is the pragmatic choice when the verifier ecosystem speaks JWT.

**Status:** Research-first track in UM. Full IETF standard. Relevant for interoperability bridges, not for UM's native format.

---

## 4. How Encryption Interacts with Signing

The Universal Manifest v0.2 signing profile uses JCS (JSON Canonicalization Scheme, RFC 8785) to produce a deterministic JSON serialization, then signs that serialization with Ed25519. This creates a challenge: JCS canonicalization operates on the full JSON structure. If some facets are encrypted JWE blobs, what exactly gets signed?

Two approaches exist:

### Sign-then-Encrypt

1. The issuer creates the full plaintext manifest with all facets in cleartext
2. The issuer signs the plaintext manifest using JCS + Ed25519
3. The signature is embedded in the manifest
4. The issuer encrypts individual facets, replacing their plaintext values with JWE objects
5. The final manifest contains: cleartext envelope, signature (computed over plaintext), and encrypted facets

**Verification flow:** The consumer decrypts the facets they have keys for, reconstructs the plaintext manifest, then verifies the Ed25519 signature over the JCS-canonicalized plaintext.

**Problem:** A consumer who cannot decrypt all facets cannot reconstruct the full plaintext and therefore cannot verify the signature. This creates a trust gap for partial-access consumers.

### Encrypt-then-Sign (Recommended for UM)

1. The issuer creates the full plaintext manifest
2. The issuer encrypts individual facets, replacing their plaintext values with JWE objects
3. The issuer signs the manifest as it now exists -- including the JWE blobs as opaque values
4. The final manifest contains: cleartext envelope, encrypted facets, and a signature computed over the manifest including the JWE objects

**Verification flow:** The consumer verifies the Ed25519 signature first (over the manifest as received, including JWE blobs), then decrypts the facets they have keys for.

**Why encrypt-then-sign is recommended:**
- Every consumer can verify the signature, regardless of whether they can decrypt any facets
- The signature covers the exact bytes the consumer received -- no reconstruction needed
- Simpler verification: verify first, decrypt second, in that order
- The signature guarantees that the encrypted facets have not been tampered with, even if the consumer cannot read them
- This aligns with the general security principle that authentication should cover the ciphertext, not the plaintext (preventing ciphertext substitution attacks)

**JCS compatibility:** JCS canonicalization treats JWE objects as regular JSON values (objects with `protected`, `recipients`, `iv`, `ciphertext`, `tag` fields). The canonicalization is deterministic over this structure, so signing works without modification.

---

## 5. Key Management for Encrypted Facets

Key management is the hardest part of any encryption system. For UM encrypted facets, the following model is recommended.

### Key identification

Each JWE header includes a `kid` (Key ID) field that identifies which recipient key was used to wrap the CEK. The `kid` value references a key in the recipient's DID Document or a well-known key registry.

### Key source

The recipient's public key for key agreement is found in their DID Document's `keyAgreement` section. This is the standard W3C DID mechanism for advertising encryption keys:

```json
{
  "id": "did:example:doctor",
  "keyAgreement": [{
    "id": "did:example:doctor#key-agree-1",
    "type": "X25519KeyAgreementKey2020",
    "publicKeyMultibase": "z6LSbysY2xFMRpGMhb7tFTLMpeuPRaqaWM1yECx2AtzE3KCc"
  }]
}
```

The issuer encrypting a facet looks up the recipient's DID Document, finds the `keyAgreement` key, and uses it for ECDH-ES key agreement.

### Key rotation

When a recipient rotates their key (generates a new X25519 key pair and publishes the new public key in their DID Document):

1. The issuer detects the key rotation (via DID Document update or notification)
2. The issuer re-wraps the existing CEK for the new public key
3. The old key wrap entry in the JWE `recipients` array is replaced with the new one
4. The ciphertext does not change -- only the key wrap metadata changes
5. The issuer re-signs the manifest (because the JWE metadata changed)

This is the envelope encryption advantage: key rotation is a metadata operation, not a data re-encryption operation.

### Key versioning

Each encrypted facet should include key version metadata so consumers can determine which key version was used. This can be conveyed through:
- The `kid` field in the JWE header (e.g., `did:example:doctor#key-agree-2` for version 2)
- A `key_version` field in the JWE unprotected header
- The DID Document itself, which tracks key versioning through document updates

### Revocation

When access to an encrypted facet should be revoked:
- The issuer removes the revoked recipient's key wrap from the JWE `recipients` array
- The issuer re-encrypts the facet with a new CEK (since the old CEK was known to the revoked recipient)
- The issuer re-signs the manifest
- The revoked consumer retains their copy of the old manifest, but it will expire based on TTL
- New resolutions of the UMID will return the manifest without the revoked recipient's key wrap

This is the fundamental limitation of any document-based encryption: you cannot un-send a document. TTL-based expiration is the primary defense against revoked consumers holding stale-but-decryptable copies.

---

## 6. Challenges and Open Questions

### Payload size

Encrypted facets are larger than their plaintext equivalents. The JWE JSON Serialization adds:
- A base64url-encoded `protected` header (~100-200 bytes)
- A `recipients` array with one entry per recipient (~150-200 bytes each)
- A base64url-encoded `iv` (initialization vector, ~20 bytes)
- Base64url encoding of the ciphertext (~33% size increase over plaintext)
- A base64url-encoded `tag` (authentication tag, ~25 bytes)

For a facet with 500 bytes of plaintext content and three recipients, the encrypted version might be 1,500-2,000 bytes. This is manageable but must be accounted for in the manifest size budget.

### Manifest size limit

The UM specification recommends a 1 MB total manifest size. Encrypted facets consume more of this budget due to encoding overhead. Manifests with many encrypted facets and many recipients could approach this limit. The mitigation is the same as for large plaintext facets: use pointers to reference external data rather than embedding it.

### Offline decryption

A consumer needs the private key locally to decrypt facets. There is no online KMS dependency -- the consumer stores their own private key and performs decryption locally. This aligns with UM's offline-tolerant design but means:
- The private key must be securely stored on the consumer's device
- Key backup and recovery are the consumer's responsibility
- Hardware security modules (HSMs) or secure enclaves are recommended for high-value keys

### Signature interaction

The encrypt-then-sign approach recommended in Section 4 resolves the primary interaction question, but edge cases remain:
- What if a consumer needs to re-encrypt a facet for a different recipient? They must have the issuer's signing key to re-sign, or the manifest must be re-issued by the original issuer.
- What about counter-signatures? If multiple parties sign the manifest, the signing order relative to encryption must be specified.

### Multiple encryption standards

Should UM mandate one encryption method, or support multiple? The internal design principle -- "multiple, flexible ways of handling private data" -- argues for supporting all three methods as opt-in profiles. The recommended approach:
- JWE for confidentiality at rest (primary, recommended for most use cases)
- BBS+ for unlinkable selective disclosure (when the specification matures)
- SD-JWT for JWT ecosystem interoperability (bridge profile)

Each would be identified by a profile marker in the manifest, similar to how signature profiles work in v0.2.

### Backward compatibility

Consumers that do not understand encrypted facets must safely ignore them. This is already guaranteed by UM's forward compatibility rule: unknown facet structures are preserved, not rejected. A consumer that encounters a JWE object where it expected a plaintext facet should treat it as an opaque value it cannot process, log a diagnostic, and continue processing the rest of the manifest.

---

## 7. What Is Revolutionary

### Per-facet encryption in a portable document

No other standard offers per-facet encryption at the envelope level. W3C Verifiable Credentials handle selective disclosure at presentation time -- the credential itself does not contain encrypted claims. DIDComm encrypts entire messages, not individual fields within a document. Solid controls access at the storage level, not within the document. OAuth and OIDC use scoped tokens but do not encrypt the data itself.

Universal Manifest proposes something genuinely new: a single portable document where different data compartments are encrypted for different recipients. The document is self-contained -- it carries the encrypted data, the key metadata, and the consent rules all in one JSON-LD envelope.

### Consent plus encryption: defense in depth

Consent and encryption serve complementary roles:
- **Consent** is a policy signal. It tells honest consumers what they are allowed to do. It is lightweight, easy to process, and universal.
- **Encryption** is a cryptographic barrier. It prevents dishonest consumers from reading data they should not see. It is heavier but mathematically enforceable.

Together, they form defense in depth. A consumer that respects consent rules never even attempts to decrypt facets it is not authorized to see. A consumer that ignores consent rules is stopped by the encryption. Neither mechanism alone is sufficient; together they are robust.

### Multi-recipient per facet

A single manifest can contain facets encrypted for different audiences:
- Your employer sees `professionalCredentials` (encrypted for their key)
- Your doctor sees `medicalHistory` (encrypted for their key)
- Your game platform sees `gameProfile` (encrypted for their key)
- All of them see `publicProfile` (plaintext)

Each recipient resolves the same UMID, receives the same manifest document, but can only read the facets encrypted for their key. The issuer does not need to create separate projections or maintain multiple document versions. One manifest, multiple audiences, cryptographic access control.

### Self-contained document

The manifest carries everything needed for encrypted facet access:
- The encrypted facet data (JWE ciphertext)
- Key identification metadata (`kid` referencing the recipient's DID Document)
- The consent rules governing use of the data
- The issuer's signature over the entire document
- TTL for automatic expiration

There is no external dependency beyond the recipient's own private key and the issuer's public key (for signature verification). No vendor KMS, no proprietary key server, no online decryption service. Standard cryptographic primitives, standard key formats, standard JSON encoding.

---

## 8. Comparison to Other Systems

| System | Approach | UM Difference |
|--------|----------|---------------|
| **W3C Verifiable Credentials** | Selective disclosure at presentation time; the credential itself is not encrypted | UM adds per-facet encryption at rest within the document; the manifest carries encrypted data, not just disclosable claims |
| **DIDComm v2** | JWE for message-level encryption; entire messages are encrypted end-to-end | UM uses JWE for document-level, per-facet encryption; different facets encrypted for different recipients within one document |
| **Solid** | Access control on storage pods; data is protected at the server level | UM carries encryption with the document; privacy travels with the data, independent of where it is stored |
| **OAuth / OIDC** | Scoped tokens control access; data itself is not encrypted | UM encrypts the data itself; access control is cryptographic, not just token-based |
| **Signal Protocol** | End-to-end encryption for messaging sessions | UM encrypts facets within a document, not a real-time communication channel; no session management needed |
| **Age / PGP** | File-level encryption for data at rest | UM provides per-facet granularity within a structured document, not whole-file encryption |

---

## 9. The Path Forward

### Immediate next step

WO-0143 (Private Encrypted Inline Facets vs Projection Model Analysis, NOT_STARTED) will produce the architectural decision on whether and how to add encrypted inline facets to the UM specification. This deep dive provides the research foundation for that decision.

### Recommended architecture

Support all three encryption methods as opt-in layers above the base protocol, each identified by a profile marker:

1. **JWE per-facet encryption** -- the primary method for confidentiality at rest. Recommended for any facet that contains sensitive data and needs to be shared with specific recipients. Uses ECDH-ES+A256KW / A256GCM with X25519 key agreement.

2. **BBS+ selective disclosure** -- for unlinkable presentation privacy. Recommended for scenarios where the holder needs to prove specific facts without revealing the full manifest and without allowing cross-session correlation. Contingent on the W3C specification reaching final Recommendation status and BLS12-381 library maturity.

3. **SD-JWT selective disclosure** -- for JWT ecosystem interoperability. Recommended as a bridge profile for systems that speak JWT natively (OIDC providers, EU eIDAS infrastructure, enterprise federation).

### Design principle

The guiding principle remains: "UM needs multiple, flexible ways of handling private data to remain truly universal." No single encryption method fits all scenarios. The specification should define clean opt-in profiles and let adopters choose the methods appropriate to their trust model, their ecosystem, and their performance requirements.

### What stays the same

- Ed25519/JCS remains the primary signing mechanism
- Consent toggles remain the primary privacy policy mechanism
- The projection model remains a normative approach for simple use cases
- The base specification (v0.1/v0.2) remains encryption-free
- Forward compatibility ensures encrypted facets can be introduced without breaking existing consumers

---

## NotebookLM Video Brief

### L3-10: Facet Privacy — Public, Encrypted, and Selective Disclosure
**Level:** 3 | **Length:** 6 min
**Audience:** Engineers, architects, and security-minded evaluators wanting the complete facet privacy story.

```
FOCUS: How facets work today as plaintext data compartments gated by default-deny consent toggles. The three privacy approaches: projection model (consumer-specific derived manifests), consent-gated access control (policy signals), and encrypted inline facets (cryptographic enforcement). The three encryption methods: JWE per-facet encryption with ECDH-ES+A256KW and X25519 key agreement, BBS+ selective disclosure with BLS12-381 for unlinkable presentation privacy, and SD-JWT for JWT ecosystem interoperability. How encryption interacts with signing: encrypt-then-sign so every consumer can verify the signature regardless of decryption access. Key management: DID Document keyAgreement for key discovery, envelope encryption for efficient key rotation, TTL-based expiration for revocation. What is revolutionary: per-facet encryption in a portable self-contained document where different recipients decrypt different facets from one manifest — something no other standard offers at the envelope level. Consent plus encryption as defense in depth. The path forward: all three methods as opt-in layers above the base protocol.

DO NOT COVER: Do not explain the resolver, portaling, IWPS, or integration lanes. Do not cover the consent model in isolation — that is L3-03. Do not discuss implementation code, TypeScript, or specific library choices. Do not cover the projection model in detail — that is established and documented elsewhere. Stay at the specification architecture level. Do not mention PeerMesh or any runtime.

WHY THIS EXISTS: The definitive explanation of how UM handles facet privacy from plaintext through cryptographic enforcement, covering the full spectrum of privacy mechanisms available to specification adopters.
```
