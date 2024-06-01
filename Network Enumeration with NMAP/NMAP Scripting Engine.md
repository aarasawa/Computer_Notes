#NMAP #NetworkEnumeration #ScriptingEngine

**NMAP Scripting Engine** (NSE) allows us to create scripts in Lua to interact with certain services. 

| Category  | Description                                                                                                      |
| --------- | ---------------------------------------------------------------------------------------------------------------- |
| auth      | Determination of authentication credentials                                                                      |
| broadcast | Scripts, for host discovery by broadcasting and discovered hosts can be automatically added to remaining scans   |
| brute     | Scripts to login to respective service by brute-forcing with credentials                                         |
| default   | same as -sC option                                                                                               |
| discovery | evaluation of accessible services                                                                                |
| dos       | Scripts to check services for DoS vulnerabilities, used less as it harms the services                            |
| exploit   | Scripts to exploit known vulnerabilities for the scanned port                                                    |
| external  | Scripts that use external services for further processing                                                        |
| fuzzer    | Scripts to identify vulnerabilities and unexpected packet handling by sending different fields (takes long time) |
| intrusive | Could negatively affect target system                                                                            |
| malware   | Checks if malware infects the target system                                                                      |
| safe      | Defensive scripts that are not intrusive and destructive                                                         |
| version   | Extension for service detection                                                                                  |
| vuln      | Identification of specific vulnerabilities                                                                       |

``` bash 
# Default Scripts
sudo nmap <target> -sC

# Specific Scripts
sudo nmap <target> --script <category>

# Defined Scripts
sudo nmap <target> --script <script-name>, <script-name>, ....

# Defined Scripts with Ports
sudo nmap 10.129.2.28 -p 25 --script banner, smtp-commands

# Aggressive scan includes -sV, -O, --traceroute, -sC
# Service detection, OS detection, traceroute, and default scripts
sudo nmap 10.129.2.28 -p 80 -A

# Vulnerability Assessment
# Service version detection, check databases for known vulnerabilities
sudo nmap 10.129.2.28 -p 80 -sV --script vuln
```