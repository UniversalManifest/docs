# Explorer Lane Schema, Content Template, and Hero-Asset Brief System

**Date:** 2026-04-22  
**Status:** Completion report for `WO-0198`

## Purpose

Define the structural schema for the interactive explorer so the UI can be built from stable content primitives rather than one-off prose.

## Lane schema

Each explorer lane must contain:

1. `id`
2. `title`
3. `shortTitle`
4. `summary`
5. `heroAsset`
6. `heroAlt`
7. `scenario`
8. `whyUmFits[]`
9. `whatTravels[]`
10. `deepDive[]`
11. `proofLinks[]`
12. `audienceLinks[]`

## Standard lane layout

### Left rail

- lane title
- short signal/teaser

### Main pane

- hero asset
- exact headline
- short summary
- “why UM fits” list
- “what actually travels” list
- expandable deeper-detail section
- links to proof/spec/supporting audience pages

## Hero-asset brief template

Each lane brief should define:

- lane name
- visual scene
- subject
- receiving surface
- what travels
- what remains authoritative elsewhere
- one visual cue for trust/consent/bounded validity
- candidate existing asset reuse path

## First lane order

1. Metaverse Portaling
2. Avatars and Portable Identity
3. Content and Asset Projection
4. Smart-Glasses Consent
5. Social/Profile Portability
6. Venue and Edge Devices
7. Proof of Personhood
8. Enterprise and Cross-System Permissions

## Relationship to audience pages

Explorer lanes are use-case-first.
Audience pages are ecosystem-first.

The same lane can feed multiple audience pages, but the lane remains the portable conceptual unit.

## Implementation asset

The structured explorer data should live in a reusable site data module so later routes and pages can consume it without copy divergence.
