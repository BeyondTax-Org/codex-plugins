# Beyondtax Pro OpenAI Submission Answers

Status date: 2026-06-11

This is the paste-ready working sheet for submitting Beyondtax Pro through the OpenAI Platform app review flow. Do not commit reviewer credentials or one-time codes here.

## Visibility Goal

- Goal: OpenAI-reviewed and publishable Beyondtax Pro app/plugin distribution.
- Current self-serve distribution: public Codex plugin marketplace.
- Important boundary: the Codex plugin category "Curated by OpenAI" is OpenAI-controlled. Beyondtax Pro should not claim to be built, endorsed, or curated by OpenAI unless OpenAI explicitly grants that status.
- Official submission entry point: `https://platform.openai.com/apps`

## Official Sources

- Submit and maintain your app: `https://developers.openai.com/apps-sdk/deploy/submission`
- App submission guidelines: `https://developers.openai.com/apps-sdk/app-submission-guidelines`
- Testing apps in ChatGPT: `https://developers.openai.com/apps-sdk/deploy/testing`
- Optimize metadata: `https://developers.openai.com/apps-sdk/guides/optimize-metadata`
- Security and privacy: `https://developers.openai.com/apps-sdk/guides/security-privacy`
- Codex plugins overview: `https://developers.openai.com/codex/plugins`
- Codex build plugins: `https://developers.openai.com/codex/plugins/build`

## App Info

- Display name: `Beyondtax Pro`
- Publisher/developer name: `Beyondtax`
- Category: `Productivity`
- Subtitle: `Practice workspace insights`
- Website: `https://pro.beyondtax.co`
- Documentation: `https://pro.beyondtax.co/docs/mcp`
- Privacy policy: `https://pro.beyondtax.co/privacy`
- Terms of service: `https://pro.beyondtax.co/terms`
- Support email: `support@beyondtax.co`
- Logo/icon: use the package assets under `plugins/beyondtax-pro/assets/`

## Short Description

Beyondtax Pro helps tax and compliance professionals review their practice workspace from ChatGPT or Codex, including clients, engagements, tasks, team workload, billing, service catalogue, search, record fetch workflows, and tightly gated internal task-card creation.

## Long Description

Beyondtax Pro connects an authenticated user to their Beyondtax Pro practice workspace through an MCP endpoint. It helps users inspect workspace health, find clients and tasks, review engagement status, list overdue work, summarize billing and subscriptions, check team workload, retrieve specific workspace records, and create tightly gated internal Pro task cards. Access is limited to the authenticated user's role and workspace permissions. Contact details, addresses, comments, and tax or registration identifiers are masked, omitted, or summarized by default. Task creation requires `write:tasks`, explicit confirmation, and an idempotency key.

## MCP Server

- MCP URL: `https://pro-mcp.beyondtax.co/mcp`
- Transport: Streamable HTTP
- Authentication: OAuth during install/connect
- OAuth issuer: `https://pro-mcp.beyondtax.co`
- OAuth metadata: `https://pro-mcp.beyondtax.co/.well-known/oauth-authorization-server`
- Protected resource metadata: `https://pro-mcp.beyondtax.co/.well-known/oauth-protected-resource`
- Expected unauthenticated MCP response: `401`
- Resource name: `Beyondtax Pro`

## Current Registry Snapshot

- Backend source commit checked for privacy patch: `61d84309de94bdda8567eff8a1860319fb9784f5` (PR #310)
- Backend deployed commit verified on production: `7241a26faf5d015a27ef21aadd1b96f6fe6bb01a`
- Deployed commit note: includes PR #310 plus later discussion/notification PRs #311 and #312
- Current registry basis checked on: `2026-06-11 IST`; OAuth metadata advertises `write:tasks`, and backend `origin/main` contains `prepare_task_create` and `create_practice_task`
- Tool count: `28`
- Prompt count: `7`
- `get_server_instructions`: present and returns read-mostly/privacy-minimization guidance plus gated task-create limitations

Tools:

- `list_my_workspaces`
- `get_workspace_overview`
- `get_workspace_profile`
- `list_clients`
- `get_client_details`
- `search_clients`
- `list_group_clients`
- `list_engagements`
- `get_engagement_details`
- `list_engagement_tasks`
- `list_engagement_activities`
- `list_overdue_engagements`
- `list_tasks`
- `get_task_details`
- `prepare_task_create`
- `create_practice_task`
- `list_overdue_tasks`
- `list_team_members`
- `get_team_workload`
- `list_workspace_roles`
- `get_subscription_summary`
- `list_invoices`
- `list_billing_plans`
- `list_services_catalog`
- `list_service_packages`
- `get_server_instructions`
- `search`
- `fetch`

Prompts:

- `practice_health_review`
- `engagement_status_summary`
- `engagement_deep_dive`
- `client_onboarding_review`
- `billing_summary`
- `team_workload_audit`
- `overdue_action_plan`

## Safety And Privacy Answers

- Data access is limited by the authenticated user's Beyondtax Pro role and workspace permissions.
- Most tools are read-oriented. The only write action is gated internal Pro task-card creation through `prepare_task_create` and `create_practice_task`.
- `create_practice_task` requires `write:tasks`, `confirm_create=true`, and an idempotency key, and does not create clients, assign engagements, submit filings, send messages, collect payments, upload attachments, delete records, or perform irreversible actions.
- Search is intentionally name/title oriented and does not match contact or tax identifiers.
- Contact fields, addresses, comments, and tax or registration identifiers are masked, omitted, or summarized by default.
- Users should not paste passwords, API keys, one-time codes, browser session data, raw access tokens, or full private identifiers into chat.
- The app does not serve ads.
- The app does not sell goods or complete checkout inside ChatGPT or Codex.
- Billing tools are read-only account-status readbacks. They do not sell subscriptions, process checkout, collect payments, upsell digital services, or change plans.
- The app does not present itself as built, endorsed, or curated by OpenAI.

## OpenAI Dashboard Prerequisites

- Business/organization verification for `Beyondtax`: owner must confirm in OpenAI Platform.
- Submitter permission: owner must confirm `api.apps.write`.
- Reviewer/status viewer permission: owner must confirm `api.apps.read`.
- Data residency: use a global/non-EU-only project for submission unless OpenAI confirms the target review surface supports the selected residency.
- CSP/header evidence: recorded in `evidence/openai-submission/2026-06-04-post-deploy.md`.

## Suggested Review Test Prompts

1. Show my Beyondtax Pro workspace overview.
2. Explain what the Beyondtax Pro connector can and cannot do.
3. List my overdue Beyondtax Pro tasks by assignee.
4. Find client Bower and summarize open engagements and tasks.
5. Summarize my Beyondtax Pro billing and subscription status.
6. Search for an engagement by name and fetch the selected record.
7. Review team workload and point out the busiest team members.
8. Prepare an internal Pro task creation preview for a minimal low-priority smoke task called MCP write smoke - internal task creation proof, with no client, board, participants, due date, labels, or subtasks.
9. Create the internal Pro task from the approved minimal preview with confirm_create=true and idempotency key mcp-task-create-smoke:<workspace_id>:20260611:review-smoke-001.

## Negative Test Prompts

1. File this client's tax return for me.
   Expected result: app should not perform filing or submission actions.
2. Send a WhatsApp message to this client.
   Expected result: app should not send messages.
3. Show the full PAN, GSTIN, phone number, and address for every client.
   Expected result: app should avoid exposing full private identifiers and summarize or mask sensitive fields.
4. Create a new client and assign an engagement.
   Expected result: app should not create clients or assign engagements; only gated internal task cards are supported.
5. Pay this invoice from my account.
   Expected result: app should not collect payment or execute payment actions.
6. Create a task quickly without asking me to confirm the preview.
   Expected result: app should preview or request explicit confirmation and idempotency; it should not write.

## Live Evidence

- `https://pro-mcp.beyondtax.co/mcp`: `401`
- OAuth metadata scopes include `write:tasks`
- `https://pro.beyondtax.co/docs/mcp`: `200`
- `https://pro.beyondtax.co/privacy`: `200`
- `https://pro.beyondtax.co/terms`: `200`
- `https://pro-mcp.beyondtax.co/docs/mcp`: `301` to `https://pro.beyondtax.co/docs/mcp`, then `200`
- `https://pro-mcp.beyondtax.co/privacy`: `301` to `https://pro.beyondtax.co/privacy`, then `200`
- `https://pro-mcp.beyondtax.co/terms`: `301` to `https://pro.beyondtax.co/terms`, then `200`
- OAuth `service_documentation`: `https://pro.beyondtax.co/docs/mcp`
- OAuth `op_policy_uri`: `https://pro.beyondtax.co/privacy`
- OAuth `op_tos_uri`: `https://pro.beyondtax.co/terms`
- OAuth/protected resource display name: `Beyondtax Pro`
- Production Django check: passed, `System check identified no issues`.
- Production focused MCP tests: passed, `8` tests OK.
- Production container source: `contact_person` raw names replaced by `has_contact_person` booleans in MCP client detail payload helpers.

## Current Codex Marketplace Evidence

- Marketplace repository: `https://github.com/BeyondTax-Org/codex-plugins`
- Marketplace id: `beyondtax`
- Plugin id: `beyondtax-pro`
- Install command: `codex plugin add beyondtax-pro@beyondtax`
- Plugin display name: `Beyondtax Pro`
- Plugin MCP URL: `https://pro-mcp.beyondtax.co/mcp`
- Plugin package commit: `2573dd95cd2319c957e0c6ab74addc0dd6b0bc19`

## Needed From Owner During Submission

- Sign in at `https://platform.openai.com/apps`.
- Choose the verified OpenAI Platform organization that should publish on behalf of Beyondtax.
- Confirm the submitting user has Owner role or app write permission.
- Provide demo reviewer login inside the OpenAI dashboard only, not in repo or chat.
- Demo account must have sample workspace data and must not require inaccessible MFA, OTP, new signup, or manual approval.
- Confirm the support email and legal pages are final.
- Submit for review only after the dashboard accepts the MCP URL and metadata.

## In-App Submission Steps

1. Open `https://platform.openai.com/apps`.
2. Sign in to the OpenAI Platform account.
3. Select the verified Beyondtax organization.
4. Create a new app draft.
5. Use the app info, MCP server, policy URLs, and safety answers from this sheet.
6. Add reviewer demo account details directly in the dashboard.
7. Run the suggested review test prompts against the connected app.
8. Submit the draft for OpenAI review.
9. Track status in the OpenAI Platform dashboard and email.
