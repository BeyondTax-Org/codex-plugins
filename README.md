# Beyondtax Codex And Claude Plugins

Public Codex plugin marketplace for Beyondtax integrations, with a local Claude Code marketplace wrapper for the same Beyondtax Pro MCP connector.

## Install Beyondtax Pro

This marketplace exposes the `beyondtax-pro` plugin. It connects Codex to the public Beyondtax Pro MCP endpoint:

`https://pro-mcp.beyondtax.co/mcp`

Marketplace repository:

`https://github.com/BeyondTax-Org/codex-plugins`

Plugin display name:

`Beyondtax Pro`

### Codex CLI install

Add the marketplace:

```powershell
codex plugin marketplace add https://github.com/BeyondTax-Org/codex-plugins
```

Install the plugin:

```powershell
codex plugin add beyondtax-pro@beyondtax
```

Confirm it is enabled:

```powershell
codex plugin list
codex mcp get beyondtax-pro
```

The plugin uses OAuth. Most tools are read-only; task writes are limited to guarded internal Pro task-card creation through `prepare_task_create` and `create_practice_task`, and guarded task-card soft-delete through `prepare_task_delete` and `delete_practice_task`. Writes require `write:tasks`, exact preview, explicit confirmation, and an idempotency key. During install, Codex should ask the user to complete the Beyondtax Pro OAuth login flow. If the plugin does not appear after adding the marketplace, refresh or restart Codex and check the plugin picker again.

### Claude Code local install

This repo also includes a Claude Code marketplace manifest at:

`.claude-plugin/marketplace.json`

Add the local marketplace:

```powershell
claude plugin marketplace add D:\BeyondTax\Beyondtax_Pro\04_Repos\codex-plugins
```

Install the plugin:

```powershell
claude plugin install beyondtax-pro@beyondtax-local
```

Confirm it is enabled and visible to Claude:

```powershell
claude plugin list
claude plugin details beyondtax-pro@beyondtax-local
claude mcp list
```

Expected pre-OAuth MCP health:

```text
plugin:beyondtax-pro:beyondtax-pro: https://pro-mcp.beyondtax.co/mcp (HTTP) - ! Needs authentication
```

After OAuth is completed inside Claude Code, the same endpoint should expose the Beyondtax Pro MCP tools, including task-board lookup, guarded task create/delete previews, confirmed task-card create/delete with idempotency, object links, and inactive task readback through `include_inactive=true`.

## Visibility Boundary

This repository makes Beyondtax Pro installable from a public Codex plugin marketplace. Built-in or curated OpenAI plugin-directory visibility is a separate OpenAI review and rollout path, and can depend on the user's plan, workspace settings, feature access, rollout status, and admin controls.

## Marketplace

Codex marketplace file:

`.agents/plugins/marketplace.json`

Claude local marketplace file:

`.claude-plugin/marketplace.json`

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
- The Pro MCP registry includes `prepare_task_create`, `create_practice_task`, `prepare_task_delete`, and `delete_practice_task` only when `write:tasks` is advertised and approved.
- The marketplace policy keeps `authentication` as `ON_INSTALL`.

## Verified Public Install

Clean-profile metadata install was verified on 2026-06-04 using a temporary Codex profile:

- Marketplace added as `beyondtax`.
- Plugin installed as `beyondtax-pro@beyondtax`.
- Display name: `Beyondtax Pro`.
- Endpoint: `https://pro-mcp.beyondtax.co/mcp`.
- OAuth was not completed during this metadata-only verification.
