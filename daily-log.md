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

## Day 9 - January 28, 2026

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



