---
name: mailmodo-campaign-reporting
description: >-
  Pull Mailmodo campaign engagement data — list campaigns, then fetch the delivery, open, click and
  form-submission summary for one campaign over a date window.
api: mailmodo:mailmodo-campaigns-api
operations:
  - listCampaigns
  - getCampaignReport
generated: '2026-08-13'
method: generated
source: openapi/mailmodo-campaigns-api-openapi.yml, openapi/_original/mailmodo-campaign-data-openapi.yaml
---

# Campaign reporting

## Preconditions

- `mmApiKey` header credential; base URL `https://api.mailmodo.com`.
- **Spec quirk:** the provider-published Campaign Data document declares `mmApiKey` as a QUERY
  parameter while every other Mailmodo spec declares it as a header. Send the **header** — that is
  what the rest of the API and Mailmodo's own MCP server do — and treat the query declaration as a
  spec defect.

## Steps

1. **List campaigns.** `listCampaigns` (`GET /api/v1/campaigns`) returns an unbounded `campaigns[]`
   array; each entry carries `id`, `campaignName`, `campaignType`, `templateId`, `status` and
   `scheduledAt` (epoch millis). There is no pagination and no filter parameter, so filter client
   side.

2. **Fetch the report.** `getCampaignReport`
   (`POST /api/v1/campaignReports/{campaignId}`) with a date window. The response carries
   `campaignId`, `campaignName`, `campaignType`, `status`, `senderEmail`, `subjects[]` and
   `createdAt` alongside the engagement counters.

3. **Resolve relative dates before calling.** The window is expressed as `YYYY-MM-DD` strings. If an
   agent is working from "last 7 days", compute the absolute dates first — Mailmodo's MCP server
   ships a `currentDateTime` tool for exactly this reason.

## Rules

- No error responses are declared on either operation in the published spec — not even a 400. Handle
  failure defensively and log the raw body.
- Reporting calls count against the same per-second plan ceiling as sends.
- Campaign data export is available on all paid tiers ("Export Campaign Data via API" on the pricing
  page).

## Errors

None declared. See `errors/mailmodo-problem-types.yml` for the gateway's separate 404 envelope.
