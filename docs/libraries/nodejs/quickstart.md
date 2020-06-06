# Quick Start

## HTTP Module, Raw API and Replay API

`exchangedataset-node` have a low-level API for HTTP Endpoints, medium and high-level streaming API.

### HTTP Module

HTTP Module is a low-level API which provides access to [HTTP Endpoints](http/) via functions named after each HTTP Endpoint.

This is mostly used internally, but exposed in public.

?> Documentation for HTTP Endpoints can be found in [HTTP Endpoints](http/).

### Raw

Raw API is a medium-level API for streaming or downloading data.

It replays market data as string given start date, end date, exchange, format etc. and takes care of all necessary requests to HTTP Endpoints.

!> Raw API does not support client-side pair level filtering. For what channels server-side filtering is not supported for, see [Recorded Exchange/Channels](data/table).

### Replay

Replay API is a high-level API for streaming or downloading data.

It formats market data into object and also supports pair level filtering for all channels.

Other functionalities are same as Raw API.

We recommend to use this API for the most use case other than what requires raw data (same format as what exchanges' streams), since you don't have to format data for yourself.

From now on, we presume that we are using replay API.

## Getting ReplayRequest

To make a request, you need two object:

- `ClientParam`
- `ReplayRequestParam`

`ClientParam` is a parameter used when connecting to HTTP Endpoint, such as API-key and timeout etc.

`ReplayRequestParam` is a parameter specific to a request, which you should provide exchange, channels to filter-in, start date, end date.

By providing two object, you will get `ReplayRequest` which represents the request which is not yet executed.

There is two ways to get `ReplayRequest`:

- By calling `replay.replay(ClientParam, ReplayRequestParam)` function
- Creating `Client` by `createClient(ClientParam)`, then call `client.replay(ReplayRequestParam)` function

Both do the same job, however, `Client` can be reused to make another request, so you don't have to provide `ClientParam` again.

We recommend you to create an client so you don't have to provide API-key for every query you make, which increases security of your app.

## Creating Client

Below code creates a `Client` for later use.

```javascript
const { createClient } = require("exchangedataset-node");

// create client
const client = createClient({
    apikey: "API-key here",
});
```

## Filtering

Multiple exchanges and channels can be specified to be filtered-in:

```javascript
const req = client.replay({
    filter: {
        bitmex: [
            // Replay API supports client-side pair level filtering for Bitmex
            "orderBookL2_XBTUSD",
            "trade_XBTUSD",
        ],
        bitflyer: [
            "lightning_board_FX_BTC_JPY",
            "lightning_executions_FX_BTC_JPY",
        ],
        bitfinex: [
            "orders_tBTCUSD",
            "book_tBTCUSD",
        ],
    },
    start: "2019-05-12 10:00Z",
    end: "2019-05-12 10:01Z",
});
```

You can use prepared builders for supported exchanges to eliminate possible typos.

```javascript
// don't forget to import replay
const { replay } = require("exchangedataset-node");

// prepare request
const req = client.replay({
    filter: {
        bitmex: replay.bitmex()
            .orderBookL2(["XBTUSD"])
            .trade(["XBTUSD"])
            .build(),
        bitflyer: replay.bitflyer()
            .board(["FX_BTC_JPY"])
            .executions(["FX_BTC_JPY"])
            .build(),
        bitfinex: replay.bitfinex()
            .orders(["tBTCUSD"])
            .book(["tBTCUSD"])
            .build(),
    },
    start: "2019-05-12 10:00Z",
    end: "2019-05-12 10:01Z",
});
```

!> Response for channels which is not supported or recorded is empty and produces no error.

## Asynchronous Streaming or Download

Once `ReplayRequest` is obtained, you can get result either by streaming or download.

### Download

Download collects all results from multiple HTTP Endpoint calls into one array.

Theoretically, this is quicker than streaming, due to the overhead of async iterator.

But storing all result takes memory space and is not always the most efficient way, easily crashing NodeJS by out of memory when large request was issued.

**Downloading is recommended only for smaller request.**

### Streaming

Streaming downloads what only needed to fill the buffer as your app goes through the result one-by-one.

The size of buffer is fixed, so it won't cause out of memory.
It can be set by giving 1st parameter to stream function.

Please note that NodeJS does not support multi-threading, only IO/Network is parallelly executed.
Because of this, usually, bigger buffer contributes to more stability and less waiting.

**Streaming is great for big request, such as one spanning days.**

We choose streaming in this tutorial.

```javascript
// for await needs to be wrapped by async function
const streaming = async () => {
    for await (const line of req.stream()) {
        if (line.type !== "msg") {
            continue;
        }
        console.log(line);
    }
}

// call async function
streaming()
.catch((e) => {
    // error handling
    console.log(e);
})
```

## Processing Lines

Downloaded or streamed lines have properties below:

- **exchange**
  Name of exchange where the line belong to
- **channel**
  Channel this line belong to
- **type**
  Type of this line, one of:
  - **msg**
    Message attached to this line is from exchange
  - **start**
    Marks the start of recording
  - **end**
    Marks the end of recording
  - **err**
    Error often followed by an end line
- **message**
  Message conveyed by this line

Start line marks the start of new recording which is equivalent to a new connection to WebSocket server.

If your app needs the initial state for channels, such as orderbook, you want to watch for not only msg line, but start line as well.

This could be done by checking the type of lines and discard previous state if you find the start line:

```javascript
for await (const line of req.stream()) {
    if (line.type === "msg") {
        console.log(line);
    } else if (line.type === "start") {
        // discard current state
        this.do_something_to_discard_state();
    }
    // you can ignore other types since they are unnecessary for tracking state
}
```

!> Even though start line is not given at the beggining of a stream, Replay API and Raw API would automatically fetch the initial state (such as board snapshot) from Snapshot Endpoint.
You can always assume that you are provided with the data needed to reconstruct a certain channel by using those APIs.
