# client-intelligence — decisions to make before full implementation

Per spec §33, define these before writing the final implementation. Each needs Amer's
input or a deliberate decision. Do not guess.

## 1. Research methodology
- What is the standard research sequence? (website → competitors → reviews → tech?)
- How deep by default, and what escalates to deeper research?
- How many sources before a claim can be labeled OBSERVED?
- What is the stop condition? Research can expand forever.

## 2. Confidence rules
- What scale — High/Medium/Low, or a percentage?
- What evidence threshold maps to each level?
- Does an inference from a single source ever exceed Low?

## 3. KPI methodology
- Which KPIs matter across Amer's typical client types?
- How is a baseline established when the client has not measured anything?
- How are estimated KPIs distinguished from client-reported ones?

## 4. ROI methodology
- Time ROI, effort ROI, financial ROI — how is each computed?
- What hourly cost is assumed for the client's staff, and where does it come from?
- Over what horizon — 6 months, 12 months?
- How are ongoing costs (API, hosting, LLM tokens, maintenance) modeled?
- What is presented when inputs are unknown? A range? A refusal?

## 5. Feature discovery methodology
- How are opportunities generated systematically rather than ad hoc?
- What is the test that separates "real value" from "invoice padding"?
- Is there a checklist of common automation patterns to scan against?

## 6. Opportunity ranking
- Ranking dimensions: value, effort, risk, dependency, time-to-value?
- How are they weighted?
- Does client-stated priority override computed ranking?

## 7. Risk analysis
- Standard risk categories (technical, adoption, data, vendor, compliance, scope)?
- How is risk severity expressed?

## 8. Missing-information detection
- What is the required-information checklist that gaps are measured against?
- How are gaps ranked by how much they block the work?

## 9. Business analysis boundary
- Where exactly does `client-intelligence` stop and `business-analysis` begin?
  Proposal: intelligence identifies and roughly sizes opportunities;
  business-analysis does rigorous costing, pricing, and viability. Confirm.

## 10. Package template
- Fill `templates/package-outline.md` with the actual prompts and table shapes
  for each of the 28 sections.

## 11. Test scenarios
- Build 2–3 realistic client scenarios to test against before moving on.
  Suggested: (a) e-commerce store wanting order-ops automation,
  (b) services firm wanting CRM + lead follow-up, (c) a vague inbound lead with
  almost no information — tests the missing-information path.
