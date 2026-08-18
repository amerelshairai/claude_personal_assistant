# Cross-stage consistency check (done first, per Amer's priority)

## Finding 1 — real gap: business-analysis never costed this specific feature
`business-analysis` has a Nova Home Goods test, but it's for **loyalty points**, a
different feature — not cart-recovery. The only effort figure that exists for
cart-recovery comes from `automation-architecture`'s technical-side estimate
(~13h). **No GO/NO-GO/CONDITIONAL viability check has ever run on cart-recovery
specifically** — no price was agreed, no margin was checked, no capacity check was
run against it. This plan is being asked to build execution scaffolding on top of
a design that skipped the costing/viability gate entirely for this feature.

This is a **pipeline-order problem**, not a numbers mismatch: the intended hand-off
is client-intelligence → business-analysis (price/viability) →
automation-architecture (technical design) → project-planning (execution plan).
For cart-recovery specifically, automation-architecture ran *before*
business-analysis ever touched it. The loyalty-points feature went through the
chain correctly; cart-recovery didn't.

**This plan proceeds using automation-architecture's ~13h as the only available
number, but flags every effort/cost figure below as pending a business-analysis
pass** — not because the number is wrong, but because nothing has confirmed a
client will pay for it or that it clears margin. Recommend running
`business-analysis` on this feature before treating this plan as ready to execute,
not after.

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
intelligence's discipline on this number.

## Scope
Order-status check → delayed recovery message → capped-discount incentive message
→ outcome logging, per automation-architecture's design.

**Out of scope**: Nova's support self-service opportunity (different feature,
different plan), the unresolved "reviews" ask (still unscoped, per client-
intelligence), and any pricing/contract work with the client (blocked on Finding 1).

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
Standard template applies: scope locked (**blocked on Finding 1 — no
business-analysis pass yet**) → build complete → delivered → post-delivery support
window starts. No exceptional pre-price demo milestone needed for this client
(existing relationship, not a new prospect).

## Risks
| Risk | Category | Severity | Mitigation |
| --- | --- | --- | --- |
| Storefront has no clean checkout-abandonment signal | Technical | Medium | Task 1 confirms before Build starts |
| Discount cap set too high, eroding margin | Data (financial) | Medium | Mitigated — pause/notify gate (Task 4), not silent auto-send |
| Feels like spam to price-sensitive customers | Adoption | Low-Medium | Two-message cap, stop on response (per automation-architecture design) |
| WhatsApp API cost scaling with ~850/day volume | Vendor | Medium | Confirm against business-analysis's cost estimate once that pass runs (Finding 1) |
| Automated messaging/discount offers may hit consumer-protection rules | Compliance | Low-Medium | Requires client answer — see below |
| This plan proceeds without a viability/pricing decision | Scope creep / process | **High** | **Do not execute past Task 1 until business-analysis runs on this feature** |

## Required client inputs (filtered to what actually blocks this build — Finding 3)
1. Storefront checkout-status signal confirmation (also Task 1).
2. Operating days/week (needed for duration estimate and compliance context).
3. Applicable consumer-protection/messaging-consent rules for automated cart offers.

## Required Amer inputs
- Discount-cap value, before Task 4.
- Decision on Finding 1: run business-analysis now, or accept the process gap and
  proceed on automation-architecture's number alone.

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
loyalty-points feature, which had a 1-week client deadline). Treat as backlog-
priority work pending Finding 1's resolution, not time-pressured.

## Implementation sequence
1. Resolve Finding 1 (business-analysis pass) — **recommended before anything
   else**, not a hard blocker on Task 1 itself, but on treating this plan as
   ready to execute.
2. Task 1 (client confirms checkout signal) — can run in parallel with step 1.
3. Tasks 2 → 3 → 4 → 5 in sequence (each depends on the prior).
4. Task 6 last.

## Report (per `.claude/rules/reporting.md`)
```
PLANNED
- Nova Home Goods cart-recovery plan produced, 13h raw / ~15.6h with contingency

NEEDS YOU
- Finding 1: no business-analysis viability/pricing pass exists for this feature
  -- recommend running it before executing this plan
- 3 client inputs needed (checkout signal, operating days/week, compliance rules)
- Discount-cap value needed before Task 4
```
