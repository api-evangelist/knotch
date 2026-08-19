---
name: Send conversion events to Knotch
description: >-
  Submit a batch of server-side conversion events (CRM milestones, offline outcomes, warehouse
  events) to the Knotch Events API so they are measured and attributed alongside on-site
  conversions in Knotch One.
api: openapi/knotch-events-api-openapi.yml
operations:
  - get_events_conversion_events_segment__account_id__post
  - health_check_health_get
generated: '2026-08-13'
method: generated
source: >-
  Grounded in openapi/knotch-events-api-openapi.yml (harvested from
  https://events.knotch.it/openapi.json) and
  https://help.knotch.com/en/articles/159-events-api-v11-technical-overview
---

# Send conversion events to Knotch

Use this when an outcome happened somewhere other than the customer's website — a deal closed in
Salesforce, a lead became an SQL in Marketo, a renewal processed — and it needs to be attributed
back to the content the visitor read.

## Before you start

You need two things, and neither is self-service:

- **An API key.** Knotch issues and rotates these through a Client Success Manager. There is no
  key-issuance endpoint and no key prefix that tells you whether a key is test or live.
- **An account ID.** The Knotch Measurement Account ID, which goes in the URL path.

Confirm reachability first with `health_check_health_get` — `GET /health`, no auth required.

## Step 1 — Make sure the event name exists in Knotch One

An event only becomes an "API Conversion" if a human has defined it in Knotch One Event Builder
and its `event_name` matches yours **exactly**. If nobody has defined it yet, the event is still
ingested and stored; it just will not show up on any dashboard until someone creates the matching
API Conversion. This is the single most common reason a successfully-accepted event appears to do
nothing.

## Step 2 — Build the batch

Call `get_events_conversion_events_segment__account_id__post`:

```
POST /conversion_events/segment/{account_id}?simulate=true
Authorization: Bearer <api-key>
Content-Type: application/json
```

Body is the `CustomEvents` schema — always an array, even for one event:

```json
{
  "events": [
    {
      "event": {
        "event_name": "ClosedWon",
        "timestamp": 1720727400,
        "event_id": "OPP-12345"
      },
      "identity": { "gclid": { "value": "...", "first_seen": 1724800000, "last_seen": 1724886400 } },
      "value": { "value": 50000.00 },
      "event_source": ["Salesforce"]
    }
  ]
}
```

Rules that are enforced, from `conventions/knotch-conventions.yml`:

- **1 to 100 events per request.** No more.
- `event.event_name`, `event.timestamp` and `event.event_id` are all required.
- `timestamp` is UTC Unix **seconds**, an integer — not milliseconds, not ISO 8601.
- `identity` is required as an object, and at least one identifier inside it must be populated.
  Knotch supports only one custom ID, agreed before integration. Available keys:
  `kn_cs_visitor_id`, `gclid`, `ecid`, `ga_client_id`, `marketo_lead_id`.
- `value.value` is a float. Currency is assumed USD and is not sent; Knotch sums it.
- Optional `click_ids` carries `msclkid`, `fbclid`, `ttclid`, `li_fat_id`.

## Step 3 — Validate before you write

**Always send `simulate=true` first.** It checks structure, required fields and authentication and
stores nothing, returning:

```json
{"message": "Events validated successfully"}
```

`simulate` defaults to **false**. If you drop the parameter, you write production data. Treat the
flag as required in your own client even though the API does not.

## Step 4 — Send for real

Re-send the identical payload with `simulate=false`. Then stop — do not re-send to "make sure".

## Retries and duplicates

Retrying is safe, and that is a deliberate property, not luck:

- Deduplication is keyed on `event_id` (and `identity` where available).
- A duplicate returns **409 Conflict**. Treat 409 as success-already-recorded, not as an error to
  alert on.
- On the Segment path, Segment's `messageId` is used when present.

There is no `Idempotency-Key` header and no way to replay a request and get the original response
body back. Your `event_id` must therefore be stable and derived from the source record — an
opportunity ID, not a generated UUID that changes each attempt.

## Handling responses

From `errors/knotch-problem-types.yml`:

| Status | Meaning | Do |
|---|---|---|
| 200 | Accepted | Done |
| 400 | Bad Request, cause unspecified | Re-check payload, then escalate to Client Success |
| 403 | Knotch labels this "Unauthorized" | Check the Bearer header and that the key matches `account_id` |
| 409 | Duplicate | Success. Stop retrying |
| 422 | Validation failure | Read `detail[].loc` for the offending field path |
| 500/502/503/504 | Knotch-side | Retry with backoff — safe, because of `event_id` dedup |

No 401 and no 429 are documented. There are **no rate-limit response headers**, so pace yourself
conservatively; the only published throughput constraint is the 100-event batch cap.

## What you will not get

- No read, list or query operations. This is write-only ingestion; you cannot confirm via the API
  that an event landed.
- No `Retry-After`, no `RateLimit-*` headers.
- Attributed content metrics on the Conversions Leaderboard refresh every **24 hours**, so do not
  expect an event to be visible in reporting immediately.
