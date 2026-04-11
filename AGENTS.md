# DealDash Agent Instructions

Use these rules when a user asks you to connect to DealDash.

## First Response

Tell the user:

1. "I will start read-only."
2. "I will not ask for your DealDash password."
3. "If an Agent key is needed, enter it only in the secure MCP/environment setup."
4. "If a Render key is needed, enter it only in the secure MCP/environment setup."
5. "I will ask before changing deals, payments, screenshots, links, sharing, or Render settings."

## Setup Links

- Simple human guide: https://docs.drdj.me/agents/agent-quick-start
- Public setup kit: https://github.com/djasha/dealdash-agent-kit
- Optional Render MCP setup: https://docs.drdj.me/agents/render-mcp-setup
- Advanced reference, only if exact tool names are needed: https://docs.drdj.me/internal/dealdash-agent-bridge-plugin

## Terminal Setup Command

```bash
git clone https://github.com/djasha/dealdash-agent-kit.git
cd dealdash-agent-kit
```

## Safe Defaults

- Default to read-only.
- Use `context.search` before guessing deal, screenshot, view log, or memory IDs.
- Use `deals.view_logs` for LinkShot View Logs.
- Use `screenshots.list_latest` for recent screenshot checks.
- Use `scope=mine-and-shared` only when the user asks for team-shared records.
- Redacted screenshot references must stay redacted unless the user has authorized screenshot access.
- Use `memory.create` only after showing the exact note to the user.
- Use `memory.archive` for stale memory; do not promise permanent deletion.
- Use Render MCP only for deploys, logs, metrics, services, databases, and environment-variable troubleshooting.
- Keep `RENDER_API_KEY` in secure MCP/environment settings only.

## Approval Needed

Ask for approval before:

- creating or updating deals
- creating, updating, or deleting payments
- deleting screenshots or short links
- changing visibility or team sharing
- changing Render service settings or environment variables
- sending external messages

## Never Do This

- Never ask for a DealDash password in chat.
- Never print service secrets.
- Never commit `.env` files.
- Never guess another user's ID.
- Never bypass approval gates.
- Never use local/private URL capture in production.
