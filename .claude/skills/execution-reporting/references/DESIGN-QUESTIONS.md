# execution-reporting — decisions to make before full implementation

Per BUILD-PLAN.md step 8 — the last skill.

Already answered elsewhere — not re-asked: where estimate-vs-actual history is
stored. `time-orchestration/SKILL.md` already decided this — derived fresh from
Todoist each time (Duration field vs. completion-timestamp gap for same-work-type
tasks), no separate tracking file. `execution-reporting`'s "ESTIMATE ACCURACY"
sections read from that, not a new store.

## 1. Morning/evening report timing — DECIDED (2026-08-19)
**On demand only, for now.** No automatic scheduling for the daily morning brief
or evening review — Amer asks when he wants one. Can revisit once the habit/value
is proven.

## 2. Weekly review — DECIDED (2026-08-19)
**Scheduled, unlike the daily reports** — every **Friday 5:00pm Asia/Amman**.
Shape:

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

Set up as a recurring cloud routine (via the `schedule` skill), not a session-only
cron job — this needs to persist across sessions, unlike an ephemeral reminder.
