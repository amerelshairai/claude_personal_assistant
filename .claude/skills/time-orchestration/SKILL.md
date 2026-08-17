---
name: time-orchestration
description: Central time-management reasoning. Combines Todoist workload, Calendar commitments, deadlines, priorities and effort estimates to compute available capacity, detect overload, and replan when circumstances change. Use when Amer asks what to work on, whether his week is realistic, how to fit new urgent work, or when a deadline or new client request lands.
when_to_use: Triggers on "what should I do today", "can I fit this", "I have X hours and Y clients", "urgent work just came in", "am I overloaded", "replan my week", "reschedule".
---

# Time Orchestration

> **STATUS: METHODOLOGY DEFINED.** Contract and methodology below are decided (see
> `references/DESIGN-QUESTIONS.md` §C for the full reasoning behind each). Test
> scenarios still pending.

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

## Effort estimation

Work type (Research / Build / Admin / Call — the same 4 categories as the
`todoist-management` label) drives the estimate.

- **Learn from historical actuals over time.** Derive this fresh from Todoist each
  time — compare the Duration field against the completion-timestamp gap for
  completed tasks carrying the same work-type label — rather than maintaining a
  separate tracking file.
- **Starting baselines**, used until enough same-type history exists to calibrate
  against:
  - Research: 1–4h
  - Build: 4–20h (wide range deliberately — `memory/business.md` notes a
    20h-planned project can run to 50h)
  - Admin: 0.5–2h
  - Call: actual meeting length, not estimated
- Pick within the range based on known task-scope details. Flag the estimate
  **ASSUMED, Low confidence** when scope is thin or no same-type history exists yet.

## Capacity numbers (from `memory/user.md`)

- Deep-work block minimum length: 45 minutes.
- Weekly buffer reserved for the unexpected: ~4 hours (~15%).
- Realistic daily capacity: 6–7h on full days, 3–4h on university/club days.

## What's fixed vs. eligible to move

- **Calendar events are fixed** — meetings, university, club. Never touched without
  approval (Level 3, per execution-policy).
- **All Todoist tasks are eligible to move/reschedule by default**, unless Amer has
  explicitly flagged one as fixed.
- **Existing deep-work blocks are fully protected** — never moved to make room for
  new work. Only the placement of *new* work blocks changes around them.

## Deprioritization order when overloaded

Strictly by Todoist priority tier: **P4 gives way first, then P3, then P2 — P1 is
touched last.** This is the default `time-orchestration` reasons from, not a hard
rule — an explicit instruction from Amer overrides it regardless of P-tier (see
`todoist-management` § Priority).
