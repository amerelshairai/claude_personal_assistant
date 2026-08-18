# Architecture diagram conventions

Diagrams are the **primary** artifact in every workflow design (see `../SKILL.md`
§ Documentation style) — built for a reader who avoids technical detail, per Amer's
own stated preference. Confirmed 2026-08-18.

## Format
Mermaid `flowchart LR` (left-to-right — matches how a workflow actually runs,
trigger to outcome).

## Node shapes
- **Trigger** — rounded/stadium shape, e.g. `([New order received])`.
- **Action** — rectangle, e.g. `[Send WhatsApp confirmation]`.
- **Condition / branch** — diamond, e.g. `{Payment confirmed?}`.
- **External system touchpoint** (CRM, DB, API) — subroutine/double-border shape,
  e.g. `[[Update CRM record]]`.

## Labeling
**Plain-language node labels — the business action, not the raw n8n node type.**
"Send WhatsApp confirmation," not "WhatsApp node — sendMessage." Someone who never
opens n8n should be able to follow the diagram.

## Extensibility
Structure the diagram so a later added feature extends it (a new branch, a new node
downstream) rather than requiring a redraw. Group related nodes so an addition has
an obvious place to attach.

## Where DB/API-key detail goes
**Not on the diagram.** Database and credential specifics live in
`workflow-design.md` § 3, held to full precision there — the diagram stays at the
"visualizing structure" level Amer actually wants to read.
