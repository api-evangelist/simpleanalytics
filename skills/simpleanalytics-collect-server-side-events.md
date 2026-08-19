---
name: simpleanalytics-collect-server-side-events
description: Send server-side events and page views to Simple Analytics from a backend or mobile app, including custom metadata — and avoid the robot filter that silently drops them.
api: Simple Analytics Events API
operations:
  - collectEvent
generated: '2026-08-13'
method: generated
source: openapi/simpleanalytics-events-api-openapi.yml, https://docs.simpleanalytics.com/events/server-side, https://docs.simpleanalytics.com/metadata
---

# Collect server-side events

Write path. No credentials, no idempotency, no undo.

## Endpoint

`collectEvent` — `POST https://queue.simpleanalyticscdn.com/events`

Note the host: collection goes to `queue.simpleanalyticscdn.com`, **not** to
`simpleanalytics.com` where the read APIs live.

`Content-Type: application/json`. No `Api-Key` and no `User-Id` — the
`hostname` in the body is the routing key.

## Event payload

```json
{
  "type": "event",
  "hostname": "example.com",
  "event": "event-name",
  "ua": "User Agent"
}
```

## Page view payload

```json
{
  "type": "pageview",
  "hostname": "example.com",
  "event": "pageview",
  "path": "/page-name",
  "ua": "User Agent"
}
```

## Optional fields

`path`, `unique`, `https`, `referrer`, `viewport_width`, `viewport_height`,
`screen_width`, `screen_height`, `language`, `timezone`, `source`, `campaign`,
`medium`, `content`, and a `metadata` object of your own key/value pairs.

`metadata` is the extension point: those keys come back as `metadata.<key>`
columns in the Export API and can be filtered as `metadata.<key>` in the Stats
API from version 6 onward.

## The user agent rule — get this wrong and nothing is recorded

Requests whose `ua` looks like a bot are classified as robot traffic and the
data point is dropped. **No error is returned.** Avoid anything containing
`bot`, `crawl`, `python-requests/…`, `curl/…`, `node-fetch/…` or `axios/…`.

Send the real end-user agent, or a deliberate custom one:

```
ServerSide/1.0 (+https://www.yourwebsite.com/)
```

## Steps

1. Choose `type`: `event` or `pageview`.
2. Set `hostname` to a site you actually own and track — there is no test or
   discard hostname, and anything you send lands in that dashboard within
   minutes.
3. Set a non-bot `ua`.
4. Attach `metadata` for anything you want to filter or export on later.
5. POST, then verify in the Events Explorer or via the export skill. Do not
   retry blind.

## Verify

```
GET https://simpleanalytics.com/api/export/datapoints?version=6&format=json&hostname=example.com&type=events&start=today&end=today
```

## Do not

- **Do not retry a request whose outcome you did not read.** There is no
  `Idempotency-Key` header and no deduplication, so a retried POST is counted
  as a second event and inflates the customer's numbers *and* their bill —
  events consume the plan's monthly data-point allowance.
- Do not use a test hostname you do not own; the payload names the destination
  dashboard.
- Do not treat a 2xx as proof of recording — the robot filter drops after
  acceptance.
- Do not send personal data. The whole product is built on collecting none, and
  `metadata` is the one field where a caller could break that; keep it to
  non-identifying values.
