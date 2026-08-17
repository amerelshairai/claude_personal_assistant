---
name: todoist-management
description: Create, update, reorganize and reprioritize Todoist tasks, subtasks, projects, sections, labels and reminders. Use when Amer wants tasks created from a plan, his Todoist reorganized, priorities or dates changed, or workload restructured after a replan.
when_to_use: Triggers on "add to Todoist", "create tasks", "reorganize my tasks", "change priority", "reschedule these", "clean up my Todoist", or after project-planning produces a work breakdown.
---

# Todoist Management

> **STATUS: TESTED.** Contract and conventions below are decided and exercised
> against the time-orchestration trio's 3 synthetic test scenarios — see
> `../time-orchestration/references/DESIGN-QUESTIONS.md` for the full reasoning and
> every fix each scenario produced.

Todoist holds **workload** — what Amer must accomplish. It does not hold meetings;
those live in Calendar.

## Conventions

- **Project structure:** one Todoist project per client. Internal/business-admin work
  (not tied to a specific client) gets its own project too.
- **Labels:** a work-type label — **Research / Build / Admin / Call** — plus a
  delegable-to-Claude flag label. Work-type also drives effort-estimation heuristics
  in `time-orchestration`.
- **Priority (P1–P4):** client-facing work defaults to P1/P2, internal/admin work
  defaults to P3/P4. Within each tier, deadline proximity splits it further:
  - P1: client-facing, due within ~48h or overdue.
  - P2: client-facing, not due within 48h.
  - P3: internal, due within a week.
  - P4: internal, no near deadline.
  This is a **default** — `time-orchestration` reasons from it, but an explicit
  instruction from Amer (e.g. university ranks above a client task right now)
  overrides it regardless of P-tier.
  **Ties within the same tier — including P1 vs. P1 — break by nearest deadline**:
  the task due soonest wins. Same rule at every tier, no special case for P1.
- **Effort estimate:** stored in Todoist's native Duration field, not the description
  or a label.
- **Task naming:** plain action-first title (e.g. "Build WhatsApp reminder flow") —
  no phase prefix. The project already identifies the client; the work-type label
  already identifies the category.
- **Linking back to project files:** a reference line in the task description, e.g.
  `Plan: projects/acme-corp/plan.md`.

## Authority

Level 1 (execute, then report): create tasks and subtasks, modify tasks, change
priority, change dates, reschedule, add reminders, organize projects and sections,
restructure, reprioritize, replan around new circumstances.

Level 3 (approval required, every time): **deleting anything.**

## Hard rules

- **Never delete a task without Amer's explicit approval.** Not "it looked done."
  Not "it was a duplicate." Ask.
- For obsolete items, prefer: complete it, move it, postpone it, relabel it, or
  recommend deletion and wait.
- Use `reschedule-tasks` to move a date, never `update-tasks` — `update-tasks`
  replaces the whole due string and destroys recurrence on recurring tasks.
- Never send an existing `projectId`, `sectionId` or `parentId` back in an update;
  those fields are treated as a move.
- Report every batch change. A silent bulk reorganization is a failure.

## Before bulk changes

Read the current state first. Show Amer what will change and how many items are
affected before executing a restructure of more than a few tasks.

## To define with Amer

See `../time-orchestration/references/DESIGN-QUESTIONS.md` §A — built together with
`time-orchestration` and `calendar-management` as one loop, per BUILD-PLAN.md.
