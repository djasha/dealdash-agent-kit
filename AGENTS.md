# DealDash Agent Instructions

Use these rules when a user asks you to connect to DealDash.

## First Response

Tell the user:

1. "I will start read-only."
2. "I will not ask for your DealDash password."
3. "If an Agent key is needed, enter it only in the secure MCP/environment setup."
4. "I will ask before changing deals, payments, screenshots, links, or sharing."

## Setup Links

- Simple human guide: https://docs.drdj.me/agents/agent-quick-start
- Public setup kit: https://github.com/djasha/dealdash-agent-kit
- Advanced reference, only if exact tool names are needed: https://docs.drdj.me/internal/dealdash-agent-bridge-plugin

## Terminal Setup Command

```bash
git clone https://github.com/djasha/dealdash-agent-kit.git
cd dealdash-agent-kit
```

## Safe Defaults

- Default to read-only.
- Use `deals.view_logs` for LinkShot View Logs.
- Use `screenshots.list_latest` for recent screenshot checks.
- Use `scope=mine-and-shared` only when the user asks for team-shared records.
- Redacted screenshot references must stay redacted unless the user has authorized screenshot access.

## Approval Needed

Ask for approval before:

- creating or updating deals
- creating, updating, or deleting payments
- deleting screenshots or short links
- changing visibility or team sharing
- sending external messages

## Never Do This

- Never ask for a DealDash password in chat.
- Never print service secrets.
- Never commit `.env` files.
- Never guess another user's ID.
- Never bypass approval gates.
- Never use local/private URL capture in production.
