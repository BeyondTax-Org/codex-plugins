---
name: beyondtax-pro-connector
description: Use when the user asks to work with Beyondtax Pro via the Pro MCP connector, including Pro clients, engagements, tasks, team workload, billing, service catalogue, workspace overview, search, fetch, or the pro-mcp.beyondtax.co endpoint.
---

# Beyondtax Pro Connector

Use this plugin for Beyondtax Pro read-only workspace assistance through:

`https://pro-mcp.beyondtax.co/mcp`

Keep Pro separate from Business and Wealth lanes. Do not promise or perform write actions such as creating clients, editing tasks, submitting filings, sending messages, collecting payments, or deleting records.

## Public Read Workflows

Use the MCP tools directly when available. Good first actions are:

- Workspace overview and account context.
- Client lookup, client summaries, and onboarding status review.
- Engagement status, phase progress, due dates, and ownership review.
- Task lists, overdue work, assignee workload, and priority summaries.
- Billing, subscription, invoices, services, packages, and service catalogue reference.
- Search and fetch for workspace records when the user asks for a specific client, task, engagement, service, or billing item.

## Safety Defaults

- Treat all connector access as read-only unless a future public review explicitly approves writes.
- Ask the user to complete OAuth in the browser when authentication is required.
- Never ask for or print login secrets, one-time codes, browser session data, raw access material, or full private identifiers.
- Summarize sensitive records with enough context to be useful, but mask private identifiers unless the user explicitly needs an exact operational reference.
- If a result depends on workspace permissions, say that access is limited by the user's Beyondtax Pro role and enabled workspace features.

## Response Shape

For broad questions, answer with source, total/counts, grouped findings, and caveats. For searches, show the closest matches and ask the user which record to inspect only when multiple records are genuinely ambiguous.
