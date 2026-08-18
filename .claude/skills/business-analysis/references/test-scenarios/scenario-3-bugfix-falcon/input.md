# Scenario 3 — input (synthetic, reusing the Falcon Realty incident)

**Reusing the exact incident from
`time-orchestration/references/test-scenarios/scenario-2-urgent-midweek/`**, this
time run through `business-analysis`'s costing lens instead of the scheduling lens.

## The incident (as originally described)
Falcon Realty's WhatsApp lead-routing integration — already delivered, existing
client — broke in production. Incoming leads silently fail to route to any agent.
Actively blocking their live business right now.

## How time-orchestration treated it (for comparison)
- Effort: **3h**, labeled **Build**.
- Priority: P1, effectively due today.
- No Diagnosis/Fix split — a single flat 3h number.
- No confidence label on the estimate.
- Consumed the entirety of that day's ~3.0h AVAILABLE (GAP = 0h, no slack).
- Resolved via the P1-vs-P1 nearest-deadline tiebreak against Nova's competing
  Thursday block.

## What's unknown about the actual fault
Leads are "silently failing to route" — no error message reported by the client.
Plausible causes span a wide range: an expired webhook subscription or API token
(fast to fix once found), a changed WhatsApp/Meta payload schema, an internal
agent-assignment logic bug, or a downstream CRM permission issue (all slower to
trace). Nobody has looked at logs yet.

## Support-period status
This integration was delivered well before this incident (it's already "in
production," not a fresh handover) — per `memory/business.md`, the free 3–5 day
post-delivery bug-fix window has almost certainly already passed. This is
**billable maintenance work**, not free support.
