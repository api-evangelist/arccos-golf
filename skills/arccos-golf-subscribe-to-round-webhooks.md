---
name: arccos-golf-subscribe-to-round-webhooks
description: >-
  Register an HTTPS webhook with Arccos, consume postRound / patchRound / deleteRound / accountDisconnected
  events idempotently, and tear the subscription down.
api: Arccos On-Course Data API
base_url: https://api.arccosgolf.com/
operations:
  - handle_create_webhook.post./v5/webhooks
  - handle_get_webhooks.get./v5/webhooks
  - handle_delete_webhook.delete./v5/webhooks/{webhookId}
  - handle_get_one_round.get./v5/users/{userId}/rounds/{roundId}
generated: '2026-08-06'
method: generated
source: >-
  openapi/arccos-golf-on-course-data-api-openapi.yml + the published Webhooks section of
  https://api.arccosgolf.com/swagger.json
---

# Subscribe to Arccos round webhooks

Webhook registration is a **client-level** operation authenticated with HTTP **Basic** credentials — not
with a golfer's OAuth token.

## Steps

1. **Register.** `POST /v5/webhooks` with Basic auth and body `{ "webhookUrl": "https://..." }`.

   The URL must be HTTPS. Use a **dedicated, high-entropy path** and keep it private — Arccos webhook v1
   payloads are **unsigned**, so URL secrecy plus a path check is the only origin control available.

2. **Verify.** `GET /v5/webhooks` returns the registered `Webhook` entries as `{ id, webhookUrl }`.

3. **Consume the events.** Arccos POSTs JSON for four event types:

   | Event | Payload |
   |---|---|
   | `postRound` | `userId`, `roundId`, `courseId`, `courseVersion`, `isEnded` |
   | `patchRound` | `userId`, `roundId`, `courseId`, `courseVersion`, `isEnded` |
   | `deleteRound` | `userId`, `roundId` |
   | `accountDisconnected` | `eventId`, `eventType`, `eventVersion`, `createdAt`, `eventBody{userId, clientId, disconnectedAt, reason}` |

   On `postRound`/`patchRound` with `isEnded`, fetch the round with
   `handle_get_one_round.get./v5/users/{userId}/rounds/{roundId}` using that golfer's access token.

4. **Be idempotent.** Delivery is **at-least-once** and ordering between event types is **not guaranteed**.

   - Dedupe by `eventId` — it is stable across retries of the same event.
   - Retries fan out per queue message: with several registered URLs, a failure on one can redeliver the
     same `eventId` to healthy URLs.
   - A golfer disconnecting twice produces *different* `eventId`s, so also make cleanup idempotent by
     `(userId, clientId)`.
   - Respond `2xx` as soon as the event is durably received; do downstream work asynchronously.

5. **Handle `accountDisconnected`.** Stop using stored Arccos tokens for that `userId` and disable local
   access for the connection. The payload carries no tokens, no email and no user PII.

6. **Stay forward-compatible.** Ignore unknown fields, unknown top-level fields, and unsupported future
   `eventVersion` values unless you have explicitly opted in to that newer contract.

7. **Tear down.** `DELETE /v5/webhooks/{webhookId}` with Basic auth.

## Rules

- Do not treat webhook receipt as authorization — always re-read data with the golfer's own token.
- HMAC signing and secret rotation are named by Arccos as *future* upgrades. Do not build a signature check
  against a header that does not exist yet.

## See also

- `asyncapi/arccos-golf-webhooks.yml` — the full webhook catalog
- `conventions/arccos-golf-conventions.yml` — idempotency contract
- `lifecycle/arccos-golf-lifecycle.yml` — `eventVersion` policy
