# 🌆 Smart Contract Template

I have created this simple template to connect with the blockchain and repeatedly use it with other smart contract codes.

```python
from web3 import Web3

INFURA = 'https://mainnet.infura.io/v3/<API KEY>'

# Connect to Blockchain

web3 = Web3(Web3.HTTPProvider(INFURA))
print(f'Connected: {web3.is_connected()}')


# Connect to contract

target_address = web3.to_checksum_address("")
target_ABI = ''

target = web.eth.contract(address=target_address, abi=target_ABI)

```



## REFERENCES

* [https://www.youtube.com/watch?v=vPIAcouxaik\&list=PLCwnLq3tOElrubfUWHa1qKrJv1apO8Aag\&index=4](https://www.youtube.com/watch?v=vPIAcouxaik\&list=PLCwnLq3tOElrubfUWHa1qKrJv1apO8Aag\&index=4)
* [https://web3py.readthedocs.io/en/stable/web3.eth.html#web3.eth.Eth.contract](https://web3py.readthedocs.io/en/stable/web3.eth.html#web3.eth.Eth.contract)
* [https://web3py.readthedocs.io/en/stable/web3.main.html#web3.Web3.is\_checksum\_address](https://web3py.readthedocs.io/en/stable/web3.main.html#web3.Web3.is\_checksum\_address)
* [https://web3py.readthedocs.io/en/stable/quickstart.html](https://web3py.readthedocs.io/en/stable/quickstart.html)
