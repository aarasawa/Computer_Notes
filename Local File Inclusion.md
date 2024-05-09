#Vulnerability #WebExploit

**Local File Inclusion** (LFI) is the process of including files present locally on the server.

For example say we have a link like this:
``` bash
http://10.10.10.10/?file=home.php
```

To test, we can curl a file from the system:
```
curl 'http://10.10.10.10/?file=/etc/passwd'
```

In the case that a directory was specified as a parameter in the program, for example, */var/www/html*, then the full path for a file we want like */etc/passwd* would be */var/www/html/etc/passwd*. To get past this we can pass something like this:
``` bash
../../../etc/passwd
```