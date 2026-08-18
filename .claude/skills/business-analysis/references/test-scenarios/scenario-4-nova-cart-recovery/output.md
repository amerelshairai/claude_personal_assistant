# Scenario 4 — business-analysis walkthrough: Nova Home Goods cart-recovery

## Cost model
| Layer | Contains |
| --- | --- |
| One-time | Research 2h (ASSUMED/Low) + Build 10h + Admin 1h = **13h raw**, from automation-architecture |
| Recurring | WhatsApp API usage at ~850/day abandoned-cart volume — likely toward the higher end of the standard $60-80/mo range, per automation-architecture's own flag |
| Maintenance | Standard 3-5 day free bug-fix window post-delivery |
| Amer's time | 13h raw / ~15.6h with project-planning's 20% greenfield contingency — the real constraint, no internal $/hour |

## Viability check — reasoned fresh for this case, not copied from the other Nova test

**1. Capacity — UNCONFIRMED, not blocking.** No live `time-orchestration` read was
run against Amer's real current load (this test suite doesn't touch real Todoist/
Calendar). Absence of a check is not the same as a failed check — recommend
confirming before scheduling, but it doesn't hold up the GO/NO-GO call itself.

**2. Profitability — this is a genuinely different situation from TechFit or
Nova's own loyalty-points case, and needs different reasoning.** In both prior
tests, a price already existed and the question was whether it matched the
effort. Here, **no price has been discussed at all** — there's no client anchor to
reconcile against, so there's no "too low, needs renegotiation" conflict to find.
Using effort-proportionality against `memory/business.md`'s stated range ($200
minimum for a simple build, $750-1,500 average, $5,000 advanced) and the two
other Nova/TechFit reference points on this same scale (23.5h ≈ $750-1,000 range;
17h ≈ $600 range, both from prior tests): 13h reasonably anchors around
**~$500-650**. This is a recommended starting point for the pricing-calculator
conversation with the client, **ASSUMED, not agreed** — business-analysis's role
here is proposing where to start, not confirming a number that already exists.

**3. Risk — reasoned specifically, not assumed to inherit TechFit's rule.**
TechFit Gym's build auto-elevated to Medium-High data risk because it pushed a
**payment link into the client's actual billing system**. This build is
different: the discount is a value included in a WhatsApp message, applied by the
customer through Nova's normal checkout — **it doesn't touch or integrate with
Nova's payment/billing system directly**. The payment/billing auto-elevation rule
(`SKILL.md` § Risk categories) is about builds that touch those systems, not any
build that happens to involve a monetary value. **This one stays at the general
default, not elevated** — a deliberate judgment call, not a mechanical rule
application, since the situations look superficially similar but aren't the same
underlying risk. Overall risk: **Medium** — technical (checkout-signal
uncertainty) and vendor (cost scaling) are the live items; financial risk is
already mitigated by the pause/notify gate; compliance (consumer-protection
rules) stays unconfirmed but not blocking, consistent with how client-intelligence
already tiered it as "helpful," not essential.

**4. Fit — PASS, stronger than TechFit's case.** Established client relationship,
directly matches Amer's stated strongest-fit segment (e-commerce/support per
`memory/business.md`), and reuses infrastructure/context Amer already has from
Nova's other work. No reputation risk from unfamiliarity.

## Verdict: GO
No criterion fails. This is not a renegotiation case (nothing to reconcile against
an existing price) and not a risk-elevated case (the payment/billing rule doesn't
actually apply here on inspection) — genuinely a clean recommendation to proceed,
price it in the standard way, and confirm capacity before scheduling.

## Report (per `.claude/rules/reporting.md`)
```
COMPLETED
- Nova cart-recovery viability check: GO. Recommended price anchor ~$500-650
  (ASSUMED, not yet discussed with client). Risk: Medium, not elevated -- payment/
  billing rule doesn't apply (discount is message content, not a billing-system
  touch). Capacity unconfirmed, not blocking -- confirm via time-orchestration
  before scheduling.

CHANGED
- project-planning's Nova cart-recovery plan can now drop its "High severity,
  don't execute" process-risk entry -- the missing business-analysis pass is
  resolved
```
