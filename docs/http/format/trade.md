# Trade Common JSON Format

Trade are formatted into JSON object:

```json
{
    "pair": pair,
    "price": price,
    "size": size
}
```

## Fields

| Field | Type    | Description                                                         |
| ----- | ------- | ------------------------------------------------------------------- |
| pair  | `pair`  | Name of the pair this trade was executed                            |
| price | `price` | Price at this trade was executed, buy if positive, sell if negative |
| size  | `size`  | Size of the trade                                                   |
