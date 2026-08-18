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

## Test scenarios
To be built once 1–4 are locked, same pattern as every other skill: synthetic
project-planning requests, run one at a time.
