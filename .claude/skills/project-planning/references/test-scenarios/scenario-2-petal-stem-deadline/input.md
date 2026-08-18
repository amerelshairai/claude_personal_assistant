# Scenario 2 — input (fresh synthetic client, real capacity data)

**Client:** Petal & Stem Florist (synthetic) — new prospect, no prior relationship
(unlike Nova, chosen deliberately to make the pre-price-demo case natural).

## Real tool verification, done before building this scenario (2026-08-18)
- **Google Calendar**: confirmed live (real `list_calendars`/`list_events` calls).
  Primary calendar empty for the next 10 days — per the new standing rule, capacity
  below uses `memory/user.md`'s recurring university/club pattern layered on top of
  that empty Calendar, not the empty Calendar alone.
- **Todoist**: confirmed live (real `get-overview` call). One placeholder task
  ("no", in a project named "yes") and one empty project — **zero real competing
  client workload**. Neither tool is yet organized per `todoist-management`'s
  confirmed conventions.
- Because real competing load is genuinely zero, tightness in this scenario comes
  from the client's own ask being demanding against real capacity — not from
  fabricated conflicts.

## Requirement
Automate large/event floral order intake (replacing manual phone-based ordering),
delivery reminders, and order-status updates via WhatsApp. Greenfield build (no
existing system).

## The client's own words
- "I've been burned by an agency before who oversold me. I want to see a working
  demo of the order-intake flow within 2 days before I commit to a price."
- "I'm exhibiting at a wedding expo this Saturday and need the full system —
  intake, reminders, status updates — live before then."

Today: **Tuesday, 2026-08-18.** Demo deadline: **Thursday, 2026-08-20.** Full
system deadline: **Saturday, 2026-08-22.**

## Effort (greenfield, per business-analysis's methodology — widest contingency)
- Research: 3h (understanding current order/delivery process)
- Build: 14h total — 6h of it is the order-intake flow specifically (the demo
  scope), 8h is reminders + status updates (the rest)
- Admin: 1.5h
- Call: 1h (discovery, actual length)
- **Raw total: 19.5h**
