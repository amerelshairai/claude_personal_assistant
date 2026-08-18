# Scenario 4 — input

Closes the pipeline-order gap `project-planning`'s scenario 1 found: this feature
(Nova Home Goods, abandoned-cart recovery) reached a technical design and a plan
before `business-analysis` ever ran a viability/pricing pass on it. Running it now,
using only what prior stages already established — no new synthetic facts invented.

## What's different from Nova's other business-analysis test (loyalty-points)
- **No price has been discussed with the client at all yet** — unlike loyalty
  points, where $600 was already agreed before discovery. There's no "client
  anchored too low" conflict to reconcile here; this is a first pricing pass, not
  a renegotiation.
- **Effort is smaller**: 13h raw (automation-architecture), vs. loyalty-points'
  eventual ~17h.
- **The build already includes its own risk mitigation** — the discount-cap
  pause/notify gate — resolved before this pass, not something business-analysis
  needs to catch.
- Client relationship is established (multiple prior engagements modeled across
  test suites), unlike TechFit Gym, a new prospect in that scenario.

## Reused, not re-derived
- Effort: Research 2h (ASSUMED/Low confidence) + Build 10h + Admin 1h = 13h raw,
  from `automation-architecture/references/test-scenarios/scenario-1-nova-cart-recovery/`.
- Financial context: $38,250/day raw exposure ceiling (never a promised recovery),
  from `client-intelligence`'s Nova package.
- Risks already identified at the design stage: technical (checkout-signal
  uncertainty), financial (discount cap — mitigated), adoption/reputation, vendor
  cost scaling, compliance (consumer-protection rules, unconfirmed).
