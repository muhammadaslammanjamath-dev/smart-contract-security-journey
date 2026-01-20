# Level [2]: [fallout]

**Date:** [20/01/2026]
**Status:** Done
**Time:** [1 hour]



## What I Had to Do

[Become the owner of the contract]



## The Bug

[So there's this function called Fal1out() - notice the 1 instead of l.

In old Solidity (before version 0.4.22), constructors had to match the contract name exactly. Contract called Fallout needs constructor called Fallout().

But this one says Fal1out() with a 1. That's a typo.

Which means it's not a constructor at all. It's just a regular public function anyone can call.
solidity
function Fal1out() public payable {
    owner = msg.sender;
    allocations[owner] = msg.value;
}


The comment says /* constructor */ but comments don't matter. The compiler sees a public function.
]


## How I Beat It

Called the function:
javascript
await contract.Fal1out()


Checked if I'm owner:
javascript
await contract.owner()


Yep. That's my address now.

Took like 20 minutes total including figuring out what was wrong.

## Why This Matters

Back in the day, if you renamed your contract but forgot to update the constructor name, boom - public ownership function.

I've actually seen protocols where this happened. Someone calls the "constructor" months after deployment and takes over the whole thing.

Users think it's a rug pull. It's just a typo that became an exploit.

As someone who's deposited into sketchy contracts before, this is exactly why I check the code first now. Old Solidity version? No explicit constructor() keyword? I'm out.



## The Fix
Modern Solidity uses the constructor keyword:
solidity
constructor() public {
    owner = msg.sender;
}


Can't typo that. And it only runs once on deployment.

Much better.

## What I Got From This

Old Solidity = constructors match contract name
- Typo = not a constructor, just public function
- Comments mean nothing to code
- Always use constructor() keyword
- Check Solidity version before trusting contracts




2/29 done.

Next one is [coin flip].
