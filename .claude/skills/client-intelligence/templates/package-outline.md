# Client Intelligence Package — <CLIENT>

Date: <YYYY-MM-DD> · Analyst: client-analyst · Sources: <count>

> Every claim below carries **OBSERVED / INFERRED / ASSUMED / UNKNOWN**, and every
> INFERRED/ASSUMED claim carries **High/Medium/Low** confidence. See `SKILL.md` for the
> full methodology behind each section.

## 1. Executive Summary
3–5 sentences: who the client is, the single recommended solution, expected value
stated against the 3 gold bars (time saved / effort reduced / profit increased), and
overall confidence in this package (High/Medium/Low, driven by how much came from
direct sources vs inference).

## 2. Business Overview
What the business does, how it operates day to day, and how long it's been running if
known. OBSERVED facts from the website/social profiles go here first.

## 3. Business Model
How the business makes money — service-based, product-based, subscription, per-visit,
per-order, etc. Note whether this is OBSERVED (stated directly) or INFERRED (reasoned
from pricing pages, service structure).

## 4. Target Customers
Who they serve — demographics, business type if B2B, geography. Label each claim.

## 5. Current Systems
| System/Tool | Purpose | Label | Confidence | Source |
| ----------- | ------- | ----- | ---------- | ------ |

Tools, CRM, databases, contact/booking systems currently in use. This is one of the
two *essential* items in the missing-information checklist (§8/§25) — if unknown, it
belongs there, not guessed here.

## 6. Current Workflow
Step-by-step description of how work currently gets done, end to end, for the process
most relevant to the likely automation opportunity.

## 7. Customer Journey
The customer's path from first contact to delivered outcome (inquiry → booking →
service → follow-up, or equivalent for the client's business).

## 8. Requirements
What the client has explicitly asked for, in their own words where possible (direct
quotes from meeting notes/documents are OBSERVED by definition).

## 9. Pain Points
| Pain point | Evidence | Label | Confidence | Source |
| ---------- | -------- | ----- | ---------- | ------ |

Include the client-articulated gap/pain point required by §8/§25 (e.g. "demand is
outpacing production capacity") if one was given.

## 10. Bottlenecks
Where work backs up or slows down — specific step in §6/§7 where friction is highest.

## 11. Publicly Observable Business Priorities
What the business appears to prioritize based on public signals (site messaging, ad
patterns, review responses) — INFERRED by nature; confidence per signal strength.

## 12. KPI Opportunities
| KPI | Current baseline | Target | Gold bar (time/effort/profit) | Label | Confidence |
| --- | ----------------- | ------ | ------------------------------ | ----- | ---------- |

Baseline is OBSERVED if client-reported, ASSUMED (with a stated estimation basis) if
not measured by the client — never invented without a basis. Pick 2–4 KPIs per
opportunity from the type-appropriate checklist in `SKILL.md` § KPI methodology.

## 13. Automation Opportunities
| Opportunity | Source (checklist pattern / beyond checklist) | Gold bar | Label | Confidence |
| ----------- | ----------------------------------------------- | -------- | ----- | ---------- |

Every client gets scanned against the standard checklist (manual intake/booking, lead
follow-up delay, re-entered data, manual reminders/confirmations, +more as the
checklist matures). Anything found beyond the checklist is flagged as such.

## 14. Recommended Features
The specific features that make up the recommended solution (§23) — each must trace to
a gold bar. This is the *main* recommendation, not the optional list (§15).

## 15. Additional Value Opportunities
| Opportunity | Gold bar | Est. cost/effort | Why it's optional |
| ----------- | -------- | ------------------ | ------------------ |

Nice-to-haves that clear the gold-bar floor but aren't bundled into scope by default.
Amer decides whether to offer each one — never silently folded into §14.

## 16. Time Savings Opportunities
Hours/week or hours/month saved per opportunity. State the basis (OBSERVED volume vs
ASSUMED estimate) for each number.

## 17. Effort Reduction Opportunities
Headcount-equivalent achieved (how many employees' worth of work this frees up), 24/7
availability value, and reduction in effort/mental overhead — the non-dollar value
that stands on its own when financial data isn't available (§19).

## 18. Financial Opportunities
Dollar-denominated opportunities — **only populate with real numbers when client staff
hourly cost or revenue-per-unit is OBSERVED.** If not available, state that explicitly
here rather than estimating a dollar figure (see §19 ROI methodology).

## 19. ROI Analysis
12-month horizon. State time-value and money-value separately (§16/§18). If money
value can't be computed responsibly, present time/effort value only and say why. Do
**not** net ongoing costs (§20) against this to produce a "net ROI" number.

## 20. Cost Considerations
Ongoing subscription/API/hosting cost — typically $60–80/month, $30 minimum — stated
as the size of the investment against the value in §19, presented **separately**, not
subtracted from it.

## 21. Risks
| Risk | Category | Severity | Mitigation |
| ---- | -------- | -------- | ---------- |

Categories: technical, adoption, data, vendor, compliance, scope creep. Severity uses
the same High/Medium/Low scale as confidence.

## 22. Alternative Solutions
Other approaches considered and why they were not the recommendation — including
simpler/cheaper options if the recommended one is more involved.

## 23. Recommended Solution
The single recommended path, and why it wins over the alternatives in §22.

## 24. Recommended Priorities
Ranked opportunity list using the three ranking dimensions in order: **1) client-
stated value/importance → 2) profit (without inflating scope) → 3) risk.** State which
dimension drove each ranking decision when it isn't obvious.

## 25. Missing Information
| Gap | Tier (essential/helpful) | Blocks |
| --- | -------------------------- | ------ |

Essential: current tools/systems in use; a client-articulated pain point/gap.
Helpful but not mandatory: monthly volume, staff count.

## 26. Questions for Client
Direct questions to close the gaps in §25, phrased ready to send/ask — not just a
restatement of the gap.

## 27. Evidence and Confidence

| # | Claim | Label | Confidence | Source |
| - | ----- | ----- | ---------- | ------ |

Roll-up table of every material claim in the package above, in section order.

## 28. Implementation Implications
What this package means for the next steps — what `automation-architecture` needs to
design, what `business-analysis` needs to cost/price, and what `project-planning`
needs to break down. Not a full design or plan itself — a handoff note.
