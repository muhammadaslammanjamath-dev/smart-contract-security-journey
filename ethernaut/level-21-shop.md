# Level 21: Shop

Date: [Today]

## What I Learned

View functions can read state and return different values on multiple calls.

## The Bug

Shop calls price() twice:
1. First: Check if >= 100 (isSold = false)
2. Second: Set final price (isSold = true)

My price() checks isSold:
- If false: return 100 (pass check)
- If true: return 1 (cheap price!)

## How I Did It

Created attack contract:
y
function price() external view returns (uint) {
    if (shop.isSold()) {
        return 1;  // After sold
    } else {
        return 100;  // Before sold
    }
}


Called shop.buy(), got item for 1 instead of 100.

## Why It Matters

View functions can change return values based on state.

Never call external view functions multiple times expecting same result.

Cache the value.

## The Fix

Call once, cache result, use cached value.

Or use msg.value instead of external function.

## Key Lesson

view ≠ constant

View functions can read changing state.

21/29 done. 72%.


