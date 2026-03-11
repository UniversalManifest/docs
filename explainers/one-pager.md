# Universal Manifest -- One-Pager

## What it is

Universal Manifest (UM) is a portable document format for sharing identity, credentials, and preferences between systems. Think of it as a Swiss Army Knife for personal data: one compact, standardized package that carries everything a receiving system needs to know about a person, device, or organization -- without requiring that system to build a custom integration for every data source it talks to.

## The problem it solves

Today, every pair of systems that needs to exchange information about a user invents its own format. Your social profile, your login credentials, your device registrations, your privacy preferences -- they all live in different shapes, in different places, with no common structure. The result is a mess of one-off integrations, duplicated data, and fragile connections that break whenever one side changes. Worse, your privacy preferences from one system are invisible to the next, so consent decisions don't travel with you.

## How it works

A Universal Manifest is a JSON-LD document with a simple structure. At its core, it says: *here's who this is about* (the subject, identified by a DID or URI), *here's when this information is valid* (issued and expiry timestamps), and *here's what you need to know* (organized into sections).

Those sections work like the tools on a Swiss Army Knife. **Facets** are fold-out compartments, each carrying a specific slice of data -- a public profile, a device registration, a venue policy. **Pointers** are like business cards with URLs: instead of copying someone's entire profile into the manifest, you include a link to where that data lives authoritatively. **Consents** are the locks on each compartment -- they follow a default-deny model, meaning nothing is shared unless the user has explicitly said "yes."

Every manifest has a built-in expiry date. Systems that receive a manifest must check the validity window and reject it once it's expired. This makes UM safe for local-first, offline-tolerant environments: you can cache a manifest on a device with limited connectivity and trust that it will stop being valid on its own, without needing a revocation check.

## Who it's for

UM is designed for three audiences. **Developers** get a well-specified format with JSON Schema validation, conformance fixtures, runnable code examples, and a TypeScript reference implementation. **Businesses** get a standard that reduces integration cost and carries privacy consent natively. **Individuals** get a format that puts them in control -- their manifest, their permissions, their data.

## What it enables

- A freelance artist's portfolio, credentials, and display preferences traveling with them to any venue or gallery
- A smart glasses layer that respects bystanders' recording-consent preferences in real time
- A proof-of-personhood credential that works across multiple verification providers
- Portable user profiles that move between social platforms without re-entering data
- Offline device enrollment at edge locations with no internet connectivity
- Cross-platform gaming profiles that carry achievements and identity between worlds

## Where to start

Explore the [v0.1 specification](../../spec/v0.1/README.md) for the full technical details. Run the [code examples](../../examples/code/README.md) to see manifests created, validated, and consumed in minutes. Visit [universalmanifest.net](https://universalmanifest.net) for the documentation site, or look up any manifest by its UMID at [myum.net](https://myum.net).
