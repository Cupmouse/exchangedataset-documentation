# Recorded Exchange/Channels

Here is the table of supported exchange/channels that are recorded and can be accessed through Exchangedataset HTTP API Endpoint.

Further detail for exchange is described in each page.

!> Not all channels/pairs are supported for some exchange.

| Exchange | Channels                                                                                                                                              | Pairs                                                                                    | Starting Date |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ------------- |
| Bitmex   | `announcement`, `chat`, `connected`, `funding`, `instrument`, `insurance`, `liquidation`, `orderBookL2`, `publicNotifications`, `settlement`, `trade` | All pairs                                                                                | 6 Jan 2019    |
| Bitfinex | `trades_{pair}`, `book_{pair}`                                                                                                                        | `tBTCUSD` + (Top 14 spot pairs by volume in USD at the time of the recording)            | 6 Jan 2019    |
| BitFlyer | `lightning_board_{pair}`, `lightning_board_snapshot_{pair}`, `lightning_executions_{pair}`, `lightning_ticker_{pair}`                                 | `FX_BTC_JPY`, `BTC_JPY`, `ETH_BTC`, `BCH_USD` + (Bitcoin/JPY Futures)                    | 6 Jan 2019    |
| Binance  | `{pair}@depth@100ms`, `{pair}@rest_depth`, `{pair}@trade`, `{pair}@ticker`                                                                            | `btcusdt`, `ethusdt` + (Top 18 spot pairs by volume in USD at the time of the recording) | TBD           |
| Liquid   | `price_ladders_cash_{pair}_buy`, `price_ladders_cash_{pair}_sell`, `executions_cash_{pair}`                                                           | Top 10 spot pairs by volume in USD at the time of the recording                          | TBD           |

* Channels - Channels recorded.
* Pairs - List of pairs recorded and available.
  For some exchange, not all pairs are recorded, mostly because of the original API limitation such as subscription limit.
* Starting Date - The date since the data are available for the exchange

## Other Information

| Exchange | Snapshot Supported                        | Server-side Pair Level Filtering                     | Server-side Formatting                                                                    |
| -------- | ----------------------------------------- | ---------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| Bitmex   | `orderBookL2`               | No (Client-side filtering are supported via library) | `orderBookL2`, `trade`, `instrument`, `liquidation`, `settlement`, `insurance`, `funding` |
| Bitfinex | `book_{pair}`                             | ✓ Yes                                                | All channels                                                                              |
| BitFlyer | x No                                      | ✓ Yes                                                | All channels                                                                              |
| Binance  | `{pair}@rest_depth` (Depth from REST API) | ✓ Yes                                                | All channels                                                                              |
| Liquid   | x No                                      | ✓ Yes                                                | All channels                                                                              |

* Snapshot Support - Channels supported by Snapshot Endpoint.
* Server-side Formatting - List of channels whose messages can be formatted on the server-side. See server-side formatting.
