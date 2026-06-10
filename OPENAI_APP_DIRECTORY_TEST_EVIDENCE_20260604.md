# Beyondtax Pro Test Evidence

Evidence date: 2026-06-04

## Production Checks

- Backend deployed commit verified: `7241a26faf5d015a27ef21aadd1b96f6fe6bb01a`
- Production container source includes PR #310 privacy patch:
  - business/group client detail payloads use `has_contact_person`
  - raw `contact_person` serializer fields are removed for those profiles
- Production Django system check: passed
- Production focused MCP test suite: passed, `8` tests OK
- Containers checked: web, celery, celery-beat, db, nginx, redis were running
- Public `/admin/`: `302` to login
- Public `/accounts/api/session/`: `401`, not `5xx`

## Public URL Checks

- `https://pro-mcp.beyondtax.co/mcp`: `401`
- `https://pro.beyondtax.co/docs/mcp`: `200`
- `https://pro.beyondtax.co/privacy`: `200`
- `https://pro.beyondtax.co/terms`: `200`
- `https://pro-mcp.beyondtax.co/docs/mcp`: `301` to `https://pro.beyondtax.co/docs/mcp`
- `https://pro-mcp.beyondtax.co/privacy`: `301` to `https://pro.beyondtax.co/privacy`
- `https://pro-mcp.beyondtax.co/terms`: `301` to `https://pro.beyondtax.co/terms`
- OAuth metadata points to canonical docs/privacy/terms URLs
- Protected resource metadata `resource_name`: `Beyondtax Pro`

## Review Prompt Matrix

| Prompt | Expected tools | Expected response shape | Status |
| --- | --- | --- | --- |
| Show my Beyondtax Pro workspace overview. | `get_workspace_overview` | Counts for clients, engagements, tasks, and team members. | Ready for reviewer test |
| Explain what the Beyondtax Pro connector can and cannot do. | `get_server_instructions` | Read-mostly scope, privacy minimization, gated task creation limits, no filing/payment/messaging claims. | Ready for reviewer test |
| List my overdue Beyondtax Pro tasks by assignee. | `list_overdue_tasks`, optionally `get_team_workload` | Grouped overdue task summary with assignee context. | Ready for reviewer test |
| Find client Bower and summarize open engagements and tasks. | `search`, then `fetch`/detail tools for selected records | Matching client/engagement/task records and a read-only summary. | Ready for reviewer test |
| Summarize my Beyondtax Pro billing and subscription status. | `get_subscription_summary`, optionally `list_invoices` | Read-only billing status, no checkout or plan-change action. | Ready for reviewer test |
| Search for an engagement by name and fetch the selected record. | `search`, `fetch` | Selected record details with a canonical Pro URL. | Ready for reviewer test |
| Review team workload and point out the busiest team members. | `get_team_workload` | Busiest members by open engagements and assigned tasks. | Ready for reviewer test |
| Prepare an internal Pro task creation preview for a minimal low-priority smoke task called MCP write smoke - internal task creation proof, with no client, board, participants, due date, labels, or subtasks. | `prepare_task_create` | Validation and preview only; no task is created. | Ready for reviewer test |
| Create the internal Pro task from the approved minimal preview with confirm_create=true and idempotency key mcp-task-create-smoke:<workspace_id>:20260611:review-smoke-001. | `create_practice_task`, then `get_task_details` | One internal task card is created and read back with task id, status, priority, empty participant/client fields, and source/idempotency proof. | Ready for reviewer test |

## Negative Prompt Matrix

| Prompt | Expected result |
| --- | --- |
| File this client's tax return for me. | App should not file or submit anything. |
| Send a WhatsApp message to this client. | App should not send messages. |
| Show the full PAN, GSTIN, phone number, and address for every client. | App should avoid exposing full private identifiers and should summarize or mask sensitive fields. |
| Create a new client and assign an engagement. | App should not create clients or assign engagements; only gated internal task cards are supported. |
| Pay this invoice from my account. | App should not collect or execute payments. |
| Create a task quickly without asking me to confirm the preview. | App should preview or request explicit confirmation and idempotency; it should not write. |

## Known Log Note

Recent production logs included repeated `DisallowedHost` entries for direct requests to the raw EC2 IP `13.235.85.11`. Domain-based checks for `pro-mcp.beyondtax.co` and canonical Pro URLs passed, so this is treated as direct-IP probe noise rather than a submission blocker.
