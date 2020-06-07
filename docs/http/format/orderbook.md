# Orderbook Common JSON Format

Orders in orderbook are individually formatted into JSON object below:

```json
{
    "pair": pair,
    "price": price,
    "size": size
}
```

## Fields

| Field | Type    | Description                                                                             |
| ----- | ------- | --------------------------------------------------------------------------------------- |
| pair  | `pair`  | Name of the pair this order is from                                                     |
| price | `price` | Price of the order                                                                      |
| size  | `size`  | Size of the order, buy if positive, sell if negative, remove from the orderbook if zero |

## Example: Keep Track of Orderbook

```python
if (size == 0) {
    del orderbook[price]
} else {
    orderbook[price] = size
}
```
