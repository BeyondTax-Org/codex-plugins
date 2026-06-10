# Beyondtax Pro Codex Plugin Public Review Packet

## Public Package

- Marketplace repository: `https://github.com/BeyondTax-Org/codex-plugins`
- Marketplace id: `beyondtax`
- Plugin id: `beyondtax-pro`
- Display name: `Beyondtax Pro`
- MCP endpoint: `https://pro-mcp.beyondtax.co/mcp`
- Install command: `codex plugin add beyondtax-pro@beyondtax`

## Canonical Public URLs

- Documentation: `https://pro.beyondtax.co/docs/mcp`
- Privacy Policy: `https://pro.beyondtax.co/privacy`
- Terms of Service: `https://pro.beyondtax.co/terms`
- MCP endpoint: `https://pro-mcp.beyondtax.co/mcp`

## Access And Safety

- Authentication: OAuth during install.
- Tool posture: read-mostly with one gated internal Pro task-card creation lane.
- Data scope: limited to records the authenticated Beyondtax Pro user can access.
- Sensitive fields: structured contact fields, addresses, comments, and tax or registration identifiers are masked, omitted, or summarized by default.
- Discovery search: intentionally name/title oriented; it does not match contact or tax identifiers.
- Write actions: limited to internal Pro task-card creation through `prepare_task_create` and `create_practice_task`; `create_practice_task` requires `write:tasks`, `confirm_create=true`, and an idempotency key. Client creation, engagement assignment, edits, filings, payments, outbound messages, attachment upload, and deletes are not promised or available.

## Verified Checks

- Public marketplace install succeeds from a clean temporary Codex profile.
- Plugin metadata shows `Beyondtax Pro`.
- Icon and logo assets are present in the installed package.
- `.mcp.json` uses `https://pro-mcp.beyondtax.co/mcp`.
- `/mcp` is live and auth-gated.
- OAuth metadata uses the canonical Pro documentation, privacy, and terms URLs.
- `https://pro-mcp.beyondtax.co/docs/mcp`, `/privacy`, and `/terms` redirect to canonical Pro UI pages.

## Visibility Boundary

The public marketplace package lets users install Beyondtax Pro by adding this repository as a marketplace. Built-in or curated OpenAI plugin-directory visibility is separate from this package and depends on OpenAI review, rollout, plan, workspace settings, feature access, and admin controls.
