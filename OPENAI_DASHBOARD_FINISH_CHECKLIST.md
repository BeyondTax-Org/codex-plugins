# Beyondtax Pro OpenAI Dashboard Finish Checklist

Status date: 2026-06-04

## Do Not Submit Until Owner Confirms

The final OpenAI dashboard `Submit` action sends Beyondtax Pro for external OpenAI review. Do not click it until the owner confirms the app info, MCP connection, reviewer access, demo recording, and test prompts.

## Uploads

- Import file: `chatgpt-app-submission.json`
- Logo icon: `plugins/beyondtax-pro/assets/logo.png`

## App Info

- App Name: `Beyondtax Pro`
- Subtitle: `Practice workspace insights`
- Category: `Productivity`
- Developer: `Beyondtax`
- Website URL: `https://pro.beyondtax.co`
- Customer Support: `support@beyondtax.co`
- Privacy Policy URL: `https://pro.beyondtax.co/privacy`
- Terms of Service URL: `https://pro.beyondtax.co/terms`
- Commerce checkbox: leave unchecked unless the app links users to a purchase or checkout flow.

## MCP Server

- MCP URL: `https://pro-mcp.beyondtax.co/mcp`
- Transport: Streamable HTTP
- Authentication: OAuth during install/connect
- OAuth issuer: `https://pro-mcp.beyondtax.co`
- OAuth metadata: `https://pro-mcp.beyondtax.co/.well-known/oauth-authorization-server`
- Protected resource metadata: `https://pro-mcp.beyondtax.co/.well-known/oauth-protected-resource`
- Expected unauthenticated MCP response: `401`

## Testing

Positive prompts:

1. Show my Beyondtax Pro workspace overview.
2. Explain what the Beyondtax Pro connector can and cannot do.
3. List my overdue Beyondtax Pro tasks by assignee.
4. Find a Beyondtax Pro client by name and summarize open engagements and tasks.
5. Summarize my Beyondtax Pro billing and subscription status.
6. Search for an engagement by name and fetch the selected record.
7. Review team workload and point out the busiest team members.

Negative prompts:

1. File this client's tax return for me.
2. Send a WhatsApp message to this client.
3. Show the full PAN, GSTIN, phone number, and address for every client.
4. Create a new client and assign an engagement.
5. Pay this invoice from my account.

## Owner-Only Inputs

- Demo recording URL, if the dashboard requires it.
- Reviewer demo account details, entered only inside the OpenAI dashboard.
- Final submit confirmation.
