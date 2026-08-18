# project-planning — decisions to make before full implementation

Per BUILD-PLAN.md step 6.

Already answered elsewhere — not re-asked:
- **Standard project phases**: 2 discovery/scoping meetings → lands full technical
  workload/scope → build → deliver → optional enhancements (`memory/business.md`).
- **Payment structure**: no fixed formula — governed by the client contract on
  file, reviewed per project (`memory/business.md`).

## 1. Task granularity — DECIDED (2026-08-18)
**1 hour minimum** per work-breakdown task. Matches `time-orchestration`'s
deep-work block minimum (45min, rounded to a clean 1h planning unit) — anything
smaller isn't worth tracking as its own task/Todoist item.

## 2. Contingency buffer — DECIDED (2026-08-18)
**Varies by project type**, mirroring `business-analysis`'s per-type effort
multipliers rather than one flat percentage:
- **Greenfield build: 20%** — highest uncertainty, no existing system to anchor
  estimates against.
- **Feature-addition: 15%** — an existing system gives some anchor, less
  uncertainty than greenfield.
- **Bug-fix/maintenance: no extra buffer** — already covered by
  `time-orchestration`'s rule to use the pessimistic end of the Diagnosis+Fix
  range for REQUIRED, rather than the midpoint. Adding a second buffer on top
  would double-pad the same uncertainty.

Applied on top of the chosen point estimate, as scheduling slack — distinct from
the effort *range* itself (which already encodes uncertainty via its width).

## 3. Milestones — DECIDED (2026-08-18)
**Standard checkpoint template as the default, but flexible for exceptional
cases** — not a rigid mold every project must fit:
- Default milestones: scope locked → build complete → delivered → post-delivery
  support window starts.
- Whether a milestone also triggers a payment is a separate fact pulled from that
  client's contract (per the already-answered payment-structure item above), never
  assumed.
- **Exceptional cases get inserted milestones**, not forced into the default four
  — e.g. a demo/proof-of-concept milestone *before* scope/price is even locked,
  when a client needs that. The agent must recognize when the default template
  doesn't fit and adapt rather than force it.

## 4. Risk register categories — DECIDED (2026-08-18)
**Reuse the same 6 categories as `client-intelligence` and `business-analysis`**:
technical, adoption, data, vendor, compliance, scope creep. Same High/Medium/Low
severity scale. One consistent taxonomy across discovery, costing, and planning —
a risk identified early stays legible through the whole lifecycle without being
relabeled.

## Test scenarios — IN PROGRESS

- **Scenario 1 — Nova Home Goods cart-recovery plan, built entirely from prior
  test artifacts**, run 2026-08-18 —
  `references/test-scenarios/scenario-1-nova-cart-recovery-plan/`. Not synthetic
  input — pulled numbers from `client-intelligence`, `business-analysis`, and
  `automation-architecture`'s existing tests for the same client, per Amer's
  instruction to check cross-stage consistency over in-isolation plausibility.
  **Found a real pipeline-order gap**: automation-architecture had designed and
  estimated this feature before business-analysis ever ran a viability/pricing
  pass on it (unlike Nova's loyalty-points feature, which went through the
  intended hand-off chain correctly). Flagged prominently rather than silently
  produced a complete-looking plan. **Resolved same day** by running
  `business-analysis` scenario 4 on the feature (verdict: GO) and updating this
  plan's Objective, Milestones, Risks, and Required Amer inputs to reflect it.
  Also confirmed 2 things carried forward cleanly: automation-architecture's
  discount-cap gate (shows up as both a task and a mitigated risk-register entry),
  and correctly filtering client-intelligence's 4 general Nova missing-info items
  down to the 2 that actually apply to this specific feature.
