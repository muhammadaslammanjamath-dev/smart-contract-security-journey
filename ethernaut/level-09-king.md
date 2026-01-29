# Level 9: King

Date: January 29, 2026

## What I learned

DoS attack - Make contract unable to function.

The King contract sends ETH to previous king when new person becomes king.

I made a contract that can SEND ETH but can't RECEIVE ETH.

When I become king, and someone tries to become new king, the contract tries to send me ETH but I reject it. Transfer fails. Transaction reverts. They can't become king.

This is called Denial of Service (DoS).

The fix: Don't send ETH directly. Let people withdraw it themselves.

9/29 done.
