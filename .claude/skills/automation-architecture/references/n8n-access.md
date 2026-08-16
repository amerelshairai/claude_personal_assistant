# n8n access — unresolved

As of scaffold creation, **no n8n connector is configured** in the environment this
project was built in. Amer stated the agent has n8n execution capability; that
capability was not observable, so it is recorded here rather than assumed.

**Do not claim to have created, tested, deployed or executed an n8n workflow unless a
working n8n tool is actually present and returned a result.**

## Options to resolve

### 1. n8n MCP server (best)
Community MCP servers exist for n8n. Adding one gives direct tool access to list,
create, update, execute and inspect workflows.

```bash
claude mcp add n8n --transport http https://<your-n8n-host>/mcp \
  --header "Authorization: Bearer <token>"
```

Verify with `/mcp` in a session, then update this file with the actual tool names.

### 2. n8n public REST API via Bash
n8n exposes a REST API with an API key (Settings → n8n API). Claude can call it with
`curl`. Workable, but every call needs the key available in the environment — use an
env var, never a literal in a file.

### 3. Design-only (current default)
Produce workflow JSON that Amer imports manually via n8n's *Import from File*. Fully
functional for design work, just not autonomous.

## What to record once resolved

- n8n base URL and version (node availability differs by version)
- Auth method
- Which environments exist (dev / prod) and which one Claude may touch
- Whether Claude may execute workflows or only create them
- The production deployment approval step (Level 3, always)
