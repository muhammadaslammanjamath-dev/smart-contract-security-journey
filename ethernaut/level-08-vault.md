
# Level 8: Vault

Date: January 28, 2026
Status: Done

## The Challenge

Unlock the vault.

The contract is locked and requires a password to unlock it.

## The Bug

The password is stored on-chain as a private variable.

The Vault contract:

contract Vault {
bool public locked;
bytes32 private password;


constructor(bytes32 _password) {
    locked = true;
    password = _password;
}

function unlock(bytes32 _password) public {
    if (_password == password) {
        locked = false;
    }
}

}

Developers assume private means secret, but all blockchain storage is public.

Anyone can read contract storage directly.

## How I Did It

I read the password directly from the contract’s storage.

Solidity stores variables in slots:
Slot 0: locked
Slot 1: password

Using the browser console, I read slot 1:

await web3.eth.getStorageAt(instance, 1)

This returned the password.

Then I passed that value into unlock():

await contract.unlock(PASSWORD_FROM_STORAGE)

The vault unlocked successfully.

## Why It Matters

Developers often assume:
Private variables are hidden
Passwords stored on-chain are safe
Users cannot read contract storage

All of these are false.

This breaks:
Authentication logic
Password-based security
Any contract relying on hidden values

## The Fix

Never store secrets on-chain.

Instead:
Store hashes instead of secrets
Use signature-based authentication
Verify data off-chain

Example using a hash:

bytes32 public passwordHash;

function unlock(string calldata password) external {
require(
keccak256(abi.encodePacked(password)) == passwordHash
);
}

## What I Learned

Private does not mean secret.

All contract storage is publicly readable.

Secrets should never be stored directly on-chain.

Progress: 8 / 29 done 
