# Arccos Golf

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Arccos Golf is the golf performance-tracking platform behind the Arccos Caddie smart sensors, smart grips and the Arccos Air wearable — the Official Game Tracker of the PGA TOUR. Club-mounted sensors and the Arccos mobile app automatically capture every shot on the course, then AI-driven Strokes Gained analytics, Smart Club Distances, an AI rangefinder and Arccos Caddie strategy turn that shot data into per-round and per-hole insight. Arccos exposes that same data to approved third parties through the Arccos On-Course Data API, a Swagger 2.0-documented REST API over rounds, round stats, clubs, users and a public course/course-version catalog, secured with an OAuth 2.0 authorization-code flow and per-resource read scopes, plus registerable HTTPS webhooks for round and account-disconnect events. Its Shopify-hosted storefront additionally publishes an llms.txt and a Universal Commerce Protocol (UCP) MCP endpoint for agent-driven commerce.

**Areas:** Company · Golf · Sports Technology · Wearables · IoT · shot-tracking · Sports Analytics · Performance Analytics · Geospatial · Consumer Hardware · Webhook · Authentication

## Arccos Golf on APIs.io

Everything profiled for Arccos Golf is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/arccos-golf/](https://apis.io/providers/arccos-golf/)** — or go straight to one of the APIs or properties below.

### APIs (6)

- [Arccos Golf Storefront UCP MCP Server](https://apis.io/apis/arccos-golf/arccos-golf-storefront-ucp-mcp-server/) — Universal Commerce Protocol (UCP) MCP endpoint published on the Arccos Golf Shopify storefront for agent-driven commerce. An anonymous JSON-RPC tools/list…
- [Arccos Golf Clubs API](https://apis.io/apis/arccos-golf/arccos-golf-clubs-api/) — The Clubs API from Arccos Golf — 2 operation(s) for clubs.
- [Arccos Golf Courses API](https://apis.io/apis/arccos-golf/arccos-golf-courses-api/) — The Courses API from Arccos Golf — 3 operation(s) for courses.
- [Arccos Golf Rounds API](https://apis.io/apis/arccos-golf/arccos-golf-rounds-api/) — The Rounds API from Arccos Golf — 3 operation(s) for rounds.
- [Arccos Golf Users API](https://apis.io/apis/arccos-golf/arccos-golf-users-api/) — The Users API from Arccos Golf — 1 operation(s) for users.
- [Arccos Golf Webhooks API](https://apis.io/apis/arccos-golf/arccos-golf-webhooks-api/) — The Webhooks API from Arccos Golf — 2 operation(s) for webhooks.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Arccos Golf Webhooks](https://apis.io/asyncapis/arccos-golf/arccos-golf-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Arccos Golf Storefront UCP MCP Server](https://apis.io/servers/arccos-golf/arccos-golf-storefront-ucp-mcp-server/)

#### Collections (6)

Postman and Open Collection request collections.

- [Arccos On-Course Data Clubs API](https://apis.io/collections/arccos-golf/open-arccos-golf-clubs-api/)
- [Arccos On-Course Data Courses API](https://apis.io/collections/arccos-golf/open-arccos-golf-courses-api/)
- [Arccos On-Course Data API](https://apis.io/collections/arccos-golf/open-arccos-golf-on-course-data-api/)
- [Arccos On-Course Data Rounds API](https://apis.io/collections/arccos-golf/open-arccos-golf-rounds-api/)
- [Arccos On-Course Data Users API](https://apis.io/collections/arccos-golf/open-arccos-golf-users-api/)
- [Arccos On-Course Data Webhooks API](https://apis.io/collections/arccos-golf/open-arccos-golf-webhooks-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Arccos Golf On Course Data Api Overlay](https://apis.io/overlays/arccos-golf/arccos-golf-on-course-data-api-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Arccos Golf Authentication](https://apis.io/security/arccos-golf/arccos-golf-authentication/)
- [Arccos Golf Domain Security](https://apis.io/security/arccos-golf/arccos-golf-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Arccos Golf Scopes](https://apis.io/scopes/arccos-golf/arccos-golf-scopes/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.arccosgolf.com/)
- [Documentation](https://api.arccosgolf.com/swagger)
- [Getting started](https://github.com/arccosgolf/on-course-data-api-example-front-end)
- [API reference](https://api.arccosgolf.com/swagger)
- [Sign up](https://www.arccosgolf.com/account/register)
- [Support](https://www.arccosgolf.com/pages/contact)
- [Blog](https://www.arccosgolf.com/blogs/community)
- [Terms of service](https://www.arccosgolf.com/policies/terms-of-service)
- [Privacy policy](https://www.arccosgolf.com/policies/privacy-policy)
- [GitHub](https://github.com/arccosgolf)

## API Evangelist rating

**Kin Score 41.8** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.7 |
| Contract quality | 45.9 |
| Contract governance | 4.5 |
| Operational transparency | 10.5 |
| Developer ergonomics | 61.3 |
| Access clarity | 34.2 |

**Agent readiness 41.5** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | platform (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | — |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | — |
| Agentic Commerce | platform (partial credit) |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 34.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/arccos-golf/](https://apis.io/providers/arccos-golf/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Arccos Golf: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/arccos-golf/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
