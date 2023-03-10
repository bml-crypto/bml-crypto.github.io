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
(chapter2_part2)=

# 2.2. Creating first request

Now we have all what we need to start interact with dydx.

Before writing requests, we should know about some dydx modules:

* **public** - Public API endpoints. You don't need authentication.
* **private** - Private API endpoints. Requires authentication.

If you want more details about modules, you can check this [page](https://dydxprotocol.github.io/v3-teacher/?python#client-initialization).

## 2.2.1. Triggering public API

Let's write our first dydx request! Firstly, we will start from public module
and get specific market data. In this [page](https://dydxprotocol.github.io/v3-teacher/?python#exchange-sources) 
you can check other markets.

```python
from dydx3.constants import MARKET_ETH_USD

markets = client.public.get_markets(MARKET_ETH_USD)
```

The result of any request to dydx via client is `dydx3.helpers.requests.Response` 
object. Due to get data you have to call `.data` attribute.

```python
markets.data
```

And you will get something like this:

```text
{'markets': {'ETH-USD': {'market': 'ETH-USD',
   'status': 'ONLINE',
   'baseAsset': 'ETH',
   'quoteAsset': 'USD',
   'stepSize': '0.001',
   'tickSize': '0.1',
   ...
```

In additional, we can get specific market orderbook.

```python
orderbook = client.public.get_orderbook(
  market=MARKET_ETH_USD,
)
orderbook.data
```

As result, we will get something like this:

```text
{'asks': [{'size': '12.627', 'price': '1629.2'},
  {'size': '22.095', 'price': '1629.4'},
  {'size': '41.909', 'price': '1629.5'},
  {'size': '44.373', 'price': '1629.6'},
  {'size': '63.363', 'price': '1629.7'},
  ...
```

If you want to see other public methods, you can check this [page](https://dydxprotocol.github.io/v3-teacher/?python#public-http-api).

## 2.2.2. Triggering private API

**Attention! If you want to use these endpoints you need at least 
`api_key_credentials` parameter in your `client` object!**

Let's get dydx user info.

```python
user = client.private.get_user()
user.data
```
And we will get dydx user info.

```text
{'user': {'publicId': 'GYUNXSZE',
  'ethereumAddress': '...',
  'isRegistered': False,
  'email': None,
  'username': None,
  ...
```

We have one account, so let's get info about it.

```python
account = client.private.get_account(API_KEY_PAIRS["walletAddress"])
account.data
```

Here info about our account.

```text
{'account': {'starkKey': 'your_stark_key...',
  'positionId': 'your_position_id...',
  'equity': '14590.324063',
  'freeCollateral': '14197.212668',
  'pendingDeposits': '0.000000',
  ...
```

If you want to see other private methods, you can check this 
[page](https://dydxprotocol.github.io/v3-teacher/?python#private-http-api).

Now we know, how to use public and private API! It's time to make orders!