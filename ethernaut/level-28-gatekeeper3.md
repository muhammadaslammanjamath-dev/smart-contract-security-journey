# Level 28: Gatekeeper Three

Date: [Today]

## Visual Summary

Three gates to pass:
1. Gate 1: Become owner via construct0r() typo
2. Gate 2: Set allowEntrance via password
3. Gate 3: Make send() fail (no receive function)

Attack: Deploy contract without receive(), call all steps

## The Bugs

1. construct0r() typo - not a constructor
2. Private password still readable from storage
3. Logic assumes send() succeeds

## Core Patterns

- Pattern 2: Access Control (typo exploit)
- Pattern 4: Logic Error (send failure assumption)
- Pattern 5: External Dependency (send() return)

## Key Lesson

Constructor typos create ownership vulnerabilities.
Send() can fail if receiver can't accept ETH.
Private variables still readable from storage.

28/~40 done. 70% complete.

---
