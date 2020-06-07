# BitFlyer

All public channels are recorded.

The URL used to record the BitFlyer Public WebSocket API is:

```url
wss://ws.lightstream.bitflyer.com/json-rpc
```

BitFlyer does not provide the way to subscribe to every pair in the market, instead, our system looks for available pairs using the REST API at the start of recording and send subscribe to those channels.

The URL used to fetch the list of pairs is:

```url
https://api.bitflyer.com/v1/markets
```

?> For information about original API messages, see [BitFlyer API Doc](https://bf-lightning-api.readme.io/docs?ljs=en).

## Maintenance Time

BitFlyer performs scheduled maintenance usually from 9:00 PM to 9:10 PM (GMT) every day.

Data in this period is not recorded.

Our system tries to reconnect to the original API server as soon as possible, and do so usually within 60 seconds after the market was reopened.

For the 2 minutes after the market has reopened, itayose will be implemented.

?> For more information about maintenance, see [BitFlyer Website](https://bitflyer.com/en-jp/faq/Maintenance).

## Itayose

Itayose is implemented when market reopens after maintenance or circuit breaker had struck.

Orders executed on itayose will be ignored and not be applied to the snapshot of lightning_board_snapshot_{pair} from HTTP Snapshot Endpint.
