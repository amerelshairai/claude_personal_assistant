# Findings before the workbook (checked first)

1. **Annualization basis checked, not assumed.** Cart abandonment happens every
   day the store is open, and nothing in Nova's package suggests the storefront
   itself closes on any day of the week (unlike the earlier "operating days/week"
   gap, which was specifically about *support-staff* scheduling, not order/cart
   volume). ×365 is used for the exposure ceiling on that basis — stated
   explicitly below, not silently assumed.
2. **No illustrative "if you recover X%" table included**, even though it would
   make the workbook feel more complete. A clearly-labeled hypothetical
   sensitivity table is arguably different from a promised figure, but risks
   being read by a client as an implied expectation regardless of disclaimers —
   safer to stay consistent with the strict rule used everywhere else in this
   system (client-intelligence, business-analysis) than to introduce a new,
   softer pattern here without checking with Amer first.
3. **Internal sheet doesn't compute a margin percentage** — there's no $/hour
   rate to compute one from (`memory/business.md`, confirmed policy). Shows
   effort and price side by side for Amer's own judgment instead of a fabricated
   number.
4. **Same pricing rule as the proposal test**: the one-time cost line is
   `[AMER TO CONFIRM]`, not a picked midpoint.

All arithmetic below is shown as a checkable formula, not just a stated result.

---

# ROI / Financial Model — Nova Home Goods — Cart Recovery (client-facing)

Date: 2026/08/19 · Shape per `templates/roi-model.md`

## Sheet 1 — Cost Breakdown
| Item | Value | Basis |
| --- | --- | --- |
| One-time (build) | **[AMER TO CONFIRM]** — recommended range $500-650 | `business-analysis` scenario 4, not yet agreed |
| Recurring (monthly) | $60-80/mo | Standard range, likely toward the higher end given Nova's order volume |
| Maintenance | Included: 3-5 days free post-delivery; billable after | `memory/business.md` |

## Sheet 2 — Time & Financial Value

**Time/effort value: not the primary driver for this specific automation.**
Cart-recovery is a revenue-recovery mechanism, not a staff-time-reduction one —
unlike Nova's *other* opportunity (order-status self-service), which does save
support time. Stating a time-saved figure here would be forcing a number that
doesn't actually apply to this engagement's scope.

**Financial value — shown as a formula, checked step by step:**

| Step | Formula | Result |
| --- | --- | --- |
| Checkout starts/day | completed orders ÷ (1 − abandonment rate) = 400 ÷ (1 − 0.68) = 400 ÷ 0.32 | **1,250/day** |
| Abandoned carts/day | checkout starts − completed orders = 1,250 − 400 (cross-check: 1,250 × 0.68 = 850 ✓ matches) | **850/day** |
| Exposure per day | abandoned carts/day × AOV = 850 × $45 | **$38,250/day** |
| Exposure per year | $38,250 × 365 (see Finding 1 for why 365 is used) | **$13,961,250/year** |

**This is a raw exposure ceiling, not a forecast or a promised recovery amount.**
No recovery/conversion rate is applied — none exists yet for this client, and
inventing one here would violate the same discipline confirmed across
`client-intelligence` and `business-analysis`, regardless of how large the number
is (if anything, the size of this ceiling is exactly why the caveat needs to stay
prominent, not be softened).

## Sheet 3 — 12-Month Projection
| Line | Value | Formula |
| --- | --- | --- |
| One-time cost | [AMER TO CONFIRM] | Paid once |
| Recurring cost (12 months) | $720-960 | $60 × 12 = $720; $80 × 12 = $960 |
| Cart-abandonment exposure (12 months) | $13,961,250 (ceiling only) | See Sheet 2 |

Recurring cost is **not netted against the exposure figure** — presented
separately, per the standing "never produce a net-ROI number" rule.

---

# ROI / Financial Model — Nova Home Goods — Cart Recovery (internal, NOT for client)

## Effort vs. price — judgment, not a computed margin
| Item | Value |
| --- | --- |
| Effort | 13h raw / 15.6h with 20% contingency |
| Price range | $500-650 (unconfirmed) |
| Target margin | 70-80% net, ~35-40% net to Amer after partner split |

**No $/hour rate exists to compute an actual margin percentage from these two
numbers** — per `memory/business.md`, Amer explicitly rejects hourly costing.
This table exists so Amer can judge proportionality himself (effort against
price), not to produce a fabricated "X% margin" figure.

## Report (per `.claude/rules/reporting.md`)
```
REVIEW_REQUIRED
- Nova ROI workbook (client-facing + internal) drafted, all figures traced to
  real prior-stage sources. One-time price still [AMER TO CONFIRM]. No recovery
  rate assumed on the $13,961,250/year ceiling -- stated as exposure only.
```
