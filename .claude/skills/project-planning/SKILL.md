---
name: project-planning
description: Break a project into scope, deliverables, work breakdown, dependencies, effort estimates, milestones, risks and approval points — structured so it converts directly into Todoist tasks and Calendar work blocks. Use when Amer starts a new client project or needs an existing one planned properly.
when_to_use: Triggers on "plan this project", "break this down", "what's the work breakdown", "create a project plan", "what are the milestones", "I have a client who wants X in Y days".
---

# Project Planning

> **STATUS: METHODOLOGY DEFINED.** Contract and methodology below are decided (see
> `references/DESIGN-QUESTIONS.md` for the full reasoning behind each). Test
> scenarios still pending.

Sits between analysis and execution: takes a recommended solution and produces a plan
that becomes real tasks and real scheduled time.

## Output structure

Objective · scope (and explicit **out of scope**) · deliverables · requirements ·
work breakdown · tasks · subtasks · dependencies · estimated effort · estimated
duration · milestones · risks · required client inputs · required Amer inputs ·
Claude-executable work · approval points · deadline analysis · implementation sequence.

## Three critical splits

Every plan must separate work by who does it — this is what makes the plan usable:

| Bucket | Meaning |
| --- | --- |
| **Claude-executable** | Research, docs, analysis, workflow building, task setup |
| **Requires Amer** | Decisions, client calls, judgment, credentials, approvals |
| **Requires client** | Access, data, sign-off, answers to open questions |

A plan that does not mark client dependencies will slip. Client blockers are the most
common cause of missed deadlines — surface them at planning time, not week three.

## Deadline analysis

Do not just lay tasks in sequence. Compare required effort against actual available
capacity via `time-orchestration` and say clearly whether the deadline is achievable.
If it is not, say so at planning time with the numbers and what would need to change.

## Output location and hand-off

Write to `projects/<client>/plan.md`. Each task must carry enough detail to become a
Todoist task without rewriting: what, effort estimate, dependency, owner, due date.

Hand off: `todoist-management` creates the tasks → `time-orchestration` decides when →
`calendar-management` blocks the time.

## Standard phases (from `memory/business.md`)

2 discovery/scoping meetings → lands full technical workload/scope → build →
deliver → optional enhancements if the client wants them.

## Task granularity

**1 hour minimum** per work-breakdown task — matches `time-orchestration`'s
deep-work block minimum, rounded to a clean planning unit. Anything smaller isn't
worth tracking as its own task.

## Contingency buffer

Applied on top of the chosen point estimate as scheduling slack, varying by
project type (mirrors `business-analysis`'s effort multipliers):
- **Greenfield build: 20%**
- **Feature-addition: 15%**
- **Bug-fix/maintenance: none** — already covered by `time-orchestration`'s
  pessimistic-end REQUIRED calculation for Bugfix tasks; a second buffer here
  would double-pad the same uncertainty.

## Milestones

Standard checkpoint template, but flexible — not a rigid mold:
- Default: scope locked → build complete → delivered → post-delivery support
  window starts.
- Whether a milestone triggers payment is a separate fact from the client's
  contract (`memory/business.md`), never assumed.
- Insert exceptional milestones when a project genuinely needs one (e.g. a
  demo/proof-of-concept *before* scope or price is locked) — recognize when the
  default template doesn't fit rather than forcing every project into it.

## Risk register

Same 6 categories and severity scale as `client-intelligence` and
`business-analysis`: technical, adoption, data, vendor, compliance, scope creep —
High/Medium/Low. One consistent taxonomy from discovery through costing through
planning.
