# Beyondtax Pro Registry Snapshot

Snapshot date: 2026-06-04 11:48 IST

Environment: production container at `https://pro-mcp.beyondtax.co/mcp`

Backend deployed commit: `7241a26faf5d015a27ef21aadd1b96f6fe6bb01a`

Backend source privacy patch: `61d84309de94bdda8567eff8a1860319fb9784f5` (PR #310)

## Summary

- Tool count: `26`
- Prompt count: `7`
- `get_server_instructions`: present
- Search scope: client display names/cities, engagement names, and task titles
- Public posture: read-oriented; no create/edit/delete/submit/pay/file/message actions
- Privacy posture: contact fields, addresses, comments, tax identifiers, and registration identifiers are masked, omitted, summarized, or exposed only as presence/status flags by default

## Tools

| Tool | Description |
| --- | --- |
| `list_my_workspaces` | List all Beyondtax Pro workspaces the authenticated user can access. |
| `get_workspace_overview` | High-level overview of a workspace: counts of clients, active/overdue engagements, open tasks, and active team members. |
| `get_workspace_profile` | Full workspace business profile, with sensitive identifiers masked. |
| `list_clients` | List clients in the workspace; search matches display name or city. |
| `get_client_details` | Detailed read-only client summary, with sensitive/contact payload minimization. |
| `search_clients` | Search clients by display name or city. |
| `list_group_clients` | List group clients with linked member count. |
| `list_engagements` | List engagements with optional status and client filters. |
| `get_engagement_details` | Engagement detail with phases, data-pack items, owners, reviewers, and progress stats. |
| `list_engagement_tasks` | List tasks for a specific engagement. |
| `list_engagement_activities` | Recent engagement activity log entries. |
| `list_overdue_engagements` | List overdue engagements not completed or filed. |
| `list_tasks` | List workspace tasks with optional status, priority, and client filters. |
| `get_task_details` | Task details with assignees, subtasks, and latest comments. |
| `list_overdue_tasks` | List overdue tasks not done. |
| `list_team_members` | List workspace team members. |
| `get_team_workload` | Per-member workload based on open engagement ownership and open task assignments. |
| `list_workspace_roles` | List workspace role types. |
| `get_subscription_summary` | Read current workspace subscription and billing-period status. |
| `list_invoices` | List invoices with optional status filter. |
| `list_billing_plans` | List active billing plans. |
| `list_services_catalog` | List services available to the workspace. |
| `list_service_packages` | List active service packages. |
| `get_server_instructions` | Return safe user-facing guidance for the Beyondtax Pro MCP server. |
| `search` | Search clients, engagements, and tasks by client display name/city, engagement name, and task title. |
| `fetch` | Fetch one selected record by composite id returned from `search`. |

## Prompts

| Prompt | Description |
| --- | --- |
| `practice_health_review` | Full practice-health review for the workspace. |
| `engagement_status_summary` | Summarize active engagement status. |
| `engagement_deep_dive` | Deep-dive review of one engagement. |
| `client_onboarding_review` | Audit client setup completeness. |
| `billing_summary` | Summarize subscription and invoice status. |
| `team_workload_audit` | Audit team workload and utilization. |
| `overdue_action_plan` | Generate an action plan for overdue items. |

## Server Instructions Summary

Live `get_server_instructions` says Beyondtax Pro MCP is read-only, scoped to the authenticated user's authorized workspace, suited for review/search/summaries/planning/follow-up, and should not be assumed to create, edit, submit, pay, delete, file, or send. It also states that structured contact fields, addresses, comments, and tax or registration identifiers are masked, omitted, or summarized by default, and that discovery search is name/title oriented rather than contact/tax-identifier oriented.

