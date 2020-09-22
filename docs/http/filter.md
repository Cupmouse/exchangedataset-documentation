# Filter Endpoint

Filter Endpoint returns one minute of filtered data from specified date and minute.

This is the only Endpoint that returns stream of dataset.

It filters so you can save your quota by only filtering-in channels that you need.

## URL

```url
https://api.exchangedataset.cc/v1/filter/<exchange>/<minute>?channels=<channels>&start=<start>&end=<end>&format=<format>
```

## Quota Use

This Endpoint consumes quota by transferred data (=size of response body in bytes).

Orderbook channels only consume 1/10 of normal.

Each request will consume at least 1024bytes (1kb) of quota.

## Parameters

| Name       | Type       | Description                                                                | Default Value        |
| ---------- | ---------- | -------------------------------------------------------------------------- | -------------------- |
| `exchange` | `string`   | Name of exchange, case sensitive                                           | ✗None (Required)     |
| `minute`   | `integer`  | Target minutes from `1970-1-1 00:00Z`                                      | ✗None (Required)     |
| `channels` | `string[]` | Name of channel, could be specified more than once, case sensitive         | ✗None (Required)     |
| `start`    | `integer`  | Datetime to start filter-in in nanosec from `1970-1-1 00:00:00.000000000Z` | 0                    |
| `end`      | `integer`  | Datetime to end filter-in in nanosec from `1970-1-1 00:00:00.000000000Z`   | 18446744073709551615 |
| `format`   | `string`   | What format response will be formatted into, case sensitive                | `raw`                |

## Time Range Filtering

Time Range Filtering are perfomed using timestamp in nanosec and data will be included in the response if below criteria is satisfied:

```javascript
start <= timestamp < end && minute <= timestamp/60/1000000000 < minute + 1
```
