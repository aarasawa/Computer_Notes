#PasswordCracking #BruteForcing #Cybersecurity 

HTTP specification provides two parallel authentication mechanisms:
	- **Basic HTTP AUTH** to authenticate user to HTTP server
	- **Proxy Server Authentication** to authenticate the user to an intermediate proxy server
Both use requests, response status codes, and response headers. 

A *Basic HTTP Authentication scheme* uses userID and password for authentication.
	- client sends request w/o authentication info
	- server sends response with *WWW-Authenticate* header to request client to provide credentials
	- client asked to submit authentication info
	- server transmits character string that tells client who is requesting the data
	- client uses Base64 for encoding identifier and password

Types of password attacks: *dictionary attack, brute force, traffic interception, man in the middle, key logging, social engineering*. 

### Brute Force Attack
**Brute Force Attack** does not depend on a wordlist of common passwords, *tries all possible character combos for a specified length*. 
Not ideal for attacks, especially over a network, like *hydra* does. 
### Dictionary Attack
**Dictionary Attack** tries to guess passwords with lists. 
### Methods of Brute Force Attacks

| Attack                     | Description                                                                                                       |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| Online Brute Force Attack  | Attacking a live application over the network (HTTP, HTTPs, SSH, FTP)                                             |
| Offline Brute Force Attack | aka Offline Password Cracking, where you attempt to crack a hash of an encrypted password                         |
| Reverse Brute Force Attack | aka brute-forcing, try a single common password with a list of usernames on a certain service                     |
| Hybrid Brute Force Attack  | Attacking a user by creating a customize password wordlist, built using known intel about the user or the service |
|                            |                                                                                                                   |
