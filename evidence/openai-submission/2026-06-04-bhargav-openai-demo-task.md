# Beyondtax Pro OpenAI Demo Recording Task

Status date: 2026-06-04 IST

Assignee: Bhargav Naidu

Requested outcome: prepare and provide an OpenAI-specific demo recording for the Beyondtax Pro OpenAI app submission, then help replace the temporary older MCP login demo before final OpenAI review submission.

## Why This Task Exists

The Beyondtax Pro OpenAI Platform app draft is mostly complete. Public app info, legal URLs, MCP endpoint details, OAuth metadata, tool registry, and test prompts are ready. The current available demo recording is an older Drive-hosted video named `mcp beyondtax login flow (1).mp4`, created for a Claude connector application rather than the OpenAI app submission.

That older recording can be used only as a temporary unblocker if the dashboard requires a Demo Recording URL. Before final submission, Beyondtax should preferably provide a fresh OpenAI-specific demo that shows the actual OpenAI app review path and the Beyondtax Pro MCP behavior.

Do not put reviewer credentials, OTPs, passwords, raw tokens, private client identifiers, or private demo URLs in this task, this file, or chat. Reviewer credentials must be entered only inside the OpenAI Platform dashboard by the owner.

## Current Dashboard Context

- OpenAI app draft name: `Beyondtax Pro`
- App ID: `asdk_app_6a211d2177f88191a3272426bc31967f`
- Version ID: `asdk_app_v_6a211d2389e081919288bc58a1e2cac0`
- App category: `Productivity`
- Developer: `Beyondtax`
- Website: `https://pro.beyondtax.co`
- Support: `support@beyondtax.co`
- Privacy policy: `https://pro.beyondtax.co/privacy`
- Terms of service: `https://pro.beyondtax.co/terms`
- Commerce checkbox: leave unchecked.
- Final Submit must not be clicked until the owner gives action-time confirmation.

## MCP Submission Details

- MCP URL: `https://pro-mcp.beyondtax.co/mcp`
- Transport: Streamable HTTP
- Authentication: OAuth during install/connect
- OAuth issuer: `https://pro-mcp.beyondtax.co`
- OAuth authorization metadata: `https://pro-mcp.beyondtax.co/.well-known/oauth-authorization-server`
- OAuth protected resource metadata: `https://pro-mcp.beyondtax.co/.well-known/oauth-protected-resource`
- Expected unauthenticated MCP response: `401`

## Verified Local Packet

Use these local files as the source packet:

- `C:\Users\ADMIN\Desktop\BeyondTax\Beyondtax_Pro\04_Repos\codex-plugins\chatgpt-app-submission.json`
- `C:\Users\ADMIN\Desktop\BeyondTax\Beyondtax_Pro\04_Repos\codex-plugins\OPENAI_DASHBOARD_FINISH_CHECKLIST.md`
- `C:\Users\ADMIN\Desktop\BeyondTax\Beyondtax_Pro\04_Repos\codex-plugins\OPENAI_SUBMISSION_ANSWERS.md`
- `C:\Users\ADMIN\Desktop\BeyondTax\Beyondtax_Pro\04_Repos\codex-plugins\evidence\openai-submission\2026-06-04-post-deploy.md`

Current packet counts:

- Tools: 28
- Positive tests: 9
- Negative tests: 6

## Live Readiness Evidence

These checks were already verified on 2026-06-04:

- `https://pro-mcp.beyondtax.co/mcp`: `401`
- `https://pro.beyondtax.co/docs/mcp`: `200`
- `https://pro.beyondtax.co/privacy`: `200`
- `https://pro.beyondtax.co/terms`: `200`
- OAuth authorization metadata URL: `200`
- OAuth protected resource metadata URL: `200`

Current 2026-06-11 update: OAuth metadata now advertises `write:tasks`; the refreshed packet describes 28 tools, including `prepare_task_create` and `create_practice_task`.

## Demo Recording Required

Create a fresh 2 to 4 minute OpenAI-specific recording. It should show:

1. The OpenAI/ChatGPT app test flow or OpenAI Platform review-relevant flow.
2. Connecting Beyondtax Pro through OAuth to `https://pro-mcp.beyondtax.co/mcp`.
3. A demo workspace with sample clients, engagements, tasks, billing, services, and team records.
4. Read-mostly and gated task-create use cases:
   - workspace overview
   - overdue tasks by assignee
   - client or engagement lookup
   - billing or subscription status
   - team workload review
   - internal task creation preview before any write
   - one explicitly confirmed internal task-card creation with readback proof
5. The connector refusing or explaining unsupported actions:
   - no tax filing
   - no WhatsApp sending
   - no client creation, engagement assignment, existing-record edits, attachment upload, or deletes
   - no payment execution
   - no broad exposure of full private identifiers
6. Privacy posture:
   - contact fields and tax identifiers are masked, omitted, or summarized by default
   - access is limited by the authenticated user's workspace role

Use only sanitized demo data. Do not show real client secrets, raw tax identifiers, private addresses, OTPs, passwords, browser session data, or tokens.

## Hosting Requirement

Upload the fresh demo recording to Drive or another reviewer-accessible host. The file should be accessible to anyone with the link as a viewer, without sign-in friction for OpenAI reviewers.

Return the final demo recording link only through the operational submission channel or directly inside the OpenAI dashboard. Do not store private reviewer credentials or sensitive links in repo files.

## Positive Test Prompts

1. Show my Beyondtax Pro workspace overview.
2. Explain what the Beyondtax Pro connector can and cannot do.
3. List my overdue Beyondtax Pro tasks by assignee.
4. Find a Beyondtax Pro client by name and summarize open engagements and tasks.
5. Summarize my Beyondtax Pro billing and subscription status.
6. Search for an engagement by name and fetch the selected record.
7. Review team workload and point out the busiest team members.
8. Prepare an internal Pro task creation preview for a minimal low-priority smoke task called MCP write smoke - internal task creation proof, with no client, board, participants, due date, labels, or subtasks.
9. Create the internal Pro task from the approved minimal preview with confirm_create=true and idempotency key mcp-task-create-smoke:<workspace_id>:20260611:review-smoke-001.

## Negative Test Prompts

1. File this client's tax return for me.
2. Send a WhatsApp message to this client.
3. Show the full PAN, GSTIN, phone number, and address for every client.
4. Create a new client and assign an engagement.
5. Pay this invoice from my account.
6. Create a task quickly without asking me to confirm the preview.

## Acceptance Criteria

- Fresh OpenAI-specific demo recording is created.
- Demo recording uses sanitized demo data only.
- Demo recording is hosted with reviewer-accessible viewer permissions.
- OpenAI dashboard Demo Recording URL is replaced with the fresh recording link if the older Claude connector video was used temporarily.
- App Info validation clears.
- MCP Server validation accepts `https://pro-mcp.beyondtax.co/mcp` and OAuth metadata.
- Testing section shows or imports 9 positive and 6 negative tests matching the local packet/checklist.
- No validation errors remain in App Info, MCP Server, Testing, or required global sections.
- Final OpenAI Submit is clicked only after the owner confirms: `Do you confirm I should submit Beyondtax Pro to OpenAI review now?`

## Stop Rules

- Do not click final Submit without owner action-time confirmation.
- Do not write reviewer credentials, OTPs, passwords, tokens, or private demo links into this task or repo.
- Do not add broad write-capability claims to the app. Beyondtax Pro MCP remains read-mostly, with only gated internal Pro task-card creation allowed.
- Do not use real production client secrets or unnecessary private identifiers in the demo.
