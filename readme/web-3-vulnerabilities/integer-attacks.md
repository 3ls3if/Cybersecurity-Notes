# 🌇 Integer Attacks

## Vulnerable Code

Below is the function from the ERC20 contract which had the initial vulnerability.  Also, a link to view the code for yourself on etherscan.  Just do ctrl+f search for the batch transfer function on the contract page.

{% embed url="https://etherscan.io/address/0xc5d105e63711398af9bbff092d4b6769c82f793d#code" %}

{% code lineNumbers="true" %}
```solidity
pragma solidity 0.6.6;

contract BEC_Target{

    mapping(address => uint) balances;

    function batchTransfer(address[] memory _receivers, uint256 _value) public returns (bool) {
        uint cnt = _receivers.length;
        uint256 amount = uint256(cnt) * _value;
        require(cnt > 0 && cnt <= 20);
        require(_value > 0 && balances[msg.sender] >= amount);

        balances[msg.sender] = balances[msg.sender]-amount;
        for (uint i = 0; i < cnt; i++) {
            balances[_receivers[i]] = balances[_receivers[i]]+_value;
            // Transfer(msg.sender, _receivers[i], _value);
        }
        return true;
    }

    function deposit() public payable {
        balances[msg.sender] += msg.value;
    }

    function getBalance() public view returns(uint){
        return balances[msg.sender];
    }

}
```
{% endcode %}



The issue with the `batchTransfer()` function is it’s performing a balance check against the amount on line 11 but that amount value comes from a mathematical operation on line 9 which has an overflow vulnerability.

You will see that the amount results from multiplying the length of the array times the value being sent. Since there are no checks that this mathematical operation does not overflow to a value lower than our balance, we can easily set the amount to 0 using a very large number as our \_value.

When the actual balances are updated on line 15, we are not using the amount of 0, but instead we are using the initial large \_value sent to the function, but this time there is no multiplication,  so it does not cause an overflow, it only updates the value to a very large number.&#x20;



## Fixing the code using SafeMath Library

```solidity
// SPDX-License-Identifier: MIT

pragma solidity 0.8.0;

// import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/math/Math.sol";

import "@openzeppelin/contracts/utils/math/SafeMath.sol";

contract BEC_Target{

    using SafeMath for uint256;

    mapping(address => uint) balances;

    function batchTransfer(address[] memory _receivers, uint256 _value) public returns (bool) {
        uint cnt = _receivers.length;
        uint256 amount = SafeMath.mul(uint256(cnt), _value);
        require(cnt > 0 && cnt <= 20);
        require(_value > 0 && balances[msg.sender] >= amount);

        balances[msg.sender] = SafeMath.sub(balances[msg.sender], amount);
        for (uint i = 0; i < cnt; i++) {
            balances[_receivers[i]] = SafeMath.add(balances[_receivers[i]], _value);
            // Transfer(msg.sender, _receivers[i], _value);
        }
        return true;
    }

    function deposit() public payable {
        balances[msg.sender] += msg.value;
    }

    function getBalance() public view returns(uint){
        return balances[msg.sender];
    }

}
```





## REFERENCES

* [https://console-cowboys.blogspot.com/2020/08/smart-contract-hacking-chapter-3.html](https://console-cowboys.blogspot.com/2020/08/smart-contract-hacking-chapter-3.html)

