# automation-architecture — decisions to make before full implementation

Per BUILD-PLAN.md step 5. n8n access resolved first (see `n8n-access.md`), as the
build order requires.

Already effectively answered by the existing SKILL.md scaffold — not re-asked:
the "Every design states" table (WHAT/WHY/HOW/DEPENDENCIES/RISKS/COST/EFFORT) and
the "Non-negotiable design elements" list already define most of what a design
document needs to contain.

## 1. n8n patterns library — DECIDED (2026-08-18)
**No fixed node-sequence library exists, and none should be forced.** Amer's own
words: "there is no common node sequence for my work, it all depends on what the
client wants." Every project starts from the requirement, not a template workflow.

What *does* recur is **trigger selection by requirement type** — a decision
framework, not reusable node chains:
- Customer support requirement → start from a webhook or Telegram trigger.
- CRM-building requirement → often a Google Sheets trigger.
- (More entries added to `references/n8n-patterns.md` as they come up in real
  projects — this file grows from experience, never invented ahead of time.)

`references/n8n-patterns.md` is this trigger-selection reference, not a library of
full reusable workflows.

## 2. Workflow design document template — DECIDED (2026-08-18)
**Diagram-first, not prose-first.** Amer's own words: documentation is "all about
the visualizing structure of how it works," and he "avoids technical details as
much as possible" — with one explicit exception: **anything related to database or
API keys must be precise**, never glossed over.

`templates/workflow-design.md` shape:
1. **Architecture diagram** (the primary artifact — see §3) showing trigger → nodes
   → outcome, extensible for features added later.
2. **WHY** — which business requirement each component serves (plain language, no
   jargon).
3. **Database / credentials / API keys** — the one area held to full technical
   precision: what's stored, where, auth method. Never hand-waved.
4. The rest of the existing "Every design states" table (DEPENDENCIES, RISKS, COST,
   EFFORT) stays, but in plain language — WHAT/HOW live in the diagram, not repeated
   as dense technical prose in the doc.

## 3. Architecture diagram conventions — DECIDED (2026-08-18)
Diagrams are the **primary** communication artifact per §2, not a supplement — so
they need to read clearly to someone who (like Amer, by his own description) avoids
technical detail. Mermaid flowchart, left-to-right, plain-language node labels (the
business action, not the raw n8n node type), distinct shapes for trigger vs. action
vs. condition/branch. Built to be extensible — adding a later feature should extend
the diagram, not force a redraw.

## Test scenarios
To be built once 1–3 are locked, same pattern as every other skill: synthetic
automation-design requests, run one at a time.
