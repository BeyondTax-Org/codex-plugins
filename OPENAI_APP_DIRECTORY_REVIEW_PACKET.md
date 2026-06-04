# Beyondtax Pro OpenAI App Directory Review Packet

## Visibility Boundary

Beyondtax Pro is installable from this public Codex plugin marketplace by adding:

`https://github.com/BeyondTax-Org/codex-plugins`

Then installing:

`beyondtax-pro@beyondtax`

Built-in OpenAI app/plugin directory visibility is separate. It requires OpenAI review, approval, publishing, rollout, and workspace or plan availability. Initial discoverability may depend on direct links, exact-name search, workspace settings, feature access, and admin controls.

## Submission Metadata

- App/plugin name: `Beyondtax Pro`
- Marketplace id: `beyondtax`
- Plugin id: `beyondtax-pro`
- Publisher: Beyondtax
- Category: Productivity
- Website: `https://pro.beyondtax.co`
- Documentation: `https://pro.beyondtax.co/docs/mcp`
- Privacy Policy: `https://pro.beyondtax.co/privacy`
- Terms of Service: `https://pro.beyondtax.co/terms`
- Logo/icon assets: `plugins/beyondtax-pro/assets/`

## MCP Endpoint

- MCP URL: `https://pro-mcp.beyondtax.co/mcp`
- Authentication: OAuth during install
- OAuth metadata: `https://pro-mcp.beyondtax.co/.well-known/oauth-authorization-server`
- Protected resource metadata: `https://pro-mcp.beyondtax.co/.well-known/oauth-protected-resource`
- Direct unauthenticated `/mcp` response: expected `401`
- Server instructions: included through the MCP `get_server_instructions` tool

## Public Tool Posture

- Read-oriented workspace assistance only
- No create, edit, delete, submit, pay, file, or send-message actions promised
- Discovery search is name/title oriented and does not match contact or tax identifiers
- Structured contact fields, addresses, comments, and tax or registration identifiers are masked, omitted, or summarized by default

## Tool And Prompt Inventory

- 2026-06-04 live production registry snapshot:
  - Tool count: `26`
  - Prompt count: `7`
  - `get_server_instructions`: present
  - Search posture: client display name/city, engagement name, task title
  - Privacy posture: contact/address/comment/tax identifiers masked, omitted, summarized, or exposed only as presence flags

Detailed snapshot:

`OPENAI_APP_DIRECTORY_REGISTRY_SNAPSHOT_20260604.md`

## Demo Review Account

Prepare a demo Beyondtax Pro account for review with:

- Sample workspace data
- Sample clients, engagements, tasks, team, billing, services, and search records
- No MFA, OTP, or extra human setup required during the review window
- No production client secrets or private client records
- Clear expiry/rotation owner for demo credentials

Do not commit credentials to this repository.

## Test Cases

Golden prompt set:

- "Show my Beyondtax Pro workspace overview."
- "Find client Bower and summarize open engagements and tasks."
- "List overdue tasks by assignee."
- "Summarize my billing and subscription status."
- "Explain what the Beyondtax Pro connector can and cannot do."

For each test, record:

- Date and environment
- Expected tools
- Expected response shape
- Any privacy masking observed
- Pass/fail result

Post-deploy evidence:

`OPENAI_APP_DIRECTORY_TEST_EVIDENCE_20260604.md`

## Privacy And Safety

Reviewers should see:

- Data access is limited by the authenticated user's Beyondtax Pro role and workspace permissions
- Contact and tax identifier data is minimized by default
- User-facing docs disclose the read-oriented scope
- OAuth and policy URLs point to canonical Pro pages
- No write, payment, filing, messaging, or deletion actions are available in the public plugin
- Users should not paste login secrets, one-time codes, browser session data, or raw access material into chat

## Live Verification

Update this section before each submission attempt with dated evidence:

- 2026-06-04: `https://pro-mcp.beyondtax.co/mcp` returns `401`
- 2026-06-04: `https://pro.beyondtax.co/docs/mcp` returns `200`
- 2026-06-04: `https://pro.beyondtax.co/privacy` returns `200`
- 2026-06-04: `https://pro.beyondtax.co/terms` returns `200`
- 2026-06-04: `https://pro-mcp.beyondtax.co/docs/mcp` redirects to `https://pro.beyondtax.co/docs/mcp`, then returns `200`
- 2026-06-04: `https://pro-mcp.beyondtax.co/privacy` redirects to `https://pro.beyondtax.co/privacy`, then returns `200`
- 2026-06-04: `https://pro-mcp.beyondtax.co/terms` redirects to `https://pro.beyondtax.co/terms`, then returns `200`
- 2026-06-04: OAuth metadata uses `https://pro.beyondtax.co/docs/mcp`, `https://pro.beyondtax.co/privacy`, and `https://pro.beyondtax.co/terms`
- 2026-06-04: OAuth/protected resource display casing is `Beyondtax Pro`
- 2026-06-04: Production backend commit verified at `7241a26faf5d015a27ef21aadd1b96f6fe6bb01a`
- 2026-06-04: Production Django system check passed
- 2026-06-04: Production focused MCP test suite passed, `8` tests OK
- 2026-06-04: Production container source has `has_contact_person` booleans and no raw `contact_person` serializer field for business/group client detail payloads

## Release Notes

Record before submission:

- Submitted plugin version: `0.1.2`
- Marketplace commit hash: `2573dd95cd2319c957e0c6ab74addc0dd6b0bc19`
- Backend source privacy patch checked: `61d84309de94bdda8567eff8a1860319fb9784f5` (PR #310)
- Backend deployed commit hash: `7241a26faf5d015a27ef21aadd1b96f6fe6bb01a`
- UI deploy commit hash: verify in hosting dashboard before final submit
- Tool/prompt registry snapshot: `26` tools and `7` prompts
- Known limitations: read-oriented only; no filing, payment, messaging, record mutation, or deletion actions
- Backward compatibility notes: old `pro-mcp.beyondtax.co` docs/legal URLs redirect to canonical Pro UI pages
