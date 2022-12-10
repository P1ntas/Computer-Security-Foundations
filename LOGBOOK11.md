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

```
[12/06/22]seed@VM:~/.../Labsetup$ openssl x509 -in server.crt -text -noout
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number: 4096 (0x1000)
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = PT, ST = PO, L = PO, O = FEUP, OU = LEIC, CN = Afonso, emailAddress = seed@labs.com
        Validity
            Not Before: Dec  6 10:02:00 2022 GMT
            Not After : Dec  3 10:02:00 2032 GMT
        Subject: C = PT, O = afonso2022 Inc., CN = www.afonso2022.com
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                RSA Public-Key: (2048 bit)
                Modulus:
                    00:d5:fe:07:81:0a:c9:1a:71:54:55:a7:60:4c:27:
                    6d:84:e2:e7:26:a2:f2:fd:a9:af:41:3d:76:05:0c:
                    74:72:93:5b:c0:a5:4c:ae:7e:d4:cc:14:61:58:c2:
                    bd:a3:4e:f8:a1:e1:4e:e8:40:05:99:81:e2:23:bc:
                    18:52:05:e7:0c:ed:b4:25:41:e0:09:35:42:6b:ad:
                    00:a7:f3:e5:12:1a:cd:20:f4:9e:33:1c:2f:f3:d5:
                    a1:96:ac:e4:73:57:b3:7d:67:0c:93:90:c1:19:0b:
                    a9:e2:e1:44:64:18:fc:90:ef:f1:5a:19:ed:b2:41:
                    ea:0d:28:bb:e2:7f:75:0f:4e:49:9b:66:d1:74:ea:
                    6b:67:eb:4b:c3:e8:59:ca:37:e0:5f:08:8e:9b:6e:
                    5c:4c:d0:45:6f:f2:c7:1b:44:5b:6a:af:6b:69:5f:
                    ba:52:48:17:f1:1e:fd:2e:05:83:c5:36:c5:40:aa:
                    9f:b2:cd:c9:cd:9c:7a:47:49:e8:12:95:21:83:44:
                    6d:d4:c4:4f:1f:99:e9:7e:d9:d6:c1:9d:70:5b:86:
                    3e:21:dc:44:49:82:95:50:62:72:88:80:52:8d:84:
                    54:a0:ed:b7:cb:d5:c9:28:2c:e0:14:a8:6e:87:33:
                    5a:cb:7d:05:9b:45:c0:14:d1:80:3a:97:b6:a0:f1:
                    02:37
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Basic Constraints: 
                CA:FALSE
            Netscape Comment: 
                OpenSSL Generated Certificate
            X509v3 Subject Key Identifier: 
                30:CD:CD:7C:83:4E:41:E1:B5:DF:4D:65:55:6E:74:52:C0:CD:70:0F
            X509v3 Authority Key Identifier: 
                keyid:4F:F0:8C:9F:6C:C5:D7:CA:82:A8:18:1A:87:93:A6:81:B1:7E:DF:02

                X509v3 Subject Alternative Name: 
                DNS:www.afonso2022.com, DNS:www.afonso2022A.com, DNS:www.afonso2022B.com
    Signature Algorithm: sha256WithRSAEncryption
         8b:fd:42:50:37:3f:d7:2d:e5:93:2a:d3:37:95:e9:ba:68:79:
         5b:70:55:6a:64:3e:26:34:aa:68:6a:6b:0a:34:25:fb:a9:fb:
         84:b6:d7:b4:45:6f:0c:98:dc:ab:98:0f:74:1c:0a:1c:bd:cf:
         15:08:67:bd:93:7e:7d:7e:10:65:69:3a:f1:70:8c:a1:4e:33:
         5e:02:c9:e8:23:40:7a:06:7f:70:9c:ee:45:1a:ee:b5:56:c9:
         40:16:cf:db:ba:aa:58:5d:35:ba:93:49:9b:15:6a:ba:64:58:
         3f:8a:8c:7e:3f:7f:8e:46:fd:4a:d5:47:5f:9f:b5:88:4a:a4:
         44:3e:e2:c0:ae:19:29:44:fd:00:f7:59:eb:8f:41:7c:de:70:
         00:b4:52:ec:36:bc:f7:48:54:68:a7:93:e6:35:54:b7:66:06:
         c2:0c:07:06:86:0e:f0:83:01:5f:e5:e2:f8:59:b8:11:9c:eb:
         45:b4:08:d9:72:2a:f1:34:1c:42:3a:d7:6d:4e:67:f0:0b:e8:
         71:c7:23:49:99:09:13:f6:e0:18:2c:70:12:6b:bb:f9:e6:66:
         23:d3:73:76:43:f9:ce:f8:c8:b5:b6:7e:b6:02:62:3d:dd:2a:
         0b:95:e3:80:f5:e1:f8:ca:d8:ba:7f:a3:5c:44:3b:73:b1:aa:
         62:66:76:7f

```

The alternative names are recognized.

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

![alt text](img/Screenshot%202022-12-09%20at%2023.45.56.JPG)

Able to access website.

# Task 5
