# Level 20: Denial

Date: [Today]

## What I Learned

DoS attack by consuming all gas.

## The Bug

Contract calls partner with no gas limit.

If partner uses ALL gas (infinite loop), owner's transfer fails.

Transaction reverts, owner can't withdraw.

## How I Did It

Created attack contract:

fallback() external payable {
    while(true) {}  // Infinite loop
}


Set it as partner.

Now owner can't withdraw (no gas left for them).

## Why It Matters

External calls without gas limits = DoS risk.

Attacker can block functionality by wasting gas.

## The Fix

1. Set gas limits on external calls
2. Separate withdrawal functions
3. Use pull pattern (users claim vs contract sends)

## Key Lesson

Never use unlimited gas for external calls.

Always set gas limits.

20/29 done
