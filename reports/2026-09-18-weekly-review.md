# Weekly Review — 2026-09-18

Scheduled Friday 5pm Asia/Amman run (fired 17:07, on schedule). Covers the completed
portion of this Jordan work week: Sunday 2026-09-13 through Thursday 2026-09-17, plus
today (Friday) up to the time of this review. Saturday 2026-09-19 has not happened yet
and is not included in the actuals below.

Note: a second scheduled run also fired for this same Friday slot (separate session,
commit `17d2c82`) and pushed a report to this same path first. That run had Todoist
and Google Calendar connectors disabled in its session and could only report a
connector-access gap, in the general COMPLETED/BLOCKED/NEEDS YOU format rather than
this skill's weekly-review format. This run had full connector access, so its
content — the report below — supersedes that one at this path; nothing from the
connector-less run is lost, since it added no facts beyond "connectors were
unavailable" (same pattern as the 2026-09-11 report, which hit an identical duplicate
run).

## WEEK IN REVIEW

- **Al Ghazal (support system)** — OBSERVED: "Fix Postgres Chat Memory bug (sessions
  keyed by channel, not user)" marked completed. Due 2026-09-15, completion logged
  2026-09-18.
- **Meeting with Mustafa** — OBSERVED: attended 2026-09-13, 08:00–09:00 (matches
  Calendar).
- **Wisal Retreats** — no Todoist activity this week. No change from
  `memory/active-projects.md`.
- Everything else completed this week (17 prayer/habit check-ins, Quran review, gym
  log, donation, personal "weekly review" task) is personal habit tracking, not
  business work.
- **Data quality flag (OBSERVED):** all 38 "completed" events the Todoist activity
  log returned for this window are timestamped in two narrow bursts — ~2026-09-14
  18:19 Amman and ~2026-09-18 06:00 Amman (each under a minute) — covering due dates
  from 2026-09-09 through 2026-09-18, most marked `wasOverdue: true`. This includes
  the Al Ghazal bug-fix completion. INFERRED (moderate confidence): this looks like a
  backlog catch-up/bulk-complete rather than tasks being checked off as they were
  actually finished — the same pattern the 2026-09-11 report found for that week's
  batch-closed backlog items. That means the completion timestamps here — including
  "completed 2026-09-18" for the Al Ghazal fix — may not reflect when the work
  actually happened. Worth confirming with Amer rather than trusting the log at face
  value.
- Plan-vs-actual comparison is limited: `memory/active-projects.md` only tracks Wisal
  Retreats, which had no movement. The one real piece of client work observed this
  week (Al Ghazal) isn't in that file at all, so there's no documented "plan" to
  compare it against.

## ESTIMATE ACCURACY

- UNKNOWN — not computable. No task in this week's Todoist data (completed or open)
  carries a Duration field or a work-type label, which is what the
  Duration-vs-completion-gap method in the skill needs. Nothing to aggregate — same
  gap the 2026-09-11 and earlier reports also hit.
- The only timing signal available is the Al Ghazal bug fix's due date (2026-09-15)
  vs. its logged completion (2026-09-18) — a 3-day gap — but per the batch-completion
  flag above, that gap may be an artifact of when it was checked off, not evidence of
  a 3-day slip in the actual work. ASSUMED nothing further here.
- Recommend: if Amer wants estimate accuracy tracked, business tasks need a Duration
  estimate and a consistent label at creation time — currently none carry either.

## CAPACITY UTILIZATION

- Calendar for Sep 13–17 matches `memory/user.md`'s fixed commitments exactly:
  University Sun–Wed 11:30–14:30, Club Sun/Tue/Thu 17:00–21:00, plus the one-off
  Mustafa meeting. Calendar is populated and consistent with memory — no
  wrong-account or disconnected-calendar concern this week.
- No Claude-created work blocks appear on the Calendar for this week — only fixed
  commitments. There's no calendar record of when/whether deep-work time was actually
  used, so day-by-day utilization can't be reconstructed from Calendar alone.
- Available (per `memory/user.md`'s model, Sun–Thu only, since Fri/Sat haven't
  completed): ~3.5h/day × 5 days ≈ **17.5h**.
- Required: not computable — no effort estimates exist for this week's tasks (see
  Estimate Accuracy above), and only one client task was completed. Honest read: 1
  client deliverable + 1 meeting against ~17.5h of theoretical capacity looks
  light, but that's a rough impression, not a measured utilization number — stating
  a precise gap here would be invented.
- Friday's 5h window (17:00–22:00 today) is reserved for reviewing this report and
  planning next week per `memory/user.md`, not build time — not counted as available
  build capacity above. Saturday (6.5h) hasn't started yet.

## CLIENT STATUS

- **Wisal Retreats** — `WAITING_FOR_CLIENT`, unchanged. This is now the fifth
  consecutive weekly review with no movement on this entry (flagged in the
  2026-09-11, 09-04, and 08-28 reports too) — it still points at the 2026-08-22
  discovery meeting as the next milestone, now ~4 weeks past with no note of its
  outcome. Needs Amer to confirm what happened and refresh the entry.
- **Al Ghazal** — still not present anywhere in memory (`clients.md`,
  `active-projects.md`, or `projects/`), a gap the 2026-09-11 report already flagged.
  OBSERVED from Todoist only: a support-system bug fix (Postgres chat memory keyed by
  channel instead of user) was completed this week; a decision task — "Decide &
  implement WhatsApp human handoff (respond.io vs Zendesk)" — is due 2026-09-20 and
  still open. This is real, active client work with zero tracked state, two weeks
  running. Recommend adding a `memory/clients.md` entry, a `projects/al-ghazal/`
  folder, and an `active-projects.md` row so this stops being invisible to planning.
- **Possible third project** — an open Todoist task, "🎯 Milestone: all 3 freelance
  projects shippable" (due 2026-10-07), implies three active engagements. Only two
  are identifiable from this week's data (Wisal, Al Ghazal). The third is UNKNOWN —
  needs Amer to say what it is so it can be tracked.

## NEXT WEEK

- **Fixed** (Calendar, Sun 2026-09-20 – Sat 2026-09-26): University Sun/Mon/Tue/Wed
  11:30–14:30 (20th, 21st, 22nd, 23rd); Club Sun/Tue/Thu 17:00–21:00 (20th, 22nd,
  24th). No fixed events returned for Friday the 25th or Saturday the 26th.
- **Carrying over:**
  - Al Ghazal — WhatsApp handoff decision, due 2026-09-20 (due the first day of next
    week; no calendar work block currently reserved for it).
  - "Finish n8n 'gmail leads' workflow end-to-end," due 2026-09-27.
  - "Package & publish google-skill-freelance plugin v1," due 2026-10-04.
  - Wisal Retreats — still blocked on client input, no self-imposed deadline.
  - 11 open Claude-Code/MCP training-course tasks now due between 2026-09-19 and
    2026-10-16 (personal skill-building, not client-billable).
- **Risk:** the Al Ghazal decision task lands right at the start of next week with no
  scheduled time against it. The training-course backlog adds real load on top of
  university and whatever Al Ghazal/Wisal work materializes — worth a capacity check
  before committing to all of it, especially since this week's actual effort
  couldn't be measured to calibrate against.
