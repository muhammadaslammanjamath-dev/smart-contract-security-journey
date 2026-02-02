# Level 12: Privacy

Date: February 1, 2026
Status: Done

## What I Learned

Advanced storage reading with packing.

## The Bug

Private array data[3] is readable from blockchain.

Need to find data[2] which is in storage slot 5.

## Storage Layout

Variables that fit in 32 bytes together = packed in same slot.

Slot 0: locked (bool)
Slot 1: ID (uint256) - takes full slot
Slot 2: flattening + denomination + awkwardness (packed)
Slot 3: data[0]
Slot 4: data[1]
Slot 5: data[2] ← We need this


## How I Did It

Read slot 5, converted bytes32 to bytes16, unlocked.
javascript
const slot5 = await web3.eth.getStorageAt(instance, 5)
const key = slot5.slice(0, 34)  // bytes32 → bytes16
await contract.unlock(key)


## Why It Matters

Private doesn't mean secret. Storage packing doesn't hide data.

Everything on blockchain is readable if you know which slot to read.

## Key Lesson

Never store secrets on-chain. Understand storage layout for security auditing.

12/29 done.
