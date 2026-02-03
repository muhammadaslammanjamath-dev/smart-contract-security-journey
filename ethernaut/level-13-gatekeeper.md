# Level 13: Gatekeeper One

Date: February 2, 2026

## What I Learned

Three gates: contract caller, exact gas, complex key.

## Gate One

msg.sender != tx.origin

Solution: Call through my contract

## Gate Two

gasleft() % 8191 == 0

Solution: Bruteforce gas amount

## Gate Three

Complex type conversions

Solution: key = my address last 2 bytes | 0xFFFFFFFF00000000

## How I Did It

Made attack contract that:
1. Creates key from my address
2. Tries different gas amounts in loop
3. Eventually finds right amount
4. Passes all gates

## Key Lesson

Type conversion cuts from left side.
uint64 → uint32 = keeps right 4 bytes.

Can bruteforce gas amounts.

13/29 done.
