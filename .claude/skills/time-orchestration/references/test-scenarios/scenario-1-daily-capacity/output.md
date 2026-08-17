# Scenario 1 — orchestrator walkthrough (synthetic)

## Step 1: read reality
- Calendar: university lecture 11:30am–2:30pm today, nothing else.
- Todoist: 5 open tasks across 2 client projects + 1 internal project (see input.md).
- `memory/user.md`: today is a university day → realistic productive hours 3–4h.

## Step 2: priority tiers (todoist-management §3)
| Task | Project tier | Due | Tier |
| --- | --- | --- | --- |
| Build WhatsApp lead-routing flow | Client (Falcon Realty) | tomorrow (within 48h) | **P1** |
| Draft support self-service question list | Client (Nova) | 5 days | P2 |
| Research cart-abandonment webhook support | Client (Nova) | 3 days | P2 |
| Reconcile last week's invoices | Internal (Business Admin) | 2 days (within a week) | P3 |
| Update pricing sheet | Internal (Business Admin) | 10 days | P4 |

## Step 3: the core calculation — re-run with the fixed formula (2026-08-17)

Three gaps were found and fixed in SKILL.md (AVAILABLE base, REQUIRED's
must-start-today test, buffer as a proportional percentage). Re-running with the
corrected formula:

**AVAILABLE (today, Monday — university day):**
`realistic_productive_hours_per_day` = 3–4h, midpoint **3.5h** (already nets out
today's recurring lecture — no extra Calendar commitments beyond it) − buffer
(15% × 3.5h = **0.525h**) = **~3.0h**.

**REQUIRED (today):** checked every open task for the must-start-today test —
remaining effort vs. remaining capacity between *tomorrow* and its due date:
- **Build WhatsApp lead-routing flow** (P1, 6h, due tomorrow/Tue): tomorrow alone
  provides only ~3.0h (also a university day) — 6h > 3.0h, so it **fails the test**
  and must start today. Pulls in `min(6h, today's AVAILABLE) = 3.0h` today; the
  remaining 3h lands on tomorrow's own REQUIRED calculation, well within tomorrow's
  ~3.0h.
- **Reconcile invoices** (P3, 1h, due in 2 days/Wed): remaining capacity Tue+Wed
  ≈6.0h ≫ 1h — passes, not pulled forward.
- **Research cart-abandonment webhook** (P2, 2h, due in 3 days/Thu): remaining
  capacity Tue+Wed+Thu ≈9.0h ≫ 2h — passes, not pulled forward.
- **Draft support self-service list** (P2, 1.5h, due in 5 days/Sat) and **Update
  pricing sheet** (P4, 1h, due in 10 days): both comfortably pass, not pulled
  forward.

REQUIRED (today) = **3.0h** (all from the Build task).

**GAP = 3.0h − 3.0h = 0h.** A tight but exact fit — not an overload, and not the
false "+3.5h of slack" the unfixed formula would have shown.

## Step 4: what this walkthrough recommends
Spend all of today's ~3.0h on **Build WhatsApp lead-routing flow** (Falcon Realty).
The remaining 3h of that task lands on tomorrow's REQUIRED automatically once
tomorrow is computed (tomorrow's own ~3.0h AVAILABLE covers it with room to spare for
whatever else is due then). Everything else (P2/P3/P4) correctly waits — not because
of overload, but because the fixed REQUIRED calculation now correctly sees that P1
needs today's time even though its deadline is tomorrow, not today.

## Step 5: work block (Level 1 — would execute, then report)
- Title: `[Work] Falcon Realty — Build WhatsApp lead-routing flow`
- Calendar: primary, marked Busy
- Time: today, sized to the available window around the 11:30am–2:30pm lecture, with
  30min buffer before/after the lecture per calendar-management conventions
- Length: under the 2.5h default cap per block — since ~3.5h is available across the
  day split by the lecture, this becomes **two blocks** (before and after the
  lecture), both within the 45min–2.5h range, not one oversized block

## Report (per `.claude/rules/reporting.md`)
```
PLANNED
- Today's plan: Falcon Realty Build task (P1, due tomorrow) — 3.0h (all of today's
  AVAILABLE after buffer); remaining 3h of the task lands on tomorrow

CHANGED
- Recommending Build task over Nova/internal tasks — P1 deadline tomorrow requires
  today's capacity even though nothing is due today itself
```

---

## Resolved 2026-08-17 — all three gaps fixed in SKILL.md, re-run above confirms clean numbers

1. **AVAILABLE base** — now explicitly sources from `memory/user.md`'s
   `realistic_productive_hours_per_day`, never the raw window; "Calendar
   commitments" subtracted on top means only extra/non-routine commitments.
2. **REQUIRED's must-start-today test** — a task pulls into today's REQUIRED when
   its remaining effort exceeds the remaining capacity between tomorrow and its due
   date. Confirmed correct here: the 6h P1 task properly split into 3h today + 3h
   tomorrow instead of showing as 0h required today.
3. **Buffer as a proportional percentage (15%)** — applied to today's 3.5h baseline
   (0.525h), not the flat ~4h weekly figure. GAP came out to a clean 0h fit instead
   of a misleading +3.5h of apparent slack.
