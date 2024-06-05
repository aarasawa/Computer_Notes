#IDS #IPS #NetworkEnumeration #Firewall #NetworkEnumeration 

### Content
	[[#Firewalls]]
	[[#IDS/IPS]]
	[[#Determine Firewalls and Rules]]

### Firewalls
To prevent unwanted connections and traffic. Monitors network traffic between the firewall and incoming data connections and decides how to handle them.
### IDS/IPS
**Intrusion Detection System** (IDS) and **Intrusion Prevention System** (IPS)  are software-based components. *IDS* scans for potential attacks, analyzes them, and reports detected attacks. *IPS* complements IDS by executing defensive measures if an attack is detected. 
### Determine Firewalls and Rules
Packets can either be *dropped* or *rejected* by a firewall. 

*Dropped* packets are ignored and no response is returned from a host. 
*Rejected* packets return with an RST flag, containing different types of ICMP error codes or nothing at all.

Nmap's TCP ACK (-sA) is *harder* for firewall and IDS/IPS systems to filter for than regular SYN (-sS) or Connect scans (-sT). Since -sS and -sT only send TCP packet with only ACK flag. If a port is closed or open, host must respond with RST flag. Connection attempts with SYN flag from external networks are usually blocked by firewalls. *ACK flag are often passed by firewall because the firewall can't determine whether connection was established externally or internally.*
### Decoys
Cases where specific subnets from different regions prevents any access to the target network. The **Decoy scanning method** (-D) generates various random IP addresses inserted into the IP header to disguise the origin of the packet sent. Generate random (RND) specific number of IP addresses separated by a colon.
``` bash
sudo nmap 10.129.2.28 -p 80 -sS -Pn -n --disable-arp-ping --packet-trace -D RND:5
```

Spoofed packets are often filtered even when they come from the same network range. To specify BPS servers' IP addresses and use them with "IP ID". To manually specify source IP address (-S), like if *individual subnets would not have access to the server's specific services*. Decoys can be used for SYN, ACK, ICMP scans, and OS detection scans. 
``` bash
# Testing Firewall rule
sudo nmap 10.129.2.28 -n -Pn -p 445 -0
```
``` bash
# Scan Using Different Source IP
sudo nmap 10.129.2.28 -n -Pn -p 445 -0 -S 10.129.2.200 -e tun0

PORT    STATE SERVICE
445/tcp open  microsoft-ds
MAC Address: DE:AD:00:00:BE:EF (Intel Corporate)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 2.6.32 (96%), Linux 3.2 - 4.9 (96%), Linux 2.6.32 - 3.10 (96%), Linux 3.4 - 3.10 (95%), Linux 3.1 (95%), Linux 3.2 (95%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (94%), Synology DiskStation Manager 5.2-5644 (94%), Linux 2.6.32 - 2.6.35 (94%), Linux 2.6.32 - 3.5 (94%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop
```
### DNS Proxying
Nmap performs a reverse DNS resolution unless otherwise specified. DNS queries queries are made over UDP port 53. **--dns-server <.ns>, <.ns>** is how we can specify DNS servers ourselves. 
``` bash
# SYN-Scan of a Filtered Port
sudo nmap 10.129.2.28 -p 50000 -sS -Pn -n --disable-arp-ping --packet-trace

SENT (0.0417s) TCP 10.10.14.2:33436 > 10.129.2.28:50000 S ttl=41 id=21939 iplen=44  seq=736533153 win=1024 <mss 1460>
SENT (1.0481s) TCP 10.10.14.2:33437 > 10.129.2.28:50000 S ttl=46 id=6446 iplen=44  seq=736598688 win=1024 <mss 1460>
Nmap scan report for 10.129.2.28
Host is up.

PORT      STATE    SERVICE
50000/tcp filtered ibm-db2
```

``` bash
# SYN-Scan from DNS Port
sudo nmap 10.129.2.28 -p 50000 -sS -Pn -n --disable-arp-ping --packet-trace --source-port 53

SENT (0.0482s) TCP 10.10.14.2:53 > 10.129.2.28:50000 S ttl=58 id=27470 iplen=44  seq=4003923435 win=1024 <mss 1460>
RCVD (0.0608s) TCP 10.129.2.28:50000 > 10.10.14.2:53 SA ttl=64 id=0 iplen=44  seq=540635485 win=64240 <mss 1460>
Nmap scan report for 10.129.2.28
Host is up (0.013s latency).

PORT      STATE SERVICE
50000/tcp open  ibm-db2
MAC Address: DE:AD:00:00:BE:EF (Intel Corporate)
```
Indicates that the firewall accepts TCP port 53, we can try to connect using netcat.

``` bash
ncat -nv --source-port 53 10.129.2.28 50000
```