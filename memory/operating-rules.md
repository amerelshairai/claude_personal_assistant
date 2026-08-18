# Standing rules from Amer

> Durable instructions Amer has given that apply across sessions.
> Add a dated line each time he states a rule. Never invent one.
> If a rule here conflicts with `.claude/rules/execution-policy.md`, the execution
> policy wins — the permission model is not overridable by preference.

## Format
`YYYY-MM-DD — <rule>`

## Rules
- 2026-08-15 — Never delete anything without explicit approval.
- 2026-08-15 — Prefer short, direct communication. Lead with the answer.
- 2026-08-15 — Calendar is fixed commitments; Todoist is workload. Never merge them.
- 2026-08-15 — Report all autonomous work. Never execute silently.
- 2026-08-15 — Do not research Amer's personal profile for client work.
- 2026-08-18 — n8n runs on Amer's localhost via a Cloudflare tunnel
  (`https://pockets-overcome-back-forgot.trycloudflare.com/mcp-server/http`), and
  the MCP connection has to be reconnected by Amer each time it's needed — it does
  not stay live session to session. **Before any n8n build/update-workflow work
  starts** (not just when a tool call fails), tell Amer explicitly that this stage
  is coming so he can reconnect it first, rather than discovering the tool is
  unavailable mid-task. Applies to `automation-architecture` primarily, but to any
  skill that ends up touching n8n.
