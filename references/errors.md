# DealDash Agent Errors

Keep troubleshooting short and give the user one next step.

## Auth

- `agent_bridge_not_configured`: production is missing `DEALDASH_AGENT_SERVICE_SECRET`.
- `agent_auth_failed`: secure Agent key is missing or wrong.
- `invalid_agent_context`: acting user, channel, actor, or request id header is missing.
- `acting_user_not_found`: the configured DealDash user id is wrong.

Never ask the user to paste a service secret into chat.

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
