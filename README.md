# Personal Business Agent — setup

Scaffold only. Structure, policy and contracts are in place; skill methodology is not.
That is deliberate (spec §32) — we build skills one at a time and test each.

## How this actually works

There is nothing to "install" and nothing to paste into Claude Code. Claude Code reads
`CLAUDE.md`, `.claude/rules/`, `.claude/skills/` and `.claude/agents/` **from whatever
folder you launch it in**. So the entire setup is: put the folder somewhere, `cd` into
it, run `claude`.

If you launch Claude Code from any other folder, none of this loads. That is the single
most common mistake.

## 1. Put the folder somewhere permanent (Windows CMD)

Not Downloads. Extract the zip, then move it. Example:

```cmd
cd /d C:\Users\%USERNAME%
move C:\Users\%USERNAME%\Downloads\personal-business-agent .
cd personal-business-agent
dir
```

`dir` should list `CLAUDE.md`, `README.md`, `BUILD-PLAN.md`, `memory`, `projects`.
The `.claude` folder is hidden — check it with `dir /a`.

> `cd /d` is required in CMD when changing drive letters. Plain `cd` will not switch
> from `C:` to `D:`.

## 2. Put it under version control

```cmd
git init
git add -A
git commit -m "Scaffold personal business agent"
```

You will iterate on these prompts constantly. When behavior changes, `git diff` is the
difference between tuning and guessing.

## 3. Run it

```cmd
claude
```

That is the whole thing. From this folder, every session loads the orchestrator role,
the permission policy, and all nine skills.

## 4. Verify it loaded

Inside the session:

| Command | Expect |
| --- | --- |
| `/context` | `CLAUDE.md` plus both `.claude/rules/` files under **Memory files** |
| `/agents` | `client-analyst` listed |
| `/mcp` | Todoist, Gmail, Google Calendar — all `connected` |
| type `/` | the nine skills in the menu |
| `/permissions` | the ask and deny rules from `settings.json` |

If a skill is missing, its YAML frontmatter is malformed. If `CLAUDE.md` is missing,
you launched from the wrong folder.

## 5. Connectors — you probably do not need to do anything

MCP servers you added on claude.ai are **automatically available in Claude Code** when
you are logged in with your claude.ai account. Since you already authorized Todoist,
Gmail and Google Calendar there, they should simply appear in `/mcp`.

Two things worth knowing:

- **Gmail and Google Calendar cannot be added with `claude mcp add`.** They are
  Anthropic-hosted connectors, and the upstream identity provider only accepts the
  redirect URL claude.ai registered. Local OAuth from Claude Code will fail by design.
  They must come from claude.ai — which they already do.
- **If `/mcp` shows nothing from claude.ai**, your authentication method is wrong, not
  your connector. Connectors are only fetched when the active credential is a claude.ai
  subscription login. Run `/status`; if it shows an API key, Bedrock, or a profile, that
  is the cause. Unset `ANTHROPIC_API_KEY`, then run `/login` and pick your claude.ai
  account.

Todoist is the exception — it also offers a direct endpoint, if you ever want it
independent of claude.ai:

```cmd
claude mcp add --transport http todoist https://ai.todoist.net/mcp
```

Then authenticate it via `/mcp`. Note that a server added this way takes precedence
over the claude.ai connector pointing at the same URL.

## 6. Fill in memory/ — do this before real use

The agent is only as good as `memory/user.md` and `memory/business.md`. Right now they
are placeholders. Without your working hours and capacity, `time-orchestration` computes
nothing real. Without your rate, `business-analysis` cannot price anything.

Fastest way — open a session in this folder and say:

> Interview me to fill in memory/user.md and memory/business.md, one question at a time.

## 7. What is enforced vs merely instructed

`.claude/settings.json` holds real permission rules. `CLAUDE.md` and `.claude/rules/`
are strong context, but the docs are explicit that memory files are *context, not
enforced configuration* — Claude reads them and tries to comply, with no guarantee.

Currently enforced:

- **Ask on every delete, trash, cancel, send, reply, forward, publish, archive** across
  all MCP servers
- **Deny** `rm`, `rmdir`, `shred`, `git clean`, `git reset --hard`, and PowerShell
  `Remove-Item` / `Clear-Content`

The ask rules use glob patterns (`mcp__*delete*`) rather than exact tool names, because
claude.ai connector tools are named `mcp__claude_ai_<server>__<tool>` while directly
added servers are named `mcp__<server>__<tool>`. The glob matches both.

Verify with `/permissions` after first launch. If a rule you expect is missing, tell
Claude the exact tool name from `/mcp` and have it tighten the rule.

If a rule ever proves important enough that Claude must *never* break it, promote it
from `rules/` to a `deny` entry or a `PreToolUse` hook.

## 8. Known gap: n8n

No n8n connector was present when this was built. `automation-architecture` currently
designs workflows and produces importable JSON but cannot touch a live instance.
See `.claude/skills/automation-architecture/references/n8n-access.md` for the three
ways to close that gap.

## Layout

```
personal-business-agent/
├── CLAUDE.md                  # orchestrator role, routing, Calendar/Todoist split
├── .claude/
│   ├── settings.json          # enforced permissions
│   ├── rules/                 # always-loaded policy
│   ├── agents/client-analyst.md
│   └── skills/                # 9 skills, loaded on demand
├── memory/                    # persistent context — read selectively
├── projects/<client>/         # per-engagement working files
├── templates/
└── reports/
```

## First real session

```cmd
cd /d C:\Users\%USERNAME%\personal-business-agent
claude
```

Then:

> Read README.md and BUILD-PLAN.md, confirm what loaded, and interview me to fill in
> memory/user.md.

Next build target is `client-intelligence` (spec §33) — but answer the questions in
`.claude/skills/client-intelligence/references/DESIGN-QUESTIONS.md` first. See
`BUILD-PLAN.md`.
