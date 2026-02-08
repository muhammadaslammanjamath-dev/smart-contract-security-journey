# Level 16: Preservation

Date: February 9, 2026

## What I Learned

Delegatecall storage collision with mismatched layouts.

## The Bug

Library has different storage layout than Preservation.

When delegatecall happens:
- Library writes to slot 0
- But slot 0 in Preservation = timeZone1Library
- Overwrites library address!

## How I Did It

**Step 1:** Deploy attack contract with MATCHING layout

**Step 2:** Call setFirstTime(attackAddress)
- Overwrites timeZone1Library with my contract

**Step 3:** Call setFirstTime(myAddress)
- Now calls MY contract via delegatecall
- MY contract writes to slot 2 (owner)
- I become owner 

## Why It Matters

Delegatecall with mismatched storage = critical vulnerability.

Must match:
- Variable order
- Variable types
- Exact layout

One mismatch = exploitable.

## The Fix

Match storage layouts exactly.

Or better: don't use delegatecall for external contracts.

Or best: use library keyword for stateless helpers.

## Key Lesson

Storage layout is CRITICAL for delegatecall safety.

16/29 done.
