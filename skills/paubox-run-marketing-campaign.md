---
name: paubox-run-marketing-campaign
description: >-
  Build a subscriber list, create and schedule a HIPAA compliant marketing campaign, and
  read its analytics through the Paubox Marketing API. Use when an agent runs patient
  outreach at list scale rather than sending a single transactional message.
api: Paubox Marketing API
base_url: https://api.paubox.com/v1/marketing
operations:
  - createSubscriptionList
  - createSubscriber
  - bulkCreateSubscribers
  - createSubscription
  - createCampaignMailing
  - sendCampaignMailingTestEmail
  - scheduleCampaignMailing
  - sendCampaignMailing
  - getCampaignAnalytics
  - unsubscribeSubscribers
  - deleteSubscription
source: openapi/paubox-marketing-api-openapi.yaml
generated: '2026-08-26'
method: generated
---

# Run a Paubox marketing campaign

## Authentication is different here

The Marketing API uses `Authorization: Token token=<API_KEY>` — **not** the Bearer form
used by the Email and Forms APIs. A key that works against `/v1/email` will not
necessarily work against `/v1/marketing`; Marketing is a separately purchased plan.

## Build the audience

1. `createSubscriptionList` (`POST /subscription_lists`) — create a static list.
2. `createSubscriber` (`POST /subscribers`) for one, or `bulkCreateSubscribers`
   (`POST /subscribers_bulk_create`) for many. Omitting a list adds the record to the
   account's default "All contacts" list.
3. `createSubscription` (`POST /subscriptions`) joins an existing subscriber to an
   existing list. **A subscriber is not on a list until this join exists.**

## Create, rehearse, then send

4. `createCampaignMailing` (`POST /campaign_mailings`) **only stores the content**. It
   does not deliver anything. This is the closest thing the API has to a dry run.
5. `sendCampaignMailingTestEmail`
   (`GET /campaign_mailings/{campaign_mailing_id}/send_test_email`) sends a one-off preview
   to a single address, subject prefixed `[Test]`, from the account's default brand
   `from_email`. **Use this before every real send.** It returns `204`.
6. Deliver with either:
   - `sendCampaignMailing` (`POST /campaign_mailing_sends`) — sends now. Note the docs
     state the message must have been created in the Paubox Marketing web interface for
     this trigger to work.
   - `scheduleCampaignMailing` (`POST /campaign_mailing_schedules`) — sends at a future
     time.
7. Read results with `getCampaignAnalytics`, `getCampaignTable`,
   `getCampaignDeliveriesTable`, `getTrackingLinks`.

## Reversibility — read this before step 6

| Action | Can it be taken back? |
| --- | --- |
| `scheduleCampaignMailing` | No cancel or unschedule operation is published. Once scheduled, there is no documented API path to stop it. |
| `sendCampaignMailing` | No. Delivery is irreversible. |
| `createSubscription` | Yes — `deleteSubscription` (`DELETE /subscriptions/{id}`) stamps `unsubscribed_at` and keeps the record; the subscriber stays on every other list. |
| `unsubscribeSubscribers` | Yes — `subscribeSubscribers` (`POST /subscriptions/subscribe`) re-subscribes by UUID. |
| `bulkGlobalUnsubscribe` | Yes — `bulkGlobalSubscribe` clears the global opt-out for the whole list. |
| `bulkDeleteCampaignMailings` | No. Permanent, and there is no single-delete operation — pass an array of one ID to delete one mailing. |
| `bulkDeleteSubscribers` | No published restore path. |

**No window is published for any of these reversals.** Do not assume one.

## Failure handling

Marketing operations declare `400`, `401`, `404`, `422` and `500` broadly.
`sendCampaignMailing` and `scheduleCampaignMailing` and the drip-campaign transitions
(`startDripCampaign`, `pauseDripCampaign`) additionally declare `422` — treat it as "the
campaign is not in a state that permits this transition" and re-read the campaign before
retrying. There are no idempotency keys, so never blind-retry a send or schedule call.
