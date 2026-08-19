# Scenario 2 — input

Real numbers pulled from prior test artifacts, not invented. Every formula below
must be independently checkable, per Amer's instruction to verify the math is
actually correct.

## Source figures (all previously established, not new)
- 400 completed orders/day (measured), AOV $45 (measured) —
  `client-intelligence`'s Nova package.
- Cart abandonment rate: 68% (measured, storefront analytics).
- `business-analysis` scenario 4 verdict: **GO**, price anchor **$500-650**
  (ASSUMED — not yet confirmed by Amer, per the new pricing hard rule).
- Ongoing cost: $60-80/month (standard range from `business-analysis`'s
  methodology, likely toward the higher end given Nova's volume).
- Effort: 13h raw / 15.6h with 20% contingency (`automation-architecture` +
  `project-planning`).
- Target margin: 70-80% net, ~35-40% net to Amer after partner split
  (`memory/business.md`) — no internal $/hour rate exists, so margin is a
  judgment call, not a computed percentage.

## What this tests
- Whether the checkout-starts / abandoned-carts / exposure-ceiling arithmetic is
  actually correct, shown as checkable formulas, not just restated conclusions.
- Whether annualizing to a 12-month figure is done on a defensible basis (days/
  week) rather than a blind ×365.
- Whether the "never invent a recovery rate" discipline holds even when asked to
  build a real workbook with real formulas — the temptation to add an illustrative
  "if you recover X%" table is real here, and should be resisted or explicitly
  reasoned about, not silently included.
- Whether the internal-margin sheet correctly avoids inventing a $/hour rate to
  produce a fake-precise margin percentage.
- Whether the same "[AMER TO CONFIRM]" pricing rule from the proposal test holds
  in this different document type too.
