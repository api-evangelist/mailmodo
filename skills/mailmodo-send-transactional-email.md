---
name: mailmodo-send-transactional-email
description: >-
  Send a single transactional email through a pre-built Mailmodo campaign, with merge data
  personalizing the AMP/HTML template. Use for password resets, receipts, verification and
  account notifications.
api: mailmodo:mailmodo-campaigns-api
operations:
  - listTemplates
  - listCampaigns
  - triggerCampaign
generated: '2026-08-13'
method: generated
source: openapi/mailmodo-campaigns-api-openapi.yml, openapi/mailmodo-templates-api-openapi.yml
---

# Send a transactional email

Mailmodo does not let you send arbitrary HTML over the API. You send an existing **campaign**,
which is bound to a template built in the Mailmodo editor. The API's job is to trigger it and
supply merge data.

## Preconditions

- An API key from **Settings > API Keys** (`https://manage.mailmodo.com/app/settings/apikey`).
  Pass it as the `mmApiKey` **header** on every request.
- A sender domain verified with SPF, DKIM and DMARC, and AMP whitelisting approved by Google/Yahoo
  (5–7 business days) if the template uses AMP.
- Base URL `https://api.mailmodo.com`.

## Steps

1. **Find the campaign.** Call `listCampaigns` (`GET /api/v1/campaigns`). The response is an
   unbounded `campaigns[]` array — there is no pagination — where each entry carries `id`,
   `campaignName`, `campaignType`, `templateId` and `status`. Take the `id` of the campaign you
   want; that is the `campaignId` path parameter.
   Optionally call `listTemplates` (`GET /api/v1/getAllTemplates`) to confirm which template the
   campaign renders.

2. **Trigger the send.** Call `triggerCampaign`
   (`POST /api/v1/triggerCampaign/{campaignId}`) with the recipient address and a `data` object of
   merge values matching the placeholders in the template.

3. **Record the `ref`.** A success body looks like
   `{"success": true, "message": "Email scheduled successfully", "ref": "<uuid>"}`.
   `ref` is the only correlation handle Mailmodo gives you — there is no request-id header. Persist
   it before you do anything else.

## Rules

- **Branch on `success`, not on the HTTP status.** Mailmodo returns HTTP 200 with
  `{"success": false, "message": "The provided email is not a valid email id"}` for several
  validation failures. A 200 is not a send.
- **Never retry blindly.** There is no `Idempotency-Key` header on this API. A retried
  `triggerCampaign` sends a second email to a real person. If a call times out, look for the `ref`
  before re-issuing.
- **Respect the plan's request ceiling.** 5 req/s on Lite, 10 on Pro, 50 on Max. No rate-limit
  response headers are published, and no 429 contract is declared — you must pace yourself.
- **There is no test mode.** Every successful call delivers mail. To exercise the contract without
  sending, use the Stoplight Prism mock in `sandbox/mailmodo-sandbox.yml`.

## Errors

Only HTTP 400 "Bad Request" is declared on this operation. 401, 403, 429 and 5xx are undocumented.
See `errors/mailmodo-problem-types.yml`.
