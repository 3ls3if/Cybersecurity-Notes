# ✒️ Sign Transactions

Below code can be used to sign and send an ethereum transaction.

{% hint style="info" %}
For this example I have used local instance using **ganache-cli**.\
\
Install ganache-cli using: **`sudo npm install -g ganache-cli`**
{% endhint %}

```
from web3 import Web3

#Make a connection
GANACHE = 'http://127.0.0.1:8545'

web3 = Web3(Web3.HTTPProvider(GANACHE))

print(f'Connected: {web3.is_connected()}')


#Accounts for transactions
first_account = "0xCc2e852AB371ba2D8ff30BBae625150F1C9503f5"
first_account_priv = "0xeadbfc38c0e6033a824640c1969a67d9489f69d45fa7f09b5a83774a74a5d932"

second_account = "0xaC37dc5FDf64Fc88a5ED1Ef1324F344D490b6A58"

#Build a transaction
transaction = {
        'nonce': web3.eth.get_transaction_count(first_account),
        'to': second_account,
        'value': web3.to_wei(1, 'ether'),
        'gas': 3000000,
        'gasPrice': web3.to_wei('0.809', 'gwei')

}

#sign and send transaction
signed_txn = web3.eth.account.sign_transaction(transaction, first_account_priv)

txn_hash = web3.eth.send_raw_transaction(signed_txn.rawTransaction)

print(web3.to_hex(txn_hash))
print(web3.eth.get_transaction(txn_hash))

```

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Output</p></figcaption></figure>





## REFERENCES

* [https://web3py.readthedocs.io/en/stable/web3.eth.html](https://web3py.readthedocs.io/en/stable/web3.eth.html)
* [https://etherscan.io/gastracker](https://etherscan.io/gastracker)
* [https://web3py.readthedocs.io/en/stable/web3.main.html](https://web3py.readthedocs.io/en/stable/web3.main.html)
