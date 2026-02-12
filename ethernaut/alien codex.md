# Level 18: Alien Codex



## What I Learned

Array underflow + storage collision = full storage control.

## The Bug

Two bugs combined:

1. **Array underflow:** `codex.length--` when length = 0
   - Results in length = 2^256-1
   - Array now "spans" all storage

2. **Storage collision:** Can calculate index to reach any slot
   - Including slot 0 (owner)

## How I Did It

1. makeContact() - enable functions
2. retract() - underflow array
3. Calculate index: 2^256 - keccak256(1)
4. revise(index, myAddress) - overwrite owner


## Why It Matters

Underflow in old Solidity = critical.

Can access ANY storage slot through arrays.

Modern Solidity (0.8.0+) prevents this automatically.

## The Fix

Use Solidity 0.8.0+ (auto-checks) or add manual checks.

## Key Lesson

Storage layout + arithmetic overflow = dangerous combo.

Always use latest Solidity version.

18/29 done.
