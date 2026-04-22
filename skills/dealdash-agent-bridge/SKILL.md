---
name: dealdash-agent-bridge
description: Safely connect AI agents to DealDash MCP tools, resources, prompts, context search, memory, screenshots, LinkShot View Logs, deals, links, contacts, tasks, suggestions, and approval-gated writes.
---

# DealDash Agent Bridge

Use this skill when a user asks an AI agent to help with DealDash.

## Start Human-Friendly

If the user is not technical, send them to:

- DealDash -> **Tools** -> **AI Agent Setup**
- https://docs.drdj.me/agents/agent-quick-start

Tell them to copy the ready prompt from the dashboard.

If you are a terminal-based agent, you may fetch the public setup kit:

```bash
git clone https://github.com/djasha/dealdash-agent-kit.git
cd dealdash-agent-kit
```

## Runtime Contract

- MCP server: `dealdash-agent-bridge`
- Simple guide: `https://docs.drdj.me/agents/agent-quick-start`
- Agent reference: `https://docs.drdj.me/internal/dealdash-agent-bridge-plugin`
- API surface: `https://docs.drdj.me/backend/api-surface`
- Public kit: `https://github.com/djasha/dealdash-agent-kit`
- Normal auth: call `agent_auth_start`, send only the returned DealDash approval link to the user, then poll `agent_auth_status`.
- Direct HTTPS bootstrap: if MCP is not installed yet but HTTPS requests are available, `POST https://dealdash.neonoir.ai/api/agent/auth/start`, send only `auth.authorizeUrl`, keep `auth.deviceCode` private in tool state, and poll `auth.statusEndpoint`.
- Internal operator auth: service-secret mode must already be preconfigured; never ask the user for service secrets or acting-user IDs.
- Default channel: `DEALDASH_AGENT_CHANNEL`, usually `mcp:generic`
- Default actor: `DEALDASH_AGENT_ACTOR_ID`, usually `dealdash-agent-bridge`

Never ask a public chat user to paste service secrets, approval confirmation secrets, internal IDs, payment payloads, passwords, or local filesystem paths.

Use the fewest links needed:

1. Send regular users to the simple guide.
2. Use this public kit for setup files and commands.
3. Open the agent reference only when exact operation names, routes, headers, or schemas are needed.

## Tool Families

- `short_links`: create from URL, list, get, stats, delete
- `screenshots`: upload photo, capture URL, reserve, link to deal, get, list latest, delete
- `deals`: search, get, get latest, create, update, find by URL, due views, view logs, bulk add view checks, progress
- `context`: search and resource hints
- `memory`: list, create, archive
- `payments`: list, create, update, delete
- `tasks`: list, get, get latest, create, complete, reopen
- `contacts`: search, get, get latest, upsert, by phone, deals, notes, labels, counts, duplicates
- `influencers`: search, get, get latest, upsert, by phone, by promo code, stats, last progress
- `activity`: feed and analytics
- `suggestions`: pipeline summary, next actions, payment followups, content followups
- `approvals`: request and status

## Read-Only First

If the bridge is not connected, start with `agent_auth_start` and wait for the
user to approve the DealDash login link. After approval, use these before any
write action:

If `agent_auth_start` is unavailable because MCP is not configured, start the
same login-link flow with direct HTTPS instead:

```bash
curl -fsS -X POST https://dealdash.neonoir.ai/api/agent/auth/start \
  -H 'content-type: application/json' \
  --data '{"actorId":"openclaw-agent","channel":"openclaw:setup"}'
```

Send only `auth.authorizeUrl` to the user. Keep `auth.deviceCode`,
`auth.statusEndpoint`, and any approved token inside your tool/session state.
If status reports `connectionState: "token_already_claimed"` without a newly
stored token, start a fresh login-link authorization for this agent process.
Do not ask for internal operator secrets, user IDs, or deployment settings for
normal setup.

- `context.search` for broad lookup across deals, screenshots, logs, links, people, and memory
- `screenshots.list_latest` for recent screenshots
- `deals.view_logs` for LinkShot View Logs and screenshot evidence
- `deals.due_views` for LinkShot To-Do style checks
- `deals.search` for deal lookup
- `contacts.search` or `influencers.search` for people lookup
- `suggestions.pipeline_summary` for overview

For shared data, use `scope=mine-and-shared` only when the user asks for shared team records.

If exact operation details are needed, read `references/tools.md`. If an error appears, read `references/errors.md`. For workflow examples, read `references/examples.md`.

## Approval Rules

- Tier 0 reads: no approval required.
- Tier 1 low-risk writes: short links, screenshot uploads, screenshot linking, notes, labels, and tasks may be allowed.
- Tier 2 sensitive writes: deal updates, payments, deletes, and visibility changes require approval.
- When the connection reports `allow_non_delete_writes`, non-delete Tier 2 writes can run after briefly stating the intended change. Delete-shaped routes still require explicit approval.

Always ask before deleting. When approval is required, explain what will change and why before retrying.

## LinkShot View Logs

Use `deals.view_logs` when the user asks about:

- checked views
- LinkShot logs
- screenshot evidence
- who uploaded or shared data
- platform totals
- missing platform labels

Return checked date, total views, per-platform views, missing platforms, visible screenshot links, redacted attachment counts, owner context, and share context.

Keep redacted attachment references redacted unless DealDash returns a visible screenshot link.

## Image Uploads

Use `screenshots.upload_photo` when the user explicitly asks to upload an image
or turn an image into a short DealDash link. PNG, JPG/JPEG, WebP, GIF, AVIF, and
BMP are accepted by default up to the configured limit. If the user sends SVG,
HEIC, or TIFF, convert it to PNG, JPG, or WebP first.

## Bulk LinkShot View Checks

Use `deals.bulk_add_view_checks` when the user sends grouped post links plus a
post date. Pass `linksText` with blank lines between people/groups, or
structured `collections` with `urls`, optional `promoCode`, and optional
`name`.

If DealDash returns `needsPromoCode`, reply with those grouped links and ask
only for the missing promo codes. Do not invent promo codes.

## Error Handling

- `missing_agent_auth`: start DealDash login authorization with MCP or direct HTTPS and send the approval link to the user.
- `agent_auth_failed`: the agent token is missing, expired, or invalid. Start a new login authorization link with MCP or direct HTTPS.
- `token_already_claimed`: start a fresh login authorization link for the current AI session.
- `agent_route_not_enabled`: stop and use only allowlisted tools.
- `approval_required`: request approval before retrying.
- `agent_cross_account_denied`: stop. Do not guess IDs.
- `invalid_media`: ask for PNG, JPG/JPEG, WebP, GIF, AVIF, or BMP image bytes under the configured size limit, or convert unsupported formats first.
- `capture_blocked_private_url`: do not bypass in production.
- Empty screenshots or logs: check the signed-in account, date filters, LinkShot upload status, and whether the user asked for shared/team records.
- Stale memory: call `memory.list`, show the stale entry, then ask before `memory.archive`.
