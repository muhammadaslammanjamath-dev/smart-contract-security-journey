# Level 17: Recovery

Date: February 6, 2026

## What I Learned

Contract addresses are predictable (calculated from deployer + nonce).

## The Challenge

Token contract was created but address was "lost".

Had 0.001 ETH in it.

Need to find it and recover the ETH.

## How I Did It

**Method 1: Etherscan**
1. Got Recovery contract address
2. Searched on Sepolia Etherscan
3. Checked "Internal Txns" tab
4. Found SimpleToken address
5. Called destroy() function
6. ETH sent to me 

**Method 2: Calculate**
- Contract address = keccak256(deployer, nonce)
- Recovery created token at nonce 1
- Can calculate the address

## The Vulnerability

SimpleToken has destroy() with NO access control.

Anyone can call selfdestruct and steal the ETH.

## Why It Matters

1. Contract addresses are NOT random
2. "Lost" contracts can be found
3. selfdestruct needs protection
4. Blockchain is fully transparent

## The Fix

Add access control to destroy():
- require(msg.sender == owner)
- Or don't use selfdestruct at all

## Key Lesson

Nothing is truly "lost" on blockchain.

Everything is traceable.

Protect destructive functions.

17/29 done.
