# Weekly Review — 2026-11-13

Scheduled Friday 5pm Asia/Amman run (routine "Weekly Review - Fri 5pm Amman",
`trig_01Wi4ehSPLZM9gjhtChVUQQe`). Fired 2026-11-13 14:18:10 UTC / 17:18 Asia/Amman —
18 minutes after the 17:00 Amman slot, in line with the scheduling lag noted in prior
weeks (14 min last week). Treating this as a normal, full-week close-out, not a
partial/manual-trigger snapshot. Window: Saturday 2026-11-07 through today, Friday
2026-11-13 (matches the Sat–Fri window used in prior reviews).

**Both Todoist and Google Calendar MCP connections failed this run** — both returned
a 502 (`CLIENT_HTTP_NOT_IMPLEMENTED`) error before any tool call could be made. This
is a harder failure than last week's: on 2026-11-06 this same routine had working
connectors throughout (it was the *other*, duplicate routine — "Personal Business
Agent — Weekly Report" — whose connectors were disabled). This week there is no
working connector at all for this routine, so **every section below that depends on
Todoist or Calendar data is UNKNOWN**, not derived from any tool call. Nothing in
this report is invented to fill that gap.

## WEEK IN REVIEW

- **UNKNOWN.** Todoist connection failed (502) — could not retrieve completed tasks,
  open backlog count, or overdue items for the week. No completed-vs-planned
  comparison is possible.
- For reference, last week's review (2026-11-06) observed a 213-task open backlog
  (212 overdue) and a third consecutive week of zero logged completions, driven
  almost entirely by a "Daily Adhan Check-ins" recurrence growing ~5 tasks/day. That
  figure is **not re-verified this week** — flagging it as stale context only, not
  as this week's state.

## ESTIMATE ACCURACY

- **UNKNOWN — not computable.** Requires Todoist Duration-vs-completion-timestamp
  data; the Todoist connector did not respond this run.

## CAPACITY UTILIZATION

- **UNKNOWN — not computable.** Google Calendar connection failed (502) — no events
  were retrieved for this week, so neither available hours (actual commitments) nor
  logged utilization can be measured from live data.
- Per `memory/user.md` (OBSERVED, confirmed 2026-08-19, not this week's data): the
  theoretical weekly capacity midpoint is ~29h gross / ~20.4–24.65h after the ~15%
  buffer, depending on which commitments apply. This is a standing reference figure,
  not a measurement of this week.

## CLIENT STATUS

- **Wisal Retreats** — `WAITING_FOR_CLIENT`, per `memory/active-projects.md`
  (OBSERVED). Entry last updated **2026-08-19** — **86 days / ~12.3 weeks stale** as
  of today. Still pointing at the 2026-08-22 discovery meeting as the next milestone,
  now 84 days past with no recorded outcome in this file. No Calendar or Todoist data
  available this run to check for any more recent activity. Flagged unchanged across
  at least six consecutive reviews now (per the 2026-11-06 report's count).
- No other workstreams are listed in `memory/active-projects.md`. Prior reviews have
  flagged an "Al Ghazal" engagement and a possible third freelance project visible
  only in Todoist task titles, not in memory — **cannot check either this week**,
  since Todoist is unreachable.

## NEXT WEEK

- **Fixed commitments:** **UNKNOWN from live Calendar** — connection failed. Per
  `memory/user.md`'s standing recurring pattern (ASSUMED stable, not confirmed
  against next week's actual calendar): University lectures Sun–Wed 11:30am–2:30pm;
  Club Sun/Tue/Thu 5:00pm–9:00pm. This is the same pattern observed in prior weeks,
  carried forward as an assumption only.
- **Carrying over:** Wisal Retreats, `WAITING_FOR_CLIENT`, per last confirmed memory
  state (2026-08-19). Everything else that was carried over in the 2026-11-06 review
  (the Todoist backlog items) could not be re-checked this week.
- **Risk:** cannot be assessed without Todoist deadline data — UNKNOWN.

## NEEDS YOU

- **Both Todoist and Google Calendar connectors failed for this routine this run**
  (502, `CLIENT_HTTP_NOT_IMPLEMENTED`) — this is a full data outage for the weekly
  review, not a partial gap. Please check the Todoist and Google Calendar connector
  configuration for this routine/session; if this persists next Friday, the weekly
  review will keep producing empty reports.
- Wisal Retreats is now ~12.3 weeks stale in `memory/active-projects.md` with no way
  to verify current status this run — confirm status or mark it `DEFERRED` when you
  next have a session with working Todoist/Calendar access.
- Per the 2026-11-06 report: two separate scheduled routines have been firing for the
  same Friday slot in recent weeks, with inconsistent connector access between them.
  If that duplicate routine ("Personal Business Agent — Weekly Report") is still
  active, worth consolidating to one routine.

## CHANGED

None this week — no reschedules, priority changes, or file updates took effect
beyond this report itself. (Todoist/Calendar state could not be checked, so no
replanning was attempted.)
