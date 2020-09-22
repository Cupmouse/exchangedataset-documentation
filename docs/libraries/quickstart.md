# Quick Start

## HTTP Module, Raw API and Replay API

`exchangedataset-node`, `exchangedataset-python`, `exdgo` have a low-level API for HTTP Endpoints, medium and high-level streaming API.

### HTTP Module

HTTP Module is a low-level API which provides access to [HTTP Endpoints](http/) via functions named after each HTTP Endpoint.

This is mostly used internally, but exposed in public.

?> Documentation for HTTP Endpoints can be found in [HTTP Endpoints](http/).

### Raw

Raw API is a medium-level API for streaming or downloading data.

It replays market data as string given start date, end date, exchange, format etc. and takes care of all necessary requests to HTTP Endpoints.

!> Raw API does not support client-side symbol level filtering. For what channels server-side filtering is not supported for, see [Recorded Exchange/Channels](data/table).

### Replay

Replay API is a high-level API for streaming or downloading data.

It formats market data into object and also supports symbol level filtering for all channels.

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

- By calling `replay(ClientParam, ReplayRequestParam)` function
- Creating `Client` by `createClient(ClientParam)`, then call `client.replay(ReplayRequestParam)` function

Both do the same job, however, `Client` can be reused to make another request, so you don't have to provide `ClientParam` again.

We recommend you to create an client so you don't have to provide API-key for every query you make, which increases security of your app.

## Creating Client

Below code creates a `Client` for later use.

<!-- tabs:start -->

#### ** NodeJS **

```javascript
const { createClient } = require("exchangedataset-node");

// create client
const client = createClient({
  apikey: "API-key here",
});
```

#### ** Python3 **

```python
from exdpy import Client

# create client
client = exdpy.Client(apikey='API-key here')
```

#### ** Golang **

```go
import "github.com/exchangedataset/exdgo"

func main() {
    // Create client
    client, err := exdgo.CreateClient(exdgo.ClientParam{
        APIKey: "API-key here",
    })
    if err != nil {
        fmt.Println(err)
        os.Exit(1)
    }
}
```

<!-- tabs:end -->

## Filtering

Multiple exchanges and channels can be specified to be filtered-in:

<!-- tabs:start -->

#### ** NodeJS **

```javascript
const req = client.replay({
  filter: {
    bitmex: [
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

#### ** Python3 **

```python
req = client.replay({
    'bitmex': [
        "orderBookL2_XBTUSD",
        "trade_XBTUSD",
    ],
    'bitflyer': [
        "lightning_board_FX_BTC_JPY",
        "lightning_executions_FX_BTC_JPY",
    ],
    'bitfinex': [
        "orders_tBTCUSD",
        "book_tBTCUSD",
    ],
},
"2019-05-12 10:00Z",
"2019-05-12 10:01Z",
)
```

#### ** Golang **

```go
start, err := time.Parse(time.RFC3339, "2019-05-12 10:00Z")
if err != nil {
  fmt.Println(err)
  os.Exit(1)
}
end, err := time.Parse(time.RFC3339, "2019-05-12 10:01Z")
if err != nil {
  fmt.Println(err)
  os.Exit(1)
}
rp := exdgo.ReplayRequestParam{
    Filter: map[string][]string{
        "bitmex": []string{
            "orderBookL2_XBTUSD",
            "trade_XBTUSD",
        },
        "bitflyer": []string{
            "lightning_board_FX_BTC_JPY",
            "lightning_executions_FX_BTC_JPY",
        },
        "bitfinex": []string{
            "orders_tBTCUSD",
            "book_tBTCUSD",
        },
    },
    Start: start,
    End: end,
}
req, err := client.Replay(rp)
if err != nil {
    // Do error handling
    fmt.Println(err)
    os.Exit(1)
}
```

<!-- tabs:end -->

!> Response for channels which is not supported or recorded is empty and produces no error.

## Streaming or Download

Once `ReplayRequest` is obtained, you can get result either by streaming or download.

### Download

Download collects all results from multiple HTTP Endpoint calls into one array.

Theoretically, this is quicker than streaming, due to the overhead of iterator.

But storing all result takes memory space and is not always the most efficient way, easily crashing application by out of memory when large request was issued.

**Downloading is recommended only for smaller request.**

### Streaming

Streaming downloads what only needed to fill the buffer as your app goes through the result one-by-one.

The size of buffer is fixed, so it won't cause out of memory.
It can be set by giving 1st parameter to stream function.

**Streaming is great for big request, such as one spanning days.**

We choose streaming in this tutorial.

<!-- tabs:start -->

#### ** NodeJS **

!> Please note that NodeJS does not support multi-threading, only IO/Network is parallelly executed.
Because of this, usually, bigger buffer contributes to more stability and less waiting.

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

#### ** Python3 **

```python
for line in req.stream():
    if line.type == 'msg':
        print(line)
```

#### ** Golang **

```go
itr, err := req.Stream()
if err != nil {
    fmt.Println(err)
    os.Exit(1)
}
defer func() {
    err = itr.Close()
    if err != nil {
        fmt.Println(err)
        os.Exit(1)
    }
}()
for {
    if line, ok, err := itr.Next(); ok {
        if line.Type == exdgo.LineTypeMessage {
            fmt.Println(line)
        }
    } else if err != nil {
        fmt.Println(err)
        os.Exit(1)
    } else {
        break
    }
}
```

<!-- tabs:end -->

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

<!-- tabs:start -->

#### ** NodeJS **

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

#### ** Python3 **

```python
for line in req.stream():
    if line.type === 'msg':
        print(line)
    elif line.type ==='start':
        self.do_something_to_discard_state()
    # you can ignore other types since they are unnecessary for tracking state
```

#### ** Golang **

```go
for {
    if line, ok, err := itr.Next(); ok {
        if line.Type == exdgo.LineTypeMessage {
            fmt.Println(line)
        } else if line.Type == exdgo.LineTypeStart {
            // doSomethingToDiscardState
        }
    } else if err != nil {
        fmt.Println(err)
        os.Exit(1)
    } else {
        break
    }
}
```

<!-- tabs:end -->

?> Even though start line is not given at the beggining of a stream, Replay API and Raw API would automatically fetch the initial state (such as board snapshot) from the Snapshot Endpoint if the channel is supported by it.
