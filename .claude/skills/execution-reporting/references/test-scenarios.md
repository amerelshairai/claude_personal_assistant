# Test scenarios — execution-reporting

Real, not synthetic — the weekly-review cloud routine (`trig_01Wi4ehSPLZM9gjhtChVUQQe`)
was fired against Amer's actual Todoist and Google Calendar, twice.

## Run 1 — 2026-08-19, session `cse_01Xs11dfhLzw5ZH45zZdcKK3`
First live test, triggered manually (off-schedule) to validate the routine before
trusting the real Friday cron fire. Findings:
- Correctly self-detected the off-schedule fire (checked `CronList`, compared
  against the configured Friday 17:00 Asia/Amman slot) and treated the output as a
  partial-week snapshot, not a false full-week close.
- All data pulled from real Todoist/Calendar, honestly labeled — 0 completions,
  1 overdue task, empty Calendar, `ESTIMATE ACCURACY`/`CAPACITY UTILIZATION` left
  `UNKNOWN` rather than fabricated.
- **Real bug found: could not push its own output.** `git push`,
  `mcp__github__push_files`, and `mcp__github__create_or_update_file` all failed
  identically: `403 Resource not accessible by integration`. The GitHub App
  installation lacked write permission on this repo. Report content recovered from
  the run transcript and committed manually (`980c30b`) so nothing was lost.
- Minor: routine's prompt told it to name the file `weekly-review-<date>.md`,
  but `reports/README.md` documents `<date>-<type>.md` — routine read the README
  but still followed the (wrong) prompt instruction. Fixed in the routine's prompt.

## Fix applied between runs
Amer installed the Claude GitHub App and granted it write access to
`amerelshairai/claude_personal_assistant`. Routine's prompt updated: correct
naming convention, explicit instruction to fail fast (not retry indefinitely) on a
permission error, explicit instruction to flag an all-zero Calendar week as a
possible wrong-account issue rather than reporting it as genuinely open time.

## Run 2 — 2026-08-19, session `cse_01CF3tWf23iJNs7BaBBjnaxo`
Re-test after the GitHub fix. **Push succeeded** — hit an unrelated non-fast-forward
git rejection (origin had moved since this session's clone, from the run-1 recovery
commit), rebased onto `origin/master`, and pushed cleanly on its own
(`980c30b..34ebc1f`). **Independently verified** (not just trusting the run log):
```
git fetch origin && git log origin/master -1
34ebc1f Weekly review 2026-08-19 (off-schedule partial-week snapshot)
```
Report content: same honest discipline as run 1, plus a new real finding — an actual
Calendar event now exists ("Internal Meeting," Aug 20, organizer
sabrine.ai29@gmail.com, RSVP still `needsAction`) that wasn't present in run 1,
while the recurring university/club commitments still don't appear in either week
checked. Reproduced across two runs, strengthening rather than resolving the
wrong-account hypothesis.

## Follow-up — resolved 2026-08-19
Investigated directly after run 2: connected calendar had changed to
`amerelshair.ai@lindrize.online` (the correct account — `simplykitchen2006@gmail.com`
was a different, earlier session-only connection). Checked a full 3-week window
(2026-08-16 to 2026-09-06) on the correct account: still only the one real event
(the Aug 20 "Internal Meeting"), confirming this was never a wrong-account issue —
the recurring university/club commitments genuinely had never been added to
Calendar. Added both as real recurring events at Amer's request (`University`:
Sun–Wed 11:30am–2:30pm; `Club`: Sun/Tue/Thu 5–9pm, both Asia/Amman, marked Busy,
plainly editable). Verified the generated instances land correctly for the next
two weeks. Future weekly reviews should now see these directly from Calendar
without needing the memory-override rule for this specific gap.
