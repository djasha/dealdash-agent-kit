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
2. If the bridge is not connected, call `agent_auth_start` and send the returned `authorizeUrl` to the user.
3. Poll with `agent_auth_status` after the user signs in and approves the link.
4. Never ask normal users for API keys, service secrets, internal IDs, or passwords.
5. Never print secrets back to the user.
6. Follow the DealDash write policy; always ask before deleting.

If `agent_auth_start` is unavailable because MCP is not connected yet, use the
public HTTPS login-link bootstrap instead:

```bash
curl -fsS -X POST https://dealdash.neonoir.ai/api/agent/auth/start \
  -H 'content-type: application/json' \
  --data '{"actorId":"openclaw-agent","channel":"openclaw:setup"}'
```

Send only `auth.authorizeUrl` to the user. Keep `auth.deviceCode`,
`auth.statusEndpoint`, and any approved token inside your tool/session state.
If status reports `connectionState: "token_already_claimed"` without a newly
stored token, start a fresh login-link authorization for the current AI session.
Normal setup is not blocked by missing internal operator env vars or deployment
settings.

## Login-Link Auth

Normal user setup does not require the user to paste keys.

1. Start authorization with `agent_auth_start`.
2. Send the returned DealDash approval link to the user.
3. The user opens the link, signs in, and approves.
4. Poll with `agent_auth_status`.
5. After approval, the bridge stores the scoped token inside the MCP process.

Operator-managed service-secret deployments are internal-only and must already
be preconfigured. They are not part of the normal user prompt.

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

- `missing_agent_auth`: start DealDash login authorization and send the approval link to the user.
- `agent_auth_failed`: the agent token is missing, expired, or invalid. Start a new DealDash login authorization link.
- `token_already_claimed`: start a fresh login authorization link for the current AI session.
- `agent_route_not_enabled`: use only the documented DealDash Agent Bridge tools.
- `approval_required`: explain the change and ask for approval before retrying.
- `agent_cross_account_denied`: stop. Do not guess IDs or try another account.
- Empty screenshots/logs: check account, filters, LinkShot upload status, and shared/team scope.
- Stale memory: list active memories, then archive the stale one.

Agent reference: https://docs.drdj.me/internal/dealdash-agent-bridge-plugin
