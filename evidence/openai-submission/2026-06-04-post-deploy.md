# Beyondtax Pro OpenAI Submission Post-Deploy Evidence

Date: 2026-06-04

## Deployment Evidence

- Production host commit: `7241a26faf5d015a27ef21aadd1b96f6fe6bb01a`
- Production host `origin/main`: `7241a26faf5d015a27ef21aadd1b96f6fe6bb01a`
- PR #310 privacy patch included: yes
- Later commits also included in deployed main: PR #311 and PR #312 discussion/notification hardening
- Production containers running: web, celery, celery-beat, db, nginx, redis
- Production Django system check: passed
- Production focused MCP tests: `8` tests passed

## Live URL Evidence

- `https://pro-mcp.beyondtax.co/mcp`: `401`
- `https://pro.beyondtax.co/docs/mcp`: `200`
- `https://pro.beyondtax.co/privacy`: `200`
- `https://pro.beyondtax.co/terms`: `200`
- `https://pro-mcp.beyondtax.co/docs/mcp`: `301` to canonical Pro docs, then `200`
- `https://pro-mcp.beyondtax.co/privacy`: `301` to canonical Pro privacy, then `200`
- `https://pro-mcp.beyondtax.co/terms`: `301` to canonical Pro terms, then `200`
- `https://pro-mcp.beyondtax.co/admin/`: `302` to admin login
- `https://pro-mcp.beyondtax.co/accounts/api/session/`: `401`, not `5xx`

## OAuth Metadata Evidence

- Issuer: `https://pro-mcp.beyondtax.co`
- Service documentation: `https://pro.beyondtax.co/docs/mcp`
- Policy URI: `https://pro.beyondtax.co/privacy`
- Terms URI: `https://pro.beyondtax.co/terms`
- Logo URI: `https://pro-mcp.beyondtax.co/logo.png`
- Resource name: `Beyondtax Pro`
- Scopes: `read:workspace`, `read:clients`, `read:engagements`, `read:tasks`, `read:billing`, `read:team`, `read:search`

## Live MCP Registry Evidence

- Tool count: `26`
- Prompt count: `7`
- `get_server_instructions`: present
- Detailed registry snapshot: `OPENAI_APP_DIRECTORY_REGISTRY_SNAPSHOT_20260604.md`

## Privacy Evidence

- Client list responses expose `has_email` and `has_phone_number` flags instead of raw email/phone.
- Workspace profile and client profile identifiers are masked or summarized.
- Client search and universal search descriptors are name/city/title oriented.
- PR #310 removed raw `contact_person` fields from business/group client detail payload helpers and replaced them with `has_contact_person` booleans.

## CSP And Headers

- HTTPS responses include HSTS, `X-Content-Type-Options: nosniff`, and `Referrer-Policy`.
- MCP endpoint is auth-gated and returns `401` without exposing workspace data.
- No public widget domain is used by the current tool-only public package.

## Demo Account Evidence

Do not write reviewer credentials in this repository. Owner must provide them directly inside the OpenAI Platform dashboard.

Required reviewer-account assertions before final submit:

- Demo workspace contains sample clients, engagements, tasks, billing, services, and team records.
- Demo account does not require inaccessible MFA, OTP, manual signup approval, or internal human approval during review.
- Demo data does not contain real production client secrets or unnecessary private identifiers.
- Demo credential expiry and rotation owner are defined.

## Screenshot Inventory

- Current plugin package has icon and logo assets.
- If OpenAI dashboard asks for screenshots, use public docs screenshots and/or sanitized demo-workspace screenshots only.
- Do not upload screenshots containing real client identifiers, raw tax identifiers, private addresses, or private contact information.

