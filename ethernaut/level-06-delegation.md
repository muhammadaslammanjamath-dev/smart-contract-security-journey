
## level 6 delegation day 1
Today was light work.
 Reviewed Ethernaut Level 6 (Delegation)
 Read Solidity docs related to delegation / delegatecall Planning to finish the level tomorrow
# Level 6: Delegation 2

Date: January 26, 2026
Status: Done

## The Challenge

Claim ownership of the Delegation contract.

## The Bug

Delegatecall vulnerability. The Delegation contract has a fallback function that delegatecalls to the Delegate contract with arbitrary msg.data.

When you call Delegation with msg.data = pwn() selector:
- Falls back to fallback()
- Delegatecalls Delegate.pwn()
- pwn() executes in Delegation's context
- Changes Delegation's owner to msg.sender
solidity
fallback() external {
    (bool result,) = address(delegate).delegatecall(msg.data);
}


Delegatecall runs the called contract's code but modifies the calling contract's storage.

## How I Did It

Called the contract with pwn() function selector as msg.data:

await contract.sendTransaction({data: "0xdd365b8b"})


This triggered the fallback, which delegatecalled pwn(), changing ownership.

## Why It Matters

Delegatecall is extremely powerful and dangerous. Storage layouts must match exactly, and access control is critical.

Real exploit: Parity Wallet hack (2017) - $150M+ frozen due to delegatecall vulnerability where attacker destroyed library contract that wallets depended on.

## The Fix

Don't expose delegatecall through fallbacks. If absolutely needed:
- Strict access control
- Whitelist allowed functions
- Ensure storage layouts match
- Better: use specific controlled functions instead of fallback

## What I Learned

Delegatecall = run their code, change my storage.

Critical for:
- Proxy patterns (upgradeable contracts)
- But extremely dangerous if misused
- Storage collision can break contracts
- Never allow arbitrary delegatecalls

.

6/29 done.
