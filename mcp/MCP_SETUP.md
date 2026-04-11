# MCP Setup Notes

MCP is the connection method many AI apps use for tools.

You do not need to explain MCP to a regular user. Ask them to open DealDash -> **Tools > AI Agent Setup** and copy the ready prompt.

## Commands

Use this repo as public setup context:

```bash
git clone https://github.com/djasha/dealdash-agent-kit.git
cd dealdash-agent-kit
```

Inspect the placeholder MCP config:

```bash
cat mcp/dealdash-agent-bridge.mcp.example.json
```

Do not write real secrets into this repo.

## Safe Setup

1. Start read-only.
2. Put keys only into secure environment or MCP settings.
3. Never paste passwords into chat.
4. Never print secrets back to the user.
5. Ask before write actions.

## Required Values

Use placeholders in docs and public files:

- `DEALDASH_AGENT_BASE_URL`: `https://dealdash.neonoir.ai`
- `DEALDASH_AGENT_SERVICE_SECRET`: `<DEALDASH_AGENT_SERVICE_SECRET>`
- `DEALDASH_AGENT_DEFAULT_USER_ID`: `<DEALDASH_USER_ID>`
- `DEALDASH_AGENT_DEFAULT_SUPABASE_USER_ID`: `<DEALDASH_SUPABASE_USER_ID>`
- `DEALDASH_AGENT_CHANNEL`: `mcp:generic`
- `DEALDASH_AGENT_ACTOR_ID`: `dealdash-agent-bridge`

## Read-Only First Checks

- latest screenshots
- LinkShot View Logs
- due view checks
- deal summaries
- contact or influencer lookup

## Common Errors

- `agent_auth_failed`: the secure Agent key is missing or wrong. Ask an admin to update secure MCP/environment settings.
- `agent_route_not_allowed`: use only the documented DealDash Agent Bridge tools.
- `agent_approval_required`: explain the change and ask for approval before retrying.
- `agent_cross_account_denied`: stop. Do not guess IDs or try another account.
- Empty screenshots/logs: check account, filters, LinkShot upload status, and shared/team scope.

Agent reference: https://docs.drdj.me/internal/dealdash-agent-bridge-plugin
