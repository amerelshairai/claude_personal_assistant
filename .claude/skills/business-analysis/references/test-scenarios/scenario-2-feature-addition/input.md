# Scenario 2 — input (synthetic)

**Client:** Nova Home Goods (existing — reused from the `client-intelligence` tests,
order-status self-service + cart-recovery flow already delivered).

## Requested feature
Add a loyalty-points program to the existing order-status flow: customers earn
points per order, redeemable via a WhatsApp message. Client wants it live within
**1 week** for an upcoming promotion.

## What happened (timeline)
1. Client and Amer agree a price **before** discovery: **$600**, based on an initial
   rough estimate of Build 8h + Admin 1h = 9h (discovery/integration wasn't assessed
   yet — priced off the feature description alone).
2. Discovery/integration work begins (the separate line business-analysis's
   methodology requires, not folded into Build): 2h in, it turns out the existing
   order-status flow is **stateless per-order** — it has no persistent per-customer
   identity to accumulate points against across multiple orders.
3. Before the loyalty feature itself can be built, the system needs **customer-
   identity persistence added first** — a foundational piece nobody scoped, revealed
   only by doing the discovery work.

## Revised effort once this is known
- Discovery/integration: 2h (already spent) — this is what surfaced the gap.
- **Unplanned foundational work** (customer-identity persistence): 6h.
- Build (the loyalty feature itself, now that the foundation exists): 8h.
- Admin: 1h.
- **New total: ~17h — nearly double the 9h the $600 price was based on.**

The $600 price is already agreed with the client. Discovery is what revealed the gap,
not a client-requested scope change.
