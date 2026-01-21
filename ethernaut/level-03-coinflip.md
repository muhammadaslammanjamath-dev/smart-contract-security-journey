## Level 3: Coin Flip

Date: January 21, 2026
Status: Done

## The Challenge

Win the coin flip 10 times in a row.

## The Bug

The contract uses blockhash to generate a "random" coin flip. But blockhash is public information on the blockchain. Anyone can read it and do the same calculation to know what the result will be.
solidity
uint256 blockValue = uint256(blockhash(block.number - 1));
uint256 coinFlip = blockValue / FACTOR;
bool side = coinFlip == 1 ? true : false;


If I can calculate the same thing, I know the answer before guessing. Not random.

## How I Did It

Made a contract that does the exact same calculation, figures out what the result will be, then calls flip() with the correct answer.

Had to call it 10 times, waiting about 15 seconds between each call for new blocks. Won every time because I knew the answer.

## Why It Matters

Seen this in real protocols. NFT drops where someone got all the rare ones. Lottery contracts that got drained. Casino games that got manipulated.

If you use public blockchain data for randomness, anyone can predict it. Blockchain has no secrets.

## The Fix

Use Chainlink VRF for actual randomness from off-chain sources. Or use commit-reveal patterns.

Don't use blockhash, block.timestamp, or block.number for anything random.

## What I Learned

Blockchain is completely public. If I can read the same data the contract reads, I can predict the outcome.

When I see blockhash or block data used for randomness in an audit, that's a vulnerability.

3/29 done.

