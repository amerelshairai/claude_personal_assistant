# Build plan

## Done

- Project structure
- `CLAUDE.md` — orchestrator role, skill routing, Calendar/Todoist split, capacity
  thinking, evidence discipline, memory policy
- `.claude/rules/execution-policy.md` — Levels 0–3, global no-delete, privacy bounds
- `.claude/rules/reporting.md` — 10 task states, report format
- `.claude/settings.json` — enforced permission layer backing the no-delete rule
- 9 skill scaffolds with fixed contracts and open questions
- `client-analyst` subagent, tool-restricted so it cannot contact anyone or write to
  Todoist/Calendar
- `memory/` templates — **filled**: `user.md` + `business.md` (2026-08-16),
  `preferences.md` (2026-08-17)
- **`client-intelligence` — STATUS: TESTED.** Full methodology, `templates/
  package-outline.md` filled, 4 synthetic test scenarios run (vague lead, clinic,
  real estate, e-commerce) — see `.claude/skills/client-intelligence/references/
  DESIGN-QUESTIONS.md`.
- **`time-orchestration` + `todoist-management` + `calendar-management` — STATUS:
  TESTED.** All 14 convention questions resolved, 3 synthetic test scenarios run
  (daily capacity, urgent mid-week work, deadline collision), plus 2 more findings
  from `business-analysis`'s tests folded back in (5th Todoist label `Bugfix`;
  Bugfix REQUIRED uses the pessimistic range end, not the midpoint) — see
  `.claude/skills/time-orchestration/references/DESIGN-QUESTIONS.md`. One follow-up
  open: real per-weekday capacity figures for `memory/user.md` (Friday differs from
  a Tuesday) — on Amer to fill in, not a blocker.
- **`business-analysis` — STATUS: TESTED.** Rate/margin/pricing model reused
  directly from `memory/business.md`; 3 open questions resolved (ROI horizon,
  effort multipliers by project type, viability threshold) plus 3 synthetic test
  scenarios (greenfield, feature-addition, bug-fix/maintenance) — see
  `.claude/skills/business-analysis/references/DESIGN-QUESTIONS.md`. Introduced a
  GO/NO-GO/CONDITIONAL/NEEDS-REPRICING verdict system and a payment/billing
  risk-elevation rule mirroring `client-intelligence`'s health-data rule.

## Not done

`automation-architecture`, `project-planning`, `document-production`,
`execution-reporting` are still scaffolds without methodology. `templates/`
(top-level, for document-production) is still empty.

## Order to build

~~**1. Fill `memory/user.md` + `memory/business.md`**~~ — done.

~~**2. `client-intelligence`**~~ — done, TESTED.

~~**3. `time-orchestration` + `todoist-management` + `calendar-management`**~~ —
done, TESTED.

~~**4. `business-analysis`**~~ — done, TESTED.

**5. `automation-architecture`** — resolve n8n access first, then build the pattern
library from workflows you have already shipped.

**6. `project-planning`** — depends on effort estimation heuristics from step 3
(now in `time-orchestration`/`business-analysis`).

**7. `document-production`** — house style, then templates.

**8. `execution-reporting`** — the format already works; add morning/evening routines
last, once the underlying skills produce trustworthy numbers.

## How to build each one

1. Open a session in the project.
2. `We're implementing the <name> skill. Ask me the open questions in its SKILL.md
   and DESIGN-QUESTIONS file one at a time, then write the implementation.`
3. Test on a real scenario immediately. Not a hypothetical — real client, real week.
4. Correct what it got wrong; fold the correction into the SKILL.md.
5. Commit. Move on.

Resist building two at once. A skill that has not been tested against real work is a
guess, and guesses compound.

## Things to decide as you go

- Should morning/evening reports run as scheduled tasks, or on demand?
- Does `client-analyst` need siblings (e.g. a `researcher`, an `n8n-builder`), or does
  one specialist plus skills cover it? Add a subagent only when parallelism or tool
  restriction gives real value — not for tidiness.
- Which rules have proven important enough to move from `rules/` into enforced
  `settings.json` deny rules or hooks?
