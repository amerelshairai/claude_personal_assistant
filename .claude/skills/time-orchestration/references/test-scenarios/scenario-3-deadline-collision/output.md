# Scenario 3 — orchestrator walkthrough (synthetic)

Running calendar-management's conflict protocol: identify precisely → present
options → ask before changing anything consequential.

## 1. Identify the conflict precisely
- **What:** two different clients each need Amer's real-time presence for a full
  hour, not just a flexible work block.
- **When:** Thursday 2026-08-20, 4:00–5:00pm.
- **Whose:**
  - Falcon Realty's discovery call — already booked, has another attendee (the
    client), created by Amer directly.
  - Nova Home Goods' platform-update verification window — new request, not yet on
    the Calendar at all, tied to an external event on Nova's side (their platform
    push happens at that exact time, not movable by Amer).

## 2. Present options — nothing executed yet
- **(a) Ask Nova if their window can shift.** The 4pm timing is driven by Nova's own
  platform update, not stated as immovable by Nova — worth asking before assuming
  Falcon's slot has to give.
- **(b) Ask Amer whether to request Falcon Realty reschedule the discovery call.**
  Two approval layers apply here, not one: moving/cancelling an event with another
  attendee needs Amer's explicit approval every time (calendar-management Level 3),
  and actually messaging the client about it is itself Level 2/3 (client messages)
  per execution-policy — drafted only after Amer says to, never sent without a
  separate explicit go-ahead.
- **(c) Ask whether Nova's verification genuinely needs Amer's full, undivided hour**,
  or whether a narrower form of availability (checking in at set intervals, being
  reachable rather than watching continuously) would satisfy it — reduces the
  collision instead of resolving it by moving something.
- **(d)** Something else Amer decides.

## 3. Ask before changing anything — stopped here
**No Calendar or Todoist changes made.** Falcon's call was not moved, and Nova's
window was not added to the Calendar as a confirmed commitment, since it isn't
resolved yet.

## Report (per `.claude/rules/reporting.md`)
```
NEEDS YOU
- Thu 4-5pm double-booked: Falcon Realty discovery call (existing, has attendee) vs
  Nova Home Goods verification window (new request, time-pinned to their platform
  update). Options: ask Nova to shift, ask to request Falcon reschedule (two approval
  layers, see above), ask if Nova's request can be satisfied with partial
  availability instead of the full hour, or something else.
```

---

## Flags for Amer's review (not yet resolved in SKILL.md)

1. **No representation for an unconfirmed, time-pinned client request.** Nova's
   verification window isn't a Todoist task (it has no flexible due date, it's a
   specific clock-time commitment) and isn't yet a Calendar event (it's not
   confirmed/accepted). Right now it only exists in this conversation. Should
   something like this get logged somewhere the moment it's raised — e.g., a
   tentative/pending Calendar event, or a note in the relevant `projects/nova-home-
   goods/` file — so it doesn't just live in chat history until resolved?
2. **This scenario didn't hit a true "time-pinned Todoist task" case** (a task with a
   specific clock-time requirement rather than a plain due date) — Nova's request
   turned out to belong on Calendar once framed as an appointment-like commitment.
   Worth confirming: is there ever a legitimate case for a *Todoist* task needing a
   specific clock time rather than just a due date, or does anything with a specific
   time-of-day always belong on Calendar instead, per the existing Todoist-vs-
   Calendar split? If the latter, no methodology gap remains here — but it wasn't
   explicit before this test.
