# Task 1

![alt text](img/Screenshot%202022-11-12%20at%2018.48.46.JPG)

After setting up server, used this query to get Alice data.

# Task 2.1

![alt text](img/Screenshot%202022-11-12%20at%2019.11.46.JPG)

With this input we were able to gain access to the admin profile. This works because we're closing the login string and commentig the rest of the code.

# Task 2.2

Using ```curl 'www.seed-server.com/unsafe_home.php?username=admin%27%23&Password=' ``` we were able to get the HTML page of the admin profile.

![alt text](img/Screenshot%202022-11-12%20at%2019.24.15.JPG)

# Task 2.3

Although we could in theory put any SQL command between ```' ``` and ``` # ```, that's not possible.

![alt text](img/Screenshot%202022-11-12%20at%2019.29.07.JPG)

This happens because the ```query```function in PHP allows only one query at a time.

# Task 3.1

![alt text](img/Screenshot%202022-11-12%20at%2020.12.09.JPG)

We can go to the NickName field in the Edit Profile page and input the query above, which will increase Alice's salary.

![alt text](img/Screenshot%202022-11-12%20at%2020.15.30.JPG)

# Task 3.2

![alt text](img/Screenshot%202022-11-12%20at%2020.20.25.JPG)

To decrease Boby's salary, we just need to input the query above in any field.

![alt text](img/Screenshot%202022-11-12%20at%2020.21.08.JPG)

# Task 3.3

![alt text](img/Screenshot%202022-11-12%20at%2022.47.48.JPG)

password hash

using the query ``` ', Password = "5baa61e4c9b93f3f0682250b6cf8331b7ee68fd8" where Name= "Boby" # ```, we were able to change Boby's password

![alt text](img/Screenshot%202022-11-12%20at%2022.58.49.JPG)

Changed password

![alt text](img/Screenshot%202022-11-12%20at%2023.01.51.JPG)

Gained access

# CTF

## Desafio 1

With the following input, we could login as admin.

![alt text](img/logbook7_ctf1.png)

## Desafio 2

