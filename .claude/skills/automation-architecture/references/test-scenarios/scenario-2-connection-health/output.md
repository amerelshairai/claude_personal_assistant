# Scenario 2 — real n8n connection-health + logic check (live tools, no build)

Per Amer's combined-approach instruction: uses the real, live n8n MCP connection —
read-only and validate-only calls only, **nothing created in real n8n**. Checks
whether Scenario 1's synthetic design is actually buildable with real nodes, and
whether the connection is genuinely healthy end to end, not just "tools appear in
ToolSearch."

## Calls made, in order

1. **`get_sdk_reference`** (section: all) — ✅ returned full SDK docs, patterns,
   expression syntax, coding rules. Confirms this tool works.
2. **`search_nodes`** (queries: whatsapp, wait, if, http request, set) — ✅ returned
   real results. Confirms every node Scenario 1's design needs actually exists:
   `n8n-nodes-base.whatsApp` (resource: message, operation: send),
   `n8n-nodes-base.wait`, `n8n-nodes-base.if`, `n8n-nodes-base.httpRequest`,
   `n8n-nodes-base.set`. Scenario 1's design is buildable with real, existing nodes
   — not a plausible-sounding design that turns out to reference nodes that don't
   exist.
3. **`get_node_types`** — ❌ **BROKEN.** Every call returns `Error: Invalid path -
   path traversal detected`, including the simplest possible single node ID
   (`n8n-nodes-base.manualTrigger`) with no discriminators at all. Tried 3 times
   with different inputs (single string, array of strings, array with discriminator
   objects) — same error every time. **This is the tool the MCP server's own
   instructions say is mandatory** ("Include the type definitions... DO NOT skip
   this — guessing parameter names creates invalid workflows"), and it does not
   work right now.
4. **`validate_workflow`** — ✅ works, tested twice:
   - A minimal manualTrigger → httpRequest workflow (parameters taken directly from
     the SDK reference's own worked example, not guessed): validated clean.
   - A fuller version of Scenario 1's design (webhook trigger → IF → Wait → WhatsApp
     send), with the WhatsApp node's parameters **deliberately guessed** (since
     `get_node_types` is down) to see what would happen: **also validated as
     `valid: true`.**

## The real finding: `validate_workflow` is not a safe substitute for `get_node_types`
Point 4's second test is the important one. The MCP server's own instructions say
never to guess node parameters — but with `get_node_types` broken, guessing was the
only way to test whether validation would catch a mistake. It didn't flag anything,
even though the WhatsApp node's `phoneNumberId`/`recipientPhoneNumber`/`textBody`
parameter names were genuinely guessed, not confirmed against real type
definitions. That strongly suggests `validate_workflow` checks structural
well-formedness (nodes connect correctly, the graph parses) rather than deep
per-node parameter correctness. **A workflow can validate clean and still fail (or
silently misbehave) against the real WhatsApp node's actual schema.**

## What this means for automation-architecture going forward
- The connection is **genuinely healthy** for design/search/validate work —
  `get_sdk_reference`, `search_nodes`, and `validate_workflow` all confirmed
  working with real results.
- **`get_node_types` cannot currently be trusted** — any design work needing exact
  node parameters should say so explicitly and flag the parameters as unconfirmed,
  rather than treating a `validate_workflow` pass as proof they're correct.
- **No workflow was created** (`create_workflow_from_code` was never called) —
  consistent with Amer's "no real building" constraint for this test suite.

## Report (per `.claude/rules/reporting.md`)
```
COMPLETED
- Verified Scenario 1's design uses only real, existing n8n nodes (search_nodes)
- Confirmed get_sdk_reference and validate_workflow work correctly

BLOCKED
- get_node_types is broken (path traversal error on every call) -- cannot get
  exact node parameters right now, which the MCP server's own instructions treat
  as mandatory before writing real workflow code
```

---

## Flag for Amer's review
`get_node_types` failing this consistently (same error, every input, including the
simplest possible case) looks like a bug in the n8n MCP server itself or how it's
proxied through your Cloudflare tunnel — not something fixable from this side. Two
options until it's resolved:
1. Treat any workflow design's exact node parameters as unconfirmed/ASSUMED until
   `get_node_types` works again — `validate_workflow` passing is not enough proof.
2. If you have access to n8n's own UI, exact parameter shapes could be confirmed by
   manually inspecting a node there instead, as a workaround.

Worth you checking whether this is a known issue with the specific n8n MCP server
build you're running, or something in the tunnel setup.
