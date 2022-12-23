# Task 1

![alt text](img/Screenshot%202022-12-06%20at%2009.20.53.JPG)

Changed the ``openssl.cnf`` file to use the one in our directory. 

![alt text](img/Screenshot%202022-12-06%20at%2009.25.03.JPG)

Created the CA certificate.

![alt text](img/Screenshot%202022-12-06%20at%2009.29.56.JPG)

The part that shows it's a CA certificate is:

````
X509v3 extensions:
            X509v3 Subject Key Identifier: 
                4F:F0:8C:9F:6C:C5:D7:CA:82:A8:18:1A:87:93:A6:81:B1:7E:DF:02
            X509v3 Authority Key Identifier: 
                keyid:4F:F0:8C:9F:6C:C5:D7:CA:82:A8:18:1A:87:93:A6:81:B1:7E:DF:02

            X509v3 Basic Constraints: critical
                CA:TRUE
````

It's self-signed because both the Subject Key Identifier and the Autority  Key Identifier are the same.

![alt text](img/Screenshot%202022-12-06%20at%2009.30.52.JPG)

Public exponent:
```
publicExponent: 65537 (0x10001) 
```

![alt text](img/Screenshot%202022-12-06%20at%2009.31.16.JPG)

The private exponent and the modulus are show in the two pictures above, and the secret numbers <i>p</i> and <i>q</i> are the numbers below prime1 and two, respectively.

# Task 2
![alt text](img/Screenshot%202022-12-06%20at%2009.47.57.JPG)

Genereated the CA to the website.

![alt text](img/Screenshot%202022-12-06%20at%2009.50.04.JPG)

![alt text](img/Screenshot%202022-12-06%20at%2009.51.09.JPG)

Ran both commands.

To add alternative names, we used the following command:

```
openssl req -newkey rsa:2048 -sha256 -keyout server.key -out server.csr -subj "/CN=www.afonso2022.com/O=afonso2022 Inc./C=PT" -passout pass:dees -addext "subjectAltName = DNS:www.afonso2022.com, DNS:www.fsi.com, DNS:www.feup.com"
```

# Task 3

![alt text](img/Screenshot%202022-12-06%20at%2010.03.04.JPG)

Signed the request.

![alt text](img/Screenshot%202022-12-06%20at%2010.09.04.JPG)
Uncommented.

![alt text](img/Screenshot%202022-12-10%20at%2023.21.12.JPG)

The alternative names are recognized (other domains because we redid the tasks before taking this screenshot).

# Task 4

![alt text](img/Screenshot%202022-12-09%20at%2023.49.37.JPG)
![alt text](img/Screenshot%202022-12-09%20at%2023.49.56.JPG)
![alt text](img/Screenshot%202022-12-09%20at%2023.50.07.JPG)
![alt text](img/Screenshot%202022-12-09%20at%2023.50.22.JPG)
The setup to run the Apache server. We also redirected the docker-compose.yml to ```build: ./task4```.

![alt text](img/Screenshot%202022-12-09%20at%2023.17.28.JPG)

We can't access the website because Firefox only allows certificates registered in their database; as such, our self-made one isn't suitable, thus getting its access blocked.

![alt text](img/Screenshot%202022-12-09%20at%2023.23.35.JPG)

We make it so the browser now recognizes our certificate as trustworthy.

![alt text](img/Screenshot%202022-12-10%20at%2023.54.36.JPG)

Able to access website.

# Task 5

![alt text](img/Screenshot%202022-12-10%20at%2023.00.35.JPG)

Edit the ```/etc/hosts``` file.

![alt text](img/Screenshot%202022-12-10%20at%2022.59.26.JPG)

Redirected user to our website.

# Task 6

![alt text](img/Screenshot%202022-12-11%20at%2000.06.33.JPG)

Added the domain ```www.google.com``` to ```/etc/hosts/```

![alt text](img/Screenshot%202022-12-11%20at%2000.14.56.JPG)

As we stole the CA credentials, we can create new certificates.

![alt text](img/Screenshot%202022-12-11%20at%2000.19.39.JPG)

After restarting the server, was able to issue a certificate to a website of the attacker's choosing, thus making a Man in the Middle Attack.

# CTF

# Challenge 1

This was our encoded message:

![alt text](img/Screenshot%202022-12-23%20at%2021.26.50.JPG)

To find ``p`` and ``q``, we used a python program that calculated the following prime from 2^512 and 2^513, respectively:

```python
import random
def isMillerRabinPassed(mrc):
    maxDivisionsByTwo = 0
    ec = mrc-1
    while ec % 2 == 0:
        ec >>= 1
        maxDivisionsByTwo += 1
    assert(2**maxDivisionsByTwo * ec == mrc-1)
    def trialComposite(round_tester):
        if pow(round_tester, ec, mrc) == 1:
            return False
        for i in range(maxDivisionsByTwo):
            if pow(round_tester, 2**i * ec, mrc) == mrc-1:
                return False
        return True
    numberOfRabinTrials = 20
    for i in range(numberOfRabinTrials):
        round_tester = random.randrange(2, mrc)
        if trialComposite(round_tester):
              return False
    return True
def nextPrime(N):
    if (N <= 1):
        return 2

    prime = N
    found = False
    while(not found):
        prime = prime + 1
        if(isMillerRabinPassed(prime) == True):
            found = True
    return prime
N = 2**513
print(nextPrime(N))
````

p:
![alt text](img/Screenshot%202022-12-23%20at%2021.27.07.JPG)

q:
![alt text](img/Screenshot%202022-12-23%20at%2021.33.12.JPG)

To find ``d``, we used the euclidean algorithm to calculate the inverse modulus of ``d * e`` and ``(p-1)*(q-1)``.

d:
![alt text](img/Screenshot%202022-12-23%20at%2021.27.20.JPG)

Putting thses values in their respective variables, and running the given script, we got our flag.

![alt text](img/Screenshot%202022-12-23%20at%2021.27.30.JPG)

# Challenge 2

We had the following values:

![alt text](img/Screenshot%202022-12-23%20at%2021.37.20.JPG)

We used this script, found online, to get  the flag:

```python
import gmpy2
class RSAModuli:
    def __init__(self):
       self.a = 0
       self.b = 0
       self.m = 0
       self.i = 0
    def gcd(self, num1, num2):
       if num1 < num2:
           num1, num2 = num2, num1
       while num2 != 0:
           num1, num2 = num2, num1 % num2
       return num1
    def extended_euclidean(self, e1, e2):
       self.a = gmpy2.invert(e1, e2)
       self.b = (float(self.gcd(e1, e2)-(self.a*e1)))/float(e2)
    def modular_inverse(self, c1, c2, N):
       i = gmpy2.invert(c2, N)
       mx = pow(c1, self.a, N)
       my = pow(i, int(-self.b), N)
       self.m= mx * my % N
    def print_value(self):
       print("Plain Text: ", self.m)
def main():
   c = RSAModuli()
   N = 29802384007335836114060790946940172263849688074203847205679161119246740969024691447256543750864846273960708438254311566283952628484424015493681621963467820718118574987867439608763479491101507201581057223558989005313208698460317488564288291082719699829753178633499407801126495589784600255076069467634364857018709745459288982060955372620312140134052685549203294828798700414465539743217609556452039466944664983781342587551185679334642222972770876019643835909446132146455764152958176465019970075319062952372134839912555603753959250424342115581031979523075376134933803222122260987279941806379954414425556495125737356327411

   c1 = 0x66b26715bc603fc77164342c395fa91a28951dfe90d9343cef9e9b56b28b6141c1e0acc695ce7e32a1d9f5de4760512a9bc665a63142d7b5a8e8533d75b814d16804228dadccffc0e465ca546df677ab29aa46ed5b9c52a962e0d1260852b637af436104ef4114e43ab3718463ac8b51c4b7deb309368f7a9f8b59947ca2e59bb84a8e92c3a5c50a9841073f7fc437d6e8f7c2c027b1ba80746ab42e4dce9aac31b79f481460f35b08c72cfc2ac8b09fd6e171e1478b5fd44fba50d7e1ef3c057b79d7cdd1c3c923265ea312917a529772e7f6e51c04398d18125c8e30ca7d5fe232ecbc9e3a2e66b8faf5237bf7be10dd28bb8ccc477df0b929934ee1d37b9c
   c2 = 0xc5d357e9f93efbb8d2cadcd97286ea625b5c4391e1be6e240f94936f92e3b448b1ec7b1799ec41c87ff885361178806f725bdd24e6c16af20c99fab24ce930c53e681cd5edfd0df2a733755ecaf3015e3a23f48150a1658170b4ad2f45e328a353280a58d3b4551959e6e47d3c433fe5bad4c38983551758cf16229a19cb2efc626022af42939cc5e1bbd01d5c4ee40ff6a5a62d65f96a238532750d2d98598995b658e36aeaf9f04e44095f766882706ce3b79a8ba7eb94416baae994bf4c28d362c5882dfedb748614f7a10f610e59c585bbc8ebbb06ab29b47c4b959d316bb1539923c76ecaa5ed3fb4201640da9ce5ce010b3c317970a47322b7d219b043
   e1 = 65537
   e2 = 65539
   c.extended_euclidean(e1, e2)
   c.modular_inverse(c1, c2, N)
   c.print_value()
if __name__ == '__main__':
   main()
````

Got the flag in plain text:

![alt text](img/Screenshot%202022-12-23%20at%2022.05.05.JPG)

Converted to text using the ``to_bytes`` function and got the flag.

![alt text](img/Screenshot%202022-12-23%20at%2022.18.14.JPG)