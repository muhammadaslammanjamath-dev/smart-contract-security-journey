# Level 25: Motorbike



## Visual Summary

UUPS Proxy + Uninitialized Implementation

Proxy → delegates to → Engine (initialized)
BUT
Direct call → Engine (uninitialized!)

Attack:
1. Find Engine address from storage slot
2. Call Engine.initialize() directly
3. Become upgrader
4. Deploy Bomb (selfdestruct)
5. Upgrade Engine to Bomb
6. Trigger selfdestruct
7. Engine destroyed → Proxy broken


## The Bug

Implementation not initialized in its own context.
Only initialized through proxy delegatecall.
Direct calls to implementation = unprotected.

## Core Patterns

- Pattern 2: Access Control (uninitialized = no protection)
- Pattern 4: Logic Error (initialization logic flaw)
- Pattern 5: External Dependency (proxy depends on impl)

## Key Lesson

UUPS implementations MUST disable initializers in constructor.
Never leave implementation contracts uninitialized.
Selfdestruct breaks all proxies pointing to it.

25/~40 done. 62% complete.

---
