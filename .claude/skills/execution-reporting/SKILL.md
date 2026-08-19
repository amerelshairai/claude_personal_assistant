---
name: execution-reporting
description: Produce the structured report of autonomous work — completed, in progress, blocked, needs-you, changed. Use at the end of any multi-step session, after a batch of autonomous work, or when Amer asks for a status update, morning brief or evening review.
when_to_use: Triggers on "what did you do", "status", "where are things", "morning brief", "evening review", "catch me up", or automatically at the end of any session with multiple Level 1 actions.
---

# Execution Reporting

> **STATUS: METHODOLOGY DEFINED.** Format was already fixed and live; the
> remaining questions are decided (see `references/DESIGN-QUESTIONS.md`). Test
> scenarios still pending.

Format and task states are defined in `.claude/rules/execution-policy.md` and
`.claude/rules/reporting.md`. This skill applies them and handles the periodic reviews.

## Core discipline

- Report every autonomous Level 1 action. Authorized ≠ silent.
- `PLANNED` is never reported as `COMPLETED`.
- "Draft prepared" is never reported as "sent".
- Every reschedule and priority change appears under `CHANGED` with its reason.
- One line per item. No padding.

## Morning routine

Read Calendar, Todoist, deadlines, and `memory/user.md` working hours. Then report:

```
TODAY
- Fixed: <meetings, with times>
- Capacity: <available hours after commitments>
- Required: <effort of work due>

PRIORITIES
1. <highest-value item> — <why>
2. ...

CONFLICTS
- <overload or collision, with the number>

RECOMMENDED SCHEDULE
- <block> <time> — <work>
```

Recommend. Do not silently restructure the day.

## Evening routine

Compare planned vs actual. Then report:

```
DONE TODAY
- <items>

NOT DONE
- <item> — <why>

ESTIMATE ACCURACY
- <where estimates were off, and by how much>

TOMORROW
- Fixed: <calendar>
- Carrying over: <items>
- Risk: <deadline pressure>

RECOMMEND
- <adjustments>
```

Estimate accuracy over time is what makes capacity planning trustworthy — track it
rather than quietly re-estimating.

## Report timing

Morning/evening: **on demand only** — Amer asks when he wants one, no automatic
scheduling. Weekly review: **scheduled**, every Friday 5:00pm Asia/Amman, via a
recurring cloud routine (the `schedule` skill) — this is different from the daily
reports specifically because it needs to persist across sessions, not fire only
when Amer happens to be in one.

## Estimate-vs-actual history

No separate tracking file — reuses `time-orchestration`'s existing approach:
derived fresh from Todoist each time (Duration field vs. completion-timestamp gap
for tasks sharing a work-type label).

## Weekly review format

```
WEEK IN REVIEW
- Completed vs. planned, across all active projects

ESTIMATE ACCURACY
- Aggregated over the week (not a single day) — where estimates were off, by how much

CAPACITY UTILIZATION
- Available vs. required over the week, over/under

CLIENT STATUS
- Per memory/active-projects.md — state changes this week

NEXT WEEK
- Fixed: <calendar>
- Carrying over: <items>
- Risk: <deadline pressure>
```
