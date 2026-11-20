# Weekly Review — 2026-11-20

Scheduled Friday 5pm Asia/Amman run (routine "Weekly Review - Fri 5pm Amman",
`trig_01Wi4ehSPLZM9gjhtChVUQQe`). Fired 17:15 Amman time (14:15 UTC) against a
17:00 schedule — within normal jitter, treated as the regular on-time weekly run,
not a partial-week snapshot.

**Duplicate-trigger flag (recurring issue):** a second scheduled routine for the
same Friday 5pm slot — "Personal Business Agent — Weekly Report"
(`trig_01JXMxVjrkQHAsfjJekHUCTm`) — also fired this slot, ~1 minute before this
run, without Todoist/Calendar access, and committed a separate, much thinner
report to this same file (commit `b4ba58d`, unpushed, now dangling since this
run's commit supersedes it on `master`). Per `git log`, this same duplicate-
trigger problem was already flagged in the 2026-11-06 report commit message.
**NEEDS YOU**: confirm only one of these
two routines should exist and disable the other — otherwise they keep racing to
write this file and losing each other's commit.

Week covered: Sat 2026-11-14 – Fri 2026-11-20 (Sat-to-Fri cycle, matching the
Sat-full-workday / Fri-review-day pattern in `memory/user.md`).

## WEEK IN REVIEW

- **OBSERVED** (Todoist `find-completed-tasks`, 2026-11-14 to 2026-11-20,
  account-wide): **0 tasks completed** this week. No completion data to review at all.
- **OBSERVED** (Todoist): the only active client project tracked is
  **"Lindrize – First Client"** (15 tasks). 14 of 15 are now overdue (due dates
  2026-11-14 through 2026-11-19) and **none are checked off**:
  - Cold calling – travel agencies ×5 (Nov 14, 15, 16, 17, 18)
  - Instagram DMs to agencies called ×2 (Nov 14, 15)
  - Film + upload 2-min demo video (Nov 14)
  - Add setter pay to hiring post, publish in 5 FB groups (Nov 14)
  - Research and post setter ad in more FB groups (Nov 15)
  - Finish the full website documentation (Nov 15)
  - Fix problems in Ghazal's e-commerce AI agent workflow (Nov 15)
  - Decide individual-establishment vs. freelancer + JoFotara, tell Claude (Nov 19)
  - Log today's numbers (recurring daily 21:00) — stuck at Nov 14, never logged
  - Only "Walk-in visits: 5–6 agencies on Wasfi At-Tall St" (due Nov 21) hasn't come due yet.
- **OBSERVED** (Calendar): matching work blocks for most of the above *were*
  time-blocked on the calendar this week (see CAPACITY UTILIZATION). A scheduled
  block existing is not evidence the work happened — it is only evidence it was
  planned.
- **ASSUMED gap, needs Amer to resolve**: either (a) this week's client work
  largely did not happen, or (b) it happened but was never checked off in
  Todoist. The data cannot distinguish these — flagging rather than guessing.
- **OBSERVED** (Todoist, separate from client work): the **"🌙 30-Day Vacation"**
  project is carrying a large stale backlog — at least 100 overdue tasks (query
  capped at 100, more exist), every one with a due date between 2026-09-19 and
  2026-10-16, none completed. This is a different, apparently abandoned
  initiative (daily prayer check-ins, a "Claude Agent Engineering" course plan,
  3 freelance-project milestones) — over a month stale, unrelated to this
  week's Lindrize work. Per the no-delete rule: flagging, not touching. Recommend
  Amer decide whether to archive/delete this project; will act only on explicit approval.
- **Business Admin** project: 0 tasks — empty.

## ESTIMATE ACCURACY

**UNKNOWN.** No tasks were completed this week (see above), so there is no
completion-timestamp vs. due-date/duration data to compare. Estimate accuracy
cannot be computed this week — not zero, not good, not bad: there is no sample.

## CAPACITY UTILIZATION

- **Available** (per `memory/user.md`, Sat–Fri cycle): Sat 6.5h + Sun/Mon/Tue/Wed/Thu
  university-or-club days × 3.5h (17.5h) + Fri 5h = **~29h**. Friday's 5h is
  reserved for review/planning, not build work, so buildable capacity is **~24h**;
  minus the ~15% buffer (~4.35h), realistic workable capacity is **~19.6–24h**.
- **Required**: **UNKNOWN** — none of the Lindrize tasks carry an effort/duration
  estimate in Todoist, so required hours can't be quantified this week.
- **OBSERVED scheduled work-block time** (Calendar, Sat–Thu, excluding today):
  Sat 3h, Sun 5h, Mon 1.5h, Tue 2h, Wed 2h, Thu 0h = **13.5h total** — well under
  the ~24h buildable capacity. Thursday had no work blocks at all (only Club
  17:00–21:00), leaving a ~3.5h productive window unscheduled.
- **CHANGED — flagging, not yet fixed**: three "Cold calling – travel agencies"
  blocks (Sun Nov 15, Tue Nov 17, Wed Nov 18, each 11:00–13:00) **overlap the
  fixed University lecture (11:30–14:30) by 1.5h**. This is a real double-booking
  against a fixed commitment already sitting on the calendar — Amer cannot be on
  a cold call and in a lecture simultaneously. It may explain some of the
  missing completions above. This pattern is on a recurring cold-calling series,
  so it will repeat next week unless moved — recommend Amer confirm and then have
  it rescheduled.

## CLIENT STATUS

- **`memory/active-projects.md` is stale.** It lists only "Lead-gen AI system —
  Wisal Retreats" (WAITING_FOR_CLIENT, last updated 2026-08-19 — three months
  ago). Nothing in Todoist or Calendar this week references Wisal Retreats.
- **Lindrize – First Client** (visible in Todoist/Calendar, **not present at all**
  in `memory/active-projects.md`): appears to be the real active engagement —
  website documentation, a travel-agency cold-calling/setter hiring campaign, and
  a bug-fix on "Ghazal's e-commerce AI agent" workflow. State per the task-state
  vocabulary: closest fit is **EXECUTING**, but with 14/15 tracked tasks overdue
  and 0 confirmed complete, actual state is uncertain — recommend Amer confirm.
- **NEEDS YOU**: `memory/active-projects.md` should be updated to track Lindrize
  (and Ghazal, if it's a distinct client) instead of — or alongside — Wisal
  Retreats, and to say whether Wisal Retreats is still live. Will update on your
  confirmation of current state for each.

## NEXT WEEK (Sat 2026-11-21 – Fri 2026-11-27)

- **Fixed** (Calendar): University Sun–Wed (Nov 22, 23, 24, 25) 11:30–14:30;
  Club Sun/Tue/Thu (Nov 22, 24, 26) 17:00–21:00. No fixed events on Sat Nov 21
  or Fri Nov 27.
- **Carrying over**: all 14 overdue Lindrize tasks listed above, plus "Walk-in
  visits: 5–6 agencies on Wasfi At-Tall St" (due Nov 21).
- **Risk**: if this week's work genuinely didn't happen, next week's backlog
  compounds on top of new due dates. The University-overlap double-booking will
  recur automatically on the same recurring cold-calling series unless fixed
  before Sunday.
