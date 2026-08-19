---
name: simpleanalytics-pull-website-stats
description: Pull aggregated traffic statistics for a Simple Analytics website — pageviews, visitors, histogram, top pages, countries, referrers and UTM breakdowns — for a date range.
api: Simple Analytics Stats API
operations:
  - getStats
generated: '2026-08-13'
method: generated
source: openapi/simpleanalytics-stats-api-openapi.yml, https://docs.simpleanalytics.com/api/stats, https://docs.simpleanalytics.com/api/helpers
---

# Pull website stats

Read the numbers the Simple Analytics dashboard shows, as JSON.

## Endpoint

`getStats` — `GET https://simpleanalytics.com/{hostname}.json`

The hostname *is* the path. For `example.com` the URL is
`https://simpleanalytics.com/example.com.json`.

## Before you call

- If the website is **public**, no credentials are needed.
- If it is **private**, send `Api-Key: sa_api_key_…`.
- You do not need `User-Id` for this API.
- Confirm the hostname is tracked with the `listWebsites` skill if a call 404s.

## Required parameters

`fields` is **required**. Omitting it returns HTTP 400 with
`{"ok": false, "error": "Fields param is required…"}` — it does not default to
everything.

| Parameter | Notes |
|---|---|
| `fields` | Comma-separated: `pageviews`, `visitors`, `histogram`, `pages`, `countries`, `referrers`, `utm_sources`, `utm_mediums`, `utm_campaigns`, `utm_contents`, `utm_terms`, `browser_names`, `os_names`, `device_types`, `seconds_on_page` |
| `version` | Always send `6`. Versions 1–5 still answer but are older shapes. |
| `start` / `end` | `YYYY-MM-DD`, or the placeholders `today`, `yesterday`, `today-1d`, `today-30d` |
| `timezone` | e.g. `Europe/Amsterdam`. Defaults to the website's own setting — pin it if you want stable results. |
| `limit` | 1–1000, caps entries per list field. Not a page size; there is no pagination. |
| `interval` | For `histogram`: `hour`, `day`, `week`, `month`, `year` (`hour` needs version 6) |
| `info` | Set `false` to strip the `__`-prefixed explanatory keys from the response |

## Steps

1. Build the URL: `https://simpleanalytics.com/<hostname>.json`.
2. Add `version=6`, your `fields` list, `start`, `end` and `timezone`.
3. Send `Api-Key` if the site is private.
4. Check `ok` in the response body before reading any figure — the Stats API
   returns `{"ok": false, "error": …}` on failure, sometimes with HTTP 400.
5. Read `generated_in_ms` if you care about query cost; wide ranges with many
   list fields are the slow ones.

## Last 30 days, headline numbers

```
GET https://simpleanalytics.com/example.com.json?version=6&fields=pageviews,visitors&start=today-30d&end=yesterday&timezone=UTC
```

## Filtering

Add any of `page`, `pages` (`/contact,/product/*`), `country`, `referrer`,
`utm_source`, `utm_medium`, `utm_campaign`, `utm_content`, `utm_term`,
`browser_name`, `os_name`, `device_type`, or `metadata.<key>` (version 6+).

## Errors

Three envelopes exist on this API family — do not write one parser:

- `{"ok": false, "error": "…"}` — bad or missing parameters, HTTP 400
- `{"status": 404, "message": "/example.com.json"}` — hostname is not a known
  Simple Analytics website
- Admin-style `{"success": false, "error": "…"}` on `/api/*` paths

Auth failures come back as **400, not 401**. See
`errors/simpleanalytics-problem-types.yml`.

## Do not

- Do not paginate — there is no cursor. Narrow with `start`/`end` instead.
- Do not assume a missing `fields` list returns everything.
- Do not pattern-match on error message text; the strings are prose and one of
  them contains a typo (`seperated`).
