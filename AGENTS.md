# DealDash Agent Instructions

Use these rules when a user asks you to connect to DealDash.

## First Response

Tell the user:

1. "I will start read-only."
2. "I will not ask for your DealDash password."
3. "If DealDash is not connected, I will send a DealDash login approval link."
4. "I will not ask for API keys, service secrets, or internal IDs."
5. "I will ask before changing deals, payments, screenshots, links, sharing, or external messages."

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
- If not connected, use `agent_auth_start` and send the returned `authorizeUrl` to the user.
- If `agent_auth_start` is unavailable because MCP is not connected, start auth with direct HTTPS:

  ```bash
  curl -fsS -X POST https://dealdash.neonoir.ai/api/agent/auth/start \
    -H 'content-type: application/json' \
    --data '{"actorId":"openclaw-agent","channel":"openclaw:setup"}'
  ```

- Send only `auth.authorizeUrl` to the user. Keep `auth.deviceCode`, `auth.statusEndpoint`, and any approved token inside your tool/session state.
- Poll with `agent_auth_status` or `auth.statusEndpoint` only after the user opens the link and approves.
- Do not report normal setup as blocked by missing internal operator env vars or deployment settings.
- Use `context.search` before guessing deal, screenshot, view log, or memory IDs.
- Use `deals.view_logs` for LinkShot View Logs.
- Use `screenshots.list_latest` for recent screenshot checks.
- Use `scope=mine-and-shared` only when the user asks for team-shared records.
- Redacted screenshot references must stay redacted unless the user has authorized screenshot access.
- Use `memory.create` only after showing the exact note to the user.
- Use `memory.archive` for stale memory; do not promise permanent deletion.

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
- Never ask a normal user for API keys, service secrets, or internal IDs.
- Never commit `.env` files.
- Never guess another user's ID.
- Never bypass approval gates.
- Never use local/private URL capture in production.
