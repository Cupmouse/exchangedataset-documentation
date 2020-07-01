# Bitmex JSON Format

?> For description of what individual fields are, please ask Bitmex.

## `orderBookL2` Channel

Formatting for `orderBookL2` comforms to [Orderbook With Order ID](http/format/orderbook-orderid.md).

## `trade` Channel

Formatting for `trade` comforms to [Trade](http/format/trade.md).

Additional fields are provided by Bitmex:

| Field           | Type           |
| --------------- | -------------- |
| timestamp       | `timestamp`    |
| trdMatchId      | `guid`         |
| tickDirection   | `string`       |
| grossValue      | `int`/`null`   |
| homeNotional    | `float`/`null` |
| foreignNotional | `float`/`null` |

## `instrument` Channel

Fields that are not `null` are instrument properties that was updated.

| Field                          | Type               |
| ------------------------------ | ------------------ |
| symbol                         | `string`           |
| rootSymbol                     | `string`/`null`    |
| state                          | `string`/`null`    |
| typ                            | `string`/`null`    |
| listing                        | `timestamp`/`null` |
| front                          | `timestamp`/`null` |
| expiry                         | `timestamp`/`null` |
| settle                         | `timestamp`/`null` |
| relistInterval                 | `duration`/`null`  |
| inverseLeg                     | `string`/`null`    |
| sellLeg                        | `string`/`null`    |
| buyLeg                         | `string`/`null`    |
| optionStrikePcnt               | `float`/`null`     |
| optionStrikeRound              | `float`/`null`     |
| optionStrikePrice              | `float`/`null`     |
| optionMultiplier               | `float`/`null`     |
| positionCurrency               | `string`/`null`    |
| underlying                     | `string`/`null`    |
| quoteCurrency                  | `string`/`null`    |
| underlyingSymbol               | `string`/`null`    |
| reference                      | `string`/`null`    |
| referenceSymbol                | `string`/`null`    |
| calcInterval                   | `duration`/`null`  |
| publishInterval                | `duration`/`null`  |
| publishTime                    | `duration`/`null`  |
| maxOrderQty                    | `int`/`null`       |
| maxPrice                       | `float`/`null`     |
| lotSize                        | `int`/`null`       |
| tickSize                       | `float`/`null`     |
| multiplier                     | `int`/`null`       |
| settlCurrency                  | `string`/`null`    |
| underlyingToPositionMultiplier | `int`/`null`       |
| underlyingToSettleMultiplier   | `int`/`null`       |
| quoteToSettleMultiplier        | `int`/`null`       |
| isQuanto                       | `boolean`/`null`   |
| isInverse                      | `boolean`/`null`   |
| initMargin                     | `float`/`null`     |
| maintMargin                    | `float`/`null`     |
| riskLimit                      | `int`/`null`       |
| riskStep                       | `int`/`null`       |
| limit                          | `float`/`null`     |
| capped                         | `boolean`/`null`   |
| taxed                          | `boolean`/`null`   |
| deleverage                     | `boolean`/`null`   |
| makerFee                       | `float`/`null`     |
| takerFee                       | `float`/`null`     |
| settlementFee                  | `float`/`null`     |
| insuranceFee                   | `float`/`null`     |
| fundingBaseSymbol              | `string`/`null`    |
| fundingQuoteSymbol             | `string`/`null`    |
| fundingPremiumSymbol           | `string`/`null`    |
| fundingTimestamp               | `timestamp`/`null` |
| fundingInterval                | `duration`/`null`  |
| fundingRate                    | `float`/`null`     |
| indicativeFundingRate          | `float`/`null`     |
| rebalanceTimestamp             | `timestamp`/`null` |
| rebalanceInterval              | `duration`/`null`  |
| openingTimestamp               | `timestamp`/`null` |
| closingTimestamp               | `timestamp`/`null` |
| sessionInterval                | `duration`/`null`  |
| prevClosePrice                 | `float`/`null`     |
| limitDownPrice                 | `float`/`null`     |
| limitUpPrice                   | `float`/`null`     |
| bankruptLimitDownPrice         | `float`/`null`     |
| bankruptLimitUpPrice           | `float`/`null`     |
| prevTotalVolume                | `int`/`null`       |
| totalVolume                    | `int`/`null`       |
| volume                         | `int`/`null`       |
| volume24h                      | `int`/`null`       |
| prevTotalTurnover              | `int`/`null`       |
| totalTurnover                  | `int`/`null`       |
| turnover                       | `int`/`null`       |
| turnover24h                    | `int`/`null`       |
| homeNotional24h                | `float`/`null`     |
| foreignNotional24h             | `float`/`null`     |
| prevPrice24h                   | `float`/`null`     |
| vwap                           | `float`/`null`     |
| highPrice                      | `float`/`null`     |
| lowPrice                       | `float`/`null`     |
| lastPrice                      | `float`/`null`     |
| lastPriceProtected             | `float`/`null`     |
| lastTickDirection              | `string`/`null`    |
| lastChangePcnt                 | `float`/`null`     |
| bidPrice                       | `float`/`null`     |
| midPrice                       | `float`/`null`     |
| askPrice                       | `float`/`null`     |
| impactBidPrice                 | `float`/`null`     |
| impactMidPrice                 | `float`/`null`     |
| impactAskPrice                 | `float`/`null`     |
| hasLiquidity                   | `boolean`/`null`   |
| openInterest                   | `int`/`null`       |
| openValue                      | `int`/`null`       |
| fairMethod                     | `string`/`null`    |
| fairBasisRate                  | `float`/`null`     |
| fairBasis                      | `float`/`null`     |
| fairPrice                      | `float`/`null`     |
| markMethod                     | `string`/`null`    |
| markPrice                      | `float`/`null`     |
| indicativeTaxRate              | `float`/`null`     |
| indicativeSettlePrice          | `float`/`null`     |
| optionUnderlyingPrice          | `float`/`null`     |
| settledPrice                   | `float`/`null`     |
| timestamp                      | `timestamp`        |

## `insurance` Channel

| Field         | Type        |
| ------------- | ----------- |
| currency      | `string`    |
| timestamp     | `timestamp` |
| walletBalance | `int`       |

## `funding` Channel

| Field            | Type        |
| ---------------- | ----------- |
| timestamp        | `timestamp` |
| symbol           | `string`    |
| fundingInterval  | `duration`  |
| fundingRate      | `float`     |
| fundingRateDaily | `float`     |

## `settlement` Channel

| Field                 | Type        |
| --------------------- | ----------- |
| timestamp             | `timestamp` |
| symbol                | `string`    |
| settlementType        | `string`    |
| settledPrice          | `float`     |
| optionStrikePrice     | `float`     |
| optionUnderlyingPrice | `float`     |
| bankrupt              | `int`       |
| taxBase               | `int`       |
| taxRate               | `float`     |

## `liquidation` Channel

| Field     | Type     |
| --------- | -------- |
| orderID   | `guid`   |
| symbol    | `string` |
| side      | `string` |
| price     | `float`  |
| leavesQty | `int`    |
