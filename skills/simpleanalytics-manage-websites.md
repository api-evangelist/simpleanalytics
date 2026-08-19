---
name: simpleanalytics-manage-websites
description: List the websites in a Simple Analytics account and add a new one, including timezone, public/private visibility and label — with the plan upgrade that adding one triggers.
api: Simple Analytics Admin API
operations:
  - listWebsites
  - addWebsite
generated: '2026-08-13'
method: generated
source: openapi/simpleanalytics-websites-api-openapi.yml, https://docs.simpleanalytics.com/api/admin, https://docs.simpleanalytics.com/api/authenticate
---

# Manage websites

The Admin API. Two operations, one safe and one billable.

## Credentials

Both operations require **both** headers:

```
Api-Key: sa_api_key_…
User-Id: sa_user_id_<UUIDv4>
```

Both are shown in account settings. The portion of `User-Id` after the prefix
must be a valid UUIDv4 or the call fails.

## listWebsites — safe

`GET https://simpleanalytics.com/api/websites`

The only Admin endpoint available on every plan. Returns all websites for the
user; the team ID has no effect on it. Use it to resolve a hostname before
calling the Stats or Export skills.

```
curl "https://simpleanalytics.com/api/websites" \
  -H 'Content-Type: application/json' \
  -H 'Api-Key: sa_api_key_…' \
  -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000'
```

## addWebsite — CONSEQUENTIAL, confirm with a human first

`POST https://simpleanalytics.com/api/websites/add`

**This endpoint changes the bill.** The documentation states that a Business or
Enterprise plan is required and that *the account will be upgraded
automatically when the endpoint is used*. Treat it as a purchasing action:
never call it speculatively, never call it in a retry loop, and get explicit
confirmation before the first call.

Body:

```json
{
  "public": false,
  "hostname": "example.com",
  "timezone": "Europe/Amsterdam",
  "label": "customer note"
}
```

| Field | Notes |
|---|---|
| `hostname` | Required. The website to track. |
| `public` | Boolean. `true` makes the dashboard — and both read APIs — answer anonymously for this hostname. Choose deliberately. |
| `timezone` | A tz database name. Defaults to `UTC` if omitted. |
| `label` | Optional free string shown on the websites overview. Strings only. |

## Steps

1. Call `listWebsites` first and check whether the hostname already exists.
2. If it does not, surface the plan-upgrade consequence to the human and wait.
3. On approval, POST with an explicit `timezone` and an explicit `public` value.
4. Call `listWebsites` again to confirm — there is no idempotency key, so
   verifying beats retrying.

## Errors

Admin errors use `{"success": false, "error": "…"}` and arrive as **HTTP 400,
not 401**, including for missing credentials:

- `No Api-Key found, specify via header`
- `No User-Id defined`
- `Invalid user id format, it should be a UUIDv4`

## Do not

- Do not retry a failed `addWebsite` blind — the API supports no
  `Idempotency-Key` and no replay semantics, so a retry can create duplicate
  state and a duplicate upgrade path.
- Do not set `public: true` without asking; it exposes the site's stats and raw
  data points to anonymous callers.
- Do not assume 400 means "bad request body" — on this API it is also what an
  auth failure looks like.

## Beyond the published surface

The Admin docs note that custom endpoints are built for larger customers on
request, so a given account's real Admin surface may be wider than this
contract. Ask before assuming an operation does not exist.
