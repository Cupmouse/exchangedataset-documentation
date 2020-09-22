# Snapshot Endpoint

## About

Snapshot Endpoint returns snapshots to reconstruct the initial states for channels that have "state".

Such channels are usually orderbook channel which requires initial book orders to reconstruct the full orderbook since almost all exchange only send difference in orderbook in real-time, not full orderbook.

It also returns subscription message if specified channels are recorded which can be used to check if the target channel are recorded.

## URL

```url
https://api.exchangedataset.cc/v1/snapshot/<exchange>/<nanosec>?channels=<channels>&format=<format>
```

## Quota Use

!> **All query to Snapshot Endpoint consume quota by scanned bytes, not returned bytes.**

Scanned bytes are calculated by how much data it had to lookup to take snapshot for a query.

If your query required the endpoint to look for 5,000,000 bytes of original datasets and returned a snapshot of 1,000 bytes, then you will be charged for 5,000,000 bytes.

Be careful if you want to make a CSV file for a orderbook channel.

Each request will consume at least 1024bytes (1kb) of quota.

## Parameters

`type[]` describes Query Parameter that could appear multiple times so as to specify multiple values.

If default value are not defined, you have to provide one.

| Parameter  | Type       | Description                                                        | Default Value    |
| ---------- | ---------- | ------------------------------------------------------------------ | ---------------- |
| `exchange` | `string`   | Name of exchange, case sensitive                                   | ✗None (Required) |
| `channels` | `string[]` | Name of channel, could be specified more than once, case sensitive | ✗None (Required) |
| `nanosec`  | `integer`  | Time of snapshot in nanosec from `1970-1-1 00:00:00.000000000Z`    | ✗None (Required) |
| `format`   | `string`   | What format response will be formatted into, case sensitive        | `raw`            |

## Response

By checking HTTP Status Code of the response, you can test if the query are successfully processed in the endpoint.

### `200 OK`

Query is processed normally.
Body is the response.

Successful response comes with a additional header:

#### Additional Header

| Header                  | Description                                 |
| ----------------------- | ------------------------------------------- |
| `ExcDataset-Quota-Used` | Amount of quota used by this query in bytes |

This header is for giving more transparency to show our system is not reporting/cheating quota value in our favor.

### `404 Not Found`

Query could not be processed because datasets are missing or requested `nanosec` is in future.
Body is empty.

### `403 Forbidden`

Authentication failed.
See [Authentication](http/authentication.md).

## Example of Query URLs

### Example 1

Bitmex orderBookL2 snapshot at `2020-5-10 09:14:48.123456789` (1589102088123456789) in raw format

```url
https://api.exchangedataset.cc/v1/snapshot/bitmex/1589102088123456789?channels=orderBookL2
```

### Example 2

Bitmex orderBookL2 and instrument snapshot at `2020-5-10 09:14:48.123456789` in json format

```url
https://api.exchangedataset.cc/v1/snapshot/bitmex/1589102088123456789?channels=orderBookL2&channels=instrument&format=json
```

## A Peek At Internal Process

Given a query, Snapshot Endpoint will process original datasets that are least needed to take snapshot.

Internal snapshot are taken every 10 minutes in advance to the query and stored in original datasets so it will lookup datasets up to 10 minutes.

An State Tracker is initialized with the internal snapshot, and it continues reading original datasets thereafter, changing internal state, until it finds the line with timestamp that exceeds the specified `nanosec`, then it returns the state.
