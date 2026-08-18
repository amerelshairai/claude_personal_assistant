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

## Test scenarios

- **Scenario 1 — greenfield build with a profitability tension**, run 2026-08-18 —
  `references/test-scenarios/scenario-1-greenfield-profitability/`. TechFit Gym
  (synthetic), 23.5h effort quoted at $400 by the client. 2 findings, both resolved
  2026-08-18:
  1. **Payment/billing risk-elevation rule** — added, mirrors `client-intelligence`'s
     health-data rule: builds touching payment/billing start at Medium-High data
     risk by default.
  2. **Three-way verdict added: GO / NO-GO / CONDITIONAL** — business-analysis-
     specific, not a new global task state. CONDITIONAL states what would change the
     verdict to GO; reports as `WAITING_FOR_AMER`, never `REVIEW_REQUIRED`.

- **Scenario 2 — feature-addition with discovery-revealed complexity**, run
  2026-08-18 — `references/test-scenarios/scenario-2-feature-addition/`. Nova Home
  Goods (synthetic) loyalty-points add-on, priced at $600 for 9h before discovery,
  revealed to actually need ~17h once a foundational gap (no persistent customer
  identity) surfaced. **2 findings, not yet resolved:**
  1. No process exists for re-evaluating viability after a price is already agreed,
     when discovery (not a client request) reveals materially more work. Should
     this route through `memory/business.md`'s existing "adjust the payment plan on
     scope change" mechanism (written for client-requested changes), or does
     discovery-revealed complexity need its own handling?
  2. GO/NO-GO/CONDITIONAL was designed as a pre-commitment gate — applying it to an
     already-agreed engagement produces a technically-correct but misleading label.
     Worth a distinct verdict for "already committed, needs repricing"?
- **Scenario 3 — bug-fix/maintenance, reusing the Falcon Realty incident from
  time-orchestration**, run 2026-08-18 —
  `references/test-scenarios/scenario-3-bugfix-falcon/`. Explicitly cross-checked
  against how `time-orchestration` originally treated the same incident (flat 3h,
  labeled "Build", zero-slack capacity allocation). Diagnosis+Fix estimate: ~2.25h
  (range 1–3.5h). **3 findings:**
  1. **Not yet resolved:** no Todoist label exists for bug-fix/maintenance work —
     the original incident was tagged "Build" despite 3h falling outside Build's own
     4–20h range.
  2. **Not yet resolved:** urgent bug-fix capacity allocations may need default
     contingency in `time-orchestration`, since Diagnosis time is inherently
     uncertain (ASSUMED/Low confidence) but was allocated with zero slack.
  3. **Resolved:** GO/NO-GO/CONDITIONAL does not apply to bug-fix/maintenance work
     for an existing client under an ongoing relationship — Capacity and Risk
     checks still run; Fit and Profitability-as-a-gate don't (it's a billing
     question, not a go/no-go decision).
