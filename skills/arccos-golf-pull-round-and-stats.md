---
name: arccos-golf-pull-round-and-stats
description: >-
  Page a golfer's Arccos rounds, pull one round's per-hole shot detail, and fetch its Strokes Gained and
  traditional stats against a goal handicap.
api: Arccos On-Course Data API
base_url: https://api.arccosgolf.com/
operations:
  - handle_search_rounds.get./v5/users/{userId}/rounds
  - handle_get_one_round.get./v5/users/{userId}/rounds/{roundId}
  - handle_get_round_stats.get./v5/users/{userId}/rounds/{roundId}/stats
  - handle_get_one_course_version.get./v5/courses/{courseId}/versions/{courseVersion}
generated: '2026-08-06'
method: generated
source: openapi/arccos-golf-on-course-data-api-openapi.yml
---

# Pull a round and its stats

Requires a connected golfer with the `openid` and `arccos/read:rounds` scopes — run
`arccos-golf-connect-a-golfer` first.

## Steps

1. **Page the rounds.**

   `GET /v5/users/{userId}/rounds?limit=&offset=`

   Pagination is limit/offset with a `{ "results": [...], "paging": { "limit", "offset" } }` envelope.
   There is **no total count and no cursor** — page until `results` comes back shorter than `limit`, and
   remember `offset` is the only position you have. Default `limit` is 10.

   Each `Round` carries `roundId`, `userId`, `startTime`, `endTime`, `totalScore`, `courseId`,
   `courseVersion`, `courseName`, `numberOfHoles`, `tee`.

2. **Pull the round detail.**

   `GET /v5/users/{userId}/rounds/{roundId}`

   Returns `RoundDetails` — the `Round` plus `RoundHole` entries, each composed of the `Hole`, the `Pin`
   `Location`, `HoleStat` entries, and the `Shot` list. Each `Shot` names `clubId`, `clubType`,
   `startLocation`/`endLocation`, `shotDistance`, `startTerrain`/`endTerrain`, penalties and
   fairway/centerline geometry. **Distances are metres.**

3. **Fetch the stats.**

   `GET /v5/users/{userId}/rounds/{roundId}/stats?goalHandicap=`

   `goalHandicap` accepts −30 to 10; a golfer targeting 20-over-par enters −20. Omitting it assumes 0
   (scratch). The response is `RoundStats` — `overall`, `driving`, `approach`, `short`, `putt` — where each
   breakdown mixes a Strokes Gained comparison (`actualVsTarget`, `actualVsScratch`) with traditional
   comparisons (`actual`, `goal`, `scratch`).

4. **Resolve the course geometry (optional, no auth needed).**

   `GET /v5/courses/{courseId}/versions/{courseVersion}` — pass **both** ids from the round. A course is
   versioned so a historic round keeps the hole pars and tees it was actually played against. This call
   needs no token.

## Rules

- Never re-derive stats client-side from shots; use the stats operation so you match what the golfer sees
  in the Arccos app.
- Treat `(courseId, courseVersion)` as one key. Looking up `courseId` alone returns the current version,
  which may not be the one the round was played on.
- Only 200 is declared in the spec. Handle the real error envelope:
  `{"error":{"code":<int>,"description":"..."}}`.
- No rate-limit policy or headers are published. Back off conservatively on any non-200.

## See also

- `conventions/arccos-golf-conventions.yml` — pagination and error envelope
- `data-model/arccos-golf-data-model.yml` — the Round → RoundHole → Shot → Club graph
