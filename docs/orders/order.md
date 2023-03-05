---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---
(chapter3_part1)=

# 3.1. Simple order

In order to execute a simple order, you need to know your `position_id`. This can be found from your account. 


```python
account_response = client.private.get_account()
position_id = account_response.data['account']['positionId']
```

Let's imagine you want to buy 1 ETH. The order is going to be the following:

```python
import time
from dydx3.constants import ORDER_SIDE_BUY, ORDER_TYPE_MARKET, MARKET_ETH_USD

client.private.create_order(
        position_id=position_id,
        market=MARKET_ETH_USD,
        side=ORDER_SIDE_BUY,
        order_type=ORDER_TYPE_MARKET,
        post_only=False,
        size="1",
        price="9999",
        limit_fee="0.1",
        expiration_epoch_seconds=time.time()+120,
        time_in_force="FOK"
)
```

And the order is created. Now, let's dive into what each parameter of this method means.

- `position_id` - required for an order to be placed
- `market` - the market you want to trade in. Currently we chose to buy 1 ETH, hence the market is MARKET_ETH_USD
- `side` - either BUY or SELL. We want to BUY, hence the side is going to be ORDER_SIDE_BUY
- `order_type` - type of an order to execute. This can be MARKET, LIMIT, STOP_LIMIT, TRAILING_STOP or TAKE_PROFIT.We want to execute a market order, hence ORDER_TYPE_MARKET.
- `post_only` - whether the order should be canceled if it would fill immediately on reaching the matching-engine. This parameter is used for testing purposes.
- `size` - size of the order, in base currency (i.e. an ETH-USD position of size 1 represents 1 ETH). We want to buy 1 ETH, so the size should be "1"
- `price` - worst accepted price of the base asset in USD.
- `limit_fee` - is the highest accepted fee for the trade.
- `expiration_epoch_seconds` - time at which the order will expire if not filled. This is the Good-Till-Time and is accurate to a granularity of about 15 seconds.
- `time_in_force` - (Optional) one of GTT (Good till time), FOK (Fill or kill) or IOC (Immediate or cancel). This will default to GTT.

We will talk about all the parameters in more detail in the next section.