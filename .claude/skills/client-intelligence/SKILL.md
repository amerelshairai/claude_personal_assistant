---
name: client-intelligence
description: Analyze a client's business deeply enough to identify the best automation solution and legitimate high-value opportunities. Use when Amer introduces a new client, shares client documents or requirements, asks what to build for a client, or asks where a client's automation opportunities are. Produces a structured Client Intelligence Package.
when_to_use: Triggers on "new client", "this client wants", "analyze this client", "what should we build for", "client requirements", "what automation opportunities", or when client documents/websites/meeting notes are shared.
---

# Client Intelligence

> **STATUS: SCAFFOLD.** This is the first skill scheduled for full implementation.
> The contract below is fixed. The methodology sections are deliberately unfinished —
> see `references/DESIGN-QUESTIONS.md` before implementing.

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
