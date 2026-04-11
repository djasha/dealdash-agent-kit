# DealDash Agent Kit

Public setup notes for connecting AI agents to DealDash safely.

This repo is intentionally simple. It is made for two readers:

- regular users who want an AI agent to help with DealDash
- AI agents that need safe setup instructions before calling DealDash tools

## Start Here

1. Open DealDash.
2. Go to **Tools** -> **AI Agent Setup**.
3. Click **Copy prompt**.
4. Paste that prompt into your AI app.
5. Start read-only.

Simple guide: https://docs.drdj.me/agents/agent-quick-start

## What Agents Can Do First

- show latest screenshots
- show LinkShot View Logs
- find deals, promo codes, creators, and view history
- summarize what needs attention

These are read-only checks. Ask before changing anything.

## Important Safety Rules

- Do not paste your DealDash password into an AI chat.
- Do not store real keys in this repo.
- Put Agent keys only into secure MCP or environment settings.
- Start read-only, then ask for approval before writes.
- Never send payment details, secrets, or private local file paths unless the user explicitly approves the exact action.

## Files

- `prompts/ready-prompt.md`: prompt users can paste into an AI app
- `skills/dealdash-agent-bridge/SKILL.md`: instructions for agents
- `mcp/MCP_SETUP.md`: plain MCP setup notes
- `mcp/dealdash-agent-bridge.mcp.example.json`: placeholder-only MCP example
- `SECURITY.md`: what must never be committed here

## Agent-Optimized References

- Agent bridge reference: https://docs.drdj.me/internal/dealdash-agent-bridge-plugin
- API surface: https://docs.drdj.me/backend/api-surface
- Task routing: https://docs.drdj.me/agents/task-routing

This public kit does not contain production secrets or private DealDash data.
