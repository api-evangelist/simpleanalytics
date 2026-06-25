# Simple Analytics (simpleanalytics)

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
