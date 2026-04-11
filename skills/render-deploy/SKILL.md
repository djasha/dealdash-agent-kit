---
name: render-deploy
description: Use Render's hosted MCP server for DealDash deployment logs, metrics, service status, and safe environment-variable troubleshooting.
---

# Render Deploy

Use this skill when the user asks an agent to inspect or troubleshoot Render deployment infrastructure for DealDash.

Do not use this skill for DealDash app data. Use `dealdash-agent-bridge` for screenshots, LinkShot logs, short links, deals, contacts, payments, tasks, context search, and memory.

## What Render MCP Is For

- checking Render services and workspace selection
- reading deploy history and deploy details
- reading recent logs
- reading service metrics
- querying Render Postgres with read-only SQL when explicitly requested
- updating service environment variables only after the user clearly approves the exact key/value change

## Secure Setup

- Hosted MCP URL: `https://mcp.render.com/mcp`
- Secure env name: `RENDER_API_KEY`
- Official docs: `https://render.com/docs/mcp-server`
- DealDash simple setup page: `https://docs.drdj.me/agents/render-mcp-setup`
- In-app guide: DealDash `/tools/render-mcp`
- Placeholder sample config: `mcp/dealdash-agent-bridge.mcp.example.json` -> `render-deploy`

Render API keys are broad. They can access all Render workspaces and services the Render account can access. Never ask the user to paste the key into normal chat. Ask them to put it only in secure MCP or environment settings.

## First Prompt To Run

Ask the host agent:

```text
Set my Render workspace to the workspace that hosts DealDash.
Then list the DealDash Render services and show the latest deploy status.
Do not update environment variables unless I approve the exact variable names and values first.
```

## Safe Tool Order

1. Select workspace.
2. List services.
3. Identify the DealDash service.
4. List latest deploys.
5. Read recent logs filtered to errors or warnings.
6. Check metrics only if troubleshooting performance.
7. Update environment variables only after explicit approval.

## Guardrails

- Do not print secret values from Render logs, env vars, databases, or service details.
- Do not modify environment variables without naming the exact service, key, and new value first.
- Do not use Render MCP as a replacement for git, CI checks, or DealDash's own MCP bridge.
- Do not promise that Render MCP can trigger deploys. Use git push or the Render dashboard for deploy triggers.
- If Render MCP cannot perform an operation, give the user one dashboard path or one command as the fallback.
