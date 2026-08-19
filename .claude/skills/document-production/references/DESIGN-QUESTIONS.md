# document-production — decisions to make before full implementation

Per BUILD-PLAN.md step 7.

## 1. House style — DECIDED (2026-08-19)
No real brand assets yet. **Structure and readability over visual style**:
- Font: **default/standard professional font per tool** (e.g. Calibri for
  Word-family documents) — no custom or branded font choice.
- Colors: minimal, neutral — no assertive accent color mandated. Amer's own
  words: "there is no specific style."
- **Must be divided by topic and easy to search/read** — this is the actual
  requirement, not visual polish: clear heading hierarchy (H1/H2/H3), a table of
  contents for longer documents, descriptive section titles, PDF bookmarks/
  outline where the format supports it.
- No logo yet — text-based header (Amer's name/business line).
- Header/footer: page numbers; "Confidential" note on client-facing docs only.

## 2. Technical documentation template — DECIDED (2026-08-19)
**Not a separate template.** Same document as `automation-architecture`'s
`templates/workflow-design.md` (diagram-first, plain language except database/
API-keys) — document-production's job is exporting that existing content to a
real PDF/DOCX file, not designing new content.

## 3. Proposal template — DECIDED (2026-08-19)
Overview → Recommended Solution (from `automation-architecture`, plain language)
→ What's Included (deliverables) → Investment (price only, from
`business-analysis` — **never internal margin/cost**) → **Payment Terms**
(deposit/schedule per `memory/business.md`'s standard terms, reviewed per
contract) → **Privacy & Data Handling** (confidentiality commitment) → Timeline
(from `project-planning`'s milestones) → Next Steps. The two bolded sections were
Amer's explicit additions to the proposed shape.

## 4. ROI / financial model workbook — DECIDED (2026-08-19)
3 sheets: Cost breakdown (one-time/recurring/maintenance, from
`business-analysis`'s cost model, client-facing — no internal margin) → Time/
effort value + financial value where real cost data exists (`business-analysis`'s
ROI methodology — never an invented recovery rate) → 12-month projection.
**Client-facing version omits internal figures entirely**; an internal version
(with margin) stays in `projects/<client>/analysis/`, never delivered.

## 5. Meeting-preparation one-pager — DECIDED (2026-08-19)
Who (client/attendees, relationship history) → Why this meeting (objective) →
Key facts to have ready (pulled from whichever of `client-intelligence`/
`business-analysis`/`project-planning` is relevant) → Open questions to raise →
Decisions needed from Amer. **Internal only — never delivered to a client.**

## Test scenarios — IN PROGRESS

- **Scenario 1 — Nova Home Goods proposal, built from real prior-stage
  artifacts**, run 2026-08-19 —
  `references/test-scenarios/scenario-1-nova-proposal/`. Not synthetic input —
  pulled from client-intelligence, automation-architecture, business-analysis
  (GO verdict, price ~$500-650), and project-planning's existing test artifacts
  for the same client, same discipline as project-planning's own tests. Confirmed
  clean: no internal cost/margin/effort-hours leaked into the client-facing
  draft; Payment Terms and Privacy & Data Handling (Amer's explicit template
  additions) both got real content, not placeholders; milestone language matches
  project-planning's plan exactly. **One real finding:** business-analysis
  produced a price *range*, not a single number — a finished proposal needs one
  figure. Handled by marking it `[AMER TO CONFIRM]` in the draft rather than
  silently picking a midpoint, consistent with business-analysis's pricing
  hard boundary. Not a methodology gap requiring a SKILL.md change — the
  boundary already existed, this scenario just confirmed it holds when a range
  (not a point estimate) is the upstream input.
