# 🧜‍♀️ Subscribing to Events

## Example Contract

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



## Python Code for Event Handling

```python
from web3 import Web3
import asyncio, json


GANACHE = 'http://127.0.0.1:8545'

# Connect to Blockchain

web3 = Web3(Web3.HTTPProvider(GANACHE))
print(f'Connected: {web3.is_connected()}')


# Connect to contract

target_address = web3.to_checksum_address("0x62838113FE0393fd723389663ce44f4667c0A94E")
target_ABI = '[{"inputs":[],"stateMutability":"payable","type":"constructor"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"sender","type":"address"},{"indexed":false,"internalType":"uint256","name":"value","type":"uint256"},{"indexed":false,"internalType":"string","name":"message","type":"string"}],"name":"DepositLog","type":"event"},{"inputs":[{"internalType":"string","name":"myMessage","type":"string"}],"name":"changeMessage","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"deposit","outputs":[],"stateMutability":"payable","type":"function"},{"inputs":[],"name":"getBalance","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"isOwner","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"owner","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"withdrawAmount","type":"uint256"}],"name":"withdraw","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"withdrawAll","outputs":[],"stateMutability":"nonpayable","type":"function"}]'

target = web3.eth.contract(address=target_address, abi=target_ABI)


# Handling Events

def EventHandler(event):
	event = Web3.to_json(event)
	event = json.loads(event)
	print(event['args']['sender'], event['args']['value'], event['args']['message'])


# Async function

async def EventLogLoop(event_filter, poll_interval):
	while True:
		for event in event_filter.get_new_entries():
			EventHandler(event)
		await asyncio.sleep(poll_interval)


# Main function

def main():
	event_filter = target.events.DepositLog.create_filter(fromBlock='latest')
	asyncio.run(EventLogLoop(event_filter, 2))
	



if __name__ == "__main__":
	main()
```





## REFERENCES

* [https://web3py.readthedocs.io/en/stable/filters.html#events-and-logs](https://web3py.readthedocs.io/en/stable/filters.html#events-and-logs)
