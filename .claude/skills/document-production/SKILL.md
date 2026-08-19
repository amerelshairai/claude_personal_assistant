---
name: document-production
description: Produce professional deliverables — PDF, DOCX, XLSX, PPTX — for technical documentation, project plans, requirements, financial models, ROI analyses, proposals, internal reports, architecture documents and meeting prep. Use when Amer needs a real file rather than an answer in chat.
when_to_use: Triggers on "write the documentation", "create a proposal", "make a report", "build the financial model", "prepare a deck", "put this in a Word doc", "export this as PDF".
---

# Document Production

> **STATUS: TESTED.** Contract and methodology below are decided and exercised
> against 2 scenarios (a client proposal and an ROI workbook, both built from real
> prior-stage artifacts with checked arithmetic) — see
> `references/DESIGN-QUESTIONS.md` for the full reasoning and every fix each
> scenario produced. Meeting-prep template exists but wasn't scenario-tested, per
> Amer — not a blocker.

## Use the format skills

Do not hand-roll document generation. Read the relevant skill first, then build:

| Output | Skill |
| --- | --- |
| Word | `docx` |
| Spreadsheet / financial model | `xlsx` |
| Presentation | `pptx` |
| PDF | `pdf` |
| Charts inside any of the above | `dataviz` |

Research and gather content **first**. Read the format skill only once the substance
is settled.

## Permissions

Level 1: creating documents, updating files created for the current task, updating
material Amer explicitly provided, updating files clearly in scope.

Level 2: any client-facing document — proposal, contract, client report. Produce it,
mark it `READY FOR REVIEW`, stop.

Level 3: sending, publishing, or delivering any document to a client.

## Hard rules

- **Never delete a file.** Ever, without explicit approval.
- Never modify unrelated files.
- Never silently overwrite existing work — if a file exists, say so and version it
  (`-v2`, or a date suffix) rather than replacing it.
- Client-facing documents never contain internal cost, margin, or internal notes.
  Check before producing.
- **Never finalize a proposal's Investment figure without Amer explicitly
  confirming the price first.** If `business-analysis` produced a range or an
  ASSUMED figure rather than an agreed number, mark it `[AMER TO CONFIRM]` in the
  draft and stop there — don't pick a midpoint, don't round to something
  "reasonable." This applies every time a price hasn't been explicitly confirmed
  by Amer, not just when the upstream figure happens to be a range. Confirmed
  2026-08-19, from the Nova proposal test.

## Output locations

- Client deliverables → `projects/<client>/deliverables/`
- Internal analysis → `projects/<client>/analysis/`
- Cross-project reports → `reports/`
- Reusable shapes → `templates/`

## House style

No real brand assets yet — **structure and readability over visual style**, per
Amer directly ("there is no specific style," but "must be divided to topics and
easy to search and read").

- Font: default/standard professional font per tool (e.g. Calibri) — no custom
  branding.
- Colors: minimal, neutral — no assertive accent color.
- **Every document**: clear heading hierarchy, a table of contents for longer
  documents, descriptive section titles, PDF bookmarks/outline where supported.
- No logo yet — text-based header. Page numbers in the footer; "Confidential" note
  on client-facing documents only.

## Templates

- **Technical documentation** — not a separate template. Reuses
  `automation-architecture/templates/workflow-design.md` content directly;
  document-production's job is exporting it to a real file, not designing new
  content.
- **Proposal**: Overview → Recommended Solution (plain language, from
  `automation-architecture`) → What's Included → Investment (price only, from
  `business-analysis` — never internal margin/cost) → Payment Terms (per
  `memory/business.md`) → Privacy & Data Handling → Timeline (from
  `project-planning`'s milestones) → Next Steps. Template:
  `templates/proposal.md`.
- **ROI / financial model workbook** (xlsx): Cost breakdown → Time/financial
  value (from `business-analysis`'s ROI methodology — never an invented recovery
  rate) → 12-month projection. Client-facing version omits internal figures
  entirely; an internal version with margin stays in `projects/<client>/analysis/`,
  never delivered. Shape: `templates/roi-workbook.md`.
- **Meeting-preparation one-pager** (internal only, never delivered): Who → Why
  this meeting → Key facts to have ready → Open questions to raise → Decisions
  needed from Amer. Template: `templates/meeting-prep.md`.
