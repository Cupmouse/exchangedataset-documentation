# Bitmex

We are recording all symbol available from Bitmex WebSocket Public API.

The URL used to connect to the Bitmex WebSocket API is:

```url
wss://www.bitmex.com/realtime?subscribe=announcement,chat,connected,funding,instrument,insurance,liquidation,orderBookL2,publicNotifications,settlement,trade,liquidation
```

For information about each topic, please see the [Bitmex Website](https://www.bitmex.com/app/wsAPI).

**Symbol level filtering** is not supported when using 'raw' format, because the Bitmex WebSocket API might send a message with more than one symbol.
It is fully supported by the server-side when using 'json' format.

## ETHUSD Orderbook Issue on 24 June 2019

On 24 June 2019 in the Bitmex platform from 09:25:54 UTC to 09:44:30 UTC, the order size of the `ETHUSD` orderbook was incorrectly streamed due to the bug in Bitmex system.

?> Further information about this issue is available at [Bitmex Blog]([https://link](https://blog.bitmex.com/ethusd-orderbook-feed-issues-24-june-2019/)).

This issue affected our service as well and caused the orderbook state in our system to go *incorrect*.

- For Filter Endpoint, all message of `orderBookL2_ETHUSD` from this period is NOT modified and *incorrect*.
- For Snapshot Endpoint, all orderbook updates/insert of `orderBookL2_ETHUSD` in this period are normally treated, so you might encounter *wrong* orderbook state as a response around this time.

Note that this issue is observed only in `ETHUSD` symbol in `orderBookL2` channel and no other symbols are affected.
