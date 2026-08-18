# Test scenarios — automation-architecture

Combined approach, per Amer (2026-08-18): **fully synthetic is the default/priority**
for exercising methodology, but some scenarios use the **real, live n8n MCP
connection** — read-only and validate-only calls only — to check connection health
and whether a synthetic design is actually buildable with real nodes. **Never a real
build/create in this test suite**, even when live tools are used.

Each folder has `input.md` (the synthetic requirement) and `output.md` (the design
produced). A scenario using live tools says so explicitly and lists exactly which
calls were made.
