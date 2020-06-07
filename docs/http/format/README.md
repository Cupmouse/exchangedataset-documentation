# JSON Format {docsify-ignore-all}

This section explains the format of message you get from HTTP Endpoint if you set format as "json".

Every message line will be formatted into JSON object:

```json
{ "like": "this" }
```

In this section, we call attributes like "like" as shown above as **field**.

## [➔ Types](http/format/types.md)

Explains types used in fields.

## Common Formatting

Some channels such as orderbook or trade channel are compiled so that it has the same format across exchanges.

Depending on exchange and channel, additional fields may be included, which is explained in each exchanges' channel.

### [➔ Orderbook](http/format/orderbook.md)

!> Orderbook channels which order is tracked by ID does not belong here. Please see below.

### [➔ Orderbook With Order ID](http/format/orderbook-orderid.md)

Some exchange force client to track individual order by order ID and have to be treated differently than normal orderbook channels which track order by price.

### [➔ Trade](http/format/trade.md)

Individual trading are formatted.

## Exchange

### [➔ Bitmex](http/format/bitmex.md)

### Bitfinex

`book` channel comforms to [Orderbook](http/format/orderbook.md).

`trade` channel comforms to [Trade](http/format/trade.md).

Bitfinex does not have other channels which support JSON format.

### [➔ BitFlyer](http/format/bitflyer.md)
