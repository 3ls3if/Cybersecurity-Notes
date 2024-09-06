# 🟤 Brownie Interactions

## Installing Brownie

```
pip3 install eth-brownie

OR

git clone https://github.com/eth-brownie/brownie.git
cd brownie
python3 setup.py install
```

## Setting up project folder

```
# Create the project folder
mkdir Bank

# Initialize brownie
cd Bank
brownie init
```

## Smart Contract Code to Test

{% hint style="info" %}
You need to copy the below code into the **Contracts** directory under the project folder.
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

## Compilation

```
brownie compile
```

## Deploy Script

{% hint style="info" %}
You need to copy the below deploy script into the **scripts** directory under the project folder.
{% endhint %}

```
from brownie import accounts, HelloWorld_Bank

account0 = accounts[0]
account1 = accounts[1]

def deployBank():
        bank = HelloWorld_Bank.deploy({"from":account0})
        return bank

def bankInteractions(bank):
        print(bank.getBalance())
        bank.deposit({"from":account0, "value":1000000000000000000})
        print(f'Accoutn0: {bank.getBalance({"from":account0})}')
        bank.deposit({"from":account1, "value":2000000000000000000})
        print(f'Accoutn1: {bank.getBalance({"from":account1})}')

def main():
        bank = deployBank()
        bankInteractions(bank) 

```

### Run the deploy script

```
brownie run scripts/deploy.py
```

## Brownie Networks List

```
brownie networks list
```







***

## REFRENCES

* [https://eth-brownie.readthedocs.io/en/stable/install.html](https://eth-brownie.readthedocs.io/en/stable/install.html)
* [https://github.com/cclabsInc/Python-SmartContact-BlockchainExploitation/blob/main/Part2\_Frameworks/Helloworld\_Bank\_Target.sol](https://github.com/cclabsInc/Python-SmartContact-BlockchainExploitation/blob/main/Part2\_Frameworks/Helloworld\_Bank\_Target.sol)ytho
