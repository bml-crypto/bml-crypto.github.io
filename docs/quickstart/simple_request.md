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
(chapter1_part1)=

# 2.2. Creating first request

Now we have all what we need to start interact with dydx.

Before writing requests, we should know about some dydx modules:

* **public** - Public API endpoints. You don't need authentication.
* **private** - Private API endpoints. Requires authentication.

If you want more details about modules, you can check this [page](https://dydxprotocol.github.io/v3-teacher/?python#client-initialization).

### 2.2.1. Triggering public API

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

### 2.2.2. Triggering private API

**Attention! If you want to use these endpoints you need at least 
`api_key_credentials` parameter in your `client` object!**

Let's get dydx account info.

```{code-cell} ipython3
user = client.private.get_user()
user.data
```