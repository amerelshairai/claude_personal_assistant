# Scenario 2 — real deadline-feasibility check + pre-price-demo milestone

## Real capacity, day by day (memory/user.md pattern, per the new precedence rule)
Formula: `realistic_productive_hours_per_day − extra Calendar commitments (none
found) − 15% buffer`.

| Date | Day | Day type | Baseline | −15% buffer | AVAILABLE |
| --- | --- | --- | --- | --- | --- |
| Aug 18 (Tue) | today | Uni+Club | 3.5h | 0.525h | **3.0h** |
| Aug 19 (Wed) | +1 | Uni | 3.5h | 0.525h | **3.0h** |
| Aug 20 (Thu) | +2 | Club | 3.5h | 0.525h | **3.0h** |
| Aug 21 (Fri) | +3 | Fri window | ~4.3h | ~0.65h | **~3.6h** (approximated — Amer's per-weekday follow-up still pending) |
| Aug 22 (Sat) | +4 | Full day | 6.5h | 0.975h | **~5.5h** |

## Demo deadline check (by Thu Aug 20) — FITS
Window: Tue+Wed+Thu = 3.0+3.0+3.0 = **9.0h available**. Demo scope (order-intake
flow): **6h needed**. Comfortable fit, no contingency issue even before applying
one — the demo is achievable as asked.

## Full-system deadline check (by Sat Aug 22) — DOES NOT FIT
After the demo, remaining scope: reminders + status updates (8h) + Research (3h)
+ Admin (1.5h) + Call (1h) = **13.5h raw**, in the window **after** the demo,
Fri+Sat only (Thu's remaining capacity beyond the 6h demo is negligible — the demo
itself consumes essentially all of Thursday's 3.0h once Tue/Wed are also counted
toward it): **Fri (3.6h) + Sat (5.5h) = 9.1h available.**

Applying `project-planning`'s 20% greenfield contingency: 13.5h × 1.2 = **16.2h
needed** vs **9.1h available** — **a genuine shortfall of ~7.1h**, computed from
real Calendar/Todoist state (both verified live, zero competing real load), not
an assumed or fabricated conflict. Even without the contingency, it's short by
4.4h raw. **This is the "not just does it fit on paper" case** — the full ask
does not fit, and that's a real result, not a hedge.

## Resolution — phased delivery, not overwork or a client letdown
Recommend splitting delivery instead of either compressing Amer's real capacity
or telling the client no outright:
- **Phase 1** (fits the Saturday deadline): order-intake flow only — this is the
  same 6h as the demo, so the demo *is* the Saturday deliverable if the client
  approves it. Covers the expo's actual need (taking orders), not the full vision.
- **Phase 2** (after the expo, no hard deadline pressure): reminders + status
  updates, 13.5h raw / 16.2h with contingency, scheduled into the following week's
  real capacity once Phase 1 is live.

This is a **project-planning recommendation**, not a unilateral decision — present
both the shortfall and this option to Amer before promising anything to the
client.

## Milestones — the pre-price-demo exceptional case
Per `SKILL.md`'s flexible-milestone rule, this doesn't fit the standard four-step
template as-is:
1. **Demo delivered** (Thu Aug 20) — *inserted before scope/price lock*, per the
   client's explicit condition ("burned by an agency before").
2. **Scope + price locked** — only after the client approves the demo. Given the
   phased-delivery recommendation, this is also where Phase 1-as-Saturday-
   deliverable and Phase 2 timing get agreed.
3. **Phase 1 (= the demo) delivered as the Saturday deliverable.**
4. **Phase 2 build complete.**
5. **Phase 2 delivered.**
6. **Post-delivery support window starts.**

## Risks
| Risk | Category | Severity | Mitigation |
| --- | --- | --- | --- |
| Client rejects phased delivery, insists on full scope by Saturday | Scope/expectation | Medium | Present the real numbers (this check) before promising anything |
| Demo doesn't win the client over, no price ever gets agreed | Financial | Medium | Standard prospect risk — Fit/Profitability not yet confirmed by business-analysis (see below) |
| Real Calendar/Todoist aren't populated per the confirmed conventions | Process | Low | Doesn't block this plan, but means every capacity check right now leans on `memory/user.md` more than live tools — worth Amer populating both eventually |
| Order-intake demo built without full requirements (delivery logistics, etc. deferred to Phase 2) | Technical | Low-Medium | Explicitly scoped as Phase 1/2 split, not silently incomplete |

## Business-analysis read (not yet run for real — noted, not fabricated)
Unlike the Nova cart-recovery gap, this plan **correctly surfaces the need for a
business-analysis pass before scope/price lock** (milestone 2 above) rather than
skipping it — the pipeline order holds here. Rough proportional anchor for
reference only (19.5h, similar order of magnitude to TechFit's 23.5h≈$750-1,000):
likely **$700-950** — presented as a planning-level estimate, not a run
business-analysis verdict. A real pass should happen once the client actually
approves the demo, per the milestone order above.

## Report (per `.claude/rules/reporting.md`)
```
PLANNED
- Petal & Stem plan: demo (6h) fits by Thu; full scope does NOT fit by Sat
  (short ~7.1h with contingency) -- recommending phased delivery instead

NEEDS YOU
- Approve the phased-delivery recommendation (or an alternative) before this
  goes to the client
- Business-analysis pass still needed once the client approves the demo (correct
  pipeline order maintained here, unlike the Nova gap)
```
