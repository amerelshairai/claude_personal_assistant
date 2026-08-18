# n8n trigger selection — by requirement type

Not a reusable-workflow library. Amer: "there is no common node sequence for my
work, it all depends on what the client wants." This file tracks **which trigger to
start from given the kind of requirement**, grown from real projects — never
invented ahead of time. Add an entry only after it's actually come up.

| Requirement type | Typical starting trigger | Notes |
| --- | --- | --- |
| Customer support / inquiry handling | Webhook, or Telegram trigger | Matches whichever channel the client's customers actually use |
| CRM building | Google Sheets trigger (often) | Depends on what the client already uses as their record store |

Confirmed by Amer, 2026-08-18.
