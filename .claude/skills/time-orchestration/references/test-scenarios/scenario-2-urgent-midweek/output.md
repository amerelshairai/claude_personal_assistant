# Scenario 2 — orchestrator walkthrough (synthetic)

Running the 13-step sudden-circumstance protocol (time-orchestration SKILL.md).

## 1–3. Understand / estimate / deadline
Falcon Realty's production WhatsApp integration is down — leads are silently failing
to route. Effort: 3h (Build). Deadline: effectively today — every hour costs the
client live leads.

## 4–6. Todoist load, Calendar, available time
- Today (Wed): AVAILABLE was 3.0h (fixed formula, Scenario 1), **already fully
  consumed** by the 6–9am Nova block that already ran. Remaining today: **0h.**
- Thu: 3.0h AVAILABLE, currently allocated to a planned Nova continuation block
  (not yet executed — still movable).
- Fri (Nova's due date): no explicit `realistic_productive_hours_per_day` figure
  exists in `memory/user.md` for Friday specifically — it only describes the raw
  5–10pm window (family time until 5pm). Approximated **~3.6h** (5h raw − breaks −
  15% buffer) for this walkthrough. **Flagged below — this is a real gap**, not
  something to keep approximating scenario to scenario.

## 7. Identify conflicts
Two P1 client-facing items are competing for the same near-term capacity:
- **Falcon Realty emergency** — 3h, needs today, 0h left today.
- **Nova Home Goods Build task** — 5h remaining, due Friday. Plan was Thu (3h) +
  Fri (2h of Fri's ~3.6h), comfortably on track.

If Thursday's block is redirected to the Falcon emergency: Nova gets 0h Thursday,
leaving 5h remaining for Friday — but Friday only has ~3.6h. **Shortfall: ~1.4h.**
Redirecting Thursday to fix today's emergency causes Nova's own Friday deadline to be
missed, on current numbers.

## 8. Recalculate priorities — a real gap found here
Both items are **P1** by the todoist-management priority mapping (client-facing,
near/at deadline) — the mapping has no tiebreaker for **P1 vs. P1**. Reasoning
informally: an active production outage blocking a client's live operations right now
plausibly outranks a build task that's currently still on-track with (some) buffer —
but that's my judgment call, not a rule the methodology currently states anywhere.
**Flagged below.**

## 9–10. Recommend / reschedule — stopped here, not executed
Recommendation: move the Falcon emergency into today's now-freed evening slot **is
not possible** — there's no legitimate capacity left today per stated working hours
(gym is a hard stop at 10pm, no sanctioned overtime window exists in `memory/user.md`).
The only real options:
- **(a)** Redirect Thursday's Nova block to the Falcon emergency instead, accepting
  that Nova's Friday deadline is now at risk (~1.4h short) unless something else
  changes.
- **(b)** Exceed today's realistic capacity ceiling as a one-off exception for a
  genuine production emergency, keeping Thursday's plan for Nova intact.
- **(c)** Something else Amer decides (e.g., tell Falcon Realty the fix lands first
  thing tomorrow instead of today).

## 11–13. Update Todoist/Calendar, report — NOT executed pending the flag below

I did **not** move Thursday's block or touch either task's schedule. Per Level 1,
rescheduling Todoist tasks and Claude-created Calendar work blocks is normally
execute-then-report — but this specific reschedule doesn't just reorganize Amer's
own time, it trades one client's (Falcon) emergency against another client's (Nova)
already-committed deadline. That reads like a business-relationship call, not a pure
scheduling optimization, so I stopped and surfaced it instead of executing option (a)
silently. **This interpretation itself is flagged below, not assumed correct.**

## Report (per `.claude/rules/reporting.md`)
```
BLOCKED
- Falcon Realty emergency fix (3h, needed today) — 0h capacity remains today

NEEDS YOU
- Choose (a) redirect Thu's Nova block to the emergency, accepting Nova's Friday
  deadline is then ~1.4h short; (b) treat today's emergency as a one-off exception
  to the capacity ceiling and keep Thu's Nova plan intact; or (c) something else
- Confirm whether a cross-client tradeoff like this should be Level 1
  (execute-then-report) or always surfaced first, per the flag below
```

---

## Flags — resolved 2026-08-17

1. **P1-vs-P1 tiebreaker:** ties within the same tier break by nearest deadline —
   same rule as every other tier, no special case. Applied here, Falcon's emergency
   (needed today) beats Nova's Friday-due task on that basis alone, without needing
   a separate "active harm" rule.
2. **Cross-client tradeoff authority:** now explicit policy in
   `.claude/rules/execution-policy.md` § Cross-client scheduling tradeoffs — a
   replan that puts a *different* client's deadline at risk always surfaces for
   approval first, never auto-executes, even though it would otherwise qualify as a
   normal Level 1 reschedule. Confirms this walkthrough's judgment call was right,
   now as a standing rule instead of an ad hoc choice.
3. **Friday capacity:** on Amer to fill in — real per-weekday capacity figures are
   being added to `memory/user.md` to replace the single flat "university/club day"
   number, since Friday's shape (family time until 5pm, then 5–10pm) isn't the same
   as a Tuesday. This walkthrough's ~3.6h approximation stands until that lands.
