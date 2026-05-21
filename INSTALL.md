# JustFix Estimator — Install on Your AI Agent

JustFix Estimator is a free, open-source MCP server that lets your AI agent quote any UK trades job (plumbing, electrical, locksmith, glazing, carpentry, handyperson, heating, gas, roofing, drains, white goods, boiler service, +1) and generate a tappable booking link the user can complete in their browser.

- **Repo:** https://github.com/Just-Fix/justfix-skill
- **MCP endpoint:** `https://estimator-mcp.justfix.app/mcp` (Streamable HTTP, no auth)
- **License:** MIT
- **ClawHub:** https://clawhub.ai/skills/adam-graham/justfix
- **MCP Registry:** `io.github.Just-Fix/justfix-skill`

---

## Claude Desktop

Edit `~/Library/Application Support/Claude/claude_desktop_config.json` on Mac (or `%APPDATA%\Claude\claude_desktop_config.json` on Windows):

```json
{
  "mcpServers": {
    "justfix-estimator": {
      "command": "npx",
      "args": ["-y", "mcp-remote@latest", "https://estimator-mcp.justfix.app/mcp"]
    }
  }
}
```

Restart Claude Desktop.

**Test:** *"How much for a plumber to fix a dripping tap?"*

---

## Cursor

Settings → Features → Model Context Protocol → Add new MCP server:

| Field | Value |
|---|---|
| Name | `justfix-estimator` |
| Type | Streamable HTTP |
| URL | `https://estimator-mcp.justfix.app/mcp` |

Optionally drop `SKILL.md` from the repo into `.cursor/rules/justfix.md` so Cursor knows when to use it.

---

## Claude Code (CLI)

```bash
claude mcp add --scope user justfix-estimator https://estimator-mcp.justfix.app/mcp --transport http
mkdir -p ~/.claude/skills && cd ~/.claude/skills
git clone https://github.com/Just-Fix/justfix-skill.git justfix
```

**Test:** `claude` → *"Quote me 2 hours of electrical work."*

---

## Codex CLI

Edit `~/.codex/config.toml`:

```toml
[mcp_servers.justfix-estimator]
command = "npx"
args = ["-y", "mcp-remote@latest", "https://estimator-mcp.justfix.app/mcp"]
```

Then:

```bash
mkdir -p ~/.codex/skills && cd ~/.codex/skills
git clone https://github.com/Just-Fix/justfix-skill.git justfix
```

Add a reference in your `AGENTS.md`:

```markdown
- **justfix** – quote UK trades jobs. See ~/.codex/skills/justfix/SKILL.md
```

---

## Gemini CLI

Edit `~/.config/gemini-cli/config.json`:

```json
{
  "mcp_servers": {
    "justfix-estimator": {
      "url": "https://estimator-mcp.justfix.app/mcp",
      "transport": "streamable-http"
    }
  }
}
```

Optionally include the skill instructions:

```bash
mkdir -p ~/.config/gemini-cli/instructions
cd ~/.config/gemini-cli/instructions
git clone https://github.com/Just-Fix/justfix-skill.git justfix
```

---

## OpenClaw

```bash
openclaw skills install justfix
```

Or manually:

```bash
cd ~/.openclaw/workspace/skills
git clone https://github.com/Just-Fix/justfix-skill.git justfix
```

OpenClaw auto-discovers it.

---

## Hermes

```bash
cd ~/.hermes/skills
git clone https://github.com/Just-Fix/justfix-skill.git justfix
```

Then add to `~/.hermes/config.yaml`:

```yaml
mcp_servers:
  justfix-estimator:
    url: https://estimator-mcp.justfix.app/mcp
    transport: streamable-http
```

Restart Hermes.

---

## Any other MCP-aware client

The server speaks the standard **Streamable HTTP MCP** protocol at:

```
https://estimator-mcp.justfix.app/mcp
```

No auth, no config, no rate limits (be reasonable). Three tools: `list_services`, `call_out_fee`, `service-estimate-card`. Full schema available via `tools/list`.

---

## Test prompt (works on any install)

> "How much would JustFix charge for a 2-hour electrical job to install some sockets?"

You should get a quote card with:

- Labour cost (hours × hourly rate)
- £50 call-out fee
- Total estimate in GBP
- A tappable booking URL pointing at `my.justfix.app` (with a tracking UUID — please don't strip query parameters)

---

## Support

- **Skill bugs / install issues:** https://github.com/Just-Fix/justfix-skill/issues
- **MCP server bugs / pricing questions:** contact JustFix at https://justfix.app/contact

## License

MIT. Use, modify, redistribute freely, commercial or not.
