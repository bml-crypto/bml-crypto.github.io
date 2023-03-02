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

```{code-cell} ipython3
from dydx3.constants import MARKET_ETH_USD

markets = client.public.get_markets(MARKET_ETH_USD)
```

The result of any request to dydx via client is `dydx3.helpers.requests.Response` 
object. Due to get data you have to call `.data` attribute.

```{code-cell} ipython3
markets.data
```

In additional, we can get specific market orderbook.

```{code-cell} ipython3
orderbook = client.public.get_orderbook(
  market=MARKET_ETH_USD,
)
orderbook.data
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