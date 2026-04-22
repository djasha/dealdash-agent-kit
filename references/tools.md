# DealDash Agent Tools

Use tools for actions, resources for context, and prompts for guided workflows.

## Best First Read

Call `context.search` before guessing exact IDs.

Useful params:

- `q`: text to search
- `scope`: `mine` or `mine-and-shared`
- `types`: comma-separated list such as `deals,screenshots,view_logs,memory`
- `limit`
- `offset`

## MCP Resources

- `dealdash://context/search`: recent searchable DealDash context.
- `dealdash://linkshot/view-logs`: recent LinkShot view logs.
- `dealdash://memory/active`: active human-visible agent memory.

## MCP Prompts

- `dealdash_read_only_start`: start with safe read-only checks.
- `dealdash_image_to_link`: upload an image and return a DealDash link after approval.

## Common Tools

- `screenshots.list_latest`: latest screenshots.
- `deals.view_logs`: LinkShot view history and screenshot evidence.
- `deals.due_views`: LinkShot To-Do style checks.
- `deals.bulk_add_view_checks`: add grouped post links for a date; ask for promo codes when DealDash returns `needsPromoCode`.
- `short_links.create_from_url`: create a DealDash short link when the user asks.
- `short_links.get`: inspect one DealDash short link.
- `tasks.get`: inspect one DealDash task.
- `screenshots.upload_photo`: upload an image when the user asks.
- `memory.create`: save a small account-scoped note after approval.
- `memory.archive`: archive stale memory.

## Memory Rules

Memory is visible DealDash data, not hidden agent thought.

Before `memory.create`, show:

- title
- content
- tags
- source

Use short, useful memory only: preferences, repeated troubleshooting steps, decisions, or known errors.
