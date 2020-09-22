# Recorded Exchange/Channels

Here is the table of supported exchange/channels that are recorded and can be accessed through Exchangedataset HTTP API Endpoint.

Further detail for exchange is described in each page.

!> Not all channels/symbols are supported for some exchange.

| Exchange | Channels                                                                                                                                                                                                               | Symbols                                                                                    | Since                   |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ | ----------------------- |
| Bitmex   | `announcement`, `chat`, `connected`, `funding_{currency}`, `instrument_{symbol}`, `insurance_{symbol}`, `liquidation_{symbol}`, `orderBookL2_{symbol}`, `publicNotifications`, `settlement_{symbol}`, `trade_{symbol}` | All symbols                                                                                | 2019-01-06 00:53:40 UTC |
| Bitfinex | `trades_{symbol}`, `book_{symbol}`                                                                                                                                                                                     | `tBTCUSD` + (Top 14 spot symbols by volume in USD at the time of the recording)            | 2019-01-06 00:53:41 UTC |
| BitFlyer | `lightning_board_{symbol}`, `lightning_board_snapshot_{symbol}`, `lightning_executions_{symbol}`, `lightning_ticker_{symbol}`                                                                                          | `FX_BTC_JPY`, `BTC_JPY`, `ETH_BTC`, `BCH_USD` + (Bitcoin/JPY Futures)                      | 2019-01-06 00:53:39 UTC |
| Binance  | `{symbol}@depth@100ms`, `{symbol}@rest_depth`, `{symbol}@trade`, `{symbol}@ticker`                                                                                                                                     | `btcusdt`, `ethusdt` + (Top 18 spot symbols by volume in USD at the time of the recording) | 2020-09-04 12:24:47 UTC |
| Liquid   | `price_ladders_cash_{symbol}_buy`, `price_ladders_cash_{symbol}_sell`, `executions_cash_{symbol}`                                                                                                                      | Top 10 spot symbols by volume in USD at the time of the recording                          | 2020-09-04 09:41:06 UTC |

* Channels - Channels recorded.
* Symbols - List of symbols recorded and available.
  For some exchange, not all symbols are recorded, mostly because of the original API limitation such as subscription limit.
* Starting Date - The date since the data are available for the exchange

## Other Information

| Exchange | Snapshot Supported                          | Server-side Symbol Level Filtering         | Server-side Formatting                                                                                                                                     |
| -------- | ------------------------------------------- | ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Bitmex   | `orderBookL2_{symbol}`                      | ✓ Partially (See [Bitmex](data/bitmex.md)) | `orderBookL2_{symbol}`, `trade_{symbol}`, `instrument_{symbol}`, `liquidation_{symbol}`, `settlement_{symbol}`, `insurance_{symbol}`, `funding_{currency}` |
| Bitfinex | `book_{symbol}`                             | ✓ Yes                                      | All channels                                                                                                                                               |
| BitFlyer | x No                                        | ✓ Yes                                      | All channels                                                                                                                                               |
| Binance  | `{symbol}@rest_depth` (Depth from REST API) | ✓ Yes                                      | All channels                                                                                                                                               |
| Liquid   | x No                                        | ✓ Yes                                      | All channels                                                                                                                                               |

* Snapshot Support - Channels supported by Snapshot Endpoint.
* Server-side Formatting - List of channels whose messages can be formatted on the server-side. See server-side formatting.
