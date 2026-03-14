# MANDATE: Portal Loading Content in Universal Manifest

**Date:** 2026-03-11
**Authority:** CEO
**Priority:** HIGH
**Status:** ACTIVE

## Directive

The Universal Manifest specification MUST support carrying destination-world loading content as part of the portaling flow. When a user initiates a portal jump from World A to World B:

1. World B's manifest (or the portal response) MUST be able to include loading content — visual assets, branding, loading animations, or instructions that World A can display immediately.
2. World A MUST be able to render this loading content while the full portal handshake (manifest transfer, consent checking, avatar loading, IWPS Teleport) completes in the background.
3. The user MUST experience a seamless visual transition — they see World B's loading experience before the technical transport finishes.

## Rationale

- Eliminates the "black screen" gap between leaving one world and arriving in another.
- Creates a branded, immersive transition that feels instant to the user.
- Allows the complex technical handshake (consent verification, asset resolution, signature checking) to happen without the user waiting on a blank screen.
- Aligns with AAA game loading patterns where the next level's content is streamed/displayed during the transition.

## Scope

- This affects the UM specification's portaling model, the metaverse integration lane, and the IWPS alignment.
- A new pointer family or facet type may be needed to carry loading content references.
- The IWPS Query API response already includes a `downloadUrl` field — this could be extended or complemented by UM loading content pointers.

## Expected Deliverables

- Updated metaverse integration lane with loading content pointer/facet definitions.
- Updated IWPS-UM alignment document reflecting this capability.
- Concept integrated into the portaling explainer and relevant vignette briefs.
