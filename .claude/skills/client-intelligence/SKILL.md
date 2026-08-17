---
name: client-intelligence
description: Analyze a client's business deeply enough to identify the best automation solution and legitimate high-value opportunities. Use when Amer introduces a new client, shares client documents or requirements, asks what to build for a client, or asks where a client's automation opportunities are. Produces a structured Client Intelligence Package.
when_to_use: Triggers on "new client", "this client wants", "analyze this client", "what should we build for", "client requirements", "what automation opportunities", or when client documents/websites/meeting notes are shared.
---

# Client Intelligence

> **STATUS: METHODOLOGY DEFINED, PARTIALLY TESTED.** Contract and methodology below
> are decided (see `references/DESIGN-QUESTIONS.md` for the full reasoning behind
> each). Amer has flagged the KPI/ROI/discovery methodology as a first pass — expect
> it to evolve as real client work exposes gaps. The synthetic vague-inbound-lead test
> (§11 of DESIGN-QUESTIONS.md) has run — see `projects/test-vague-lead/`. The 2–3
> real-client tests are still pending, deferred until Amer can walk through real
> anonymized clients.

## Purpose

Not "research a website." The goal is:

> Understand the client's business deeply enough to identify the best automation
> solution, and legitimate additional opportunities that create measurable value.

## Inputs

Any subset of: client documents, website, CRM information, current systems,
screenshots, meeting notes, stated requirements, workflow descriptions, business
information Amer provides, public business information, public social/business
profiles, public competitor information.

Store client material under `projects/<client>/source/`.

## Permitted research

Company website, public business information, public social profiles, company
LinkedIn, publicly stated goals, services, customer journey, public positioning,
public reviews, competitors, technology clues, publicly observable operational
problems and priorities.

## Prohibited

- Researching Amer's personal profile. Never, for any reason.
- Contacting the client. This skill produces analysis only.
- Claiming private knowledge of anyone's feelings, psychology, intentions, or
  vulnerabilities.
- Recommending features that do not trace to a stated business benefit.
- Deleting anything (see `.claude/rules/execution-policy.md`).

## Evidence rules

Every material claim carries a label: **OBSERVED**, **INFERRED**, **ASSUMED**, or
**UNKNOWN**. Inferences carry a confidence level. An inference presented as fact is a
defect, not a style issue.

- **OBSERVED**: one direct, first-party source is enough — the client's own website,
  their own social posts, their own meeting notes/documents speaking about their own
  work or business. Treat it as essential input to the analysis.
- **INFERRED / ASSUMED**: reasoning from indirect signals rather than a direct
  statement. A single indirect signal never exceeds **Low** confidence, no matter how
  strong it looks — multiple consistent signals can reach Medium; only a direct source
  or 2+ independent corroborating sources reach High.

**Confidence scale: High / Medium / Low** (one scale, reused for risk severity too —
see Risk analysis below).

- **High** — confirmed by a direct first-party source, or corroborated by 2+
  independent sources.
- **Medium** — a reasonable inference from multiple consistent indirect signals.
- **Low** — inferred from a single indirect signal, or a stretch/assumption.

## Research methodology

Default sequence: **website → LinkedIn/social profiles → competitors → reviews →
tech clues**. Client-supplied material (documents, meeting notes, screenshots) is a
source too, and can be used alongside or ahead of public research.

Escalating beyond the default pass is a judgment call, not a fixed rule — driven by
thin/ambiguous requirements or apparent high value, not a rigid trigger. Ask Amer if
genuinely unsure whether to go deeper.

If the client hasn't supplied a business name, website, or social handle, the sequence
has nothing to start from — do not guess or search blind. Skip straight to Missing
Information / Questions for Client (§25/§26) and stop there until an identifier comes
back.

Stop condition: work through the standard sequence by default. If that isn't enough to
support the analysis, go beyond it — no fixed source or time cap; keep going until the
package can be produced with confidence.

## KPI methodology

Amer flagged this as a first pass, not fixed — expect revision as real client work
exposes gaps.

1. Identify problems from research + the client's own stated pain points.
2. Capture expectations — personal (what the client as a person wants: less stress,
   more free time) and business (revenue, growth, efficiency).
3. Map every opportunity to one of the **3 gold bars**: time saved / effort reduced /
   profit increased.
4. Pick 2–4 concrete KPIs per opportunity from a type-appropriate checklist, e.g.:
   - Salons/clinics: no-show rate, booking response time, staff hours on scheduling
   - E-commerce/customer support: response/resolution time, order processing time,
     cart recovery rate
   - Real estate: lead response time, follow-up consistency, inquiries-to-viewing rate
5. Baseline: if the client hasn't measured it, don't invent a number — estimate a
   rough range from observable signals (order volume, review complaint patterns, staff
   size), label it **ASSUMED**, and list it under Missing Information / Questions for
   Client so a real number can replace it later. If there is no observable signal to
   estimate from either — ASSUMED still needs something to reason from — leave the
   baseline **UNKNOWN** rather than forcing a guess, and list it under Missing
   Information.
6. Estimated vs client-reported KPIs are distinguished by the OBSERVED/ASSUMED label —
   client-reported numbers are OBSERVED, estimated ones are ASSUMED.

## ROI methodology

- **Horizon: 12 months** — bigger, more compelling growth picture for the client.
- Estimate both time and money where possible.
- If client staff hourly cost is unknown, do **not** guess a dollar figure. Focus on
  time/effort-native measures instead: hours saved, headcount-equivalent achieved (how
  many employees' worth of work this replaces/frees up), 24/7 availability value, and
  reduction in effort/mental overhead. Only convert to a dollar ROI when real cost data
  (staff wage, revenue per order, etc.) is OBSERVED from the client or a confirmed
  source.
- Ongoing costs (API/hosting/LLM tokens/subscription — typically $60–80/month, $30
  minimum) are **never netted against savings** to produce a "net ROI" figure — that
  framing makes the investment look riskier than it is. Present them separately: state
  the savings/value, and separately note the small ongoing cost as the size of the
  investment against what the client will save, not subtracted from it.
- Rigorous costing, pricing, and viability analysis is `business-analysis`'s job, not
  this skill's — see Hand-offs.

## Feature discovery methodology

- **Standard checklist is the baseline** — every client is scanned against the same
  core patterns: manual intake/booking, lead follow-up delay, re-entered data across
  systems, manual reminders/confirmations, plus other common patterns as the checklist
  matures (build out in `references/` over time). Keeps discovery consistent; nothing
  obvious gets missed.
- **Beyond the checklist**: client-specific opportunities the checklist wouldn't catch
  are still surfaced, flagged separately as "beyond standard checklist" so Amer can see
  which recommendations are pattern-matched vs genuinely bespoke.
- **Real value vs invoice padding**: must tie to at least one of the 3 gold bars
  (time/effort/profit) — no exceptions, that's the floor.
- Small/nice-to-have items that clear that bar are **not** bundled into the main
  recommendation by default. List them separately under "Additional Value
  Opportunities," labeled optional, each with its own small cost/effort estimate. Amer
  decides whether to offer it — never silently fold a nice-to-have into scope just
  because it's easy to build.

## Opportunity ranking

Three dimensions, in priority order:

1. **Value** — how much it boosts the client's work without displacing them or costing
   too much, and how it reflects on their standing/value (personal + business).
2. **Profit** — must not work against the client's own profit goals; favor genuine
   value over padded scope.
3. **Risk** — security of the client's data and financial systems.

Client-stated priority leads the ranking by default — what the client says matters
most to them comes first. Effort and time-to-value are not separate ranking
dimensions; consider them qualitatively within the above.

## Risk analysis

Check every opportunity against: **technical** (integration/breakage risk),
**adoption** (staff won't actually use it), **data** (privacy/security), **vendor**
(third-party API dependency/cost changes), **compliance** (industry-specific rules),
**scope creep**.

Severity: **High/Medium/Low** — same scale as confidence, not a separate scale.

## Missing-information detection

Required-info checklist, two tiers:

- **Essential**: current tools/systems/databases/contact systems in use; a
  client-articulated gap/pain point (e.g. "demand is outpacing production capacity").
- **Helpful but not mandatory**: monthly volume, staff count.

Captured primarily through client conversations — meeting notes are the main source of
clarity, not just public research. When missing, list under Missing Information /
Questions for Client, tiered essential vs helpful so Amer knows what genuinely blocks
scoping vs what's just useful context.

## Output: Client Intelligence Package

Write to `projects/<client>/intelligence/YYYY-MM-DD-package.md`. Machine-readable
enough for the orchestrator to consume — use these exact section headings:

1. Executive Summary
2. Business Overview
3. Business Model
4. Target Customers
5. Current Systems
6. Current Workflow
7. Customer Journey
8. Requirements
9. Pain Points
10. Bottlenecks
11. Publicly Observable Business Priorities
12. KPI Opportunities
13. Automation Opportunities
14. Recommended Features
15. Additional Value Opportunities
16. Time Savings Opportunities
17. Effort Reduction Opportunities
18. Financial Opportunities
19. ROI Analysis
20. Cost Considerations
21. Risks
22. Alternative Solutions
23. Recommended Solution
24. Recommended Priorities
25. Missing Information
26. Questions for Client
27. Evidence and Confidence
28. Implementation Implications

Template: `templates/package-outline.md`

## Relationship to the client-analyst subagent

For a substantial client, delegate to the `client-analyst` subagent so research runs in
parallel with other work. The subagent returns the package; the orchestrator consumes
it and decides next steps. For a small follow-up question, run this skill inline —
do not spawn a subagent for a single lookup.

## Hand-offs

- Cost / ROI / pricing depth → `business-analysis`
- Turning the recommended solution into a design → `automation-architecture`
- Turning the plan into tasks and time → `project-planning`, then `time-orchestration`
