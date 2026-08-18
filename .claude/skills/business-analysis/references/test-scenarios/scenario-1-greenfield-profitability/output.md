# Scenario 1 — business-analysis walkthrough (synthetic)

## Cost model
| Layer | Contains |
| --- | --- |
| One-time | Research 3h, Build 18h, Admin 1.5h, Call 1h = **23.5h total** |
| Recurring | ~$45/month (client's own calculator run — accepted by them) |
| Maintenance | Standard 3–5 day free bug-fix window post-delivery, per `memory/business.md`; billable after |
| Amer's time | 23.5h — the real constraint, not priced by the hour |

## Viability check — all 4 criteria

**1. Capacity — PASS.** No competing client work in this window (synthetic state).

**2. Profitability — CONDITIONAL.**
Client anchored at **$400** ("this seems simple"). But 23.5h of effort — 18h of it
Build, near the top of the 4–20h range, touching billing integration — is not a
"$200-minimum simple Gmail workflow" scope; by effort alone this sits closer to the
middle of the stated $750–$1,500 average range. No fixed $/hour exists to compute
this precisely (by design, per `memory/business.md`), so this is a proportionality
judgment, not a formula: **$400 for this scope does not look like it clears the
70–80% target margin as quoted.** A fix is available, so this is CONDITIONAL, not
NO-GO:
- **(a) Cut scope to fit ~$400:** drop the billing-link push (step 5) and the
  post-tour follow-up (step 4), leaving auto-respond + tour scheduling + reminder
  (~10h, not 23.5h) — proportionate to the client's anchor.
- **(b) Keep full scope, renegotiate price** toward the $750–$1,000 range to match
  23.5h of effort and the billing integration's added complexity.

**3. Risk — Medium-High, per the payment/billing auto-elevation rule.** The build
pushes payment links into the gym's billing system after signup — the only
money-handling touch in this scope. Per `business-analysis`'s risk-category rule
(mirrors `client-intelligence`'s health-data elevation), payment/billing-touching
builds start at Medium-High data risk by default, even though this scope only pushes
a link rather than processing card data directly.

**4. Fit — PASS.** CRM/booking/messaging automation with a calendar and a billing
handoff is core to Amer's stated service line.

## Verdict: CONDITIONAL — report as WAITING_FOR_AMER
Not GO (profitability as quoted doesn't clear the margin bar) and not NO-GO (a fix
exists). Present both options (a) and (b) to Amer for a pricing/scope decision before
anything goes to the client — per the hard boundary, pricing recommendations are for
Amer, never sent externally without his approval.

## Report (per `.claude/rules/reporting.md`)
```
WAITING_FOR_AMER
- TechFit Gym greenfield build: CONDITIONAL verdict. $400 client anchor doesn't
  clear target margin for 23.5h/5-step scope touching billing. Options: (a) cut to
  ~10h/3-step scope to fit $400, or (b) keep full scope, renegotiate toward
  $750-1,000. Risk: Medium-High (payment-link push), per business-analysis's
  payment/billing risk rule.
```

---

## Flags — resolved 2026-08-18

1. **Payment/billing risk-elevation rule** — added to `business-analysis/SKILL.md`
   § Risk categories, mirroring `client-intelligence`'s health-data rule exactly:
   payment/billing-touching builds start at Medium-High data risk by default.
2. **Three-way verdict added:** GO / NO-GO / CONDITIONAL, specific to
   `business-analysis` — not a new global task state. CONDITIONAL states exactly
   what would change the verdict to GO, and reports as `WAITING_FOR_AMER`
   (a decision only Amer can make), never `REVIEW_REQUIRED` (which means a finished
   Level 2 artifact, not an open renegotiation call).
