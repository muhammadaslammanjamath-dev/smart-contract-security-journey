## Level 4: Telephone (In Progress)

Started looking at this. tx.origin vs msg.sender issue.

Need to finish tomorrow. Traveling today.

Working on it

## level 4: telephone day 2 

date: jan 23, 2026
status: done
goal
take ownership of the contract.

the bug
the contract checks tx.origin instead of msg.sender.

tx.origin = the wallet that started the transaction

msg.sender = who is calling the function right now

the contract says:
**if tx.origin != msg.sender, change owner.**

that’s bad.

**if (tx.origin != msg.sender) {
    owner = _owner;**
}
exploit
call the contract through another contract.

i start tx → tx.origin = me

my contract calls target → msg.sender = attack contract

not equal → check passes

i become owner

**contract TelephoneAttack {
    function attack() public {
        telephone.changeOwner(msg.sender);
    }
}**

why this is bad
**using tx.origin lets malicious contracts trick users.**
**real phishing attacks use this.**.

fix
never use tx.origin.

**require(msg.sender == owner);**

lesson
if i see tx.origin for auth → it’s a vulnerability.

progress
4/29  done
