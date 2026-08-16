---
name: project-planning
description: Break a project into scope, deliverables, work breakdown, dependencies, effort estimates, milestones, risks and approval points — structured so it converts directly into Todoist tasks and Calendar work blocks. Use when Amer starts a new client project or needs an existing one planned properly.
when_to_use: Triggers on "plan this project", "break this down", "what's the work breakdown", "create a project plan", "what are the milestones", "I have a client who wants X in Y days".
---

# Project Planning

> **STATUS: SCAFFOLD.** Contract fixed; estimation model to be built.

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

## To define with Amer

- Standard project phases for his delivery model
- Task granularity — smallest useful unit (1h? half-day?)
- Contingency buffer percentage
- Standard milestone / payment structure
- The standard risk register categories
