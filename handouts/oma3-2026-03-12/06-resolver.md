# 06 -- The Resolver: How Manifests Are Found

---

## The Analogy

DNS resolves domain names to IP addresses. You type `example.com` into a browser, and DNS tells the browser which server to contact. DNS does not host websites. It just connects names to locations.

The Universal Manifest **resolver** works the same way. You send a **UMID** to the resolver, and it tells you where to find the manifest. The resolver does not store identity data (for redirect records). It does not verify signatures. It does not enforce consent. It is a thin lookup service -- a phone book for manifests.

---

## Why

A portable document needs a way to be found. If System A creates a manifest and System B needs to read it, System B needs a standard way to look it up. Without a resolver, every pair of systems would need to agree on where manifests are stored -- recreating the point-to-point integration problem that UM was designed to solve.

## What

The resolver at **myum.net** is a public lookup service. Any system with a UMID can resolve it to a manifest in one HTTP call. No authentication, no API key, no session. Just a GET request.

The resolver is defined at the specification level. myum.net is the reference deployment. Any organization can run a conformant resolver for their own ecosystem, just as anyone can run their own DNS server.

## How -- The Resolution Flow

```
Consumer                     myum.net Resolver                 Canonical Source
   |                              |                                  |
   |  GET /urn:uuid:abc-123       |                                  |
   |----------------------------->|                                  |
   |                              |                                  |
   |                              |  Look up UMID in registry        |
   |                              |                                  |
   |  307 + Location: {url}       |                                  |
   |<-----------------------------|                                  |
   |                              |                                  |
   |  GET {url}                   |                                  |
   |------------------------------------------------------------>   |
   |                              |                                  |
   |  200 + manifest JSON         |                                  |
   |<------------------------------------------------------------|  |
   |                              |                                  |
   |  Validate: TTL, signature,   |                                  |
   |  consent, structure          |                                  |
```

### The four possible outcomes

| Response | Meaning | What the consumer does |
|----------|---------|----------------------|
| **307 Temporary Redirect** | UMID found. Follow the `Location` header to the manifest's canonical source. | Fetch the manifest from the redirect URL. |
| **200 OK** | UMID found. The manifest is returned directly in the response body. | Use the manifest. |
| **404 Not Found** | UMID is not registered. | The manifest does not exist or was never published. |
| **410 Gone** | UMID was registered but has been revoked. | The manifest should not be used. |

### Why 307 (not 301)

The resolver uses 307 Temporary Redirect deliberately. Unlike 301 (Permanent), 307 tells consumers that the resolver is the authoritative lookup point and the canonical source URL may change. Issuers can update their resolver registration to point to a new location at any time. The UMID never changes.

### Consumer-side validation

The resolver's job ends at delivery. After receiving a manifest, the consumer is responsible for:

1. **TTL check:** Is the current time before `expiresAt`? If expired, reject.
2. **Signature verification:** Does the Ed25519 signature verify? (Required for v0.2.)
3. **Consent check:** Does the consent array allow the consumer's intended use?
4. **Structure validation:** Does the manifest conform to the expected schema?

### Caching

Successful responses include `Cache-Control: public, max-age=60` and an ETag. Consumers can use `If-None-Match` for efficient polling -- if the manifest has not changed, the resolver returns `304 Not Modified` with no body, saving bandwidth.

### Who owns the data

The manifest issuer owns the data. Always. The resolver stores only the mapping: "this UMID lives at this URL." If the issuer moves to a new host, they update the resolver registration. The UMID stays the same. There is no vendor lock-in.

---

*Next: [07 -- IWPS + UM](07-iwps-integration.md) explains how Universal Manifest integrates with the Inter-World Portaling Standard.*
