---
icon: wreath-laurel
---

# Solidity Audit using Mythril

<figure><img src="../../.gitbook/assets/image (235).png" alt="" width="375"><figcaption></figcaption></figure>

## Introduction

[Mythril](https://github.com/Consensys/mythril) is a security analysis tool for EVM bytecode. It detects security vulnerabilities in smart contracts built for Ethereum, Hedera, Quorum, Vechain, Rootstock, Tron and other EVM-compatible blockchains. It uses symbolic execution, SMT solving and taint analysis to detect a variety of security vulnerabilities.

## Installation

```
pipx install mythril
```

## Usage

```
myth analyze <solidity-file>

or

myth analyze -a <contract-address>
```

## Example

### Vulnerable Code

```solidity

contract EtherStore {
    uint256 public withdrawalLimit = 1 ether;
    mapping(address => uint256) public lastWithdrawTime;
    mapping(address => uint256) public balances;
    
    function depositFunds() public payable {
        balances[msg.sender] += msg.value;
    }
    
    function withdrawFunds (uint256 _weiToWithdraw) public {
        require(balances[msg.sender] >= _weiToWithdraw);
        // limit the withdrawal
        require(_weiToWithdraw <= withdrawalLimit);
        // limit the time allowed to withdraw
        require(now >= lastWithdrawTime[msg.sender] + 1 weeks);
        require(msg.sender.call.value(_weiToWithdraw)());
        balances[msg.sender] -= _weiToWithdraw;
        lastWithdrawTime[msg.sender] = now;
    }
 }
```

### Running [Mythril](https://github.com/Consensys/mythril)

```
myth a vulnerable.sol
```



***

## REFERENCES

* [https://github.com/Consensys/mythril](https://github.com/Consensys/mythril)
* [https://gist.github.com/vasa-develop/01f8a36a9129fd43e1ced7eb7769c341](https://gist.github.com/vasa-develop/01f8a36a9129fd43e1ced7eb7769c341)
* [https://github.com/sigp/solidity-security-blog#1-re-entrancy-1](https://github.com/sigp/solidity-security-blog#1-re-entrancy-1)
