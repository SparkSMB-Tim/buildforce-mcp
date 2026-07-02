# Buildforce — Agentic Ops MCP

**Turn your AI assistant into your Salesforce / HubSpot / ServiceNow operations team.**

Buildforce is a hosted (remote) MCP server that connects Claude, ChatGPT, Gemini, and Copilot to the back-end of your SaaS platforms — so your AI can run health checks, quantify configuration debt in dollars, assess deployment safety, and ship approved changes with sandbox-first guardrails.

- **Endpoint:** `https://mcp.buildforce.io/mcp` (Streamable HTTP)
- **Auth:** OAuth 2.1 + PKCE ([authorization server metadata](https://mcp.buildforce.io/.well-known/oauth-authorization-server))
- **Registry:** [`io.buildforce/agentic-ops`](https://registry.modelcontextprotocol.io/v0/servers?search=buildforce) on the official MCP registry
- **Website:** [buildforce.io/mcp](https://www.buildforce.io/mcp) · **Docs:** [buildforce.io/docs/mcp](https://www.buildforce.io/docs/mcp) · **Privacy:** [buildforce.io/privacy](https://www.buildforce.io/privacy) · **Terms:** [buildforce.io/terms](https://www.buildforce.io/terms)

## Install (60 seconds)

### Claude (claude.ai / Claude Desktop / Claude Code)
Settings → Connectors → **Add custom connector** → paste:

```
https://mcp.buildforce.io/mcp
```

Sign in (or create a free account) when the OAuth screen appears, then ask:

> "Run a Buildforce health check on our Salesforce org."

### Claude Code (CLI)

```bash
claude mcp add --transport http buildforce https://mcp.buildforce.io/mcp
```

### ChatGPT (Developer Mode / Apps)
Settings → Connectors → **Add connector** → `https://mcp.buildforce.io/mcp` (OAuth, supports `offline_access` refresh tokens).

### Gemini CLI

Install as an extension (bundles the consultant context + OAuth config):

```bash
gemini extensions install https://github.com/SparkSMB-Tim/buildforce-mcp
```

Or add the raw MCP server:

```bash
gemini mcp add buildforce https://mcp.buildforce.io/mcp --transport http
```

## What it does

~70 tools, capability-gated per organization — a connected account only sees tools for the platforms it actually has:

| Capability | Examples |
|---|---|
| **Health checks** (always on) | 200+ checks across security, data quality, automation, adoption, cost; dollar-quantified tech-debt impact; trend prediction; anomaly detection |
| **Salesforce** | SOQL, metadata, Apex deploy/tests, permission sets, validation rules, sandboxes, Data Cloud (segments, identity resolution, calculated insights), Agentforce agents/topics/actions, OmniStudio |
| **Deployment & CI/CD** | Environment comparison, deployment preview/validate/execute/rollback, automated pipelines, test orchestration |
| **ServiceNow** | Instance operations and health |
| **HubSpot** | CRM operations and health |

### Safety model

- Read tools are annotated `readOnlyHint`; write tools carry `destructiveHint`.
- Writes route **sandbox-first** with explicit production confirmation.
- OAuth-scoped to your org membership — the server enforces row-level security; no service-role access from the connector.

## Pricing

Free to start — connect an org and run assessments at no cost. Pay per outcome with credit packs, subscribe to a monthly Connector plan, or go fully managed. See [buildforce.io/pricing](https://www.buildforce.io/pricing).

## About this repository

This repo hosts the public MCP manifest ([`server.json`](./server.json)) and documentation for the hosted Buildforce connector. The server itself runs on Cloudflare Workers at `mcp.buildforce.io`.

© Buildforce · [buildforce.io](https://www.buildforce.io)
