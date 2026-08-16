---
name: time-orchestration
description: Central time-management reasoning. Combines Todoist workload, Calendar commitments, deadlines, priorities and effort estimates to compute available capacity, detect overload, and replan when circumstances change. Use when Amer asks what to work on, whether his week is realistic, how to fit new urgent work, or when a deadline or new client request lands.
when_to_use: Triggers on "what should I do today", "can I fit this", "I have X hours and Y clients", "urgent work just came in", "am I overloaded", "replan my week", "reschedule".
---

# Time Orchestration

> **STATUS: SCAFFOLD.** Contract fixed; methodology to be built.

This is the reasoning layer, not an execution layer. It decides *what should happen*.
`todoist-management` and `calendar-management` carry out the changes.

## Always start by reading reality

Never plan from memory. Before any recommendation:

1. Read Calendar for the relevant window → fixed commitments.
2. Read Todoist → open workload, priorities, due dates.
3. Read `memory/user.md` → working hours, constraints, protected time.

## The core calculation

```
AVAILABLE  = working hours in window − Calendar commitments − buffer
REQUIRED   = Σ estimated effort of tasks due in window
GAP        = AVAILABLE − REQUIRED
```

State the numbers explicitly. If `GAP` is negative, that is an overload — name the
size of it and recommend what moves. Never quietly assume everything fits.

## Sudden-circumstance protocol

When urgent work arrives, do not just add a task. Run the full sequence:

1. Understand the new work.  2. Estimate effort.  3. Check its deadline.
4. Check current Todoist load.  5. Check Calendar.  6. Compute available time.
7. Identify conflicts.  8. Recalculate priorities.  9. Recommend changes.
10. Reschedule eligible work.  11. Update Todoist (Level 1).
12. Update Calendar work blocks (Level 1).  13. Report exactly what changed and why.

Cancelling a meeting is Level 3 — recommend, never execute.

## What to surface

Available capacity · overload · underused time · urgent work · deep-work windows ·
scheduling conflicts · unrealistic plans · what should be postponed · what Claude can
take over · what genuinely requires Amer.

## Priority reasoning

Client work is generally high priority — but reason, do not rank blindly. Explicit
instructions from Amer (university, personal commitments) override the default.
Protect existing deep-work blocks where possible; fragmenting them has a real cost.

## To build

- Effort estimation heuristics per work type (see `references/estimation.md`)
- Default buffer percentage and daily capacity ceiling
- Deep-work block minimum length
- Rules for which tasks are eligible to move vs fixed
