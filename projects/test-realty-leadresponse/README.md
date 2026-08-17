# TEST SCENARIO — not a real client

Synthetic test case for the `client-intelligence` skill (round 3 of the deferred
real-scenario tests — see
`.claude/skills/client-intelligence/references/DESIGN-QUESTIONS.md` §11). Models a
small real-estate brokerage with a lead-response-delay problem. Chosen to contrast
with `test-clinic-noshow`: this client has a *measured* baseline (rough CRM export)
but *no* dollar/commission data at all, exercising the ROI methodology's
time/effort-only branch, and has no health-data angle, to confirm that risk escalation
correctly does not fire for a non-health client.

Caveat: the business is fictional — no real public presence to research. Exercises the
client-supplied-material path and KPI/ROI/ranking/risk methodology, not the public
research sequence itself.

Not a real engagement. Do not add to `memory/clients.md` or
`memory/active-projects.md`. Safe to delete once the skill is validated (ask Amer
first, per the no-delete rule).
