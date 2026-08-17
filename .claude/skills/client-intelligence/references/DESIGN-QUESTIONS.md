# client-intelligence — decisions to make before full implementation

Per spec §33, define these before writing the final implementation. Each needs Amer's
input or a deliberate decision. Do not guess.

## 1. Research methodology — DECIDED
- Sequence: website → LinkedIn/social profiles → competitors → reviews → tech clues.
  Client-supplied material (documents, meeting notes, screenshots) counts as a source
  too and can be used alongside/ahead of public research.
- Escalation to deeper research: no fixed rule — judgment call in the moment based on
  what's found (thin/ambiguous requirements, high apparent value, etc.). Claude should
  use judgment, not a rigid trigger, and can ask Amer if genuinely unsure.
- How many sources before OBSERVED: one is enough IF it's a direct, first-party source
  speaking about the client's own work/business/personality (their own website, their
  own social posts, their own meeting notes/documents). Treat that as OBSERVED and
  treat it as essential input to the analysis. Indirect/inferred claims (reasoning from
  signals rather than a direct statement) stay INFERRED regardless of source count.
- Stop condition: work through the standard sequence (website → LinkedIn/social →
  competitors → reviews → tech clues) by default. If that isn't enough to support the
  analysis, go beyond it — no fixed source/time cap, judgment-based on whether the
  package can be produced with confidence yet.

## 2. Confidence rules — DECIDED
- Scale: High / Medium / Low.
- High — confirmed by a direct first-party source, or corroborated by 2+ independent
  sources.
- Medium — a reasonable inference from multiple consistent indirect signals.
- Low — inferred from a single indirect signal, or a stretch/assumption.
- A single indirect signal never exceeds Low, regardless of how strong it seems.
- **Refinement (2026-08-17, from the clinic test scenario):** a client's own verbal
  guess about their own business ("I'd say about 1 in 5") is still first-party, so it
  stays OBSERVED — but OBSERVED numeric claims now carry a `(measured)` /
  `(estimated)` tag so downstream skills (especially `business-analysis`) know not to
  treat a guess as precise enough to justify a confident dollar figure on its own.

## 3. KPI methodology — DECIDED (Amer flagged this is a first pass, not fixed —
   revisit as real client work exposes gaps)
1. Identify problems from research + client's own stated pain points.
2. Capture expectations — personal (what the client as a person wants: less stress,
   more free time) and business (revenue, growth, efficiency).
3. Map every opportunity to one of the "3 gold bars": time saved / effort reduced /
   profit increased.
4. Pick 2–4 concrete KPIs per opportunity from a type-appropriate checklist, e.g.:
   - Salons/clinics: no-show rate, booking response time, staff hours on scheduling
   - E-commerce/customer support: response/resolution time, order processing time,
     cart recovery rate
   - Real estate: lead response time, follow-up consistency, inquiries-to-viewing rate
5. Baseline: if the client hasn't measured it, don't invent a number — estimate a rough
   range from observable signals (order volume, review complaint patterns, staff size),
   label it ASSUMED, and list it under Missing Information / Questions for Client so a
   real number can replace it later.
- Estimated vs client-reported KPIs are distinguished by the OBSERVED/INFERRED/ASSUMED
  label per §2 — client-reported numbers are OBSERVED (first-party), estimated ones are
  ASSUMED.

## 4. ROI methodology — DECIDED
- Horizon: 12 months (bigger, more compelling growth picture for the client).
- Estimate both time and money where possible.
- If client staff hourly cost is unknown, do NOT guess a dollar figure. Instead focus
  on time/effort-native measures: hours saved, headcount-equivalent achieved
  (how many employees' worth of work this replaces/frees up), 24/7 availability value,
  and reduction in effort/mental overhead ("overthinking"). Only convert to a dollar
  ROI when real cost data (staff wage, revenue per order, etc.) is available from the
  client or a confirmed OBSERVED source.
- Ongoing costs (API/hosting/LLM tokens/subscription — typically $60–80/month,
  $30 minimum): do NOT net these against the estimated savings to produce a "net ROI"
  figure — that framing makes the investment look riskier/costlier than it is. Instead
  present them separately: state the savings/value, and separately note the small
  ongoing cost as "this is the size of the investment against what you'll save," not
  subtracted from it.

## 5. Feature discovery methodology — DECIDED
- Standard checklist is the baseline: every client gets scanned against the same core
  patterns — manual intake/booking, lead follow-up delay, re-entered data across
  systems, manual reminders/confirmations, plus other common patterns to be built out
  in `references/` as the checklist matures. Keeps discovery consistent; nothing
  obvious gets missed.
- Beyond the checklist: client-specific opportunities the checklist wouldn't catch are
  still surfaced, but flagged separately as "beyond standard checklist" so Amer can see
  which recommendations are pattern-matched vs genuinely bespoke.
- Real value vs invoice padding: must tie to at least one of the 3 gold bars
  (time/effort/profit) — no exceptions, that's the floor.
- Small/nice-to-have items that clear that bar are NOT bundled into the main
  recommendation by default. List them separately under "Additional Value
  Opportunities," labeled optional, each with its own small cost/effort estimate.
  Amer decides whether to offer it. Never silently fold a nice-to-have into scope
  just because it's easy to build.

## 6. Opportunity ranking — DECIDED
- Three ranking dimensions, in priority order:
  1. Value — how much it boosts the client's work without displacing them or costing
     too much, and how it reflects on their standing/value (personal + business,
     per §3's expectations capture).
  2. Profit — must not work against the client's own profit goals; favor what's
     genuinely valuable over what pads scope.
  3. Risk — security of the client's data and financial systems.
- Client-stated priority leads the ranking by default (what the client says matters
  most to them comes first).
- Effort and time-to-value are NOT separate ranking dimensions — considered
  qualitatively within the above rather than tracked independently.

## 7. Risk analysis — DECIDED
- Standard categories, checked for every opportunity: technical (integration/breakage
  risk), adoption (staff won't actually use it), data (privacy/security), vendor
  (third-party API dependency/cost changes), compliance (industry-specific rules),
  scope creep.
- Severity: High/Medium/Low — same scale as confidence (§2), reused rather than
  introducing a separate scale.
- **Refinement (2026-08-17, from the clinic test scenario):** health/medical-adjacent
  clients automatically start the **data** risk at Medium-High rather than the
  general default — patient-data regulatory exposure is higher by default,
  independent of what's otherwise known about the client.

## 8. Missing-information detection — DECIDED
- Required-info checklist, two tiers, plus one conditional tier:
  - Essential: current tools/systems/databases/contact systems in use; a
    client-articulated gap/pain point (e.g. "demand is outpacing production capacity").
  - Conditional essential (2026-08-17, from the clinic test): for health/medical-
    adjacent clients only, applicable data-privacy/compliance rules — pairs with the
    §7 risk-severity refinement above.
  - Helpful but not mandatory: monthly volume, staff count.
- These get captured primarily through client conversations — meeting notes are the
  main source of clarity here, not just public research. When missing, list under
  "Missing Information" / "Questions for Client," tiered essential vs helpful so Amer
  knows what genuinely blocks scoping vs what's just useful context.

## 9. Business analysis boundary — DECIDED (confirmed, can revisit)
- `client-intelligence` identifies opportunities and roughly sizes them (§3/§4 KPI and
  ROI methodology). `business-analysis` does the rigorous costing, pricing, and
  viability call. Confirmed by Amer; open to change once real work exposes gaps.

## 10. Package template — DONE
- `templates/package-outline.md` filled with prompts and table shapes for all 28
  sections, reflecting the decided methodology above.

## 11. Test scenarios — DONE (4 synthetic scenarios spanning the intended industry mix)
- **Round 1 — vague inbound lead**, run 2026-08-17 — `projects/test-vague-lead/`.
  Confirmed the missing-information path (§8/§25) works. Fixed in `SKILL.md`:
  1. No guidance for zero business identifier — research sequence had nothing to
     start from. Fixed: skip straight to Missing Information rather than searching
     blind.
  2. No guidance for zero observable signal for even an ASSUMED KPI baseline. Fixed:
     leave UNKNOWN instead of forcing a guess.
- **Round 2 — dermatology clinic (no-shows)**, run 2026-08-17 —
  `projects/test-clinic-noshow/`. Exercised KPI baselines, dollar ROI, ranking, risk
  analysis. Fixed in `SKILL.md`:
  3. OBSERVED numeric claims now tag `(measured)` vs `(estimated)` — a client's own
     guess isn't treated as precise as a tracked figure.
  4. Health/medical-adjacent clients auto-elevate data risk to Medium-High and add
     compliance rules as a conditional-essential missing-info item.
- **Round 3 — real-estate brokerage (lead response delay)**, run 2026-08-17 —
  `projects/test-realty-leadresponse/`. Contrast case: measured baseline, zero dollar
  data by explicit client choice (not just unknown), no health-data angle. Confirmed
  round 2's health-data rule correctly doesn't fire for a non-health client. The
  declined-vs-unknown distinction Amer confirmed as **ad hoc per-scenario judgment,
  not a fixed SKILL.md rule** — left out of the methodology deliberately.
- **Round 4 — e-commerce/support (~400 orders/day)**, run 2026-08-17 —
  `projects/test-ecom-support/`. Mirrors the example client profile in
  `memory/business.md`. First test with real dollar data on both cost and revenue
  sides — confirmed the no-invented-recovery-rate discipline still holds at much
  larger dollar magnitudes. Fixed in `SKILL.md`:
  5. Added "automated order-status/FAQ self-service" as a 5th standard checklist
     pattern.
  6. Vague-but-stated client asks ("something with our reviews") are never turned
     into a recommendation — always routed to Missing Information; if other findings
     suggest a plausible interpretation, note it there as an INFERRED hypothesis, not
     a recommendation.
  7. No recovery/conversion/deflection rate is ever invented to turn an exposure
     ceiling into a dollar figure, at any scale — but the "raw exposure, not a
     forecast" caveat's *placement* scales with the figure's size: for large numbers,
     put it immediately next to the figure (including in the Executive Summary),
     not deferred to the ROI section alone.
- Covers the intended industry spread (salon/clinic, real estate, e-commerce/support)
  plus the missing-information edge case. Status banner updated to TESTED.
