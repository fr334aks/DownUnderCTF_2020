# Return To What

#### Category: `Pwn`
#### Points: `200`

> This will show my friends!
>
> `nc chal.duc.tf 30003`
>
> Attachment 

## Challenge Overview

This challenge was a `return to libc` challenge similiar to [shellthis](shellthis) but this time we do not have a function to return to. We have to be creative to spawn a shell and read the flag. We are not provided with the libc version or any libc file. We therefore have to leak the libc address and look it from the libc database to get the libc version.

## Exploit

We will leak the libc address using `puts` and `puts@got` and get the libc version. We will finally get the offsets and return to system and spawn a shell.
Remember the calling convention in 64-bit systems where arguments are stored in registers.

`A*offset + ret + pop_rdi + bin_sh + system`

Full exploit [exploit.py](exploit.py)

## Flag

`DUCTF{ret_pUts_ret_main_ret_where???}`



