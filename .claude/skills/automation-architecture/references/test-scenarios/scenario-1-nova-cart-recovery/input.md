# Scenario 1 — input (synthetic, fully synthetic per Amer's priority default)

**Client:** Nova Home Goods (existing — reused from `client-intelligence` and
`business-analysis` tests).

## Requirement
Design the **abandoned-cart recovery flow** recommended in Nova's client-
intelligence package (§14/§15) and sized in the e-commerce business-analysis
scenario (~$38,250/day raw exposure ceiling — never a promised recovery figure).
Never actually designed at the technical level until now.

## What's known from prior work (reused, not re-derived)
- Storefront platform triggers checkout events; ~1,250 checkout starts/day, ~850
  abandoned (68% rate, per the client-intelligence package).
- AOV ~$45.
- Existing systems: storefront platform (has cart/checkout data), bundled helpdesk
  tool for support — no dedicated marketing-automation tool.
- Messaging channels: WhatsApp/IG/FB DMs (matches Amer's Meta-channel stack).

## New for this design
- Amer (client-facing constraint, standard for this kind of flow): a recovery
  message should go out a set delay after abandonment (not instantly — avoid
  feeling pushy), and a second follow-up with an incentive only if the first gets
  no response. Discount amount on the incentive message needs a cap someone
  approves, not an unlimited auto-generated number.
