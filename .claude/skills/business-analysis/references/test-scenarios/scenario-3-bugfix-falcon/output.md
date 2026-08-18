# Scenario 3 — business-analysis walkthrough (synthetic), cross-checked against
# time-orchestration's earlier treatment

## Diagnosis + Fix estimate (business-analysis's bug-fix/maintenance methodology)
- **Diagnosis** — genuinely uncertain, per the causes listed in input.md: fast
  (~0.5h) if an obvious cause like an expired token shows up immediately in logs,
  slow (~2.5h) if it requires tracing through multiple integration points with no
  clear error message. Midpoint estimate **~1.5h, flagged ASSUMED/Low confidence**
  by default, per `SKILL.md` § Effort multipliers.
- **Fix** — once the root cause is known, applying it (refresh a token, patch a
  webhook handler, redeploy) is typically fast: **~0.75h**, more confidence here
  since fixing a known cause is more predictable than finding an unknown one.
- **Total: ~2.25h, plausible range ~1h (best case) to ~3.5h (worst case).**

## Cross-check against time-orchestration's original 3h "Build" estimate

**1. Magnitude — roughly consistent, but not for a good reason.** The original 3h
sits inside this scenario's plausible range (1h–3.5h), close to the pessimistic
end. It isn't wildly wrong in total size — but that's coincidental. It was a single
flat guess, not a Diagnosis+Fix decomposition, so there was no way to know at the
time whether 3h was optimistic, realistic, or already assuming the worst case.

**2. Label — inconsistent, and reveals a real gap.** Time-orchestration tagged this
task **"Build."** But `time-orchestration`'s own Build baseline range is **4–20h**
— a 3h estimate doesn't even fall inside the range it was labeled with. This isn't
a rounding issue: it's a sign the task was never actually Build-type work. The
`todoist-management` label taxonomy only has four values — **Research / Build /
Admin / Call** — with no slot for bug-fix/maintenance work, which
`business-analysis` now treats as a genuinely distinct project type (Diagnosis +
Fix, not the Build range at all). **Flagged below** — this is a structural gap in
the label taxonomy, not something to route around ad hoc each time.

**3. Confidence/slack — a real operational risk, not just a labeling nitpick.**
Time-orchestration's capacity calculation treated the 3h as a fixed, certain number
and allocated it against exactly the day's full AVAILABLE (GAP = 0h — no slack).
But `business-analysis`'s own rule says Diagnosis time is inherently uncertain and
should default to ASSUMED/Low confidence. If diagnosis runs to the pessimistic end
(2.5h) instead of the assumed number, **total effort could reach ~3.5h against a
day that had zero spare capacity to begin with** — the plan time-orchestration built
doesn't have anywhere to absorb that. **Flagged below** — should urgent bug-fix
capacity allocations carry extra contingency by default, given this uncertainty?

## Does the GO/NO-GO/CONDITIONAL gate even apply here?
**No — resolving the boundary question raised before this scenario ran.**
GO/NO-GO/CONDITIONAL is a pre-commitment gate for deciding whether to *take on* a
project. Falcon Realty is an existing client under an ongoing relationship
(`memory/business.md`: "stays with the client to fix bugs... not a one-off
handoff") — there's no "should I do this" decision here, only "what does it cost
and is it billable." Of the four viability checks:
- **Fit** — moot; already serving this client.
- **Profitability** in the go/no-go sense — moot; this isn't optional work to
  evaluate, it's an existing commitment. The real question is just billing status.
- **Capacity** — still applies, and already resolved by `time-orchestration`'s
  scenario (P1, today, tight but fit).
- **Risk** — still applies in principle (nothing elevated here; no payment/health
  data touch), so a normal Low.

**Billing:** per input.md, the free post-delivery window has almost certainly
passed — this is billable maintenance work, costed at ~2.25h (range 1–3.5h).

## Report (per `.claude/rules/reporting.md`)
```
COMPLETED
- Falcon Realty bug-fix costed: Diagnosis ~1.5h (ASSUMED/Low confidence) + Fix
  ~0.75h = ~2.25h, range 1-3.5h. Billable (support window has passed).

NEEDS YOU
- Cross-skill gap: no Todoist label exists for bug-fix/maintenance work; the
  original incident was tagged "Build" despite being outside Build's own 4-20h
  range. See flags below.
```

---

## Flags for Amer's review (not yet resolved in SKILL.md/todoist-management)

1. **No Todoist label exists for bug-fix/maintenance work.** The taxonomy has
   Research/Build/Admin/Call; `business-analysis` now treats bug-fix/maintenance as
   a distinct project type with its own Diagnosis+Fix costing. Should a 5th label
   (e.g. "Bugfix") be added to `todoist-management`, or does this work stay tagged
   under one of the existing four for Todoist purposes while `business-analysis`
   costs it differently regardless of label?
2. **Urgent bug-fix capacity allocations may need default contingency.**
   Time-orchestration allocated the original 3h estimate with zero spare capacity
   that day. Given `business-analysis` now flags Diagnosis time as inherently
   uncertain (ASSUMED/Low confidence) by default, should `time-orchestration` add a
   standard contingency margin (e.g. pad urgent bug-fix estimates by some %) when
   computing REQUIRED for that kind of task, rather than treating the point
   estimate as certain?
3. **Confirmed, no change needed:** GO/NO-GO/CONDITIONAL doesn't apply to bug-fix/
   maintenance work for an existing client under an ongoing relationship — Capacity
   and Risk checks still run, Fit and Profitability-as-a-gate don't. Worth stating
   this explicitly in `SKILL.md` so it isn't re-derived ad hoc next time.
