#  Ethernaut Level 18 — MagicNumber (Very Simple)

##  Goal

Deploy a contract that returns `42`.



##  Idea

EVM cannot return values directly.

So we:

1. Store 42 in memory
2. Return 32 bytes from memory



##  Runtime Bytecode (returns 42)


0x602a60005260206000f3


- 2a = 42 in hex
- Store 42 at memory position 0
- Return 32 bytes



##  Full Deployment Bytecode


0x69602a60005260206000f3600052600a6016f3


##  Solve in Console

Paste this in Ethernaut console:


bytecode = "0x69602a60005260206000f3600052600a6016f3"

tx = await web3.eth.sendTransaction({
  from: player,
  data: bytecode
})

solver = tx.contractAddress

await contract.setSolver(solver)


Click **Submit**.


Contract returns `42`.

Level solved.

