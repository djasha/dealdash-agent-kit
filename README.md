# DealDash Agent Kit

Public setup notes for connecting AI agents to DealDash safely.

This repo is intentionally simple. It is made for two readers:

- regular users who want an AI agent to help with DealDash
- AI agents that need safe setup instructions before calling DealDash tools

## Start Here

Regular users do not need to read GitHub first.

1. Open DealDash.
2. Go to **Tools > AI Agent Setup**.
3. Click **Copy prompt**.
4. Paste that prompt into your AI app.
5. If the agent is not connected, open the DealDash login approval link it sends back.
6. Start read-only.

Simple guide: https://docs.drdj.me/agents/agent-quick-start

## Commands For Agents

Terminal-based agents can fetch these public setup files with:

```bash
git clone https://github.com/djasha/dealdash-agent-kit.git
cd dealdash-agent-kit
```

Then read these files in order:

1. `AGENTS.md`
2. `prompts/ready-prompt.md`
3. `mcp/MCP_SETUP.md`
4. `skills/dealdash-agent-bridge/SKILL.md`
5. only the reference files needed from `references/`

## What Agents Can Do First

- show latest screenshots
- show LinkShot View Logs
- search DealDash context before guessing IDs
- find deals, promo codes, creators, and view history
- summarize what needs attention
- shorten a link or upload an image when the user explicitly asks
- save a useful memory only after showing the exact note to the user

The first five are read-only checks. Short links, screenshot uploads, and memory creation create DealDash records, so ask before doing them.

## Important Safety Rules

- Do not paste your DealDash password into an AI chat.
- Do not store real keys in this repo.
- Normal users should approve the DealDash login link, not paste API keys.
- Service secrets are only for internal operator-managed deployments.
- Start read-only, then ask for approval before writes.
- Never send payment details, secrets, or private local file paths unless the user explicitly approves the exact action.

## Common Problems

| Problem                                 | What To Do                                                                                                               |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| User only wants help, not setup details | Send them to DealDash > Tools > AI Agent Setup and ask them to copy the prompt.                                          |
| Agent asks for API keys or IDs          | Ask it to use DealDash login-link auth. Normal users should not paste service secrets or internal IDs.                   |
| Password requested by mistake           | Stop and correct course. DealDash passwords must not be pasted into chat.                                                |
| No screenshots or LinkShot logs         | Check account, filters, upload status, and whether shared/team records should be included.                               |
| Image upload fails                      | Use PNG, JPG/JPEG, WebP, GIF, AVIF, or BMP up to the configured limit. Convert SVG, HEIC, or TIFF to PNG/JPG/WebP first. |
| Write action blocked                    | Explain what would change and ask for approval before retrying.                                                          |

## Files

- `prompts/ready-prompt.md`: prompt users can paste into an AI app
- `skills/dealdash-agent-bridge/SKILL.md`: instructions for agents
- `mcp/MCP_SETUP.md`: plain MCP setup notes
- `mcp/dealdash-agent-bridge.mcp.example.json`: placeholder-only MCP example
- `references/tools.md`: tool, resource, prompt map
- `references/errors.md`: troubleshooting notes
- `references/examples.md`: short workflows agents can follow
- `SECURITY.md`: what must never be committed here

## Why This Repo Exists

The DealDash dashboard gives regular users one copy/paste prompt. This public repo gives AI agents safe setup files and commands without exposing the private DealDash app repo.

## Agent-Optimized References

- Agent bridge reference: https://docs.drdj.me/internal/dealdash-agent-bridge-plugin
- API surface: https://docs.drdj.me/backend/api-surface
- Task routing: https://docs.drdj.me/agents/task-routing

This public kit does not contain production secrets or private DealDash data.
