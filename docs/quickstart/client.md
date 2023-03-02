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
(chapter2_part1)=

# 2.1. Create dydx client

Client - key ingredient, that allows you to interact with dydx via their library, so let's create one.

## 2.1.1. Import libs

In order to set up dydx connection, we will use `dydx3` lib, that responsible
for dydx interacting logic and `web3` lib, that responsible for blockchain 
connection and works inside client.
```python
from dydx3 import Client
from web3 import Web3, HTTPProvider
```

## 2.1.2. Create variables

These variables configures dydx connection
```python
HOST='https://api.stage.dydx.exchange'
WEB3_PROVIDER='https://goerli.infura.io/v3/5a0bd09254d94ac1af88953907f4136c'
STARK_PRIVATE_KEY=STARK_KEY_PAIRS["privateKey"]
NETWORK_ID=5

KEY=API_KEY_PAIRS["key"]
SECRET=API_KEY_PAIRS["secret"]
PASSPHRASE=API_KEY_PAIRS["passphrase"]
DEFAULT_ETHEREUM_ADDRESS=API_KEY_PAIRS["walletAddress"]
```

Let's figure out what these variables mean. Here we simplify explanation from
official [documentation](https://dydxprotocol.github.io/v3-teacher/?python#client-initialization).

- `HOST` - as you remember dydx has mainnet and testnet blockchains and in this 
guide we will use testnet, but in future you can change it easily.
- `WEB3_PROVIDER` - you need to choose web3 provider which will scan blockchain. 
For example, it can be infura.
- `STARK_PRIVATE_KEY` - this key allows dydx platform to identify their users.
For more information, you can check this [page](https://help.dydx.exchange/en/articles/4797307-what-is-a-stark-key).
- `DEFAULT_ETHEREUM_ADDRESS` - your ethereum wallet address that linked to your
dydx account.
- `NETWORK_ID` - blockchain ID (1 - mainnet, 5 - testnet).
- `KEY` - UUID that identifies your dydx credentials.
- `SECRET` - secret string used for HMACs generation.
- `PASSPHRASE` - pass phrase used for encrypt/decrypt `SECRET`.

If you want some more details about `KEY`, `SECRET` and `PASSPHRASE`, you can 
check this [page](https://dydxprotocol.github.io/v3-teacher/?python#api-key-authentication).

## 2.1.3. Creating client

If we want to use `public` and `private` dydx apis we should create client
as follows.

```python
client = Client(
    host=HOST,
    web3=Web3(HTTPProvider(WEB3_PROVIDER)),
    stark_private_key=STARK_PRIVATE_KEY,
    default_ethereum_address=DEFAULT_ETHEREUM_ADDRESS,
    network_id=NETWORK_ID,
    api_key_credentials={
        "key": KEY,
        "secret": SECRET,
        "passphrase": PASSPHRASE
    }
)
```

And now we can interact with dydx via our `client`.