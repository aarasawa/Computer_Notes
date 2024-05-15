#NMAP #NetworkEnumeration #ServiceEnumeration #PortScanning 

### Content
	[[#Service Version Detection]]

#### Service Version Detection
Performing a *quick* scan is advantageous because it causes less traffic and helps to avoid detection and or being blocked by security measures. There is another option *--stats-every=5s* to define periods of time statuses can be shown on how much longer a scan is going to take. You can specify in units of seconds (s) or minutes (m). 

*Verbosity* can be changed too using *-v* or *-vv* and can be used to write to console when nmap detects open ports without having to wait until the scan is over. 

#### Banner Grabbing
After a scan completes, open ports are printed, when the *-sV* option is used, it writes the corresponding service and versions. To find the version/service of a port, it looks for things called *banners*. Usually it directly prints them, but if i can't find the information, nmap searches through a *signature-based matching system* (but this increases the scan duration). 
``` bash
sudo nmap 10.129.2.28 -p- -sV -Pn -n --disable-arp-ping --packet-trace
```
##### Output
The output for this command in the example prints an error that occurs during the banner grabbing process. This occurs if nmap doesn't know how to handle information it gets from banner grabbing.
``` shell-session
NSOCK INFO [0.4200s] nsock_trace_handler_callback(): Callback: READ SUCCESS for EID 18 [10.129.2.28:25] (35 bytes): 220 inlane ESMTP Postfix (Ubuntu)..
Service scan match (Probe NULL matched with NULL line 3104): 10.129.2.28:25 is smtp.  Version: |Postfix smtpd|||
NSOCK INFO [0.4200s] nsock_iod_delete(): nsock_iod_delete (IOD #1)
Nmap scan report for 10.129.2.28
Host is up (0.076s latency).

PORT   STATE SERVICE VERSION
25/tcp open  smtp    Postfix smtpd
MAC Address: DE:AD:00:00:BE:EF (Intel Corporate)
Service Info: Host:  inlane

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.47 seconds
```
Reading the nsock_trace_handler_callback() we can see there is additional information not provided under the version for port 25. It indicates that *220 inlane ESMTP Postfix (Ubuntu)* was not included. After a 3-way handshake, the server sends a banner for ID'ing, but some services do not provide much info OR banners can be manipulated or removed. 
##### Manually collecting SMTP message
``` shell session
# tcpdump
sudo tcpdump -i eth0 host 10.10.14.2 and 10.129.2.28

tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 262144 bytes

# netcat
nc -nv 10.129.2.28 25

Connection to 10.129.2.28 port 25 [tcp/*] succeeded!
220 inlane ESMTP Postfix (Ubuntu)

# Tcpdump - Intercepted Traffic
18:28:07.128564 IP 10.10.14.2.59618 > 10.129.2.28.smtp: Flags [S], seq 1798872233, win 65535, options [mss 1460,nop,wscale 6,nop,nop,TS val 331260178 ecr 0,sackOK,eol], length 0
18:28:07.255151 IP 10.129.2.28.smtp > 10.10.14.2.59618: Flags [S.], seq 1130574379, ack 1798872234, win 65160, options [mss 1460,sackOK,TS val 1800383922 ecr 331260178,nop,wscale 7], length 0
18:28:07.255281 IP 10.10.14.2.59618 > 10.129.2.28.smtp: Flags [.], ack 1, win 2058, options [nop,nop,TS val 331260304 ecr 1800383922], length 0
18:28:07.319306 IP 10.129.2.28.smtp > 10.10.14.2.59618: Flags [P.], seq 1:36, ack 1, win 510, options [nop,nop,TS val 1800383985 ecr 331260304], length 35: SMTP: 220 inlane ESMTP Postfix (Ubuntu)
18:28:07.319426 IP 10.10.14.2.59618 > 10.129.2.28.smtp: Flags [.], ack 36, win 2058, options [nop,nop,TS val 331260368 ecr 1800383985], length 0
```

| 1.  | [SYN]     | 18:28:07.128564 IP 10.10.14.2.59618 > 10.129.2.28.smtp: Flags [S], <SNIP>  |
| --- | --------- | -------------------------------------------------------------------------- |
| 2   | [SYN-ACK] | 18:28:07.255151 IP 10.129.2.28.smtp > 10.10.14.2.59618: Flags [S.], <SNIP> |
| 3.  | [ACK]     | 18:28:07.255281 IP 10.10.14.2.59618 > 10.129.2.28.smtp: Flags [.], <SNIP>  |
| 4   | [PSH-ACK] | 18:28:07.319306 IP 10.129.2.28.smtp > 10.10.14.2.59618: Flags [P.], <SNIP> |
| 5   | [ACK]     | 18:28:07.319426 IP 10.10.14.2.59618 > 10.129.2.28.smtp: Flags [.], <SNIP>  |
1 through 3 shows us the 3-way handshake. From there, the SMTP server sends us a TCP packet with *PSH* and *ACK* flags. In 4, *PSH* states the server is sending data and *ACK* simultaneously tells us that all required data is sent. 5 is the last TCP packet to confirm the receipt of data with an *ACK*. 