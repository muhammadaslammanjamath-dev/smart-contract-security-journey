# Level 5: Token

Date: January 4, 2026
Status: Done

## The Challenge

Get more than 20 tokens.

## The Bug

Integer underflow in Solidity 0.6.0.

The contract tries to check if you have enough balance:
solidity
require(balances[msg.sender] - _value >= 0);


But this check is useless because uint can never be negative. When you subtract below 0, it wraps around to the maximum value.

## How I Did It

Transferred 21 tokens when I only had 20.

await contract.transfer(player, 21)


Math: 20 - 21 = wraps to huge number (2^256 - 1)

Now have unlimited tokens.

## Why It Matters

Before Solidity 0.8.0, integer overflow/underflow was a major issue.

Real exploits:
- BeautyChain: $900M bug
- Multiple token contracts drained

This is why modern Solidity has built-in protection.

## The Fix

Use Solidity 0.8.0+ (automatic overflow/underflow checks).

Or for older versions, use SafeMath:
solidity
using SafeMath for uint;
balance = balance.sub(value);


## What I Learned

uint wrapping: subtraction below 0 = wraps to max value.

Always check Solidity version. Pre-0.8.0 needs SafeMath.

When auditing, old Solidity + unchecked math = vulnerability.

5/29 done.
