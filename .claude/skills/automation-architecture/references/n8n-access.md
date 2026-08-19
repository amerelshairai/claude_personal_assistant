# n8n access — resolved 2026-08-18

## Connection
- n8n runs on Amer's **localhost**, exposed via a Cloudflare tunnel.
- MCP connection: `https://pockets-overcome-back-forgot.trycloudflare.com/mcp-server/http`
  — already configured as an MCP server in Claude (this satisfies option 1 from the
  original unresolved note below).
- Also available: a **webhook connector**, visible through Claude's connectors.

## Known issue: connection is not persistent (updated 2026-08-19)
The tunnel/MCP connection does **not** reliably stay live — confirmed dropping both
between sessions and (per Amer, 2026-08-19) potentially mid-session too, unlike
Todoist/Calendar which stay authenticated once connected. A tool search for n8n
tools may come back empty even when Amer believes it's connected. Confirmed
empirically 2026-08-18: a tool search at the start of that session found no n8n
tools available; they appeared a short time later without any explicit reconnect
action in that instance — so the failure mode isn't fully consistent yet.

**Impact:** any routine/scheduled task that touches n8n (not just an interactive
session) will silently fail if it fires while the connection is dropped — this
matters for the same reason the weekly-review routine's GitHub write access
mattered: an unattended failure nobody sees until they go looking.

**Not yet isolated — two live hypotheses, per Amer:**
1. n8n is connected via claude.ai's OAuth connector, and that token has a short
   expiry that doesn't auto-refresh.
2. n8n is connected via the self-hosted instance's own MCP endpoint (the Cloudflare
   tunnel to Amer's localhost), which requires that instance to actually be up and
   reachable — if it sleeps, restarts, or the tunnel URL changes, the connection
   breaks independent of any OAuth token.

**Diagnostic step, next time it drops:** check `/mcp` in Claude Code immediately and
note the exact status shown — `needs auth` points to hypothesis 1 (re-auth fixes
it); `unreachable`/`not found` points to hypothesis 2 (the n8n instance/tunnel
itself needs to stay up). Amer to capture this next occurrence.

**Standing rule** (see `memory/operating-rules.md`, 2026-08-18): tell Amer explicitly
*before* any n8n build/update-workflow stage starts, so he can check/reconnect
first — don't wait for a tool call to fail mid-task. This holds regardless of which
hypothesis turns out to be right.

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

## Known issue: `get_node_types` is broken (found 2026-08-18, still broken 2026-08-19)
**Exact verbatim error, already captured — not an open diagnostic question:**
```
Error: Invalid path - path traversal detected
```
Reproduced 3 separate ways during the original test (all identical error):
1. `get_node_types({ nodeIds: ["n8n-nodes-base.wait"] })` — plain string, no
   discriminators.
2. `get_node_types({ nodeIds: [{ nodeId: "n8n-nodes-base.webhook" }, ...6 more with
   discriminators] })` — full batch call as the MCP server's own instructions
   describe.
3. `get_node_types({ nodeIds: ["n8n-nodes-base.manualTrigger"] })` — simplest
   possible single call, isolated from the batch, still identical error.

Isolated to this one tool: `get_sdk_reference`, `search_nodes`, and
`validate_workflow` all work correctly with real results. **This means exact node
parameters cannot currently be confirmed**, and `validate_workflow` passing is
**not** a safe substitute — it appears to check structural well-formedness, not
per-node parameter correctness (confirmed by deliberately feeding it guessed
WhatsApp node parameters, which it validated as `valid: true` anyway). See
`references/test-scenarios/scenario-2-connection-health/` for the full test.

**Given this has now held across two separate days/sessions** (2026-08-18 and
2026-08-19 checks), treat it as a standing limitation, not a one-off glitch — see
the interim workaround now in `../SKILL.md` § Documentation style / node parameters.
If a future call to `get_node_types` ever returns something *other* than this exact
error text, that's the signal worth capturing verbatim and flagging — it would mean
the failure mode changed, which matters for diagnosis.

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
