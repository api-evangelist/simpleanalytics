# Simple Analytics (simpleanalytics)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Simple Analytics is a privacy-first, cookieless web analytics platform built in the EU. It collects no personal data and needs no cookie banner, while exposing a REST API to pull aggregated dashboard stats, export raw data points (page views and events), collect custom events server-side, and manage the websites in an account.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/simpleanalytics/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/simpleanalytics/refs/heads/main/apis.yml)

## Tags

- Analytics
- Web Analytics
- Privacy
- Cookieless
- GDPR

## Timestamps

- **Created:** 2026-06-21
- **Modified:** 2026-06-21

## APIs

### Simple Analytics Stats API

Returns the aggregated statistics shown in the dashboard as JSON - pageviews, visitors, histogram, pages, countries, referrers, UTM dimensions, and device/browser breakdowns - filterable by date range, page, country, referrer, and UTM parameters.

- **Human URL:** [https://docs.simpleanalytics.com/api/stats](https://docs.simpleanalytics.com/api/stats)
- **Base URL:** `https://simpleanalytics.com`

#### Tags

- Stats
- Aggregated
- Page Views
- Referrers
- UTM

#### Properties

- [Documentation](https://docs.simpleanalytics.com/api/stats)
- [API Reference](https://docs.simpleanalytics.com/api)
- [OpenAPI](openapi/simpleanalytics-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/simpleanalytics.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/simpleanalytics.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Simple Analytics Export API

Exports raw, per-event data points (pageviews or events) for a hostname as CSV or JSON, with selectable fields and hourly or daily date granularity. Requires an Api-Key and User-Id and a Business or Enterprise plan.

- **Human URL:** [https://docs.simpleanalytics.com/api/export-data-points](https://docs.simpleanalytics.com/api/export-data-points)
- **Base URL:** `https://simpleanalytics.com`

#### Tags

- Export
- Data Points
- Raw Data
- Events

#### Properties

- [Documentation](https://docs.simpleanalytics.com/api/export-data-points)
- [OpenAPI](openapi/simpleanalytics-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/simpleanalytics.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/simpleanalytics.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Simple Analytics Events API

Collects custom events and pageviews server-side by POSTing a JSON payload (event type, hostname, path, optional metadata) to the collection endpoint, mirroring what the client-side sa_event() function sends.

- **Human URL:** [https://docs.simpleanalytics.com/events/server-side](https://docs.simpleanalytics.com/events/server-side)
- **Base URL:** `https://queue.simpleanalyticscdn.com`

#### Tags

- Events
- Collect
- Server Side

#### Properties

- [Documentation](https://docs.simpleanalytics.com/events/server-side)
- [API Reference](https://docs.simpleanalytics.com/events)
- [OpenAPI](openapi/simpleanalytics-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/simpleanalytics.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/simpleanalytics.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Simple Analytics Websites API

Admin endpoints to list the websites in an account and add a new website (hostname, timezone, public flag, label). Listing works on all plans; adding requires a Business or Enterprise plan.

- **Human URL:** [https://docs.simpleanalytics.com/api/admin](https://docs.simpleanalytics.com/api/admin)
- **Base URL:** `https://simpleanalytics.com`

#### Tags

- Websites
- Admin
- Management

#### Properties

- [Documentation](https://docs.simpleanalytics.com/api/admin)
- [OpenAPI](openapi/simpleanalytics-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/simpleanalytics.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/simpleanalytics.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/simpleanalytics)
- [LinkedIn](https://www.linkedin.com/company/simpleanalytics)
- [Website](https://www.simpleanalytics.com)
- [Documentation](https://docs.simpleanalytics.com/api)
- [Plans](plans/simpleanalytics-plans-pricing.yml)
- [Rate Limits](rate-limits/simpleanalytics-rate-limits.yml)
- [Fin Ops](finops/simpleanalytics-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
