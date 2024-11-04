---
icon: ethereum
---

# Fuzzing Ethereum Smart Contract

## Introduction

Fuzzing is known as one of the most efficient techniques to find bugs in software. Sadly, when dealing with Ethereum smart contracts, the number of fuzzers and documentation available is really limited.

## [Echidna](https://github.com/crytic/echidna)

Echidna is a weird creature that eats bugs and is highly electrosensitive (with apologies to Jacob Stanley)

More seriously, Echidna is a Haskell program designed for fuzzing/property-based testing of Ethereum smart contracts. It uses sophisticated grammar-based fuzzing campaigns based on a [contract ABI](https://solidity.readthedocs.io/en/develop/abi-spec.html) to falsify user-defined predicates or [Solidity assertions](https://solidity.readthedocs.io/en/develop/control-structures.html#id4). It is  designed with modularity in mind, so it can be easily extended to include new mutations or test specific contracts in specific cases.

### Installation

```
wget https://github.com/crytic/echidna/releases/download/v2.2.5/echidna-2.2.5-x86_64-linux.tar.gz

tar -xf echidna-2.2.5-x86_64-linux.tar.gz

./echidna
```

### Usage

#### Example Solidity File

flags.sol

```solidity
contract Test {
  event Flag(bool);

  bool private flag0 = true;
  bool private flag1 = true;

  function set0(int val) public returns (bool){
    if (val % 100 == 0) 
      flag0 = false;
  }

  function set1(int val) public returns (bool){
    if (val % 10 == 0 && !flag0) 
      flag1 = false;
  }

  function echidna_alwaystrue() public returns (bool){
    return(true);
  }

  function echidna_revert_always() public returns (bool){
    revert();
  }

  function echidna_sometimesfalse() public returns (bool){
    emit Flag(flag0);
    emit Flag(flag1);
    return(flag1);
  }

}
```

#### Running Echidna

```
./echidna ~/Desktop/solidity/flags.sol
```





***

## REFERENCES

* [https://github.com/crytic/echidna](https://github.com/crytic/echidna)
* [https://secure-contracts.com/program-analysis/echidna/index.html](https://secure-contracts.com/program-analysis/echidna/index.html)
* [https://www.youtube.com/watch?v=EA8\_9x4D3Vk\&list=WL\&index=5\&ab\_channel=FuzzingLabs](https://www.youtube.com/watch?v=EA8\_9x4D3Vk\&list=WL\&index=5\&ab\_channel=FuzzingLabs)
* [https://github.com/crytic/echidna/blob/master/tests/solidity/basic/flags.sol](https://github.com/crytic/echidna/blob/master/tests/solidity/basic/flags.sol)
* [https://docs.soliditylang.org/en/latest/installing-solidity.html](https://docs.soliditylang.org/en/latest/installing-solidity.html)
* [https://fuzzinglabs.com/ethereum-smart-contact-fuzzing-2022/](https://fuzzinglabs.com/ethereum-smart-contact-fuzzing-2022/)
* [https://dev.to/mbogan/avoid-smart-contract-hacks-with-fuzz-testing-1a3a](https://dev.to/mbogan/avoid-smart-contract-hacks-with-fuzz-testing-1a3a)
