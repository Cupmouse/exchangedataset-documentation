# Binance

20 symbols with the highest volume in 24h in USD will be picked on the start of recording.

The URLs used to calculate volumes are:

```url
https://www.binance.com/api/v3/ticker/24hr
https://www.binance.com/api/v3/exchangeInfo
```

For each symbol, `{symbol}@depth@100ms`, `{symbol}@rest_depth`, `{symbol}@trade` and `{symbol}@ticker` are recorded.

The URL used to connect to the Binance WebSocket API is:

```url
wss://stream.binance.com:9443/stream?streams={array_of_channels}
```

## REST Depth Channel

To reconstruct orderbooks, depth data from the REST API is needed.

This data is recorded and can be accessed as `{symbol}@rest_depth` channel, and its message part is raw data from the REST API.

This data is collected after our client had connected to the WebSocket server.

If the collected data does not suffice the requirement to construct orderbook, WebSocket connection will be restarted (closed and reopened) to try again.
