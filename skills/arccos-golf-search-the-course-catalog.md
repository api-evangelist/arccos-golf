---
name: arccos-golf-search-the-course-catalog
description: >-
  Search the Arccos public golf-course catalog by name and resolve a course to its versioned hole and tee
  geometry. The only part of the Arccos API callable with no credentials.
api: Arccos On-Course Data API
base_url: https://api.arccosgolf.com/
operations:
  - handle_search_courses.get./v5/courses
  - handle_get_one_course.get./v5/courses/{courseId}
  - handle_get_one_course_version.get./v5/courses/{courseId}/versions/{courseVersion}
generated: '2026-08-06'
method: generated
source: >-
  openapi/arccos-golf-on-course-data-api-openapi.yml, verified live against
  https://api.arccosgolf.com/v5/courses on 2026-08-06
---

# Search the Arccos course catalog

These three operations declare **no security requirement** and were confirmed callable with no
`Authorization` header on 2026-08-06. Everything else on `api.arccosgolf.com` returns
`401 {"error":{"code":40101,...}}`.

## Steps

1. **Search by name.**

   `GET /v5/courses?name=Pebble&limit=2`

   Verified response shape (2026-08-06):

   ```json
   {"results":[{"courseId":540,"courseVersion":6,"name":"Pebblebrook GC","numberOfHoles":18,
   "mensPar":72,"womensPar":72,"location":{"latitude":33.653835586098,"longitude":-112.332383950485},
   "city":"Sun City West","state":"AZ","country":"US","altitude":368.14,"holes":[...],"tees":[...]}],
   "paging":{"limit":2,"offset":0}}
   ```

   `name` is a **partial** match. Paginate with `limit`/`offset`; default `limit` is 10; there is no total
   count and no cursor.

2. **Resolve one course.** `GET /v5/courses/{courseId}` returns the current version.

3. **Pin a version.** `GET /v5/courses/{courseId}/versions/{courseVersion}` returns the exact geometry a
   historic round was played against. A `Round` carries both `courseId` and `courseVersion` — always use
   both when reconstructing a round.

## What you get

- `Course` — `courseId`, `courseVersion`, `name`, `numberOfHoles`, `mensPar`, `womensPar`, `location`
  (lat/lon), `city`, `state`, `country`, `altitude` (metres), `holes`, `tees`
- `CourseHole` — `holeId`, `mensPar`, `womensPar`
- `Tee` — `teeId`, `teeName`

## Rules

- An empty `results` array is a normal answer — a bare `GET /v5/courses` returns
  `{"results":[],"paging":{"limit":10,"offset":0}}`. Always pass `name`.
- No rate limits are published and no rate-limit headers are returned. Because this surface is anonymous,
  be conservative: serialize requests and cache aggressively by `(courseId, courseVersion)`, which is
  immutable.
- `HEAD` is not supported the way `GET` is — a `HEAD /v5/courses` returns 401. Use `GET`.

## See also

- `conventions/arccos-golf-conventions.yml`
- `data-model/arccos-golf-data-model.yml`
