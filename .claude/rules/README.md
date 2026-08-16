# Rules directory

Files here load into context at the start of **every** session, at the same priority as
`CLAUDE.md`. Keep them short — every line costs context on every request.

Current rules:

- `execution-policy.md` — permission levels 0–3, global no-delete rule, privacy bounds
- `reporting.md` — task states and the report format

Anything that is a multi-step *procedure* belongs in a skill, not here. Skills load on
demand; rules load always. If you find yourself writing "first do X, then Y, then Z"
in this directory, it should be a skill instead.

To scope a rule to certain files only, add `paths:` frontmatter:

```markdown
---
paths:
  - "projects/**/*.md"
---
```
