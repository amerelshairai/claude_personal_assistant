# business-analysis — decisions to make before full implementation

Per BUILD-PLAN.md step 4. Already known, not re-asked (from `memory/business.md`):
no internal hourly rate is used (Amer explicitly rejects hourly costing); pricing
model is value-based, fixed price per project; target margin 70–80% net, ~35–40%
net to Amer after the technical-partner split.

## 1. Default ROI horizon — DECIDED
Same as `client-intelligence`: **12 months.** Confirmed 2026-08-18.

## 2. Effort multipliers by project type — DECIDED
Base ranges are `time-orchestration`'s Research/Build/Admin/Call baselines
(Research 1–4h, Build 4–20h, Admin 0.5–2h, Call = actual length). How they apply
differs by project type:

- **Greenfield build:** Research/Build/Admin/Call ranges apply directly, at the
  **widest** end of their contingency — no existing system to anchor estimates
  against, so uncertainty is highest here.
- **Feature-addition** (extending an existing workflow/system): same Build range for
  the core work, **plus explicit discovery/integration time tracked as a separate
  line**, not folded into the Build estimate. This lets Amer see how much time goes
  to "understanding the existing system" vs. "building the new part."
- **Bug-fix/maintenance:** smaller baseline than a full build, split into two
  phases — **Diagnosis** and **Fix**. Diagnosis time is inherently unpredictable
  (root cause could be trivial or a rabbit hole) — **flag diagnosis estimates
  ASSUMED/Low confidence by default**, same discipline as thin-scope tasks
  elsewhere (`client-intelligence`'s KPI baselines, `time-orchestration`'s effort
  estimation).

## 3. Viability threshold — DECIDED
A project is a "no" if it fails **any one** of these four (they don't need to
stack — one failure is enough):

1. **Capacity** — genuinely doesn't fit even after replanning, without dropping
   existing client commitments below acceptable minimums.
2. **Profitability** — the margin between the agreed price and the estimated effort
   doesn't clear an acceptable floor, and no scope cut recovers it. No fixed
   internal hourly rate is used for this check (confirmed, matches
   `memory/business.md`). Amer's actual process: run the client's requested scope
   through the pricing calculator (`memory/business.md` § Pricing tools) to get a
   price anchor, agree a price with the client, then separately estimate effort —
   profitability is the judgment call on that price-vs-effort margin, not a formula
   with an invented $/hour figure.
3. **Risk** — hits a risk category (compliance, data privacy, vendor dependency)
   Amer isn't willing to accept regardless of price.
4. **Fit** — genuinely outside Amer's skillset, where delivering it poorly would
   cost more in reputation than the project is worth.

**Deadline's role:** confirmed it affects **Capacity/feasibility** (a
`time-orchestration` question — can this be delivered in time given current load),
**not** the Profitability check. A tight deadline doesn't shift a rate up or down;
it either fits or it doesn't, judged separately from margin.
