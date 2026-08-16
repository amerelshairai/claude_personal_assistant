---
name: todoist-management
description: Create, update, reorganize and reprioritize Todoist tasks, subtasks, projects, sections, labels and reminders. Use when Amer wants tasks created from a plan, his Todoist reorganized, priorities or dates changed, or workload restructured after a replan.
when_to_use: Triggers on "add to Todoist", "create tasks", "reorganize my tasks", "change priority", "reschedule these", "clean up my Todoist", or after project-planning produces a work breakdown.
---

# Todoist Management

> **STATUS: SCAFFOLD.** Contract fixed; conventions to be defined with Amer.

Todoist holds **workload** — what Amer must accomplish. It does not hold meetings;
those live in Calendar.

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

- Project structure: one project per client? per engagement?
- Label taxonomy (client / type / energy level / delegable-to-Claude?)
- Priority mapping: what makes something P1 vs P2?
- Where estimated effort is stored (description, label, or duration field)
- Naming convention for tasks generated from a project plan
- How a Todoist task links back to `projects/<client>/`
