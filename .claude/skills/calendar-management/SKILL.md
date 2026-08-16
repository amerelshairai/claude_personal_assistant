---
name: calendar-management
description: Read Google Calendar commitments, find free time, and create or move work blocks around fixed meetings. Use when Amer asks what his schedule looks like, wants work time blocked out, needs to find a free slot, or when a plan needs to be placed into real time.
when_to_use: Triggers on "what's on my calendar", "block time for", "when am I free", "schedule this work", "move my work blocks", or after time-orchestration decides when work should happen.
---

# Calendar Management

> **STATUS: SCAFFOLD.** Contract fixed; conventions to be defined with Amer.

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

## Conflict protocol

When new work collides with an existing meeting:

1. Identify the conflict precisely (what, when, whose).
2. Present options — move the work, shorten it, split it, or move the meeting.
3. Ask before cancelling or changing anything consequential.

Never silently move a meeting. Other people's time is not Claude's to reallocate.

## Work block conventions

- Title work blocks so they are obviously Claude-generated and safe to move.
- Never place a work block over an existing commitment.
- Respect Amer's timezone (Asia/Amman) and working hours from `memory/user.md`.
- Leave transition buffer around meetings rather than butting blocks against them.

## To define with Amer

- Work block title format (proposal: `[Work] <client> — <task>`)
- Which calendar work blocks go on (primary vs a dedicated one — a dedicated
  calendar makes bulk cleanup far safer)
- Minimum and maximum block length
- Buffer minutes around meetings
- Whether blocks should be marked busy or free
