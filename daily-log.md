# Daily Log

## Day 1 - January 19, 2026

**Completed:**
- Set up GitHub
- Level 1 ethernaut

Status:success

## Day2 -January 20, 2026

**Completed**

- level 2 ethernaut
- solidity document review

 Status:sucess

 ## Day 3- January 21 2026

 **Completed**

 - level 3 ethernaut
 - coin flip level
  
  status :success

## Day 4 - January 22,2026

Travel day to Dubai.

Did 30 min research on Level 4
Understand the vulnerability
Will complete tomorrow.

## day 5 - January 23 , 2026

Completed level 4 of Ethernaut and understood,
how the contract uses tx.origin instead of msg.sender.

It was a small concept, but an important one

 ## - Day 6 january 24 , 2026
Completed
• Ethernaut Level 5: Token
• Learned about integer underflow
• First time exploiting math vulnerability
*Learned:*
 How uint wrapping works
 Why Solidity 0.8.0+ is important
 SafeMath for older contracts

 ## Day 7 January 25,2026

 Today was very minimal work—just looked at Level 6 and read the Solidity docs about delegation.

 ## Day 8 - January 26, 2026

**Completed:**
- Ethernaut Level 6: Delegation
- Learned delegatecall mechanics
- Understanding proxy patterns now

**Learned:**
- Delegatecall runs code but changes caller's storage
- Storage layout must match exactly
- Never expose delegatecall through fallback
- Parity Wallet hack was delegatecall-related

**Situation:**
- 6-day streak alive
- Building foundation

**Tomorrow:**
- Level 7: Force
- Continue job search
- Keep building

**Status:**  Day 8 complete. 6/29 Ethernaut.

## Day 9 - January 27, 2026

**Completed:**
- Ethernaut Level 7: Force
- Learned about selfdestruct forced transfers
- First time deploying attack contract via Remix

**Learned:**
- selfdestruct forces ETH into any address
- Target contract can't refuse
- address(this).balance is unreliable for logic
- Always track balances in state variables

**Situation:**
- 9-day streak in chaos



**Tomorrow:**
- Level 8: Vault
- This one involves reading private storage
- Will use the storage reading techniques

**Status:**  Day 9 done. Full week complete. 7/29 Ethernaut


## Day 10  January 28, 2026

Level: 8 – Vault

What I Did

Read the Vault contract

Checked storage layout

Read password from storage

Unlocked the contract

Bug / Concept

Private variables are not secret

On-chain storage is public

How It Was Exploited

Read storage slot 1

Used the value to unlock the vault

What I Learned

Never store secrets on-chain

Private only hides from Solidity

Progress

8 / 29 levels completed

## Day 11 - January 29, 2026

**Completed:**
- Ethernaut Level 9: King
- DoS (Denial of Service) attack
- Learned withdrawal pattern

**Learned:**
- DoS via failed ETH transfers
- Contracts can reject ETH (no receive/fallback)
- Push vs Pull payment patterns
- External calls can always fail
- Withdrawal pattern is best practice

**Attack:**
- Created contract without receive()
- Became king
- Anyone trying to reclaim → transfer fails → reverts
- Permanent king (DoS)

**Situation:**
- 9-day streak strong
- Week 1+ complete
- Pattern library growing

**Tomorrow:**
- Level 10: Re-entrancy (THE classic attack)
- Most famous vulnerability in Ethereum

**Status:** Day 9 complete. 9/29 Ethernaut. DoS attacks understood. Moving to reentrancy (the big one).

## Day 12 - January 30, 2026

**Level:** Re-entrancy

**Attack:** Reentrancy - withdraw multiple times before balance updates

**How it works:** 
- Withdraw sends money first
- My contract receives it
- My contract calls withdraw again
- Balance not updated yet
- Get money again
- Repeat

**Real hack:** The DAO (2016) - $60M

**Fix:** Update balance BEFORE sending money (CEI pattern)

**Status:** 10/29

## Day 13

**What I did:** Tricked elevator

**How:** Made light switch that flips each time elevator asks

**Result:** Elevator gets different answers, sets top = true

**Lesson:** Can lie by flipping switch

11/29

## Day 14 
**what I did :** just have a look at ethernault level 12

## Day 15

**Level:** Privacy

**Attack:** Read private array from storage slot 5

**Storage packing:** Multiple small variables can share one slot

**Learned:** 
- How to calculate storage slots with packing
- bytes32 → bytes16 conversion
- Fixed arrays take consecutive slots

## Day 16 
# Level 13: Gatekeeper One

Date: February 3, 2026

## What I Learned

Three gates: contract caller, exact gas, complex key.

## Day 17 
just have a look at level 14
ethernuat gatekeeper two

## Day 18 - February 5, 2026

**Level:** Gatekeeper Two

**Attack:** Constructor timing + XOR

**Key lesson:** Constructor = code size 0

14/29. 48% complete.
**Level:** Naught Coin

**Attack:** Bypass transfer lock using transferFrom

**ERC20 learned:**
- transfer() vs transferFrom()
- approve() mechanism
- allowances
- Self-approval trick

**Key lesson:** Lock ALL methods, not just one

15/29. Over halfway!









