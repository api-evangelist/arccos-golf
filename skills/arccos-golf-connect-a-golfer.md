---
name: arccos-golf-connect-a-golfer
description: >-
  Connect an Arccos golfer to your client with the OAuth 2.0 authorization-code flow, resolve their Arccos user
  id from the id_token, and confirm access by reading their profile.
api: Arccos On-Course Data API
base_url: https://api.arccosgolf.com/
operations:
  - handle_get_one_user.get./v5/users/{userId}
generated: '2026-08-06'
method: generated
source: >-
  openapi/arccos-golf-on-course-data-api-openapi.yml + the published Authentication section of
  https://api.arccosgolf.com/swagger.json
---

# Connect an Arccos golfer

Use this before any other Arccos skill. Nothing under `/v5/users/{userId}` works without a delegated
access token, and the `{userId}` value is not something the client picks — it comes out of the id token.

## Prerequisites

- A `client_id` (and `client_secret` if Arccos issued one). Access is restricted; Arccos grants clients
  the privilege of requesting each scope. There is no self-serve signup — contact `john@arccosgolf.com`.
- A registered `redirect_uri`.

## Steps

1. **Send the golfer to Arccos to authorize.**

   `GET https://signin.arccosgolf.com/login?response_type=code&client_id=<client id>&redirect_uri=<redirect uri>&scope=<scopes>`

   Request every scope you will ever need in this one call. Scopes **cannot be added retroactively** —
   a missing scope means sending the golfer through the whole flow again.

   - `openid` is mandatory for every operation whose path contains `{userId}` — which is all of them
     except the course catalog.
   - Add `arccos/read:rounds`, `arccos/read:clubs`, `arccos/read:users` as needed.

2. **Exchange the code for tokens.**

   `POST https://api.arccosgolf.com/oauth2/token`, `Content-Type: application/x-www-form-urlencoded`, with
   `grant_type=authorization_code`, `code`, `client_id`, `redirect_uri`, and `client_secret` if issued.

   The code is single-use. If you lose the response, restart at step 1.

3. **Resolve the Arccos user id.** Decode the `id_token` and read the `custom:arccosUserId` claim. That
   string is the `{userId}` path parameter. The `id_token` **cannot** authenticate requests — only
   `access_token` can.

4. **Confirm access.** Call `handle_get_one_user.get./v5/users/{userId}` with
   `Authorization: Bearer {access_token}`. A 200 returns `userId`, `firstName`, `lastName`, `email`,
   `stance`, `gender`, `estimatedHandicap`.

5. **Keep the connection alive.** Access tokens are short-lived. Refresh with
   `POST /oauth2/token` and `grant_type=refresh_token`. Revoke at `POST /oauth2/revoke` with either the
   refresh token or `arccos_user_id` (which revokes every token for that golfer).

## Rules

- Store `refresh_token` encrypted and treat `email` + name fields as PII (see `data-model/`).
- A 401 body is always `{"error":{"code":40101,"description":"No Authorization header passed."}}`. The API
  returns 401 for unknown paths too, so a 401 is not evidence the resource exists.
- When you receive an `accountDisconnected` webhook for a `userId`, stop using stored tokens for that
  golfer immediately and disable local access.

## See also

- `authentication/arccos-golf-authentication.yml`
- `scopes/arccos-golf-scopes.yml`
- `errors/arccos-golf-problem-types.yml`
