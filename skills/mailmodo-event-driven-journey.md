---
name: mailmodo-event-driven-journey
description: >-
  Drive Mailmodo automation from product behaviour — send a custom event, start a contact into an
  automated journey, and abort that journey when the user completes the goal.
api: mailmodo:mailmodo-events-api
operations:
  - addEvent
  - post-hooks-start-journey-id
  - post-hooks-abort-journey-id
  - addContactToList
generated: '2026-08-13'
method: generated
source: openapi/mailmodo-events-api-openapi.yml, openapi/mailmodo-user-journeys-api-openapi.yml
---

# Event-driven journeys

## Preconditions

- `mmApiKey` header credential.
- A journey built in the Mailmodo UI. **There is no read operation for journeys** — no list, no get,
  no status. You must obtain the `journey-id` from the Mailmodo interface and configure it.

## Base URL warning

The journey endpoints are the one part of Mailmodo that sits **outside** the `/api/v1` prefix:

- events: `https://api.mailmodo.com/api/v1/addEvent`
- journeys: `https://api.mailmodo.com/hooks/start/{journey-id}` and `.../hooks/abort/{journey-id}`

Do not prepend `/api/v1` to the hooks paths.

## Steps

1. **Make sure the contact exists.** `addContactToList` (`POST /api/v1/addToList`) upserts the
   contact with any attributes the journey's conditions read.

2. **Send the behavioural event.** `addEvent` (`POST /api/v1/addEvent`) with `email`,
   `event_name`, an `event_properties` object, and optionally `ts` (epoch). Success returns
   `{"success": true, "ref": "<uuid>"}`. Events feed segments and journey triggers.

3. **Start the journey explicitly** when you want to control entry rather than rely on a trigger:
   `post-hooks-start-journey-id` (`POST /hooks/start/{journey-id}`) with the contact's email.
   The response `ref` is the **journey instance id** — the only handle you will ever get for that
   contact's run. Persist it.

4. **Abort on goal completion.** `post-hooks-abort-journey-id`
   (`POST /hooks/abort/{journey-id}`) with the contact's email. This is what stops a nudge sequence
   once the user has done the thing you were nudging them toward. Skipping it is the most common way
   a lifecycle sequence annoys a converted user.

## Rules

- No idempotency key: a repeated `hooks/start` can enroll the contact twice. Check your own record
  of the instance `ref` before starting.
- `addEvent` is append-only by design; sending the same event twice creates two events, which will
  double-count in segments.
- Branch on `success`, not the HTTP status — the abort operation's own 200 example in the published
  spec is `{"success": true, "message": "The provided email is not a valid email id"}`.

## Errors

400 "Bad Request" on all three operations. See `errors/mailmodo-problem-types.yml`.
