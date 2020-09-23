# My first echo server

>**Category**: `Pwn`
>
>**Points**: `416`
>
>Hello there! I learnt C last week and already made my own SaaS product, 
>check it out! I even made sure not to use compiler flags like --please-make-me-extremely-insecure
>so everything should be swell.
>
> `nc chal.duc.tf 30001`
>
>Hint - The challenge server is running Ubuntu 18.04.
>
> **Attachment**: [echos](echos)
## Challenge Overview

The Binary is a 64-bit elf exceutable that has a `FSB` and that is a loop that exits after three inputs. The binary has all protections enabled :(

## Exploit Overview

We will exploit the challenge in the following steps:

* ### Leak Addresses

Since `PIE` is enabled we will leak some address from the stack. Looking at the stack we see the address of main at `%23$p`.We can then use it to get the base address
of the binary by subracting main's offset.

`libc_base = leaked_address - address_of_main`

We will also leak the stack address to find the `return address` and the address of local variable's in the stack that will be useful later to create an infinite loop.
This stack address is located at `%16$p`. 

`return_address = leaked_address - 216`

After we leaked the addresses we will now have the `base address` of the binary and `return address` of the stack.

* ### Libc Address 

Since we have the `base_address` we can now leak the address from `printf@got` and get the address of printf. `%s` is used to read values in specified addresses.
The leaked addresses can then be used to obtain the libc version of the binary. Hmmm.....One more input to go and the program exits :( any ideas on what to do next?

* ### Over~Writing the Loop variable to get infinite writes

Since we already have the `return_address` we all know that `rsp` the stack pointer is located right before the `return address` and all variables on the stack are
refrenced with `rsp`. Looking at the disassembly we can see that the loop variable is located at `rsp-0x54`.

`variable = (return_address - 8) - 0x54`

Our goal is to overwrite this value with a negative value that will give us a inifinite loop. I choose 0xfffffff6 (-10) and i used `fmtstr_payload` from pwntools.

`payload = fmtstr_payload(8, {variable:0xfffffff6})`

* ### Over write the return address

Finally.... We can now control the return address. First we need to remember the hint from the challenge. `Ubuntu 18.04`.
We want to overwrite the return address so that it will return to system. The `MOVAPS` issue in `Ubuntu 18.04`, so we have to prepend `ret`
to spawn a shell.

Using 'ropper' we can find the `pop_rdi`, `ret` gadgets offsets. Since we leaked the libc address we can get the offset for `system` & `bin_sh`,
We will finally overwrite the address with  `ret + pop_rdi + _bin_sh + system`.


* ### Exit the loop
To exit the loop we have to overwrite the local variable on the stack with a number greater than 2 and the loop exits and spawns a shell :D.

The final exploit [exploit.py](exploit.py)
