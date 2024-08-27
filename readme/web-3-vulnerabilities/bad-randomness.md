# 🌉 Bad Randomness

## Blockhash Example

Let’s start out taking a look at a simple example of using a blockhash value with a blocknumber value. While a hash of a block might seem like a good idea as a random number there are numerous issues with it. Firstly, a blocknumber is a known value set by a miner that persists for a set length of time and can be queried and used in an attacker’s similar algorithm to produce the same result and bypass controls. But there is also an underlying vulnerability to this approach when coupled with a blockchash which we will take a look at below.

**Action Steps:**

> 1\.  Open up your terminal and launch ganache-cli
>
> 2\.  Type out the code below into Remix
>
> 3\.  Within the Deploy Environment section dropdown change the JavaScript VM to the web3 Provider option.
>
> 4\.  Deploy the contract to ganache with the deploy button in Remix

{% code lineNumbers="true" %}
```solidity
pragma solidity ^0.6.6;

contract simpleVulnerableBlockHash {
  uint32 public block_number;
  bytes32 public checkHash;
 
  function get_block_number() public  {   
    block_number = uint32(block.number);
  }
 
  function check_hash() public{
     checkHash = bytes32(blockhash(block_number));
     
  }
 
  function wasteTime() public{
     uint test = uint(block.number);
  }
 
}
```
{% endcode %}

The simple contract above is querying for the current block number in the get\_block\_number function on line 7 and storing it within a block\_number variable created on line 4.  This is the current block number running on the blockchain.

Then we have a function on line 11 which takes the block number and uses it with the blockhash button to retrieve the blockhash and store it in the myHash variable.

## Blockhash Vulnerability

**Action Steps:**

> 1\.  Execute the get\_block\_number function
>
> 2\.  Execute the set\_hash function
>
> 3\.  Check the block\_number value
>
> 4\.  Check the myHash value
>
> 5\.  Execute the wasteTime function 256 times
>
> 6\.  Execute the set\_hash function
>
> 7\.  Check your myHash Value
>
> 8\.  What happened and what implications would this have on calculations your using this value with?





## REFERENCES

* [https://console-cowboys.blogspot.com/2020/10/smart-contract-hacking-final-free.html](https://console-cowboys.blogspot.com/2020/10/smart-contract-hacking-final-free.html)
* [https://github.com/cclabsInc/BlockChainExploitation/blob/master/2020\_BlockchainFreeCourse/bad\_randomness/simpleVulnerabileBlockHash.sol](https://github.com/cclabsInc/BlockChainExploitation/blob/master/2020\_BlockchainFreeCourse/bad\_randomness/simpleVulnerabileBlockHash.sol)
* [https://docs.chain.link/docs/get-a-random-number](https://docs.chain.link/docs/get-a-random-number)
* [https://nvd.nist.gov/vuln/detail/CVE-2018-14715](https://nvd.nist.gov/vuln/detail/CVE-2018-14715)

