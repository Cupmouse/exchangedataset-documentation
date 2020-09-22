# Trade Common JSON Format

Trade are formatted into JSON object:

```json
{
    "symbol": symbol,
    "price": price,
    "size": size
}
```

## Fields

| Field  | Type     | Description                                                         |
| ------ | -------- | ------------------------------------------------------------------- |
| symbol | `symbol` | Name of the symbol this trade was executed                          |
| price  | `price`  | Price at this trade was executed, buy if positive, sell if negative |
| size   | `size`   | Size of the trade                                                   |
