---
name: beyondtax-pro-connector
description: Use when the user asks to work with Beyondtax Pro via the Pro MCP connector, including Pro clients, engagements, tasks, team workload, billing, service catalogue, workspace overview, search, fetch, or the pro-mcp.beyondtax.co endpoint.
---

# Beyondtax Pro Connector

Use this plugin for Beyondtax Pro operational work through the MCP endpoint:

`https://pro-mcp.beyondtax.co/mcp`

Default to read-only actions. Keep Pro separate from Business and Wealth lanes.

Use the MCP tools directly when available. Expected read workflows include workspace overview, client lookup, engagement review, task listing, team workload review, billing review, service catalogue review, search, and fetch.

Do not print secrets, tokens, cookies, full private identifiers, or internal proof references. If OAuth login is needed, ask the user to complete the browser login flow rather than requesting credentials in chat.
