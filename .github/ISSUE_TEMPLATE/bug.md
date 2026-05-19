---
name: Bug report
about: Report a problem with the JustFix Skill
labels: bug
---

**Harness**
Which harness is the skill running in? (OpenClaw, Hermes, Claude Code, Cursor, Codex CLI, Gemini CLI, other)

**Skill version**
Output of `cd <path-to-skill> && git rev-parse --short HEAD`:

**Steps to reproduce**
1. What did you ask the agent?
2. What tools did it call?
3. What response did it give?

**Expected behaviour**

**Actual behaviour**

**Logs / MCP response**
If you have the raw MCP tool response, paste it here.

**JustFix MCP server health**
Is the underlying server reachable? Quick check:
```bash
curl -s -X POST -H "Content-Type: application/json" -H "Accept: application/json, text/event-stream" \
  https://estimator-mcp.justfix.app/mcp \
  -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2024-11-05","capabilities":{},"clientInfo":{"name":"check","version":"1.0"}}}'
```

If the MCP server is the problem, contact JustFix at https://justfix.app/contact – this skill repo only handles skill-level issues.

**Additional context**
