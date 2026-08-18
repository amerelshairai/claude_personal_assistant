---
name: business-analysis
description: Cost, effort, ROI, pricing and viability analysis for projects and proposed automations. Use when Amer asks what a project will cost, what to charge, whether a project is worth pursuing, how two solutions compare, or what the return on an automation would be.
when_to_use: Triggers on "how much should I charge", "what will this cost", "is this project worth it", "compare these options", "what's the ROI", "price this", "should I take this project".
---

# Business Analysis

> **STATUS: METHODOLOGY DEFINED.** Contract and methodology below are decided (see
> `references/DESIGN-QUESTIONS.md` for the full reasoning behind each). Test
> scenarios still pending.

## Scope

Business-model analysis · cost analysis · project cost calculation · setup costs ·
monthly operating costs · time and effort estimates · time / effort / financial ROI ·
risk identification · solution comparison · feature and project prioritization ·
pricing recommendations · project viability ("should this be pursued?").

## Hard boundary

Pricing recommendations are **for Amer**. This skill never makes an external
commitment, never quotes a client directly, and never produces a number that goes out
without Amer's approval. A pricing output is Level 2 at most — `READY FOR REVIEW`.

## Cost model shape

Every costing separates:

| Layer | Contains |
| --- | --- |
| One-time | Discovery, design, build, testing, documentation, handover |
| Recurring | Hosting, API/LLM usage, subscriptions, monitoring |
| Maintenance | Expected support hours per month, change requests |
| Amer's time | Hours × internal rate — the real constraint |

Never quote a build cost without the recurring and maintenance lines. That is the
number that determines whether the client is actually happy in month six.

## Honesty rules

- State assumptions explicitly and label them **ASSUMED**.
- When inputs are unknown, give a range and say what would narrow it — do not invent
  a precise-looking figure.
- If a project is not worth pursuing, say so plainly and give the reason.
- Do not inflate scope. A recommendation must trace to a stated business benefit.

## Output

Comparison tables and financial models are usually clearer as spreadsheets — use the
`xlsx` skill for models with real numbers, and `document-production` for the
narrative. Deliver to `projects/<client>/analysis/`.

## Pricing and margin (from `memory/business.md`)

No internal hourly rate — Amer explicitly rejects hourly costing. Value-based, fixed
price per project. Target margin 70–80% net, ~35–40% net to Amer after the
technical-partner split. Actual pricing process: run the client's requested
feature/usage scope through the pricing calculator (`memory/business.md` § Pricing
tools) to get a price anchor, agree a price with the client from that, then estimate
effort separately.

## ROI horizon

**12 months** — same as `client-intelligence`, for consistency across skills.

## Effort multipliers by project type

Base ranges are `time-orchestration`'s Research/Build/Admin/Call baselines (Research
1–4h, Build 4–20h, Admin 0.5–2h, Call = actual length). Applied differently by
project type:

- **Greenfield build:** ranges apply directly, at the widest end of contingency —
  no existing system to anchor against, highest uncertainty.
- **Feature-addition:** same Build range for the core work, **plus a separate
  discovery/integration line** for understanding the existing system — never folded
  into the Build estimate, so "understanding" time stays visible from "building"
  time.
- **Bug-fix/maintenance:** smaller baseline, split into **Diagnosis** + **Fix**
  phases. Diagnosis is inherently unpredictable — flag it **ASSUMED/Low confidence**
  by default, same discipline as thin-scope estimates elsewhere in the system.

## Viability threshold

A project is a **"no" if it fails any one** of these four — they don't need to
stack:

1. **Capacity** — doesn't fit even after replanning (a `time-orchestration`
   question), without dropping existing client commitments below acceptable
   minimums. A tight deadline affects this, not profitability.
2. **Profitability** — the margin between the agreed price (from the pricing
   calculator + client negotiation) and the estimated effort doesn't clear an
   acceptable floor, and no scope cut recovers it. Judgment call on the specific
   price-vs-effort combination — never invent a $/hour figure to force a formula,
   since no internal hourly rate is used.
3. **Risk** — hits a risk category (compliance, data privacy, vendor dependency)
   Amer isn't willing to accept regardless of price.
4. **Fit** — genuinely outside Amer's skillset; delivering it poorly would cost more
   in reputation than the project is worth.
