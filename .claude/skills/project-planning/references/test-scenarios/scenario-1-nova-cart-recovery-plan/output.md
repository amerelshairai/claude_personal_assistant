# Cross-stage consistency check (done first, per Amer's priority)

## Finding 1 — RESOLVED 2026-08-18: business-analysis pass now run
`business-analysis` scenario 4 (`.claude/skills/business-analysis/references/
test-scenarios/scenario-4-nova-cart-recovery/`) closed this gap: **verdict GO**.
Recommended price anchor **~$500-650** (ASSUMED — not yet discussed with the
client, since none existed before this pass). Risk stays **Medium, not elevated**
— reasoned specifically that the payment/billing auto-elevation rule doesn't apply
here (the discount is message content, not a touch on Nova's actual billing
system, unlike TechFit Gym's payment-link case). Capacity remains unconfirmed
(no live `time-orchestration` read in this test suite) but doesn't block the GO —
confirm before scheduling, not before deciding.

This was a genuine pipeline-order problem, now closed: the intended hand-off is
client-intelligence → business-analysis (price/viability) → automation-architecture
(technical design) → project-planning (execution plan). Cart-recovery skipped the
second step; it's now been run, after the fact but before this plan is treated as
execution-ready.

## Finding 2 — the discount-cap gate carries forward correctly
Automation-architecture's resolved flag (auto-send under a pre-approved discount
cap, pause + notify if a computed value would exceed it — nodes M/N in the design)
**does** show up correctly below: as a Build sub-task (implementing the gate
itself) and as a risk-register entry (financial risk, now mitigated). No mismatch
here — the fix from that stage propagated cleanly into this one.

## Finding 3 — real gap: client-intelligence's missing-info items don't cleanly map to this specific feature
Client-intelligence flagged 4 missing-info items for Nova generally: ticket-type
breakdown, operating days/week, the "reviews" clarification, and consumer-
protection/compliance rules. Of these, only **operating days/week** and
**compliance rules** are actually relevant to cart-recovery specifically — the
other two (ticket breakdown, "reviews") belong to the support/self-service
opportunity, a different piece of Nova's package. Carrying all 4 forward into this
plan's "Requires client" bucket without filtering would incorrectly bloat this
plan's scope with questions that don't block *this* build. **Filtered below to the
2 that actually apply.**

## Finding 4 — effort figure is otherwise consistent
Automation-architecture's ~13h (Research 2h ASSUMED/Low + Build 10h + Admin 1h) is
carried forward unchanged below — no discrepancy in the number itself, only in the
missing upstream viability check (Finding 1).

---

# Project Plan — Nova Home Goods — Abandoned Cart Recovery

## Objective
Build the abandoned-cart recovery flow recommended in Nova's client-intelligence
package. Targets the $38,250/day raw exposure ceiling — **stated as a ceiling, not
a promised recovery**, consistent with business-analysis's and client-
intelligence's discipline on this number. Business-analysis: **GO**, price anchor
~$500-650 (ASSUMED, pending client conversation).

## Scope
Order-status check → delayed recovery message → capped-discount incentive message
→ outcome logging, per automation-architecture's design.

**Out of scope**: Nova's support self-service opportunity (different feature,
different plan), the unresolved "reviews" ask (still unscoped, per client-
intelligence), and actually agreeing the price with the client (Amer's call, per
business-analysis's hard boundary — the ~$500-650 figure is a recommendation, not
an agreed number).

## Deliverables
- Working n8n workflow matching the automation-architecture design (diagram +
  nodes A–N).
- Outcome log accessible for future ROI measurement.
- Short handover note (per Amer's diagram-first documentation style).

## Requirements
Storefront checkout-status signal (webhook or pollable query — **not confirmed**,
automation-architecture flagged this ASSUMED/Low confidence), WhatsApp Business API
access, a discount-cap value Amer sets before build starts.

## Work breakdown (1h minimum granularity)
| # | Task | Bucket | Effort | Dependency |
| - | --- | --- | --- | --- |
| 1 | Confirm storefront checkout-status signal (webhook vs. polling) | Requires client | 2h (Research, ASSUMED/Low confidence) | None |
| 2 | Build checkout-status trigger + query node | Claude-executable | 3h | Task 1 |
| 3 | Build wait-delay + recovery message #1 flow | Claude-executable | 3h | Task 2 |
| 4 | Build discount-cap check + pause/notify gate + message #2 flow | Claude-executable | 3h | Task 3, discount cap value from Amer |
| 5 | Build outcome logging | Claude-executable | 1h | Task 4 |
| 6 | Write handover documentation | Claude-executable | 1h | Task 5 |

Raw total: **13h** (matches automation-architecture exactly).

## Estimated effort with contingency
Treated as a **greenfield build** (no existing cart-recovery automation to extend)
→ **20% contingency** per `project-planning`'s methodology: 13h × 1.20 = **~15.6h
planned**.

## Estimated duration
Depends on Nova's operating days/week (missing — see Requires client below) and
Amer's available capacity that week, via `time-orchestration`. Not computed here
without that input.

## Milestones
Standard template applies: scope locked (technical scope is locked; **price still
needs Amer to actually agree it with the client** — the ~$500-650 figure is a
recommendation, not a milestone-clearing event on its own) → build complete →
delivered → post-delivery support window starts. No exceptional pre-price demo
milestone needed for this client (existing relationship, not a new prospect).

## Risks
| Risk | Category | Severity | Mitigation |
| --- | --- | --- | --- |
| Storefront has no clean checkout-abandonment signal | Technical | Medium | Task 1 confirms before Build starts |
| Discount cap set too high, eroding margin | Data (financial) | Medium | Mitigated — pause/notify gate (Task 4), not silent auto-send |
| Feels like spam to price-sensitive customers | Adoption | Low-Medium | Two-message cap, stop on response (per automation-architecture design) |
| WhatsApp API cost scaling with ~850/day volume | Vendor | Medium | Noted in business-analysis's cost model (scenario 4) — likely toward the higher end of the standard $60-80/mo range |
| Automated messaging/discount offers may hit consumer-protection rules | Compliance | Low-Medium | Requires client answer — see below |
| Discount is message content, not a billing-system touch | Data (financial) | Not elevated | Confirmed by business-analysis (scenario 4) — reasoned distinct from TechFit Gym's payment-link case, doesn't trigger the payment/billing auto-elevation rule |

## Required client inputs (filtered to what actually blocks this build — Finding 3)
1. Storefront checkout-status signal confirmation (also Task 1).
2. Operating days/week (needed for duration estimate and compliance context).
3. Applicable consumer-protection/messaging-consent rules for automated cart offers.

## Required Amer inputs
- Discount-cap value, before Task 4.
- Agree a price with the client, using the ~$500-650 anchor from business-analysis
  (scenario 4) as a starting point, not a fixed number.
- Confirm capacity for this work via `time-orchestration` before scheduling
  (business-analysis flagged this unconfirmed, not blocking the GO itself).

## Claude-executable work
Tasks 2, 3, 4 (build), 5 (logging), 6 (docs) — all Level 1, execute-then-report.
Task 1 is research but depends on a client answer, so it's blocked, not purely
Claude-executable.

## Approval points
- Deploying the finished workflow to production — Level 3, per
  `automation-architecture`'s permissions (`publish_workflow`).
- Any price/scope conversation with the client — Level 2 at most, per
  `business-analysis`'s hard boundary.

## Deadline analysis
No deadline was ever stated for this feature in any prior stage (unlike Nova's
loyalty-points feature, which had a 1-week client deadline). Treat as
backlog-priority work, not time-pressured.

## Implementation sequence
1. Amer agrees a price with the client (~$500-650 anchor) and confirms capacity —
   both now unblocked by business-analysis's GO verdict, but still real steps
   before build starts.
2. Task 1 (client confirms checkout signal) — can run in parallel with step 1.
3. Tasks 2 → 3 → 4 → 5 in sequence (each depends on the prior).
4. Task 6 last.

## Report (per `.claude/rules/reporting.md`)
```
PLANNED
- Nova Home Goods cart-recovery plan produced, 13h raw / ~15.6h with contingency
- business-analysis GO verdict obtained (scenario 4) -- pipeline-order gap closed

NEEDS YOU
- Agree price with client (~$500-650 anchor, not fixed)
- Confirm capacity via time-orchestration before scheduling
- 3 client inputs needed (checkout signal, operating days/week, compliance rules)
- Discount-cap value needed before Task 4
```
