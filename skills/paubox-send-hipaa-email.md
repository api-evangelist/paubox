---
name: paubox-send-hipaa-email
description: >-
  Send a HIPAA compliant transactional email through the Paubox Email API and confirm it
  was delivered. Use when an agent must deliver PHI-bearing content — appointment
  reminders, care instructions, results notifications — to a patient inbox without a
  portal or password.
api: Paubox Email API
base_url: https://api.paubox.com/v1/email
operations:
  - sendMessage
  - sendBulkMessages
  - getMessageReceipt
source: openapi/paubox-email-api-openapi.yaml
generated: '2026-08-26'
method: generated
---

# Send a HIPAA compliant email with Paubox

## Before you start

- The `from` address **must** be on a domain verified in the Paubox dashboard. Sending from
  an unverified domain (including `@gmail.com`) returns `400 Bad Request` with
  `{"errors": "Sender domain not verified"}`. This is the single most common failure.
- Authenticate with `Authorization: Bearer YOUR_API_KEY`. The legacy
  `Authorization: Token token=YOUR_API_KEY` form is still accepted but Bearer is preferred.
- Keys are issued **per domain** and displayed only once at creation.

## Steps

1. **Send the message** — `sendMessage` (`POST /messages`).
   Build `data.message` with `recipients` (at least one address, max 100),
   `headers.subject` (required), `headers.from`, and `content` carrying at least one of
   `text/plain` or `text/html`. Attachments go in `data.message.attachments` with `content`
   base64-encoded; total attachment size per message must not exceed 50 MB.
   The 200 response returns a `sourceTrackingId`. **Keep it** — it is the only handle on
   the message afterwards.

2. **Sending to many recipients?** Use `sendBulkMessages` (`POST /bulk_messages`) rather
   than looping `sendMessage`. Paubox recommends batches of 50 or fewer per request.
   Source tracking IDs come back in the same order as the `messages` array, so zip them
   against your input list positionally.

3. **Confirm delivery** — `getMessageReceipt` (`GET /message_receipt`), passing the
   `sourceTrackingId`. The response carries delivery status plus open and click tracking.
   A `404` means the tracking ID does not exist.

## Reacting to failure

`sendMessage` and `sendBulkMessages` declare only `200` and `400` in the spec, but the
documented error surface is wider (see `errors/paubox-problem-types.yml`):

| Status | What to do |
| --- | --- |
| `400` | Fix the request. Check: verified `from` domain, `subject` present, non-empty `recipients`, valid base64 attachments, at least one body part. Do **not** retry unchanged. |
| `401` | Credential missing or malformed. Do not retry. |
| `403` | Key is valid but lacks permission for this action. Do not retry. |
| `422` | Semantically invalid — most often an unverified `from` domain. Do not retry unchanged. |
| `429` | Back off and retry with exponential backoff. For volume, switch to `sendBulkMessages`. |
| `500` / `502` / `504` | Retry with backoff. |
| `503` | Temporary outage — check https://status.paubox.com before retrying. |

Error bodies are a JSON object with an `errors` (or `message`) field. Paubox does **not**
use RFC 9457 `application/problem+json`.

## Safety rules an agent must honour

- **There is no idempotency key on this API.** A retried `POST /messages` sends the email
  again. Before retrying a send, call `getMessageReceipt` with the tracking ID from the
  original attempt if you have one; if the original request failed before returning an ID,
  treat a retry as a possible duplicate send and say so.
- **There is no unsend, recall or void operation.** A delivered message cannot be taken
  back. Confirm recipient, subject and body with the user *before* calling `sendMessage`,
  not after.
- Never post PHI, recipient addresses or message bodies into public channels such as the
  Paubox community discussions.
