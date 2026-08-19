---
name: mailmodo-manage-subscriptions
description: >-
  Honor a recipient's consent choices in Mailmodo — unsubscribe or suppress, update per-email-type
  subscription preferences, resubscribe, and permanently archive a contact for erasure requests.
api: mailmodo:mailmodo-contacts-api
operations:
  - unsubscribeContact
  - resubscribeContact
  - archiveContact
  - getContactDetails
generated: '2026-08-13'
method: generated
source: openapi/mailmodo-contacts-api-openapi.yml, openapi/_original/mailmodo-contact-management-openapi.json
---

# Manage subscription state and erasure

Consent operations are the ones you least want to get wrong. Mailmodo separates three distinct
states: **suppressed** (unsubscribed, record retained), **subscribed**, and **archived**
(permanently removed).

## Preconditions

- `mmApiKey` header credential; base URL `https://api.mailmodo.com`.

## Steps

1. **Look up current state first.** `getContactDetails`
   (`GET /api/v1/getContactDetails?email=`) confirms the contact exists. `archiveContact` returns
   400 `"Email address doesn't exist"` if it does not, so a blind archive on an unknown address is
   an error, not a no-op.

2. **Unsubscribe / suppress.** `unsubscribeContact`
   (`POST /api/v1/contacts/unsubscribe`) with `email`. Adds the contact to the suppression list
   across the workspace.

3. **Granular preferences.** `POST /api/v1/contacts/updateSubscription` sets per-email-type
   subscription state and returns `currentUnsubscribedEmailTypes[]`. This operation is present in the
   provider-published Contact Management spec but is **not exposed by Mailmodo's MCP server** — call
   it over REST. Its 400 response is declared without a description or example, so treat any failure
   as opaque and log the raw body.

4. **Resubscribe.** `resubscribeContact` (`POST /api/v1/contacts/resubscribe`) with `email`.
   Only do this on an explicit, recorded opt-in from the recipient.

5. **Erasure.** `archiveContact` (`DELETE /api/v1/contacts`) with `email`. This is permanent.
   Success: `{"success": true, "message": "The contact is successfully deleted"}`.

## Rules

- Removing a contact from a list (`removeContactFromList`) is **not** an unsubscribe. Do not
  substitute one for the other when honoring an opt-out.
- Branch on `success`, not the HTTP status.
- These operations have no idempotency key, but unsubscribe/resubscribe/archive are state-setting
  and therefore safe to repeat — archive being the exception, which errors on a second call.

## Errors

400 `"Email address doesn't exist"` (archive), 400 undescribed (`updateSubscription`).
See `errors/mailmodo-problem-types.yml`.
