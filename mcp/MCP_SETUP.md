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
- `RENDER_API_KEY`: `<YOUR_RENDER_API_KEY>` only for optional Render MCP deploy/log checks

## Read-Only First Checks

- context search
- latest screenshots
- LinkShot View Logs
- due view checks
- deal summaries
- contact or influencer lookup

## MCP Resources And Prompts

If your MCP host supports resources, read:

- `dealdash://context/search`
- `dealdash://linkshot/view-logs`
- `dealdash://memory/active`

If your MCP host supports prompts, start with:

- `dealdash_read_only_start`
- `dealdash_image_to_link`

## Image Uploads

DealDash accepts PNG, JPG/JPEG, WebP, GIF, AVIF, and BMP images by default.
The default image limit is 40MB. If a user sends SVG, HEIC, or TIFF, convert it
to PNG, JPG, or WebP before calling the screenshot upload tool.

## Common Errors

- `agent_auth_failed`: the secure Agent key is missing or wrong. Ask an admin to update secure MCP/environment settings.
- `agent_route_not_allowed`: use only the documented DealDash Agent Bridge tools.
- `agent_approval_required`: explain the change and ask for approval before retrying.
- `agent_cross_account_denied`: stop. Do not guess IDs or try another account.
- Empty screenshots/logs: check account, filters, LinkShot upload status, and shared/team scope.
- Stale memory: list active memories, then archive the stale one.

Agent reference: https://docs.drdj.me/internal/dealdash-agent-bridge-plugin

## Optional Render MCP

Use Render MCP only for deployment infrastructure:

- services
- deploy status
- logs
- metrics
- databases
- environment-variable troubleshooting

Use DealDash MCP for screenshots, LinkShot logs, short links, deals, contacts,
tasks, payments, and memory.

Hosted MCP URL:

```text
https://mcp.render.com/mcp
```

Secure env name:

```text
RENDER_API_KEY
```

For HTTP MCP clients:

```toml
[mcp_servers.render]
url = "https://mcp.render.com/mcp"
http_headers = { Authorization = "Bearer <YOUR_RENDER_API_KEY>" }
```

For mcp-remote clients:

```json
{
  "mcpServers": {
    "render": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://mcp.render.com/mcp",
        "--header",
        "Authorization: Bearer ${RENDER_API_KEY}"
      ],
      "env": {
        "RENDER_API_KEY": "<YOUR_RENDER_API_KEY>"
      }
    }
  }
}
```

Simple guide: https://docs.drdj.me/agents/render-mcp-setup
Official docs: https://render.com/docs/mcp-server
