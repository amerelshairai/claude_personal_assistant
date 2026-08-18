---
name: automation-architecture
description: Turn business requirements into technical automation designs — n8n workflows, API integrations, webhooks, data flows, AI/LLM components, error handling and monitoring. Use when Amer needs an automation designed, an n8n workflow architected or debugged, or a technical approach chosen for a client requirement.
when_to_use: Triggers on "design this automation", "how should I build", "n8n workflow", "architect this integration", "API design", "webhook", "this workflow is failing", "technical approach".
---

# Automation Architecture

> **STATUS: SCAFFOLD.** Contract fixed; patterns library to be built.
>
> **ENVIRONMENT NOTE (updated 2026-08-18):** An n8n MCP connector is configured
> (`references/n8n-access.md`), but it runs against Amer's localhost via a
> Cloudflare tunnel that he must reconnect manually every session — it is not
> reliably live. **Tell Amer before any build/update-workflow stage starts** so he
> can reconnect first (see `memory/operating-rules.md`). If it's genuinely
> unavailable, this skill still produces importable workflow JSON without executing
> against a live instance. Do not claim a workflow was deployed or tested when it
> was only designed, or when the connector wasn't actually confirmed live.

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

## To build

- `references/n8n-patterns.md` — reusable node patterns Amer keeps rebuilding
- `references/n8n-access.md` — how to connect n8n (MCP, REST API, or manual import)
- `templates/workflow-design.md` — the standard design document shape
- `templates/architecture-diagram.md` — Mermaid conventions for data flow diagrams
