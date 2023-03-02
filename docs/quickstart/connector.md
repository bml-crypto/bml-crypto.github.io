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

# Create dydx client

Client - key ingredient, that allows you to interact with dydx via their library,
so let's create one.

### Import libs

In order to set up dydx connection, we will use `dydx3` lib, that responsible
for dydx interacting logic and `web3` lib, that responsible for blockchain 
connection and works inside client.
```python
from dydx3 import Client
from web3 import Web3, HTTPProvider
```

### Create variables

These variables configures dydx connection
```python
HOST='https://api.stage.dydx.exchange'
WEB3_PROVIDER='https://goerli.infura.io/v3/5a0bd09254d94ac1af88953907f4136c'
STARK_PRIVATE_KEY='your start_private_key'
DEFAULT_ETHEREUM_ADDRESS='your ethereum_address'
NETWORK_ID=5

WALLET_ADDRESS="your wallet address"
KEY="your api_key"
SECRET="your secret_key"
PASSPHRASE="your passphrase"
LEGACY_SIGNING=False
WALLET_TYPE="METAMASK"
```

Let's figure out what these variables mean. Here we simplify explanation from
official [documentation](https://dydxprotocol.github.io/v3-teacher/?python#client-initialization).

`HOST` - as you remember dydx has mainnet and testnet blockchains and in this 
guide we will use testnet, but in future you can change it easily.

`WEB3_PROVIDER` - you need to choose web3 provider which will scan blockchain. 
For example, it can be infura.

`STARK_PRIVATE_KEY` - this key allows dydx platform to identify their users.
For more information, you can check this [page](https://help.dydx.exchange/en/articles/4797307-what-is-a-stark-key).

`DEFAULT_ETHEREUM_ADDRESS` - ...

`NETWORK_ID` - ...

`WALLET_ADDRESS` - ...

`KEY` - ...

`SECRET` - ...

`PASSPHRASE` - ...

`LEGACY_SIGNING` - ...

`WALLET_TYPE` - ...

### Creating client

```python
client = Client(
    host=HOST,
    web3=Web3(HTTPProvider(WEB3_PROVIDER)),
    stark_private_key=STARK_PRIVATE_KEY,
    default_ethereum_address=DEFAULT_ETHEREUM_ADDRESS,
    network_id=NETWORK_ID,
    api_key_credentials={
        "walletAddress": WALLET_ADDRESS,
        "key": KEY,
        "secret": SECRET,
        "passphrase": PASSPHRASE,
        "legacySigning": LEGACY_SIGNING,
        "walletType": WALLET_TYPE
    }
)
```