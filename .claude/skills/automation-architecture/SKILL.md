---
name: automation-architecture
description: Turn business requirements into technical automation designs — n8n workflows, API integrations, webhooks, data flows, AI/LLM components, error handling and monitoring. Use when Amer needs an automation designed, an n8n workflow architected or debugged, or a technical approach chosen for a client requirement.
when_to_use: Triggers on "design this automation", "how should I build", "n8n workflow", "architect this integration", "API design", "webhook", "this workflow is failing", "technical approach".
---

# Automation Architecture

> **STATUS: METHODOLOGY DEFINED.** Contract and methodology below are decided (see
> `references/DESIGN-QUESTIONS.md` for the full reasoning behind each). Test
> scenarios still pending.
>
> **ENVIRONMENT NOTE (updated 2026-08-18):** An n8n MCP connector is configured and
> **confirmed live** (`references/n8n-access.md`) — 24 tools, verified by a real
> `search_workflows` call returning Amer's actual workflows. It runs against
> Amer's localhost via a Cloudflare tunnel that he must **reconnect manually every
> session** — it is not reliably live session to session, even though it's working
> right now. **Tell Amer before any build/update-workflow stage starts** so he can
> reconnect first (see `memory/operating-rules.md`) — verify with a real read call
> (e.g. `search_workflows`) before relying on it, don't assume a prior session's
> connection carried over. If genuinely unavailable, this skill still produces
> importable workflow JSON without executing against a live instance. Never claim a
> workflow was deployed, tested, or executed without an actual tool result to show
> for it. **`get_node_types` is currently broken** (see `references/n8n-access.md`)
> — do not treat a `validate_workflow` pass as proof of correct node parameters
> while it's down; flag exact parameters as unconfirmed instead.

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
- **Human approval points** — where a person must confirm before an irreversible step
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

## Documentation style — diagram-first

Amer avoids technical detail wherever possible and thinks in terms of *"the
visualizing structure of how it works"* — **except** database and API-key handling,
which stay fully precise, never glossed over. Every design leads with the
architecture diagram (`templates/architecture-diagram.md`); everything else
(WHY, dependencies, risks, cost, effort) stays in plain language. See
`templates/workflow-design.md` for the full shape.
