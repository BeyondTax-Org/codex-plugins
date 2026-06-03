# Beyondtax Codex Plugins

Public Codex plugin marketplace for Beyondtax integrations.

## Install Beyondtax Pro

This marketplace exposes the `beyondtax-pro` plugin. It connects Codex to the public Beyondtax Pro MCP endpoint:

`https://pro-mcp.beyondtax.co/mcp`

The plugin is read-oriented and uses OAuth. On first use, Codex may ask the user to complete the Beyondtax Pro OAuth login flow.

## Marketplace

Marketplace file:

`.agents/plugins/marketplace.json`

Plugin package:

`plugins/beyondtax-pro`

## Public Readiness

Before describing the plugin as publicly ready, verify:

- `https://pro-mcp.beyondtax.co/mcp` is live and auth-gated.
- `https://pro.beyondtax.co/docs/mcp` returns 200 and renders the MCP documentation route.
- `https://pro.beyondtax.co/privacy` returns 200.
- `https://pro.beyondtax.co/terms` returns 200.
- `https://pro-mcp.beyondtax.co/docs/mcp`, `/privacy`, and `/terms` redirect to the canonical Pro pages.
- The Pro MCP registry includes `get_server_instructions`.
