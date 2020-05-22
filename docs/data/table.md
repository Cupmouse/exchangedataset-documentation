# Recorded Exchange/Channels

Here is the table of supported exchange/channels that are recorded and can be accessed through Exchangedataset HTTP API Endpoint.

Further detail for exchange is described in each page.

!> Not all channels/pairs are supported for some exchange.

| Exchange | Channels                                                                                                                        | Pairs                                                                 | Starting Date |
| -------- | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- | - |
| Bitmex   | `announcement`, `chat`, `connected`, `funding`, `instrument`, `insurance`, `liquidation`, `orderBookL2`, `publicNotifications`, `settlement`, `trade` | All pairs                                                             | 6 Jan 2019    |
| Bitfinex | `trades_{pair}`, `book_{pair}`                                                                                                    | `tBTCUSD` + (Top 14 spot pairs by volume in USD at the time of the recording) | 6 Jan 2019    |
| Bitflyer | `lightning_board_{pair}`, `lightning_board_snapshot_{pair}`, `lightning_executions_{pair}`, `lightning_ticker_{pair}`                   | `FX_BTC_JPY`, `BTC_JPY`, `ETH_BTC`, `BCH_USD` + (Bitcoin/JPY Futures)         | 6 Jan 2019    |

* Channels - Channels recorded.
* Pairs - List of pairs recorded and available.
  For some exchange, not all pairs are recorded, mostly because of the original API limitation such as subscription limit.
* Starting Date - The date since the data are available for the exchange

## Other Information

| Exchange | Snapshot Supported              | Server-side Pair Level Filtering                     | Server-side Formatting                                                                                        |
| -------- | ------------------------------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| Bitmex   | `orderBookL2`, `instrument`         | No (Client-side filtering are supported via library) | `orderBookL2`, `trade`, `instrument`, `liquidation`, `settlement`, `insurance`, `funding`                                   |
| Bitfinex | `trades_{pair}`                  | ✓ Yes                                                | `trades_{pair}`, `book_{pair}`                                                                                    |
| Bitflyer | `lightning_board_snapshot_{pair}` | ✓ Yes                                                | `lightning_board_snapshot_{pair}`, `lightning_board_{pair},` `lightning_executions_{pair}`, `lightning_ticker_{pair}` |

* Snapshot Support - Channels supported by Snapshot Endpoint.
* Server-side Formatting - List of channels whose messages can be formatted on the server-side. See server-side formatting.
