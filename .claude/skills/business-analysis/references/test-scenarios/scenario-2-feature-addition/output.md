# Scenario 2 — business-analysis walkthrough (synthetic)

## Cost model (revised, post-discovery)
| Layer | Contains |
| --- | --- |
| One-time | Discovery/integration 2h + unplanned foundational work 6h + Build 8h + Admin 1h = **17h** |
| Recurring | Not changed by this feature (existing subscription line unaffected) |
| Maintenance | Standard 3–5 day free bug-fix window applies to the *new* feature once delivered |
| Amer's time | 17h — the real constraint. No internal $/hour; judged against the agreed price. |

The discovery/integration line did exactly what it's designed to do: it made the
**customer-identity persistence gap visible as its own line**, not silently absorbed
into the Build estimate. That's the point of tracking it separately (per
`SKILL.md` § Effort multipliers).

## The real question this scenario raises
The price ($600) was agreed **before** this discovery happened. This isn't a
client-requested scope change — it's Amer's own side uncovering that the existing
system needs more foundational work than anyone knew when the price was set.
`business-analysis`'s viability threshold (GO/NO-GO/CONDITIONAL) is framed as a
**pre-commitment** decision — a gate before agreeing to a project. There's no
defined process for **re-running it after a price is already agreed**, once new
information changes the effort picture this much (9h → 17h, near double).

`memory/business.md` already has a relevant term, but for a different trigger:
*"adjusting the payment plan when client scope changes mid-project"* — written for
scope changes the **client** requests, not complexity Amer's own discovery
uncovers. Whether the same "adjust the payment plan" handling should extend to this
case (discovery-revealed complexity, not a client request) isn't stated anywhere.
**Flagged below, not assumed.**

## Viability re-check, applying the existing framework as best I can
- **Capacity:** 17h against a 1-week deadline — plausible in isolation (memory/
  user.md's realistic weekly capacity is ~27h midpoint), but this test doesn't model
  what else is on Amer's plate that week. Flagged as a simplification, not a firm
  answer — a real run needs the live Todoist/Calendar state.
- **Profitability:** $600 for 17h looks proportionate to roughly half of what $600
  was priced for (9h) — i.e., **not proportionate for the actual scope.** Judgment
  call, same discipline as Scenario 1: this doesn't clear the target margin at the
  now-known effort level.
- **Risk:** none of the existing risk categories are specifically hit (no payment/
  health-data touch here) — Low.
- **Fit:** PASS — squarely within skillset.

Applying GO/NO-GO/CONDITIONAL mechanically would say **CONDITIONAL** (profitability
fails, but a fix — renegotiating the price or descoping — recovers it). But this
verdict was designed for a decision **before** agreeing to a project, and here the
agreement already happened. Presenting it as an ordinary CONDITIONAL "should I take
this" call would misrepresent what's actually going on: this is a **repricing
conversation about an already-agreed engagement**, not a fresh go/no-go.

## Recommendation (pending Amer's answer to the flag below)
Do not silently absorb the extra 8h (unplanned foundational work + the effort gap)
into the original $600. Surface it to Amer as a mid-project repricing decision —
closest existing mechanism is `memory/business.md`'s scope-change payment-plan
adjustment, applied here even though the trigger is discovery, not a client request.

## Report (per `.claude/rules/reporting.md`)
```
WAITING_FOR_AMER
- Nova Home Goods loyalty-points add-on: discovery revealed a foundational gap
  (no persistent customer identity), effort now ~17h vs. the 9h the agreed $600
  price was based on. Needs a repricing decision before continuing build work.
```

---

## Flags — resolved 2026-08-18

1. **Discovery overruns route through the same mechanism as client-requested scope
   changes** — `memory/business.md`'s existing payment-plan-adjustment term, even
   though the trigger here was Amer's own discovery, not a client ask. Added to
   `business-analysis/SKILL.md` § Mid-project discovery overruns.
2. **New verdict added: `NEEDS-REPRICING`**, distinct from GO/NO-GO/CONDITIONAL.
   This scenario's actual verdict is `NEEDS-REPRICING`, not `CONDITIONAL` —
   CONDITIONAL stays reserved for pre-commitment decisions; this situation is an
   already-agreed deal that needs revisiting, a different thing. Reports as
   `WAITING_FOR_AMER` either way.
