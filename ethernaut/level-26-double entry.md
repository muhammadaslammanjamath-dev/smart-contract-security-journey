# Ethernaut – Double Entry Point

## Level Goal

Prevent the CryptoVault from being drained by detecting a hidden delegateTransfer() backdoor using a Forta Detection Bot.

---

##  Vulnerability Overview

The vulnerability exists because:

1. CryptoVault.sweepToken() calls LegacyToken.transfer()
2. LegacyToken.transfer() internally calls DoubleEntryPoint.delegateTransfer()
3. delegateTransfer() uses delegatecall
4. The original sender becomes the vault
5. The vault’s tokens can be drained

The system relies on Forta to detect suspicious activity.

---

##  Objective

Create and register a Detection Bot that:

- Monitors transactions
- Detects when delegateTransfer() is triggered
- Identifies if the origSender is the CryptoVault
- Calls raiseAlert() to block the transaction

---

## 🛠 Solution Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

interface IForta {
    function raiseAlert(address user) external;
}

contract DetectionBot {

    address public vault;

    constructor(address _vault) {
        vault = _vault;
    }

    function handleTransaction(address user, bytes calldata msgData) external {

        address origSender;

        assembly {
            origSender := calldataload(0xa8)
        }

        if (origSender == vault) {
            IForta(msg.sender).raiseAlert(user);
        }
    }
}
