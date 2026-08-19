---
name: mailmodo-sync-contacts
description: >-
  Push contacts from an application or CRM into a Mailmodo list, individually or in batch, read a
  contact back, and remove one from a list.
api: mailmodo:mailmodo-contacts-api
operations:
  - addContactToList
  - addContactsToListBatch
  - getContactDetails
  - removeContactFromList
  - getAllContactLists
generated: '2026-08-13'
method: generated
source: openapi/mailmodo-contacts-api-openapi.yml, openapi/mailmodo-contact-lists-api-openapi.yml
---

# Sync contacts into Mailmodo

## Preconditions

- `mmApiKey` header credential; base URL `https://api.mailmodo.com`.
- A regular contact list. **Static segmentation lists cannot be written to** — the batch endpoint
  returns HTTP 400 `"Cannot add users to static segmentation list"`.

## Steps

1. **Confirm the target list exists.** `getAllContactLists`
   (`GET /api/v1/getAllContactLists`) returns `listDetails[]`. Write operations address the list by
   its `name`, so take `name`, not `id`.

2. **Write one contact.** `addContactToList` (`POST /api/v1/addToList`) with `email`, `listName`
   and a free-form `data` object of custom attributes. This is an **upsert** — posting an email that
   already exists updates its attributes. That is the only way to update a contact; there is no
   dedicated update operation.
   Success: `{"success": true, "message": "The contact is successfully added/updated"}`.

3. **Write many.** `addContactsToListBatch` (`POST /api/v1/addToList/batch`) with `listName` and a
   `values[]` array of contact objects. The batch response is a **partial-success** shape carrying
   `errors[]` (each `{email, "failure reason"}`) and `warnings[]`. Always read `errors[]` — a 200
   does not mean every row landed.

4. **Read a contact back.** `getContactDetails` (`GET /api/v1/getContactDetails?email=`) returns
   `contactIdentifier`, `email` and the `data` object. `contactIdentifier` is read-only and appears
   nowhere else in the API; keep addressing contacts by email.

5. **Remove from a list.** `removeContactFromList` (`POST /api/v1/removeFromList`) with `email` and
   `listName`. This removes list membership only — it does not unsubscribe or delete the contact.
   For those, use `mailmodo-manage-subscriptions`.

## Rules

- No pagination anywhere in this API: `getAllContactLists` returns everything in one array.
- No idempotency key. The single-contact write is naturally idempotent because it upserts, but the
  batch write is not — a retried batch re-processes every row.
- Pace batches against the plan ceiling (5 / 10 / 50 req/s).

## Errors

400 `"Cannot add users to static segmentation list"` (batch), 400 `"Bad Request"`
(`getContactDetails`, `removeFromList`). See `errors/mailmodo-problem-types.yml`.
