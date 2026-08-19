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
- **`automation-architecture` — STATUS: TESTED.** n8n MCP connection confirmed
  live (24 tools, verified with a real `search_workflows` call). No fixed
  node-pattern library — trigger selection tracked by requirement type instead
  (`references/n8n-patterns.md`); documentation is diagram-first, plain language
  except database/API-key handling. 2 test scenarios (synthetic design +
  real-n8n connection-health check) — see `.claude/skills/automation-architecture/
  references/DESIGN-QUESTIONS.md`. **Known issue found and documented, on Amer to
  check:** `get_node_types` fails on every call ("path traversal" error); until
  fixed, exact node parameters can't be confirmed and `validate_workflow` passing
  is not proof they're correct.
- **`project-planning` — STATUS: TESTED.** Task granularity 1h minimum,
  contingency buffer by project type (greenfield 20% / feature-addition 15% /
  bug-fix none), standard-but-flexible milestone template, risk register reuses
  the same 6 categories as `client-intelligence`/`business-analysis` — see
  `.claude/skills/project-planning/references/DESIGN-QUESTIONS.md`. 2 test
  scenarios: one found and closed a real pipeline-order gap (a feature reached
  design/estimation before ever getting a `business-analysis` viability pass);
  the other verified Google Calendar and Todoist are genuinely live with real
  read calls (found Calendar empty for 10 days, Todoist with zero real workload)
  and used that to compute a real deadline shortfall, not a fabricated one — which
  led to a new standing rule (Calendar-vs-memory precedence for recurring
  commitments) in `time-orchestration/SKILL.md`.
- **`document-production` — STATUS: TESTED.** House style prioritizes structure/
  searchability over visual polish (no brand assets yet) — see
  `.claude/skills/document-production/references/DESIGN-QUESTIONS.md`. 3 real
  templates built in `templates/` (proposal, ROI workbook shape, meeting-prep).
  2 test scenarios, both built from real prior-stage artifacts for Nova Home
  Goods rather than synthetic input: a client proposal (confirmed no internal
  cost/margin leaks; added a hard rule that a proposal's price is never
  finalized without Amer's explicit confirmation) and an ROI workbook with every
  figure traced as a checked, correct formula. Meeting-prep template exists but
  wasn't scenario-tested, per Amer — not a blocker.
- **`execution-reporting` — STATUS: TESTED.** Morning/evening reports stay
  on-demand; weekly review is scheduled (Fridays 5pm Asia/Amman) as a persistent
  cloud routine (`trig_01Wi4ehSPLZM9gjhtChVUQQe`) via the `schedule` skill, backed
  by a new private GitHub repo
  (`github.com/amerelshairai/claude_personal_assistant`) — see
  `.claude/skills/execution-reporting/references/DESIGN-QUESTIONS.md` +
  `references/test-scenarios.md`. Fired **twice against real Todoist/Calendar
  data**, not synthetic: run 1 found the cloud routine couldn't push its own
  output (GitHub App lacked write access — fixed by Amer, report recovered
  manually); run 2's push was independently verified (`git log origin/master -1`
  showed the real new commit). One open follow-up, not a blocker: recurring
  university/club commitments haven't appeared in either real-data run —
  possible wrong Google Calendar account, needs Amer to confirm.

## Not done

Nothing — **all 8 build steps are done and TESTED.** Remaining work is the
"Things to decide as you go" items below and any follow-ups noted per-skill above,
not new skills.

## Order to build

~~**1. Fill `memory/user.md` + `memory/business.md`**~~ — done.

~~**2. `client-intelligence`**~~ — done, TESTED.

~~**3. `time-orchestration` + `todoist-management` + `calendar-management`**~~ —
done, TESTED.

~~**4. `business-analysis`**~~ — done, TESTED.

~~**5. `automation-architecture`**~~ — done, TESTED.

~~**6. `project-planning`**~~ — done, TESTED.

~~**7. `document-production`**~~ — done, TESTED.

~~**8. `execution-reporting`**~~ — done, TESTED. **Build plan complete.**

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
