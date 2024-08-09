# 🎆 Reentrancy Vulnerabilities

## 1. Reentrancy Vulnerability

The EtherStore Reentrancy Vulnerability is a flaw in the smart contract design that allows an attacker to exploit reentrancy and withdraw more funds than they are entitled to from the EtherStore contract. The vulnerability arises due to the withdrawFunds function in the EtherStore contract, where the Ether is transferred to the attacker's address before updating their balance. This allows the attacker's contract to make a reentrant call back to the withdrawFunds function before the balance update, leading to multiple withdrawals and potentially draining all the Ether from the EtherStore contract.

**Read More** [Here](https://github.com/SunWeb3Sec/DeFiVulnLabs/blob/main/src/test/Reentrancy.sol)**.**



## 2. Cross-Function Reentrancy Vulnerability

**Cross-function reentrancy** is another level of **reentrancy** in terms of complexity. Typically, the root cause of this issue is that there are multiple functions mutually sharing the same state variable, and some of them update that variable insecurely.

**Read More** [Here](https://medium.com/valixconsulting/solidity-smart-contract-security-by-example-04-cross-function-reentrancy-de9cbce0558e)**.**







