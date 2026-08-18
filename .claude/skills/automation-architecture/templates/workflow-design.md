# Automation Design — <CLIENT> — <WORKFLOW NAME>

Date: <YYYY/MM/DD> · Designer: automation-architecture

> Diagram-first. Plain language everywhere except database/API-key handling, which
> stays fully precise. See `../SKILL.md` § Documentation style.

## 1. Architecture Diagram
The primary artifact — see `architecture-diagram.md` for conventions. Shows
trigger → nodes → outcome. Built to extend cleanly when a later feature is added,
not to be redrawn from scratch.

## 2. Why (business requirement served)
Plain language — which pain point or opportunity (from `client-intelligence`'s
package, if one exists) this design addresses. No jargon.

## 3. Database / Credentials / API Keys
**The one section held to full technical precision — never glossed over.**
- What's stored, where.
- Auth method per integration.
- Never a real secret in this document — reference how it's held (env var,
  credential store), not the value.

## 4. Dependencies
Accounts, access, other systems, client actions needed before this can be built.

## 5. Risks
Failure modes and what happens when each occurs. Plain language — what breaks and
what the user sees, not a stack trace.

## 6. Cost
Setup and per-month, including API/LLM usage at expected volume. Hand off to
`business-analysis` for the rigorous version — this is the technical-design-side
estimate.

## 7. Effort
Realistic build hours — feeds `business-analysis` and `project-planning`. Use
`time-orchestration`'s Research/Build/Admin/Call/Bugfix baselines.

## 8. Non-negotiable elements checklist
Confirm each is addressed somewhere above, per `../SKILL.md`:
- [ ] Error handling — what happens when each external call fails
- [ ] Retry logic — with backoff, and a dead-letter path
- [ ] Logging — enough to debug a failure three days later
- [ ] Human approval points — where a person must confirm before an irreversible step
- [ ] Credential handling — never hardcoded, never a real secret in this doc
