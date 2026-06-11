---
name: beyondtax-pro-connector
description: Use when the user asks to work with Beyondtax Pro via the Pro MCP connector, including Pro clients, engagements, tasks, gated task creation, team workload, billing, service catalogue, workspace overview, search, fetch, or the pro-mcp.beyondtax.co endpoint.
---

# Beyondtax Pro Connector

Use this plugin for Beyondtax Pro workspace assistance through:

`https://pro-mcp.beyondtax.co/mcp`

Keep Pro separate from Business and Wealth lanes. Most access is read-only. The only approved write lanes are internal Pro task-card creation through `prepare_task_create` and `create_practice_task`, and internal Pro task-card soft-delete through `prepare_task_delete` and `delete_practice_task`. Writes must require `write:tasks`, exact preview, explicit confirmation, and an idempotency key. Do not promise or perform other write actions such as creating clients, editing existing tasks, submitting filings, sending messages, collecting payments, uploading attachments, hard-deleting records, or deleting anything outside task cards.

## Public Read Workflows

Use the MCP tools directly when available. Good first actions are:

- Workspace overview and account context.
- Client lookup, client summaries, and onboarding status review.
- Engagement status, phase progress, due dates, and ownership review.
- Task lists, overdue work, assignee workload, and priority summaries.
- Billing, subscription, invoices, services, packages, and service catalogue reference.
- Search and fetch for workspace records when the user asks for a specific client, task, engagement, service, or billing item.

## Gated Task Write Workflow

Use task creation only for low-risk internal Pro follow-up cards.

- First call `prepare_task_create` to validate and preview the exact task payload.
- Check workspace, client, owner, assignee, reviewer, watcher, board, status, priority, due date, labels, and subtasks before writing.
- Only call `create_practice_task` after the preview matches the user's intent.
- `create_practice_task` must include `confirm_create=true` and a unique idempotency key.
- Immediately read back the task with `get_task_details` or task search and report the created task id, title, assignee/owner, watchers, subtasks, and activity/source proof.

Use task delete only for exact internal Pro task-card cleanup.

- First call `prepare_task_delete` to validate and preview the exact task id, title, board, status, client, participants, and counts.
- Confirm the preview matches the user's intended card before deleting.
- Only call `delete_practice_task` after explicit user approval.
- `delete_practice_task` must include `confirm_delete=true` and a unique idempotency key.
- Treat the result as a soft-delete only; immediately read back or search to verify the exact task is no longer active.

## Safety Defaults

- Treat all connector access as read-only except the gated internal Pro task-card creation and task-card soft-delete lanes.
- Stop before any task write if the OAuth token lacks `write:tasks`, the user did not explicitly approve the exact preview, or the idempotency key is missing.
- Ask the user to complete OAuth in the browser when authentication is required.
- Never ask for or print login secrets, one-time codes, browser session data, raw access material, or full private identifiers.
- Summarize sensitive records with enough context to be useful, but mask private identifiers unless the user explicitly needs an exact operational reference.
- If a result depends on workspace permissions, say that access is limited by the user's Beyondtax Pro role and enabled workspace features.

## Response Shape

For broad questions, answer with source, total/counts, grouped findings, and caveats. For searches, show the closest matches and ask the user which record to inspect only when multiple records are genuinely ambiguous.
