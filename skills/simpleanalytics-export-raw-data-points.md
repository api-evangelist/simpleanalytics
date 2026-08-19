---
name: simpleanalytics-export-raw-data-points
description: Export raw, unsampled Simple Analytics data points — individual page views and events with their full field set — as JSON or CSV over a date range.
api: Simple Analytics Export API
operations:
  - exportDataPoints
generated: '2026-08-13'
method: generated
source: openapi/simpleanalytics-export-api-openapi.yml, https://docs.simpleanalytics.com/api/export-data-points, https://docs.simpleanalytics.com/api/helpers
---

# Export raw data points

Pull individual page views and events, not aggregates. This is the endpoint
that backs warehouse loads and BI pipelines.

## Endpoint

`exportDataPoints` — `GET https://simpleanalytics.com/api/export/datapoints`

## Before you call

- Private websites need `Api-Key: sa_api_key_…` **and** a Business or
  Enterprise plan.
- Public websites answer anonymously — verified 2026-08-13 against
  `hostname=simpleanalytics.com`.
- Retention bounds what exists: the free plan keeps one month of history, paid
  retention is set by plan. A range older than retention returns nothing, not
  an error.

## Required parameters

| Parameter | Required | Notes |
|---|---|---|
| `version` | yes | `6` |
| `format` | yes | `csv` or `json` |
| `hostname` | yes | The website to export |
| `type` | yes | `pageviews` or `events` |
| `start` / `end` | yes | `YYYY-MM-DD` or placeholders (`today-30d`, `yesterday`) |
| `fields` | no | Comma-separated column allow-list; omit for the default set |
| `timezone` | no | Defaults to **UTC** on this API (the Stats API defaults to the website setting instead) |

## Available fields

`added_unix`, `added_iso`, `hostname`, `hostname_original`, `path`, `query`,
`is_unique`, `is_robot`, `document_referrer`, `utm_source`, `utm_medium`,
`utm_campaign`, `utm_content`, `utm_term`, `scrolled_percentage`,
`duration_seconds`, `viewport_width`, `viewport_height`, `screen_width`,
`screen_height`, `user_agent`, `device_type`, `country_code`, `browser_name`,
`browser_version`, `os_name`, `os_version`, `lang_region`, `lang_language`,
`uuid`, `session_id`, and any `metadata.<key>` the customer defines.

## Steps

1. Decide `type` — page views and events are separate exports.
2. Pick an explicit `fields` list. Narrower exports are dramatically smaller
   and there is no pagination to fall back on.
3. Set `timezone` explicitly so repeat runs bucket identically.
4. Chunk the range. A single call returns the whole window in one response,
   uncapped and unpaginated, with no documented size ceiling. Day-at-a-time or
   week-at-a-time is the safe pattern for a large site.
5. Use `format=csv` for warehouse loads, `format=json` when you need to read
   `metadata.*` structurally.

## Example

```
GET https://simpleanalytics.com/api/export/datapoints?version=6&format=json&hostname=example.com&type=pageviews&start=2026-08-01&end=2026-08-02&timezone=UTC
```

## Identity fields — read this before you model the data

- There is **no visitor identifier**. No cookies, no fingerprints, no profiles.
- `session_id` is a **legacy field name**. The current concept is a *page-load
  ID*: it groups rows within one page load only, is never stored on the
  device, and does not survive a reload or navigation. It is kept under the old
  name purely so existing exports do not break. Do not treat it as a session.
- `uuid` is per data point and the docs warn it "is not always unique" — it is
  not a primary key.
- `is_robot` is already computed; filter on it rather than re-deriving from
  `user_agent`.

## Do not

- Do not build visitor-level joins — the data intentionally cannot support them.
- Do not request a multi-month range in one call on a high-traffic site.
- Do not hand-build the URL if a human can generate it instead: the dashboard's
  export interface emits a correct URL with the fields already selected.
