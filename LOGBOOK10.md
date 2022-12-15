# Task 1

Logged in as Charlie with the credentials given, went to his profile and wrote the script to his description.

![alt text](img/Screenshot%202022-11-22%20at%2009.34.01.JPG)

When going to his profile, the following popup appears:

![alt text](img/Screenshot%202022-11-22%20at%2009.35.23.JPG)

# Task 2

In the same profile, put the following script:

![alt text](img/Screenshot%202022-11-22%20at%2009.40.58.JPG)

Popup with cookies:

![alt text](img/Screenshot%202022-11-22%20at%2009.40.32.JPG)

# Task 3

In the same profile, write the following script:

![alt text](img/Screenshot%202022-11-22%20at%2010.11.39.JPG)

After this, logged out of Charlie and logged in on Alice's profile. Then visit her friend Charlie profile, and receive her cookies:
![alt text](img/Screenshot%202022-11-22%20at%2012.13.52.JPG)

# Task 4

![alt text](img/Screenshot%202022-11-22%20at%2012.25.55.JPG)
How a friend request is encoded.

The script used:
![alt text](img/Screenshot%202022-11-22%20at%2011.37.39.JPG)

![alt text](img/Screenshot%202022-11-22%20at%2011.56.53.JPG)
Alice has no friends.

![alt text](img/Screenshot%202022-11-22%20at%2012.23.30.JPG)
After visiting Samy's profile, she now has one :).

``` Question 1 ```

Lines 1 and 2 send the token needed to authenticate the user when the request is made.

```Question 2```

No, because can only be successful because the Editor mode adds extra HTML and changes symbols.

# CTF

## Challenge 1

We have the id for the Give the flag button, we just need to access it. These buttons are only enbaled to the admin so our purpose is to make the admin click the button Give the flag for us. 

![alt text](img/1st_part_ctf10.png)

We use the following JavaScript to click the button with that id: `<script>document.getElementById('giveflag').click(); </script>`

![alt text](img/2nd_part_ctf10.png)

We got the flag!

![alt text](img/3rd_part_ctf10.png)

## Challenge 2

Since we don't have credentials, we have to find a way to retrieve the flag.

![alt text](img/logbook10_ctf2_1.png)

When a user submits a user request, the system uses the ping command to send packets to the host. Which gives us access to various commands and allows us to exploit them. Using the `;` allows to inject different commands and access information which we wouldn't be able to access.

![alt text](img/logbook10_ctf2_2.png)

We got the flag!

![alt text](img/logbook10_ctf2_3.png)
