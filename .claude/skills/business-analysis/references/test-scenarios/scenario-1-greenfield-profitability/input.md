# Scenario 1 — input (synthetic)

**Client:** TechFit Gym (synthetic) — 3-location gym chain, new prospect, no prior
engagement. Greenfield build.

## Requested scope (from discovery call)
Automate inbound trial-membership inquiries across their website contact form and
Instagram DMs:
1. Auto-respond to a new inquiry, collect basic info.
2. Schedule a tour at one of the 3 locations (checks a shared booking calendar).
3. Send a reminder before the scheduled tour.
4. Post-tour follow-up: if no signup within 48h, send a special-offer message.
5. On signup, push the new member's info + a payment link into their existing
   membership/billing system.

## Effort estimate (greenfield — widest contingency, per business-analysis methodology)
- Research: 3h (understanding their existing booking calendar + billing system's API)
- Build: 18h (near the top of the 4–20h range — multi-channel, multi-step, touches
  billing)
- Admin: 1.5h (docs, handover)
- Call: 1h (discovery call, actual length)
- **Total: 23.5h**

## Pricing (client conversation, informed by the pricing calculator)
Client ran their expected usage through the calculator conceptually and saw a
~$45/month recurring estimate (acceptable to them). For the one-time build, the
client anchored low: **"this seems simple, we were thinking around $400."**
`memory/business.md`'s stated range is $200 (minimum, e.g. a simple Gmail workflow)
to $5,000 (advanced), averaging $750–$1,500.

## Other factors
- Capacity: no other client work competing for this window (per synthetic Todoist
  state — treat as clear for this test).
- The build touches the gym's **billing/payment system** to push payment links after
  signup — the only client-facing money-handling touch in this scope.
