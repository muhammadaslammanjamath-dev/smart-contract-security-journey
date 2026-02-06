# Level 15: Naught Coin

Date: February 4, 2026

## What I Learned

ERC20 tokens have two transfer methods.

## The Bug

Contract locked transfer() for 10 years.

But forgot to lock `transferFrom()`!

## How I Did It

1. Approve myself to spend my own tokens
2. Use transferFrom to move tokens out
3. Bypass the 10-year lock
javascript
await contract.approve(player, balance)
await contract.transferFrom(player, "0x000...", balance)


## Why It Matters

**Must lock ALL transfer paths, not just one.**

ERC20 has multiple ways to move tokens:
- transfer()
- transferFrom()
- And others

Lock ONE method = partial protection = no protection.

## The Fix

Override ALL transfer methods with lock.

Or use _beforeTokenTransfer() hook (locks everything).

## Key Lesson

Check inherited functions from OpenZeppelin.

Incomplete protection = vulnerability.

15/29 done.
