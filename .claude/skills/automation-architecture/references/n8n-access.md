# n8n access — resolved 2026-08-18

## Connection
- n8n runs on Amer's **localhost**, exposed via a Cloudflare tunnel.
- MCP connection: `https://pockets-overcome-back-forgot.trycloudflare.com/mcp-server/http`
  — already configured as an MCP server in Claude (this satisfies option 1 from the
  original unresolved note below).
- Also available: a **webhook connector**, visible through Claude's connectors.

## The catch — reconnection required every session
The tunnel/MCP connection does **not** stay live session to session — Amer has to
reconnect it manually each time before it's usable. A tool search for n8n tools may
come back empty even when Amer believes it's connected, simply because it hasn't
been reconnected yet this session. Confirmed empirically 2026-08-18: a tool search
at the start of this conversation found no n8n tools available.

**Standing rule** (see `memory/operating-rules.md`, 2026-08-18): tell Amer explicitly
*before* any n8n build/update-workflow stage starts, so he can reconnect first —
don't wait for a tool call to fail mid-task.

## Still to record once actually building against it
- n8n version (node availability differs by version) — not yet confirmed.
- Which environments exist (dev / prod) and which one Claude may touch.
- Whether Claude may execute workflows or only create/modify them.
- Production deployment approval step — **Level 3, always**, per
  `automation-architecture/SKILL.md` § Permissions. Not affected by any of the above.

## Fallback
If the MCP connection isn't available and reconnecting isn't practical in the
moment, `automation-architecture` still produces importable workflow JSON designs
without executing against a live instance — see the STATUS note in `../SKILL.md`.
Never claim a workflow was deployed or tested when it was only designed.
