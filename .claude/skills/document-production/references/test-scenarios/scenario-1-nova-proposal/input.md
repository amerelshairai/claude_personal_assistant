# Scenario 1 — input

Not new synthetic input — produces an actual client-facing proposal for Nova Home
Goods' abandoned-cart recovery flow, pulling from every prior stage's real
artifacts, same discipline as `project-planning`'s own test.

## Source artifacts
- `client-intelligence`'s Nova package: business context, positioning.
- `automation-architecture/references/test-scenarios/scenario-1-nova-cart-recovery/`:
  the design (diagram, WHY, deliverables shape).
- `business-analysis/references/test-scenarios/scenario-4-nova-cart-recovery/`:
  **verdict GO**, price anchor ~$500-650 (ASSUMED — no client agreement yet).
- `project-planning/references/test-scenarios/scenario-1-nova-cart-recovery-plan/`:
  deliverables, milestones (scope locked → build complete → delivered → support
  window starts).
- `memory/business.md`: payment terms (deposit-based, governed by contract, not a
  fixed split) and support period (3-5 days free bug-fix window).

## What this tests
- Correct exclusion of internal cost/margin/effort-hours from a client document.
- Whether a *range* ($500-650) from business-analysis gets handled correctly in a
  document meant to state one Investment figure — this needs a decision, not a
  silent pick.
- Whether Payment Terms and Privacy & Data Handling (Amer's explicit additions to
  the template) actually get populated with real content, not left as
  placeholders.
- The Level 2 boundary: produced and marked READY FOR REVIEW, never sent.
