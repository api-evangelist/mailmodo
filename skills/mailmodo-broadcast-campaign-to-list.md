---
name: mailmodo-broadcast-campaign-to-list
description: >-
  Send one Mailmodo campaign to an entire contact list in a single API call, resolving the list by
  name to its id first.
api: mailmodo:mailmodo-campaigns-api
operations:
  - getAllContactLists
  - listCampaigns
  - bulkTriggerCampaign
generated: '2026-08-13'
method: generated
source: openapi/mailmodo-campaigns-api-openapi.yml, openapi/mailmodo-contact-lists-api-openapi.yml
---

# Broadcast a campaign to a list

## Preconditions

- `mmApiKey` header credential; base URL `https://api.mailmodo.com`.
- A campaign of type `CONTACT_LIST` and a populated contact list.

## Steps

1. **Resolve the list id.** Call `getAllContactLists` (`GET /api/v1/getAllContactLists`). The
   response carries `listDetails[]` with `id`, `name`, `created_at` and `contacts_count`. Match on
   `name` and take the `id`.
   This step is not optional: contact WRITE operations address a list by `listName`, but
   `bulkTriggerCampaign` addresses it by `listId`. The same entity has two different handles.

2. **Resolve the campaign id.** Call `listCampaigns` (`GET /api/v1/campaigns`) and take the `id`
   of the campaign whose `campaignType` is `CONTACT_LIST`.

3. **Broadcast.** Call `bulkTriggerCampaign`
   (`POST /api/v1/bulktriggerCampaign/{campaignId}`) with the `listId` and any campaign-level merge
   data. Success returns `{"success": true, "message": "Email scheduled successfully", "ref": "<uuid>"}`.

4. **Confirm before repeating.** Check `contacts_count` from step 1 against the send you intended.
   A duplicate broadcast mails the entire list again — there is no idempotency key and no
   deduplication window.

## Rules

- Sends consume plan sending credits (2,000/month on Lite, 3,000 on Pro, unlimited on Max).
  Verify the list size against remaining credits before triggering.
- Branch on the `success` field, not the HTTP status.
- Reporting on the result is a separate flow — see `mailmodo-campaign-reporting`.

## Errors

HTTP 400 "Bad Request" is the only declared failure. See `errors/mailmodo-problem-types.yml`.
