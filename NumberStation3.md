Executing the command provided, we get an encrypted message:

![](img/Screenshot%202022-12-15%20at%2009.59.57.JPG)

Analysing the program provided, we found out it was composed of three functions: one that generated a key, another that encrypted it and another that decrypt it.
In the generator function, we see its range is 16; as such, there are 2^16 possibilities to find the flag. Because of this, we just needed to create a loop that run the program 2^16 times, or until it found a key starting with "flag". We also removed any  lines that depended on ``FLAG_FILE``, as we didn't use that variable and it would cause an error. This was the program used:

```py
shell = b"9124f3619b985a12fef8690483992d18b5fa3c0c40c49c9d0c8815690881955e6d52712c1c48316f87c3461ef9ed073d65409154fd32d5d24ed61927db5bf819abb476932e05c95f84df1dc1d9bfdbf26d52712c1c48316f87c3461ef9ed073ded4cd307624f7b151a84bda3e288932e1db1169390f3f3aa6117d26c329759119cb2886df6783bdeee63a3bcf2250319dbc5cbe16170d9bb01e89c730cc3c0d61adee304db06a00569549f9fba4d6d4ed4cd307624f7b151a84bda3e288932e1db1169390f3f3aa6117d26c3297591f7b79330929fde7fc788bee0c32ca517d3d2c56fa8be10767519dac90bb5e74815b51161c4d98167889e1772e30f9bffd61adee304db06a00569549f9fba4d6d45b51161c4d98167889e1772e30f9bffd6d52712c1c48316f87c3461ef9ed073dd011718304875bce0fe1721e02157b491db1169390f3f3aa6117d26c3297591fd011718304875bce0fe1721e02157b49ed4cd307624f7b151a84bda3e288932e9dbc5cbe16170d9bb01e89c730cc3c0d8298bb2722ea9bf49e30ddcad9aa93383d2c56fa8be10767519dac90bb5e74819dbc5cbe16170d9bb01e89c730cc3c0daa345beb2a9718a79e9b7ff8fc2126c7d011718304875bce0fe1721e02157b49d011718304875bce0fe1721e02157b49c0d5db61206a09c16d4f28837552d096c0d5db61206a09c16d4f28837552d096dc92bc2c6b24906ea6936b70c1bf45c5d011718304875bce0fe1721e02157b49d011718304875bce0fe1721e02157b496d52712c1c48316f87c3461ef9ed073d3d2c56fa8be10767519dac90bb5e748136e04744e6107a77e2e492f2f08b0aaa737d41e51a0a15b8a9da6b314ea69f70"

for i in range(2**16):
	print (i)
	key2 = gen()
	if (dec(key2, unhexlify(shell)).decode('latin-1')[0:4] == "flag"):
		print(dec(key2,unhexlify(shell)).decode('latin-1'))
		break
```

Our flag:

![](img/Screenshot%202022-12-15%20at%2010.27.52.JPG)