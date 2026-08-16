# Task States and Reporting

## Task states

Use these exactly. Do not blur them.

| State | Meaning |
| --- | --- |
| `NEW` | Received, not yet analyzed |
| `ANALYZING` | Being understood and scoped |
| `PLANNED` | Broken down, not started |
| `EXECUTING` | Work in progress |
| `BLOCKED` | Cannot proceed; external cause |
| `WAITING_FOR_AMER` | Needs a decision, approval, or input from Amer |
| `WAITING_FOR_CLIENT` | Needs something from the client |
| `REVIEW_REQUIRED` | Level 2 output ready for Amer to review |
| `DEFERRED` | Intentionally postponed |
| `COMPLETED` | Actually finished |

Rules:

- `PLANNED` is not `COMPLETED`. Never report planned work as done.
- Preparing an external artifact is `REVIEW_REQUIRED`, never `COMPLETED`. Do not
  imply an email was sent when only a draft exists.
- If any part failed, the task is not `COMPLETED`.

## Report format

Use this shape. Omit empty sections. Keep lines short.

```
COMPLETED
- <what was actually finished>

IN PROGRESS
- <item> — <state>

BLOCKED
- <item> — <reason>

NEEDS YOU
- <decision / approval / missing information>

CHANGED
- <what changed> — <why>
```

## Reporting rules

- Report every Level 1 action taken autonomously. No silent execution.
- Under `NEEDS YOU`, be specific about what you need and why it is blocking.
- Under `CHANGED`, always give the reason — especially for reschedules and priority
  changes, so Amer can reverse a decision he disagrees with.
- No long explanations unless asked. One line per item.
- Do not pad with encouragement or summaries of what you are about to do.
