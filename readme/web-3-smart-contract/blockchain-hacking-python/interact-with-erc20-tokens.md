# 🎆 Interact with ERC20 Tokens

Below code can be used to interact with ERC20 tokens.

```python
from web3 import Web3

INFURA = 'https://mainnet.infura.io/v3/<API KEY>'

# Connect to Blockchain

web3 = Web3(Web3.HTTPProvider(INFURA))
print(f'Connected: {web3.is_connected()}')


# Connect to contract

target_address = web3.to_checksum_address("0x514910771AF9Ca656af840dff83E8264EcF986CA")
target_ABI = '[{"constant":true,"inputs":[],"name":"name","outputs":[{"name":"","type":"string"}],"payable":false,"stateMutability":"view","type":"fu>

target = web3.eth.contract(address=target_address, abi=target_ABI)

print(target.functions.name().call())
print(target.functions.symbol().call())
print(target.functions.totalSupply().call() / 10 ** target.functions.decimals().call())

print(web3.from_wei(target.functions.totalSupply().call(), 'ether'))

```



## REFERENCES

* [https://etherscan.io/token/0x514910771af9ca656af840dff83e8264ecf986ca#code](https://etherscan.io/token/0x514910771af9ca656af840dff83e8264ecf986ca#code)

