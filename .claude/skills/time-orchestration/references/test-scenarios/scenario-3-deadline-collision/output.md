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

## Flags — resolved 2026-08-17

1. **Unconfirmed time-pinned requests:** represented as a tentative Calendar event
   from the moment they're raised — titled `[Tentative] <client> — <what>` — not a
   new third state. Once Amer accepts it, the `[Tentative]` prefix drops and it's a
   normal confirmed event. Nova's verification window would have been logged this
   way immediately, rather than living only in conversation.
2. **Confirmed, no change needed:** a specific-clock-time requirement always belongs
   on Calendar once accepted; Todoist due dates stay date-only.
