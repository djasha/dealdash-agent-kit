# DealDash Agent Errors

Keep troubleshooting short and give the user one next step.

## Auth

- `missing_agent_auth`: start DealDash login authorization and send the approval link to the user.
- `agent_auth_failed`: the agent token is missing, expired, or invalid. Start a new login authorization link.
- `invalid_agent_context`: the request id header is missing, or operator-managed auth is missing acting user context.
- `acting_user_not_found`: the approved DealDash user is no longer available.

If MCP auth tools are unavailable but HTTPS is available, start login-link auth
directly with `POST https://dealdash.neonoir.ai/api/agent/auth/start`, send only
`auth.authorizeUrl`, and keep `auth.deviceCode` inside tool state.

Never ask the user to paste a service secret, API key, internal ID, deployment
key, or password into chat.

## Approval

- `approval_required`: explain what would change and ask for approval.
- `approval_not_approved`: wait for manager approval.
- `approval_user_mismatch`: stop. The approval is for a different user.

## Data

- Empty screenshots/logs: check account, date filters, LinkShot upload status, and shared/team scope.
- Redacted attachment: keep it redacted. The user can only preview screenshots they own or can access through sharing.
- Cross-account data: stop and do not guess another user's ID.

## Images

- `invalid_media`: use PNG, JPG/JPEG, WebP, GIF, AVIF, or BMP.
- Too large: reduce image size or ask admin about the configured limit.
- SVG, HEIC, or TIFF: convert to PNG/JPG/WebP before upload.

## Memory

- Stale memory: list active memory, show the stale item, ask before archive.
- Bad memory candidate: skip it if it is a secret, private path, payment payload, password, or unverifiable guess.
