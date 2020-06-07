# Orderbook With Order ID Common JSON Format

Orders in orderbook are individually formatted into JSON object below:

```json
{
    "pair": pair,
    "price": price,
    "id": int,
    "size": size
}
```

## Fields

| Field | Type    | Description                                                                             |
| ----- | ------- | --------------------------------------------------------------------------------------- |
| pair  | `pair`  | Name of the pair this order is from                                                     |
| price | `price` | Price of the order, 0 if order is already appeared before                               |
| id    | `int`   | Order ID                                                                                |
| size  | `size`  | Size of the order, buy if positive, sell if negative, remove from the orderbook if zero |

## Example: Keep Track of Orderbook

```python
if (price == 0) {
    price = id_vs_price[id]
}
if (size == 0) {
    del orderbook[price]
    del id_vs_price[id]
} else {
    orderbook[price] = size
}
```
