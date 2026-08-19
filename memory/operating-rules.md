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
- 2026-08-18 — Google Calendar is connected and confirmed live. When Calendar and
  `memory/user.md` disagree about a recurring commitment, trust `memory/user.md`'s
  stated pattern over an empty Calendar slot. See `time-orchestration/SKILL.md`
  § Always start by reading reality. **2026-08-19 update:** the university/club
  gap this rule was written for is now resolved at the source — both are real
  recurring Calendar events on the correct account (`amerelshair.ai@lindrize.online`;
  an earlier session-only connector had briefly pointed at a different account,
  now fixed). The precedence rule itself stays as a general safety principle for
  any future memory/Calendar mismatch, not specific to this one gap anymore.
- 2026-08-18 — n8n runs on Amer's localhost via a Cloudflare tunnel
  (`https://pockets-overcome-back-forgot.trycloudflare.com/mcp-server/http`), and
  the MCP connection has to be reconnected by Amer each time it's needed — it does
  not stay live session to session. **Before any n8n build/update-workflow work
  starts** (not just when a tool call fails), tell Amer explicitly that this stage
  is coming so he can reconnect it first, rather than discovering the tool is
  unavailable mid-task. Applies to `automation-architecture` primarily, but to any
  skill that ends up touching n8n. **2026-08-19 update, confirmed by Amer:** this
  is architectural, not a bug to diagnose — n8n runs on his localhost, so a
  permanent connection genuinely isn't possible; may drop mid-session too, not just
  between sessions. Standing behavior: **always ask Amer first**, he'll
  re-establish the MCP connection each time. See
  `automation-architecture/references/n8n-access.md`.
- 2026-08-19 — `get_node_types` (n8n MCP) fails with a captured, reproducible error
  (`Error: Invalid path - path traversal detected`), confirmed across two separate
  sessions. Interim workaround now standing in `automation-architecture/SKILL.md`
  § Node parameter verification: cross-check node parameters manually in the n8n
  UI before relying on generated workflow code; never treat a `validate_workflow`
  pass as proof they're correct.
