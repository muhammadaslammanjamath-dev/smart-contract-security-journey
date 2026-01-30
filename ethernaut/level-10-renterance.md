# Level 10: Re-entrancy

Date: January 30, 2026
Status: Done

## What I Learned

**Reentrancy attack** - Call a function again before it finishes.

## The Bug

Withdraw function sends money BEFORE updating balance.

So I can:
1. Withdraw 1 ETH
2. Receive 1 ETH
3. My receive() calls withdraw again
4. Balance still says 1 ETH (not updated yet)
5. Get another 1 ETH
6. Repeat until contract empty

## How I Did It

Made attack contract with receive() function that calls withdraw again.

## Why It Matters

- The DAO hack (2016) - $60M stolen
- Biggest attack in Ethereum history
- Ethereum had to hard fork

## The Fix

**CEI Pattern** - Checks, Effects, Interactions

1. Check conditions
2. Update balance FIRST
3. Send money LAST

Or use ReentrancyGuard.

## Key Lesson

Never send money before updating state.

Update state first, send money last.

10/29 done.
