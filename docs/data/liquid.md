# Liquid

10 symbols with the highest volume in 24h in USD will be picked on the start of recording.

The URLs used to calculate volumes are:

```url
https://api.liquid.com/products
```

We also uses arbitrary set USDJPY price of ¥100 to calculate the volumes.

For each symbol, `price_ladders_cash_{symbol}_buy`, `price_ladders_cash_{symbol}_sell`, and `executions_cash_{symbol}` are recorded.

The URL used to connect to the Liquid WebSocket API is:

```url
wss://tap.liquid.com/app/LiquidTapClient
```
