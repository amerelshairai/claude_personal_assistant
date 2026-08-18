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

## Tool set — CONFIRMED LIVE 2026-08-18
24 tools available via the MCP connection above (all under the
`mcp__claude_ai_n8n__` prefix):

`search_workflows`, `get_workflow_details`, `create_workflow_from_code`,
`update_workflow`, `validate_workflow`, `test_workflow`, `execute_workflow`,
`get_execution`, `publish_workflow`, `unpublish_workflow`, `archive_workflow`,
`search_nodes`, `get_node_types`, `get_suggested_nodes`, `get_sdk_reference`,
`prepare_test_pin_data`, `search_folders`, `search_projects`,
`search_data_tables`, `create_data_table`, `rename_data_table`,
`add_data_table_column`, `rename_data_table_column`, `delete_data_table_column`,
`add_data_table_rows`.

**Verification:** first tool search attempt (immediately after Amer said he'd
reconnected) came back empty — three separate searches found nothing. A short time
later, the tools appeared and `search_workflows` was called: it returned 36 real
workflows from Amer's actual n8n instance (e.g. "gmail leads", "RAG", "script
scraper"), confirming the connection is genuinely live, not just configured. The
earlier empty searches were likely the connection still propagating, not a
session-restart requirement as first guessed.

**Build workflow, per the MCP server's own instructions** (`get_sdk_reference` →
`search_nodes` for needed services/utilities → `get_suggested_nodes` optionally →
`get_node_types` for exact params on every node used → write SDK code →
`validate_workflow` → `create_workflow_from_code` with a short description →
`update_workflow` for changes → `archive_workflow` when retiring one). Follow this
exactly — do not guess node parameter names; `get_node_types` is not optional.

## Permissions mapping, applying `../SKILL.md` § Permissions to the real tools
- **Level 1 (execute, then report):** `search_workflows`, `get_workflow_details`,
  `create_workflow_from_code`, `update_workflow`, `validate_workflow`,
  `test_workflow`, `get_execution`, `search_nodes`, `get_node_types`,
  `get_suggested_nodes`, `get_sdk_reference`, `prepare_test_pin_data`, data-table
  tools. `execute_workflow` is Level 1 for testing/debugging, but be aware a
  workflow with real external side effects (an actual message sent, a real record
  created) can have consequences beyond the test itself — think about what the
  workflow actually does before running it, not just whether calling the tool is
  permitted.
- **Level 3 (always ask):** `publish_workflow` / `unpublish_workflow` — this is the
  "deploying to production" step SKILL.md already gates.
- **No delete tool exists for workflows** — only `archive_workflow`, which is
  reversible, not a hard delete. This naturally satisfies "never delete a workflow"
  at the tool level, similar to how `.claude/settings.json` backs the global
  no-delete rule elsewhere in this project.

## Still to record once actually building against it
- n8n version (node availability differs by version) — not yet confirmed.
- Which environments exist (dev / prod) and which one Claude may touch — Amer's
  `search_workflows` result shows one project's workflows; multi-environment setup
  not yet confirmed.

## Fallback
If the MCP connection isn't available and reconnecting isn't practical in the
moment, `automation-architecture` still produces importable workflow JSON designs
without executing against a live instance — see the STATUS note in `../SKILL.md`.
Never claim a workflow was deployed or tested when it was only designed.
