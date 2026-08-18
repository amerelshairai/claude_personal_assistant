# automation-architecture — decisions to make before full implementation

Per BUILD-PLAN.md step 5. n8n access resolved first (see `n8n-access.md`), as the
build order requires.

Already effectively answered by the existing SKILL.md scaffold — not re-asked:
the "Every design states" table (WHAT/WHY/HOW/DEPENDENCIES/RISKS/COST/EFFORT) and
the "Non-negotiable design elements" list already define most of what a design
document needs to contain.

## 1. n8n patterns library — OPEN
`references/n8n-patterns.md` — reusable node patterns Amer keeps rebuilding across
client projects. Needs Amer's real experience: what patterns come up often enough
to be worth documenting once rather than re-deriving per project?

## 2. Workflow design document template — OPEN
`templates/workflow-design.md` — the standard shape. Likely follows directly from
the "Every design states" table already in SKILL.md, but needs confirming as an
actual template (section-by-section, like `client-intelligence`'s
`templates/package-outline.md`).

## 3. Architecture diagram conventions — OPEN
`templates/architecture-diagram.md` — Mermaid conventions for data-flow diagrams
(node shapes for triggers vs. actions vs. conditions, etc.).

## Test scenarios
To be built once 1–3 are locked, same pattern as every other skill: synthetic
automation-design requests, run one at a time.
