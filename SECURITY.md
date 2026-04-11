# Security

This repo is public.

Do not commit:

- real Agent keys
- DealDash passwords
- Supabase keys or URLs that are not already public
- database URLs
- API tokens
- cookies or session values
- payment payloads
- screenshots containing private data
- local machine paths
- user IDs copied from private accounts

Use placeholders instead:

- `<DEALDASH_AGENT_SERVICE_SECRET>`
- `<DEALDASH_USER_ID>`
- `<DEALDASH_SUPABASE_USER_ID>`

If a secret is accidentally committed:

1. Remove it from the repo.
2. Rotate the secret immediately.
3. Check recent agent and app logs.
4. Treat the old value as exposed.

DealDash docs: https://docs.drdj.me/agents/agent-quick-start
