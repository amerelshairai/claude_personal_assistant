---
name: calendar-management
description: Read Google Calendar commitments, find free time, and create or move work blocks around fixed meetings. Use when Amer asks what his schedule looks like, wants work time blocked out, needs to find a free slot, or when a plan needs to be placed into real time.
when_to_use: Triggers on "what's on my calendar", "block time for", "when am I free", "schedule this work", "move my work blocks", or after time-orchestration decides when work should happen.
---

# Calendar Management

> **STATUS: TESTED.** Contract and conventions below are decided and exercised
> against the time-orchestration trio's 3 synthetic test scenarios — see
> `../time-orchestration/references/DESIGN-QUESTIONS.md` for the full reasoning and
> every fix each scenario produced.

Calendar holds **fixed commitments** — meetings, university, appointments, events.
It answers: *when is Amer already committed?* It is not the task system.

The one exception: **work blocks** Claude schedules to execute Todoist work. Those
belong here because they consume real time. The task itself stays in Todoist.

## Authority

Level 1 (execute, then report): read meetings and events, identify free time, create
work blocks, move work blocks Claude created, reorganize the work schedule, protect
deep-work blocks.

Level 3 (approval required): cancelling or rescheduling **any event with another
attendee**, or any meeting Amer created. Deleting any event.

## Unconfirmed, time-pinned requests

A client request tied to a specific clock time (not just a due date) that Amer
hasn't accepted yet — e.g. "we need you available 4–5pm Thursday for our platform
update" — goes on the Calendar immediately as a **tentative event**, titled
`[Tentative] <client> — <what>`. Not a new third state alongside Todoist/Calendar —
it's a Calendar event from the start, just not yet confirmed. Once Amer accepts it,
drop the `[Tentative]` prefix and it's a normal confirmed event like any other.

## Conflict protocol

When new work collides with an existing meeting:

1. Identify the conflict precisely (what, when, whose).
2. Present options — move the work, shorten it, split it, or move the meeting.
3. Ask before cancelling or changing anything consequential.

Never silently move a meeting. Other people's time is not Claude's to reallocate.

## Work block conventions

- **Title:** `[Work] <client> — <task>` — the `[Work]` prefix makes it instantly
  obvious the block is Claude-generated and safe to move.
- **Calendar:** primary calendar (not a dedicated one).
- **Length:** minimum 45 minutes (per `memory/user.md` — below that, a block is
  pointless). Maximum 2.5 hours as the default cap, but **dynamic based on need** — if
  a task genuinely needs longer, don't force an arbitrary split just to respect the
  cap.
- **Buffer:** 30 minutes before/after fixed commitments before placing a work block.
- **Busy/free:** marked **Busy** — work blocks represent real committed time, not
  optional time.
- Never place a work block over an existing commitment.
- Respect Amer's timezone (Asia/Amman) and working hours from `memory/user.md`.

## To define with Amer

See `../time-orchestration/references/DESIGN-QUESTIONS.md` §B — built together with
`time-orchestration` and `todoist-management` as one loop, per BUILD-PLAN.md.
