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
- `memory/` templates (placeholders — must be filled)

## Not done

Every skill is a contract without methodology. `templates/` is empty. `memory/` has no
real values. No test scenarios exist.

## Order to build

**1. Fill `memory/user.md` + `memory/business.md`** — blocks everything. Nothing can
compute capacity or price without these.

**2. `client-intelligence`** (spec §33) — answer `references/DESIGN-QUESTIONS.md`
first, then write methodology, then fill `templates/package-outline.md`, then test on
3 realistic scenarios including one with almost no information.

**3. `time-orchestration` + `todoist-management` + `calendar-management`** — build
together; they are one loop. This trio is what you will use daily, and it is where a
mistake is most visible. Define Todoist project structure and work-block conventions
before writing any logic.

**4. `business-analysis`** — needs your rate and pricing model from step 1.

**5. `automation-architecture`** — resolve n8n access first, then build the pattern
library from workflows you have already shipped.

**6. `project-planning`** — depends on effort estimation heuristics from step 3.

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
