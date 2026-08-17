# TEST SCENARIO — not a real client

Synthetic test case for the `client-intelligence` skill (round 4 of the deferred
real-scenario tests — see
`.claude/skills/client-intelligence/references/DESIGN-QUESTIONS.md` §11). Models a
~400-orders/day e-commerce store with a support/cart-abandonment problem — deliberately
mirrors the example client profile already in `memory/business.md`. Unlike the clinic
and realty scenarios, this one has real disclosed dollar data on both cost (staff wage)
and revenue (AOV) sides, exercising the full dollar-ROI computation path, and includes
a vague client ask ("something with our reviews") to test that vague requirements get
routed to Missing Information rather than turned into an invented feature.

Caveat: the business is fictional — no real public presence to research. Exercises the
client-supplied-material path and KPI/ROI/ranking/risk methodology, not the public
research sequence itself.

Not a real engagement. Do not add to `memory/clients.md` or
`memory/active-projects.md`. Safe to delete once the skill is validated (ask Amer
first, per the no-delete rule).
