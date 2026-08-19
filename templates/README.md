# templates/

Reusable document and workflow shapes, built 2026-08-19 (`document-production`
step 7):

- `proposal.md` — client proposal structure
- `roi-model.md` — financial model shape; instantiate as a real `.xlsx` via the
  `xlsx` skill when producing one for a client, don't hand-roll the spreadsheet
- `meeting-prep.md` — one-pager before a client call (internal only)

**No separate technical-documentation template exists here** — that document is
`automation-architecture/templates/workflow-design.md`; document-production's job
is exporting its existing content to a real file, not designing new content.

Skill-specific templates live with their skill, in
`.claude/skills/<skill>/templates/`. Put something here only when more than one
skill uses it.
