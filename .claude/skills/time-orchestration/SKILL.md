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
AVAILABLE = realistic_productive_hours_per_day (memory/user.md, by day type)
            − extra Calendar commitments beyond that day's usual recurring pattern
            − buffer
REQUIRED  = Σ effort of tasks due in window
            + Σ effort of tasks due later that must start now to hit their deadline
GAP       = AVAILABLE − REQUIRED
```

**AVAILABLE always sources from `memory/user.md`'s `realistic_productive_hours_per_day`
for that day's type (6–7h full day, 3–4h university/club day) — never recomputed from
the raw 6am–10pm window.** That figure already nets out the day's *usual* recurring
pattern (the standard university lecture or club block). "Calendar commitments"
subtracted on top of it means only *extra*, non-routine commitments — a one-off
meeting, an unscheduled call — not the recurring lecture/club itself; subtracting
that again would double-count it.

**Buffer is a percentage (~15%, per `memory/user.md`), applied proportionally to
whatever window is being computed** — a day or a week — never the flat weekly figure
(~4h) subtracted from a single day's calculation.

**REQUIRED means "must be started today to hit its deadline," not "due in window."**
For each open task due within the next few days, check whether its remaining effort
exceeds the remaining capacity between *tomorrow* and its due date (summing each of
those days' AVAILABLE). If it does, the task can't wait — pull as much of it as fits
into today's REQUIRED (up to today's AVAILABLE), and let the rest land on the
following days' own REQUIRED calculations. A "due in window" test alone misses this:
a large task due tomorrow can show 0 required today while actually needing all of
today's capacity.

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
- Buffer reserved for the unexpected: **15%** — apply this percentage to whichever
  window is being computed (a day's or a week's realistic productive hours), not a
  flat figure. `memory/user.md`'s ~4h/week is that 15% already applied to the ~27h
  midpoint weekly figure, shown there as a reference instance, not a constant to
  subtract from every calculation regardless of window size.
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
`todoist-management` § Priority). **Ties within the same tier (including P1 vs. P1)
break by nearest deadline** — same rule at every tier.

**Cross-client exception:** if the only way to fit new work is a replan that would
cause a *different* client's existing deadline to slip, that is not a normal Level 1
reschedule — surface it for approval first, every time (see
`.claude/rules/execution-policy.md` § Cross-client scheduling tradeoffs). State what
slips and by how much; do not execute it unasked.
