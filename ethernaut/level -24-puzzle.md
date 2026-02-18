# Level 24: Puzzle Wallet



## Visual Summary

Storage Collision:
Proxy Slot 0 = pendingAdmin ←→ owner
Proxy Slot 1 = admin ←→ maxBalance

Attack:
1. Set pendingAdmin → become owner
2. Whitelist self
3. Nested multicall → inflate balance
4. Drain contract
5. Set maxBalance to address → become admin


## The Bugs

1. **Storage collision**: Proxy and Wallet share slots
2. **Multicall bypass**: Nested calls reset depositCalled flag
3. **Balance inflation**: Deposit credited twice, value sent once

## Core Patterns

- Pattern 1: State Inconsistency (storage + multicall)
- Pattern 2: Access Control (become owner)
- Pattern 4: Logic Error (multicall check)

## Complexity

Hardest Ethernaut level
Combines 3 vulnerabilities
Multi-step attack required

## Key Lesson

Proxy patterns MUST have matching storage layouts.
Multicall functions vulnerable to nested call bypasses.
Always check balance accounting matches actual transfers.

24/29 done. 83% complete.

---
