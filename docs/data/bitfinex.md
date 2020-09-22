# Bitfinex

Only spot symbols are recorded.

Due to the API subscription limit, we record only tBTCUSD and other top 14 symbols by the hightest 24h volume in USD.

Volume are calculated based on the list of symbols from Bitfinex REST API and the URL used is:

```url
https://api.bitfinex.com/v2/tickers?symbols=ALL
```
