# 🪢 Smart Contract Interactions

## Example Bank Contract

Deploy the below code in remix and set the environment as Dev - Ganache. We are running the contract locally using ganache and interacting with the contract using python's web3.py library.

{% hint style="info" %}
Install ganache using **`npm install -g ganache-cli`**
{% endhint %}

```solidity
pragma solidity ^0.8.0; 

contract HelloWorld_Bank{
address public owner;
string private message;

  	mapping (address => uint) private balances;
  
  	constructor ()  payable {
    		owner = msg.sender; 
		message = "Hello";
 	 }

//Create Deposit Event
    event DepositLog(address indexed sender, uint value, string message);

//Setting Up authorization
    	function isOwner () public view returns(bool) {
        		return msg.sender == owner;
  	}

    	modifier onlyOwner() {
        		require(isOwner());
         		_;
  	}
  
	function changeMessage(string memory myMessage) public {
		message = myMessage;
	}

  	function deposit () public payable {
        		require((balances[msg.sender] + msg.value) >= balances[msg.sender]);
        		balances[msg.sender] += msg.value;
                emit DepositLog(msg.sender, msg.value ,"Deposited Eth");
    	}

    	function withdraw (uint withdrawAmount) public {
        		require (withdrawAmount <= balances[msg.sender]);
        
        		balances[msg.sender] -= withdrawAmount;
        		payable(msg.sender).transfer(withdrawAmount);
    	}
  
  
    	function withdrawAll() public onlyOwner {
        		payable(msg.sender).transfer(address(this).balance);
 	 }

	    function getBalance () public view returns (uint){
        		return balances[msg.sender];
    	}
}
```



## Python code for Interaction

The below python3 code will help you to interact with the above contract and perform various types of operations.

```python
from web3 import Web3

#Make Connection To Local Ganache Blockchain
GANACHE = 'http://127.0.0.1:8545'
web3 = Web3(Web3.HTTPProvider(GANACHE))
print(f'Connected to Ganache: {web3.is_connected()}')


#Connect to contract
target_address = web3.to_checksum_address("0x8aBDADb26EAF6fc69493E8AE0AEDe4F6A2142Ebc")
target_ABI = '[{"inputs":[],"stateMutability":"payable","type":"constructor"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"sender","type":"address"},{"indexed":false,"internalType":"uint256","name":"value","type":"uint256"},{"indexed":false,"internalType":"string","name":"message","type":"string"}],"name":"DepositLog","type":"event"},{"inputs":[{"internalType":"string","name":"myMessage","type":"string"}],"name":"changeMessage","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"deposit","outputs":[],"stateMutability":"payable","type":"function"},{"inputs":[],"name":"getBalance","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"isOwner","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"owner","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"withdrawAmount","type":"uint256"}],"name":"withdraw","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"withdrawAll","outputs":[],"stateMutability":"nonpayable","type":"function"}]'
target = web3.eth.contract(address=target_address, abi=target_ABI)


#print(web3.eth.accounts[0])
#print(web3.eth.accounts[1])

fist_account = web3.eth.accounts[0]
second_account = web3.eth.accounts[1]
second_account_priv = '0x8617a319c33c2fdbb2081ad36b8ef1137ffa0190c169c4a29115065c116b96e0'


web3.eth.default_account = web3.eth.accounts[1]

print(web3.eth.get_storage_at(target_address, 1).decode())

tx_hash = target.functions.changeMessage('test').transact()

web3.eth.wait_for_transaction_receipt(tx_hash)

print(web3.to_hex(tx_hash))
print(web3.eth.get_transaction(tx_hash))
print(web3.eth.get_storage_at(target_address, 1).decode())


print(target.functions.getBalance().call())


deposit_eth = target.functions.deposit().build_transaction({
        'nonce': web3.eth.get_transaction_count(second_account),
        'from': second_account,
        'value': web3.to_wei(2, 'ether'),
        'gas': 3000000,
        'gasPrice': web3.to_wei('0.809', 'gwei')
})


signed_deposit = web3.eth.account.sign_transaction(deposit_eth, second_account_priv)
txn_hash = web3.eth.send_raw_transaction(signed_deposit.rawTransaction)

print(web3.to_hex(txn_hash))
print(web3.eth.get_transaction(tx_hash))

print(target.functions.getBalance().call())


withdraw_eth = target.functions.withdraw(1000000000000000000).build_transaction({
        'nonce': web3.eth.get_transaction_count(web3.eth.accounts[1]),
        'from': web3.eth.accounts[1],
        'gas': 3000000,
        'gasPrice': web3.to_wei('50', 'gwei')
})


signed_deposit = web3.eth.account.sign_transaction(withdraw_eth, second_account_priv)
txn_hash = web3.eth.send_raw_transaction(signed_deposit.rawTransaction)

print(web3.to_hex(txn_hash))
print(web3.eth.get_transaction(tx_hash))

print(target.functions.getBalance().call())
```



## REFERENCES

* [https://github.com/cclabsInc/Python-SmartContact-BlockchainExploitation/blob/main/Part1\_Manual\_Interactions/Helloworld\_Bank\_Target.sol](https://github.com/cclabsInc/Python-SmartContact-BlockchainExploitation/blob/main/Part1\_Manual\_Interactions/Helloworld\_Bank\_Target.sol)

