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