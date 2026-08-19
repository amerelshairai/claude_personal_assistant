---
name: automation-architecture
description: Turn business requirements into technical automation designs — n8n workflows, API integrations, webhooks, data flows, AI/LLM components, error handling and monitoring. Use when Amer needs an automation designed, an n8n workflow architected or debugged, or a technical approach chosen for a client requirement.
when_to_use: Triggers on "design this automation", "how should I build", "n8n workflow", "architect this integration", "API design", "webhook", "this workflow is failing", "technical approach".
---

# Automation Architecture

> **STATUS: TESTED.** Contract and methodology below are decided and exercised
> against 2 scenarios (a fully synthetic design, and a real-n8n connection-health/
> logic check) — see `references/DESIGN-QUESTIONS.md` for the full reasoning and
> every fix each scenario produced.
>
> **ENVIRONMENT NOTE (updated 2026-08-19):** An n8n MCP connector is configured
> (`references/n8n-access.md`) but **cannot stay permanently connected — confirmed
> architectural, not a bug**: n8n runs on Amer's localhost, so the connection
> requires him to re-establish it each time it's needed, and may drop mid-session
> too. **Always ask Amer before any build/update-workflow stage starts** so he can
> make the connection again (see `memory/operating-rules.md`) — verify with a real
> read call (e.g. `search_workflows`) before relying on it, don't assume a prior
> session's connection carried over. If genuinely unavailable, this skill still
> produces importable workflow JSON without executing against a live instance.
> Never claim a workflow was deployed, tested, or executed without an actual tool
> result to show for it. **`get_node_types` is broken with a captured, reproducible
> error** (`references/n8n-access.md`) — see § Node parameter verification below
> for the interim workaround.

## Input → output

Takes business requirements (usually from `client-intelligence` or Amer directly),
produces a technical design that another person could build from.

## Design surface

n8n architecture · workflow design · API architecture · webhooks · authentication ·
data flows · AI/LLM components · databases · CRM integrations · messaging systems ·
error handling · retry logic · logging · monitoring · security · cost · scalability ·
maintenance · human approval points.

## Every design states

| Dimension | Must answer |
| --- | --- |
| WHAT | The components and how data moves between them |
| WHY | Which business requirement each component serves |
| HOW | Concrete implementation — nodes, endpoints, auth method, schema |
| DEPENDENCIES | Credentials, accounts, access, other systems, client actions |
| RISKS | Failure modes and what happens when each occurs |
| COST | Setup and per-month, including API/LLM usage at expected volume |
| EFFORT | Realistic build hours, feeding `business-analysis` and `project-planning` |

## Non-negotiable design elements

A design without these is incomplete, not "v1":

- **Error handling** — what happens when each external call fails
- **Retry logic** — with backoff, and a dead-letter path
- **Logging** — enough to debug a failure that happened three days ago
- **Human approval points** — where a person must confirm before an irreversible
  step. For a recurring automated action bounded by a pre-approved cap (e.g. a
  discount amount, a spend limit): **auto-execute under the cap, but pause and
  notify Amer if a computed value would exceed it** — a per-run gate on every
  normal execution would defeat the point of automating it, but a value outside
  what he approved is exactly the case worth catching before it sends, not after.
  Confirmed 2026-08-18, from the Nova cart-recovery test.
- **Credential handling** — never hardcode; never put a real secret in a design doc

## Permissions

Designing, building, modifying, testing and debugging automations is Level 1 —
execute and report. **Deploying to production is Level 3** — always ask.
Never delete a workflow.

## Trigger selection (not a fixed pattern library)

There is no reusable node-sequence library — every design starts from what the
client actually needs, not a template workflow. What recurs is **trigger choice by
requirement type**; see `references/n8n-patterns.md` for the running list (grows
from real projects, never invented ahead of time). E.g.: customer support →
webhook/Telegram trigger; CRM-building → often a Google Sheets trigger.

## Node parameter verification (interim workaround, added 2026-08-19)

`get_node_types` has failed identically across two separate sessions (2026-08-18,
2026-08-19) — see `references/n8n-access.md` for the exact captured error. Treat it
as a standing limitation, not a transient glitch, until proven otherwise:

- **Never treat a `validate_workflow` pass as confirmation of correct node
  parameters** — it checks structural well-formedness, not per-node schema
  correctness (proven by feeding it deliberately wrong WhatsApp parameters, which
  it still validated as fine).
- For any node whose exact parameters can't be confirmed via `get_node_types`,
  **flag them explicitly as unconfirmed/ASSUMED** in the design and in any
  generated workflow code — never present them as verified.
- **Interim workaround**: cross-check unfamiliar node parameters manually against
  n8n's own UI (Amer has direct access; Claude doesn't) before Amer imports or
  relies on generated workflow code. This is a real extra step, not optional,
  until `get_node_types` is fixed.
- If a future `get_node_types` call ever returns something other than the exact
  captured error text, that's worth flagging immediately — it means the failure
  mode changed.

## Documentation style — diagram-first

Amer avoids technical detail wherever possible and thinks in terms of *"the
visualizing structure of how it works"* — **except** database and API-key handling,
which stay fully precise, never glossed over. Every design leads with the
architecture diagram (`templates/architecture-diagram.md`); everything else
(WHY, dependencies, risks, cost, effort) stays in plain language. See
`templates/workflow-design.md` for the full shape.
