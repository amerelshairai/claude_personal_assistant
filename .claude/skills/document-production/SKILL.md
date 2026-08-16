---
name: document-production
description: Produce professional deliverables — PDF, DOCX, XLSX, PPTX — for technical documentation, project plans, requirements, financial models, ROI analyses, proposals, internal reports, architecture documents and meeting prep. Use when Amer needs a real file rather than an answer in chat.
when_to_use: Triggers on "write the documentation", "create a proposal", "make a report", "build the financial model", "prepare a deck", "put this in a Word doc", "export this as PDF".
---

# Document Production

> **STATUS: SCAFFOLD.** Contract fixed; house style and templates to be built.

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

## Output locations

- Client deliverables → `projects/<client>/deliverables/`
- Internal analysis → `projects/<client>/analysis/`
- Cross-project reports → `reports/`
- Reusable shapes → `templates/`

## To build

- Amer's house style: fonts, colors, logo, header/footer
- Proposal template
- Technical documentation template
- ROI / financial model workbook template
- Meeting preparation one-pager template
