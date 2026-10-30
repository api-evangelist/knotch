# Knotch

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

Knotch is a New York-based content intelligence company founded by Anda Gansca and Aron Tzimas. Its Knotch One platform measures and optimizes owned-content performance for enterprise marketing teams, and its newer product, Ace, is positioned as AI experience infrastructure for the conversational web: it ingests a brand's existing web properties, content hubs, video and feeds, atomizes them into modular content units tagged by topic, audience, funnel stage and intent, then composes adaptive page experiences for human visitors while emitting structured, citable content for AI agents and answer engines. Named enterprise customers include Google, Deloitte, Ally, Zillow, Cox Automotive, GEICO, Synchrony, Square, Dropbox, FOX and Chime. Knotch does publish a developer surface, on two hosts that are not linked from the marketing site: docs.knotch.it documents the browser-side Measurement Unit API, Event Pixel and Verification Pixel, and help.knotch.com documents the server-side Knotch Events API v1.1, which accepts batched conversion events over HTTPS with Bearer authentication and is backed by a live OpenAPI 3.1.0 definition served at https://events.knotch.it/openapi.json. Credentials are issued by Client Success rather than self-service, and no pricing, status page, changelog, SDK or public GitHub organization is published.

**Areas:** Company · Content Intelligence · Content Marketing · Analytics · Artificial Intelligence · Personalization · Marketing Technology · Agentic Web · Conversion Tracking · Attribution · Event Ingestion · Web Analytics

## Knotch on APIs.io

Everything profiled for Knotch is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/knotch/](https://apis.io/providers/knotch/)** — or go straight to one of the APIs or properties below.

### APIs (5)

- [Knotch Events API](https://apis.io/apis/knotch/events-api/) — Server-side conversion event ingestion. Accepts batches of up to 100 events over HTTPS with Bearer authentication, so conversions that happen off-site (CRM…
- [Knotch Measurement Unit API](https://apis.io/apis/knotch/unit-api/) — Browser-side JavaScript API exposed by the Knotch tag for controlling Measurement Units on a page at runtime: Knotch.addUnit(), Knotch.removeUnit(),…
- [Knotch Event Pixel](https://apis.io/apis/knotch/event-pixel/) — HTTP beacon endpoint for signalling arbitrary events from a web page — conversion events, site journey steps and visitor signals. A single GET to the…
- [Knotch Verification Pixel](https://apis.io/apis/knotch/verification-pixel/) — Publisher traffic verification tag, a component of Knotch Blueprint. A single script element carrying a data-kvpid attribute, fired once on document onLoad,…
- [Knotch Health API](https://apis.io/apis/knotch/knotch-health-api/) — The Health API from Knotch — 1 operation(s) for health.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [knotch-mcp.yml](https://apis.io/servers/knotch/knotch-mcp-yml/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Knotch Events Api Overlay](https://apis.io/overlays/knotch/knotch-events-api-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Knotch Authentication](https://apis.io/security/knotch/knotch-authentication/)
- [Knotch Domain Security](https://apis.io/security/knotch/knotch-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Knotch Plans Pricing](https://apis.io/plans/knotch/knotch-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Knotch Rate Limits](https://apis.io/rate-limits/knotch/knotch-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://knotch.com/)
- [Documentation](https://docs.knotch.it/)
- [Getting started](https://help.knotch.com/en/collections/1-getting-started)
- [API reference](https://help.knotch.com/en/articles/159-events-api-v11-technical-overview)
- [Support](https://help.knotch.com/)
- [Privacy policy](https://knotch.com/legal/privacy-policy)

## API Evangelist rating

**Kin Score 35.6** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 41.0 |
| Contract governance | 4.5 |
| Operational transparency | 21.1 |
| Developer ergonomics | 63.7 |
| Access clarity | 10.5 |

**Agent readiness 27.9** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | yes |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 19.1** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/knotch/](https://apis.io/providers/knotch/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Knotch: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/knotch/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
