# Beyondtax Pro MCP Task Write Pilot Runbook

Status date: 2026-06-12

## Goal

Use the Pro MCP write lanes for safe internal task-card creation or exact task-card soft-delete pilots, then verify exact readback.

## Allowed Write

- Tool: `create_practice_task`
- Required preview: `prepare_task_create`
- Required OAuth scope: `write:tasks`
- Required confirmation: `confirm_create=true`
- Required idempotency: unique `idempotency_key`

## Allowed Soft-Delete

- Tool: `delete_practice_task`
- Required preview: `prepare_task_delete`
- Required OAuth scope: `write:tasks`
- Required confirmation: `confirm_delete=true`
- Required idempotency: unique `idempotency_key`
- Effect: soft-delete one exact internal Pro task card only (`is_active=false`)

## Hard Stops

- Stop if `write:tasks` is not present in OAuth metadata or the granted token.
- Stop if `prepare_task_create` returns validation errors.
- Stop if `prepare_task_delete` returns validation errors.
- Stop if the preview does not exactly match the intended task create/delete action.
- Stop if the user has not approved the exact preview.
- Stop for filings, payments, billing changes, hard deletes, outbound messages, attachment upload, existing task edits beyond the approved task soft-delete lane, client creation, or engagement assignment.

## First Pilot Payload Shape

Use a clearly internal smoke task. Keep the first pilot minimal: no client, board, owner, reviewer, assignees, watchers, due date, labels, or subtasks.

```json
{
  "workspace_id": "<NUMERIC_WORKSPACE_ID_FROM_list_my_workspaces>",
  "title": "MCP write smoke - internal task creation proof",
  "description": "Readback-only smoke test for Beyondtax Pro MCP task creation. No client work, filing, payment, invoice, external portal action, or client message is authorized.",
  "status": "todo",
  "priority": "low",
  "task_type": "task",
  "custom_fields": {
    "pilot": "mcp_task_create_smoke",
    "pilot_date": "2026-06-11",
    "stop_rules": "readback_only_no_external_action"
  },
  "idempotency_key": "mcp-task-create-smoke:<workspace_id>:20260611:<short_run_id>"
}
```

Use a concrete numeric `workspace_id` from `list_my_workspaces`. Stop if the workspace is ambiguous. Add owner, assignee, watcher, board, client, due date, labels, or subtasks only in a later pilot after this minimal write is proven.

## Verification

After `create_practice_task`, immediately read back:

- Task id and title
- Workspace and client, if any
- Owner, assignee, reviewer, and watchers
- Status, priority, due date, labels, and subtasks
- Activity/source metadata showing MCP creation
- Idempotency behavior by retrying the same key only if the first response is unclear

After `delete_practice_task`, immediately verify:

- Exact task id/public id and title from the preview
- Returned readback has `is_active=false`
- The exact task no longer appears in active task search/list results
- Activity/source metadata shows MCP soft-delete
- Idempotency behavior by retrying the same key only if the first response is unclear
