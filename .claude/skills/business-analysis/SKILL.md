---
name: business-analysis
description: Cost, effort, ROI, pricing and viability analysis for projects and proposed automations. Use when Amer asks what a project will cost, what to charge, whether a project is worth pursuing, how two solutions compare, or what the return on an automation would be.
when_to_use: Triggers on "how much should I charge", "what will this cost", "is this project worth it", "compare these options", "what's the ROI", "price this", "should I take this project".
---

# Business Analysis

> **STATUS: TESTED.** Contract and methodology below are decided and exercised
> against 3 synthetic scenarios (greenfield build, feature-addition, bug-fix/
> maintenance) — see `references/DESIGN-QUESTIONS.md` for the full reasoning and
> every fix each scenario produced.

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
| Amer's time | Hours — the real constraint. No internal $/hour; judged directly
  against the agreed price (see § Viability threshold, Profitability). |

Never quote a build cost without the recurring and maintenance lines. That is the
number that determines whether the client is actually happy in month six.

## Mid-project discovery overruns

If discovery/diagnosis work reveals materially more effort than an already-agreed
price covers — even though the client never asked for anything extra — treat it the
same as a client-requested scope change: route through `memory/business.md`'s
existing payment-plan-adjustment mechanism. Pause before absorbing the extra work
silently, explain what discovery found, and bring a revised price/plan to Amer
rather than continuing on the original number. The trigger differs (Amer's own
discovery vs. the client asking for more) but the handling is the same either way.

**Verdict: `NEEDS-REPRICING`** — distinct from GO/NO-GO/CONDITIONAL, which is a
pre-commitment gate for a decision that hasn't happened yet. This situation is
different: the commitment already exists, and the question is how to adjust it, not
whether to make it. Report as `WAITING_FOR_AMER`, same as CONDITIONAL, but labeled
`NEEDS-REPRICING` so a report never conflates "should I take this" with "this
already-agreed deal needs revisiting."

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
- **Bug-fix/maintenance:** tagged with its own `Bugfix` Todoist label (added
  2026-08-18 — it never fit inside Build's 4–20h range). Split into **Diagnosis** +
  **Fix** phases. Diagnosis is inherently unpredictable — flag it **ASSUMED/Low
  confidence** by default, same discipline as thin-scope estimates elsewhere in the
  system.

## Risk categories

Same categories and severity scale as `client-intelligence`: **technical, adoption,
data, vendor, compliance, scope creep** — High/Medium/Low.

**Payment/billing-touching builds** (added 2026-08-18, from the TechFit Gym test —
mirrors `client-intelligence`'s health-data rule): automatically raise the **data**
risk to at least **Medium-High**, even if the build only pushes a payment link and
never processes or stores card data directly. Regulatory/reputational exposure for
money-handling is higher by default than for a typical non-financial client.

## Viability threshold

**Scope: applies to the decision to take on a project or client — not to bug-fix/
maintenance work for an existing client under an ongoing relationship.** For that
kind of work, Capacity and Risk still get checked, but Fit is moot (already serving
the client) and Profitability isn't a go/no-go call — it's a billing question
(inside the free post-delivery window, or billable maintenance). Confirmed
2026-08-18, from the Falcon Realty bug-fix test.

A project gets a three-way verdict, not a binary yes/no: **GO / NO-GO /
CONDITIONAL.**

- **GO** — clears all four checks below cleanly.
- **NO-GO** — fails one or more checks and nothing recovers it. Say so plainly, with
  the reason (per Honesty rules).
- **CONDITIONAL** — fails a check, but something specific would fix it (a scope cut,
  a price change, a timeline shift). State exactly what would need to change to
  reach GO. **Report the task's state as `WAITING_FOR_AMER`** — this is a decision
  only Amer can make, not a Level 2 artifact ready to review. Never label a
  CONDITIONAL verdict `REVIEW_REQUIRED`; that state means something different (a
  finished Level 2 artifact), not an open renegotiation call.

Checked against these four — any one failing (without a fix available) is enough
for NO-GO; a failing check with a fix available is CONDITIONAL:

1. **Capacity** — doesn't fit even after replanning (a `time-orchestration`
   question), without dropping existing client commitments below acceptable
   minimums. A tight deadline affects this, not profitability.
2. **Profitability** — the margin between the agreed price (from the pricing
   calculator + client negotiation) and the estimated effort doesn't clear an
   acceptable floor. Judgment call on the specific price-vs-effort combination —
   never invent a $/hour figure to force a formula, since no internal hourly rate is
   used. A scope cut or price renegotiation that would recover the margin makes this
   CONDITIONAL, not NO-GO.
3. **Risk** — hits a risk category (see above) Amer isn't willing to accept
   regardless of price.
4. **Fit** — genuinely outside Amer's skillset; delivering it poorly would cost more
   in reputation than the project is worth.
