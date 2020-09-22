# Shell This

![](https://i.imgur.com/eBrZgDc.png)

## Challenge Overview

This was a simple pwn challenge that was begginer friendly since we had the source code.
The binary was using gets for user input that is vulnerable to a `BOF` attack and all we had to do was call the `get_shell` function and spawn a shell ;).

![](https://i.imgur.com/jiyXWy2.png)

No PIE and stack cookie therefore we are ready to go \0/.[exploit.py](exploit.py)

## Flag
`DUCTF{h0w_d1d_you_c4LL_That_funCT10n?!?!?}`
