# Perkadoo skills

Pick giveaway winners fairly and get a results page that proves it.

Paste your comments and say how many winners. [Perkadoo](https://perkadoo.com) locks the list in, picks winners with public [drand](https://drand.love) randomness nobody controls, and gives you a results page and share image to post. No account needed.

This repo has the Perkadoo giveaway skill and the config to connect the [Perkadoo MCP server](https://perkadoo.com/docs/api/mcp) (`https://mcp.perkadoo.com/mcp`) in each tool below.

## Install

**Claude Code**

```sh
/plugin marketplace add perkadoo/perkadoo-skills
/plugin install perkadoo@perkadoo
```

**Claude.ai and Claude Desktop:** add `https://mcp.perkadoo.com/mcp` under Settings → Connectors → Add custom connector. Then zip `skills/perkadoo-giveaway` and upload it under Settings → Capabilities → Skills.

**Gemini CLI**

```sh
gemini extensions install https://github.com/perkadoo/perkadoo-skills
```

**Cursor:** [add the Perkadoo MCP server](cursor://anysphere.cursor-deeplink/mcp/install?name=perkadoo&config=eyJ1cmwiOiJodHRwczovL21jcC5wZXJrYWRvby5jb20vbWNwIn0=), or add this to `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "perkadoo": { "url": "https://mcp.perkadoo.com/mcp" } } }
```

**Codex:** add this to `~/.codex/config.toml`, and copy `skills/perkadoo-giveaway` into `~/.codex/skills/`:

```toml
[mcp_servers.perkadoo]
url = "https://mcp.perkadoo.com/mcp"
```

**Any other MCP client:** connect `https://mcp.perkadoo.com/mcp` over streamable HTTP.

## Try it

- "Pick 2 winners from these comments: …"
- "Draw 1st, 2nd and 3rd place from this list and write my winner announcement."
- "Run a hosted giveaway for my 10k milestone." (needs a Perkadoo account; the assistant asks you to sign in)

## What needs an account

Drawing from a list, the results page and the share image are free with no account. Hosted giveaways with an entry page, streaks and perks sign in with Perkadoo over OAuth.

## Links

- [How Perkadoo draws are verified](https://perkadoo.com/docs/api/mcp)
- [Free giveaway tools](https://perkadoo.com/tools)

MIT licensed. This repo is mirrored from Perkadoo's main codebase, so open issues here and changes land in the next sync.
