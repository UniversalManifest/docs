# Agent Prompt — Universal Manifest Home-Cluster IA Review

Use this prompt when asking another agent to review the Universal Manifest homepage information architecture, sitemap, and copy structure.

The goal is **not** to implement the site. The goal is to determine whether the current information architecture is actually good, where it is weak, and how it should change before more homepage rewriting happens.

---

## Prompt

You are reviewing the proposed public information architecture for the Universal Manifest project.

Your task is to evaluate whether the proposed sitemap and page structure are actually optimized for human comprehension, use-case discovery, audience routing, and standards discoverability.

Do **not** implement the website.
Do **not** create mockups, presentations, landing pages, or visual redesigns.
Respond in **plain markdown only**.

### Project context

Universal Manifest is a portable document format for carrying identity references, claims, consents, policies, pointers, and related state between compatible systems.

The public site currently needs a better homepage and better information architecture, but the current sprint is **copy-first and sitemap-first**.

Important:

- treat the sitemap as the proposed source of truth for the next phase
- do not let any already-built site implementation override the sitemap review
- review the structure as if the team is deciding what the site *should be*, not defending what has already been built

The current working rule is:

- no more homepage or public-site rewriting until the sitemap and copy architecture are approved
- the global public navigation is approved and should stay limited to:
  - `Home`
  - `Latest Spec`
- deeper explanation should happen inside a `Home` cluster rather than on one overloaded homepage
- `/explorer/` should use the approved visible label `Scenario Explorer`; do not evaluate or recommend the bare visible label `Explorer` unless explicitly discussing a regression
- audience-specific pages should exist, but one layer down from the homepage
- the homepage should stay low-noise and should not collapse into a giant explanation of the whole project
- the latest spec must remain highly discoverable without dominating the entire public experience
- the review should prioritize first-time human understanding over internal architectural elegance
- standalone venue/spatial framing is not approved; `venues` is too narrow, and `spatial` is covered by the metaverse / digital-world portaling lane
- the EU digital identity / SSI path is confirmed and must be grounded in public standards, specifications, architecture references, or public implementation direction
- peer-to-peer crypto payment framing should stay abstract and must not name a specific chain, offer protocol, wallet provider, or payment rail in public lane copy unless explicitly approved
- private facets, encrypted data, and attested identifier/control binding are cross-cutting material. They should strengthen the credential/verifier, privacy, how-it-works, and standards-fit surfaces without reopening the approved seven-lane Scenario Explorer structure unless a later IA decision explicitly does so
- privacy/encryption copy should distinguish the normative projection model from optional encrypted inline facets
- identifier/control binding copy should distinguish v0.2 Tier 1 `claims[].claimProof` / `identity.crossDidBinding` support from deferred stronger cryptographic or multi-party binding tiers
- canonical public reader pages should include a bottom-page link to download or view their markdown/source version
- future site updates must keep markdown/source, rendered HTML, machine-readable files, and agent-facing variants from drifting

### Files to review

Use these files as source of truth:

- `"/Users/grig/work/repo/universalmanifest/docs/HOME-CLUSTER-SITEMAP.md"`
- `"/Users/grig/work/repo/universalmanifest/docs/README.md"`
- `"/Users/grig/work/repo/universalmanifest/README.md"`
- `"/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md"`
- `"/Users/grig/work/repo/universalmanifest/docs/DOMAIN-ARCHITECTURE.md"`
- `"/Users/grig/work/repo/universalmanifest/docs/STATE-OF-THE-PROJECT.md"`
- `"/Users/grig/work/repo/universalmanifest/docs/COMPREHENSIVE-PROJECT-PROPERTIES-AND-SURFACES-MAP.md"`

Implementation/background context may be read if needed, but it must not override the sitemap:

- `"/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/why-um.md"`
- `"/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/one-pager.md"`
- `"/Users/grig/work/repo/universalmanifest/site/src/content/docs/about/standards-landscape.md"`
- `"/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/did-vc.md"`

### What to evaluate

Evaluate the sitemap against these questions:

1. Does the top-level IA make sense for a first-time human reader?
2. Is the homepage being asked to do too much or too little?
3. Are the `Home` cluster pages the right pages?
4. Is the order of the `Home` cluster correct?
5. Are any pages missing?
6. Are any pages unnecessary?
7. Are any pages at the wrong level of the hierarchy?
8. Are the audience pages in the right place in the structure?
9. Is the relationship between `Home`, `Latest Spec`, `Use Cases`, `Scenario Explorer`, `How It Works`, and `Standards Fit` clear and defensible?
10. Does the IA support the project's strategic audiences, especially:
    - metaverse / portaling / digital worlds
    - EU self-sovereign identity / digital identity
    - platform builders and interoperability evaluators
    - credential issuers and verifiers
    - agent builders / agent transaction flows
    - payment and wallet builders for peer-to-peer crypto payments
    - privacy, consent, private facets, encrypted data, and attested identifier/control binding as cross-cutting trust/privacy themes
11. Is the spec sufficiently discoverable without dominating the whole site?
12. Is the structure scalable if more use cases and audiences are added later?
13. Are the page labels themselves understandable, or are any of them too internal, abstract, or vague?
14. Is the distinction between:
    - `Use Cases`
    - `Scenario Explorer`
    - `How It Works`
    - `Standards Fit`
    
    clear enough for a first-time reader?
15. Does the sitemap create a sensible progression from:
    - first-contact explanation
    - to concrete scenarios
    - to conceptual understanding
    - to standards evaluation
16. Does the sitemap create a reusable process for markdown/source and rendered-site parity?
17. Are machine-readable and agent-facing surfaces treated as linked variants that need consistency checks?

### What to look for specifically

Look for:

- page overload
- missing explanation layers
- duplicated page roles
- unclear transitions between levels of understanding
- audience clutter on the homepage
- misplaced standards material
- misplaced tool/proof surfaces
- confusion between `/explorer/` as the `Scenario Explorer` and `/tools/concept-explorer/` as a separate tool surface
- accidental reintroduction of venue/spatial as approved top-level scenario framing
- payment examples that imply one required blockchain, intermediary, provider, or rail
- EU digital identity claims that are not grounded in public standards or public implementation direction
- privacy/encryption copy that treats encrypted inline facets as mandatory core behavior instead of optional guidance
- identity-binding copy that overclaims attested cross-DID binding as absolute proof of ownership/control
- missing surfacing for `claimProof`, proof-of-personhood DID binding examples, private facets, or encrypted inline facets in the right public surfaces
- missing markdown/source download links or missing source-fidelity process
- rendered-page and markdown/source drift risks
- machine-readable and agent-facing variant drift risks
- IA choices that sound good internally but would confuse a first-time visitor
- page names that are accurate internally but weak externally
- places where a first-time reader would not know where to click next
- places where strategic audiences might still feel under-served
- places where the information architecture is elegant on paper but weak in real user flow

### Additional review instructions

- Be willing to say the sitemap is wrong.
- Prefer clarity over diplomacy.
- If you think a page should be renamed, say so directly.
- If you think two pages should merge, say so directly.
- If you think a page should move up or down a level, say so directly.
- Do not protect prior work just because it exists.

### Required output format

Respond using exactly this structure:

#### 1. Overall verdict

One short paragraph answering:
- Is this information architecture strong, weak, or mixed?
- Is it ready for copy work, or does the structure still need changes first?

Then include a score out of 10 for:
- clarity
- navigability
- audience coverage
- scalability

#### 2. What is working

- concise bullets

#### 3. What is not working

- concise bullets
- focus on structure, not visual design

#### 4. Structural risks

- list the biggest IA mistakes or likely failure points

#### 5. Recommended sitemap changes

For each recommended change, state:
- what to change
- why
- what problem it solves

Separate changes into:
- required changes before copy work
- optional improvements after copy work

#### 6. Missing pages or unnecessary pages

List:
- pages that should be added
- pages that should be removed or merged
- pages that should move to a different level

Also include:
- page names that should be renamed

#### 7. Final recommendation

Choose one:

- `APPROVE SITEMAP AS-IS`
- `APPROVE WITH CHANGES`
- `DO NOT APPROVE YET`

Then explain why in one short paragraph.

### Important constraints

- Do not redesign the UI.
- Do not propose component libraries.
- Do not write homepage copy.
- Do not create new web pages or mockups.
- Do not drift into visual design commentary.
- Stay focused on sitemap, hierarchy, page roles, and reader flow.

---

## Intended use

This prompt is meant to be sent to multiple agents so their IA judgments can be compared side by side before the next copy pass begins.
