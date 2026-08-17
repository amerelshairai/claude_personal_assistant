# time-orchestration + todoist-management + calendar-management — decisions to make

Per BUILD-PLAN.md step 3: these three are one loop, built together. Shared here
rather than split three ways, since several decisions (effort estimation, work-block
conventions) cross skill boundaries. Each question needs Amer's input or a deliberate
decision. Do not guess.

Already decided — do not re-ask:
- Deep-work block minimum length: **45 minutes** (`memory/user.md`).
- Weekly buffer to reserve for the unexpected: **~4 hours (~15%)** (`memory/user.md`).
- Realistic daily capacity: 6–7h full days, 3–4h university/club days (`memory/user.md`).

## A. Todoist structure (`todoist-management`) — DECIDED
1. **Project structure:** one Todoist project per client.
2. **Label taxonomy:** work-type label + a delegable-to-Claude flag label. Work-type
   values: **Research / Build / Admin / Call** (4 categories — Research = client
   analysis/discovery, Build = n8n/automation work, Admin = docs/invoicing/planning,
   Call = meetings/discovery calls). These same 4 categories drive effort-estimation
   heuristics in §C.
3. **Priority mapping:** client-facing work defaults to P1/P2, internal/admin work
   defaults to P3/P4 (deadline is a tiebreaker/override within each tier, not the
   primary driver). Within each tier, split by deadline proximity:
   - P1: client-facing, due within ~48h or overdue.
   - P2: client-facing, not due within 48h.
   - P3: internal, due within a week.
   - P4: internal, no near deadline (someday/backlog).
   **This is a default `time-orchestration` reasons from, not a hard rule** — if Amer
   explicitly states something (university, personal commitment) ranks higher than a
   client task, that overrides the default regardless of P-tier. Confirmed 2026-08-17.
4. **Effort storage:** Todoist's native Duration field.
5. **Task naming:** plain action-first title (e.g. "Build WhatsApp reminder flow") —
   no phase prefix; the Todoist project already identifies the client, and the
   work-type label already identifies the category.
6. **Task → file link:** a reference line in the task description (e.g.
   "Plan: projects/acme-corp/plan.md").

## B. Calendar work-block conventions (`calendar-management`) — DECIDED
7. **Title format:** `[Work] <client> — <task>`.
8. **Which calendar:** primary calendar (not a dedicated one).
9. **Maximum block length:** 2.5 hours as the default cap, but dynamic based on need
   — if a task genuinely needs longer, don't force an arbitrary split just to respect
   the cap. 2.5h is the normal ceiling, not a hard wall.
10. **Buffer around meetings:** 30 minutes before/after fixed commitments before
    placing a work block.
11. **Busy/free marking:** Busy — work blocks represent real committed time.

## C. Time-orchestration methodology — DECIDED
12. **Effort estimation:** learn from historical actuals over time. Derived fresh
    from Todoist each time (duration field vs. completion timestamp gap for
    completed tasks of the same work-type label) — no separate tracking memory file.
    **Starting baselines** (used until enough same-type history exists to calibrate
    against): Research 1–4h, Build 4–20h (wide range — `memory/business.md` notes a
    20h-planned project can run to 50h), Admin 0.5–2h, Call = actual meeting length
    (not estimated). Claude picks within range based on known task-scope details;
    flag the estimate ASSUMED/Low confidence when scope is thin or no history exists
    yet for that work type.
13. **Movability rules:** Calendar events (meetings, university, club) are fixed —
    never touched without approval. All Todoist tasks are eligible to move/reschedule
    by default unless Amer has explicitly flagged one as fixed. Existing deep-work
    blocks are **fully protected** — never moved to make room for new work; only the
    placement of new work blocks changes around them.
14. **Deprioritization order when overloaded:** strictly by Todoist priority tier —
    P4 gives way first, then P3, then P2; P1 is touched last. Confirmed 2026-08-17.

## Test scenarios — IN PROGRESS
Data source confirmed 2026-08-17: **fully synthetic**, same as `client-intelligence`
— invented Todoist/Calendar state, no calls to Amer's real accounts. Scenarios live
in `references/test-scenarios/`.

- **Scenario 1 — daily capacity check**, run 2026-08-17 —
  `references/test-scenarios/scenario-1-daily-capacity/`. Exercised the core
  AVAILABLE/REQUIRED/GAP calculation and priority-tier bucketing. Surfaced 3 real
  gaps in the formula as written in SKILL.md, all fixed 2026-08-17, re-run confirmed
  clean numbers:
  1. AVAILABLE base was ambiguous (raw window vs. `memory/user.md`'s pre-netted
     figure) — fixed to always source from `realistic_productive_hours_per_day`,
     "Calendar commitments" now means only extra/non-routine commitments on top.
  2. REQUIRED only counted tasks due strictly inside the window, missing near-term
     deadlines needing today's time — fixed to a must-start-today test (remaining
     effort vs. remaining capacity between tomorrow and the due date).
  3. Buffer was being treated as a flat weekly figure — fixed to a 15% proportional
     rate applied to whatever window (day or week) is being computed.
