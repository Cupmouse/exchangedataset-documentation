# BitFlyer JSON Format

?> For description of what individual fields are, please ask BitFlyer.

## `lightning_board` Channel

Formatting for `lightning_board` comforms to [Orderbook Common](http/format/orderbook.md).

## `lightning_board_snapshot` Channel

Formatting for `lightning_board_snapshot` comforms to [Orderbook Common](http/format/orderbook.md).

## `lightning_executions` Channel

Formatting for `lightning_executions` comforms to [Trade Common](http/format/trade.md).

## `lightning_ticker` Channel

| Field             | Type   |
| ----------------- | ------ |
| product_code      | string |
| timestamp         | string |
| tick_id           | int    |
| best_bid          | float  |
| best_ask          | float  |
| best_bid_size     | float  |
| best_ask_size     | float  |
| total_bid_depth   | float  |
| total_ask_depth   | float  |
| ltp               | float  |
| volume            | float  |
| volume_by_product | float  |
