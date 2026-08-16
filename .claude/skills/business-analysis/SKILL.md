---
name: business-analysis
description: Cost, effort, ROI, pricing and viability analysis for projects and proposed automations. Use when Amer asks what a project will cost, what to charge, whether a project is worth pursuing, how two solutions compare, or what the return on an automation would be.
when_to_use: Triggers on "how much should I charge", "what will this cost", "is this project worth it", "compare these options", "what's the ROI", "price this", "should I take this project".
---

# Business Analysis

> **STATUS: SCAFFOLD.** Contract fixed; models to be built.

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

## To define with Amer

- Amer's internal hourly rate and target margin
- Standard pricing model: fixed / hourly / value-based / retainer
- Default ROI horizon
- Effort multipliers by project type
- The viability threshold — what makes a project a "no"
