# ROI / Financial Model — shape (build as .xlsx via the `xlsx` skill)

> Two versions of every workbook: **client-facing** (this shape, no internal
> figures) and **internal** (adds margin/cost, stays in
> `projects/<client>/analysis/`, never delivered). Check which one before
> producing — this is exactly the kind of internal-notes leak
> `document-production/SKILL.md`'s hard rule exists to prevent.

## Sheet 1 — Cost Breakdown
From `business-analysis`'s cost model: One-time / Recurring / Maintenance layers.
Client-facing: dollar figures only, no internal margin. Every ASSUMED figure
labeled as such, per the evidence discipline used everywhere else in this system.

## Sheet 2 — Time & Financial Value
From `business-analysis`'s ROI methodology:
- Time/effort value (hours saved, headcount-equivalent) — always includable.
- Financial value — **only when real cost data is OBSERVED** from the client or a
  confirmed source. Never an invented recovery/conversion rate applied to an
  exposure ceiling, at any scale (the discipline confirmed across the
  client-intelligence and business-analysis test suites).
- Ongoing costs (Sheet 1's Recurring line) presented separately, never netted
  against savings to produce a "net ROI" figure.

## Sheet 3 — 12-Month Projection
Same horizon as `client-intelligence` and `business-analysis`, for consistency.
Time value and money value stay in separate columns/rows, never combined into one
number when money value is only partially known.
