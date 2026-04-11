# Render And Supabase Helpers

Use these only when the user asks about deployment, secrets, logs, or database/search setup.

## Render

Helpful free/low-friction options:

- Render official skills: deploy, debug, and monitor apps from Codex, Claude Code, Cursor, and similar tools.
- Render MCP server: inspect services, deploys, logs, metrics, and databases from MCP-capable clients.
- Render `llms.txt` and markdown docs: useful for agent-readable deployment help.

Never print Render API keys or service environment values.

## Supabase

Helpful built-in pieces:

- Postgres for DealDash source of truth.
- Storage for screenshot objects.
- `pgvector` for future semantic search.
- Edge Functions only if a future async embedding job needs a serverless worker.

Current DealDash context search is plain Postgres text/OCR search. Add pgvector only after deciding:

- embedding model
- refresh job
- retention rules
- cost limit
- deletion/archive behavior

Graphiti-style temporal memory is useful later if DealDash needs relationship/time reasoning across many entities. It is not required for the first reliable agent context layer.
