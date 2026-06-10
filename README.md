# Beyondtax Codex Plugins

Public Codex plugin marketplace for Beyondtax integrations.

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

The plugin uses OAuth. Most tools are read-only; the only write lane is guarded internal Pro task-card creation through `prepare_task_create` and `create_practice_task`, requiring `write:tasks`, `confirm_create=true`, and an idempotency key. During install, Codex should ask the user to complete the Beyondtax Pro OAuth login flow. If the plugin does not appear after adding the marketplace, refresh or restart Codex and check the plugin picker again.

## Visibility Boundary

This repository makes Beyondtax Pro installable from a public Codex plugin marketplace. Built-in or curated OpenAI plugin-directory visibility is a separate OpenAI review and rollout path, and can depend on the user's plan, workspace settings, feature access, rollout status, and admin controls.

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
- The Pro MCP registry includes `prepare_task_create` and `create_practice_task` only when `write:tasks` is advertised and approved.
- The marketplace policy keeps `authentication` as `ON_INSTALL`.

## Verified Public Install

Clean-profile metadata install was verified on 2026-06-04 using a temporary Codex profile:

- Marketplace added as `beyondtax`.
- Plugin installed as `beyondtax-pro@beyondtax`.
- Display name: `Beyondtax Pro`.
- Endpoint: `https://pro-mcp.beyondtax.co/mcp`.
- OAuth was not completed during this metadata-only verification.
