# Scenario 1 — input

Not a new synthetic client — pulls entirely from prior test artifacts for Nova Home
Goods, per Amer's instruction: reuse numbers rather than re-derive them, and check
consistency across stages before trusting the plan's own output.

## Source artifacts
- `client-intelligence/references/test-scenarios/../projects/test-ecom-support/`
  (via `.claude/skills/client-intelligence/...` — Nova's original package):
  recommended the abandoned-cart recovery flow, sized the $38,250/day raw exposure,
  flagged risks and missing info for Nova generally.
- `business-analysis/references/test-scenarios/scenario-2-feature-addition/`: costed
  Nova's **loyalty-points** feature (a *different* feature) — $600 quoted for 9h,
  revised to ~17h after discovery. **No business-analysis pass exists for
  cart-recovery specifically.**
- `automation-architecture/references/test-scenarios/scenario-1-nova-cart-recovery/`:
  designed the cart-recovery flow itself — diagram, risks, dependencies, and an
  effort estimate (Research 2h + Build 10h + Admin 1h = ~13h, Research portion
  ASSUMED/Low confidence). Also added the discount-cap pause/notify gate
  (nodes M/N) after a resolved flag.

## Task
Produce `projects/nova-home-goods/plan.md`-shape output for the cart-recovery
build, and explicitly check whether project-planning's inputs actually agree with
what business-analysis and automation-architecture already produced.
