#PortScanning #NMAP #NetworkEnumeration #HostScanning

### Content
	[[#States of Ports]]
	[[#Discovering Open TCP Ports]]
	[[#Filtered Ports]]
	[[#Discovering Open UDP Ports]]
#### States of Ports
##### Open
*Connection to scanned port has been established*. Connections can be either TCP, UDP, or SCTP.
##### Closed
*TCP indicates packet received contains RST flag*. Can be used to determine if a target is alive or not.
##### Filtered
*No response or error code returned from target*. NMAP cannot identify if scanned port is open or closed.
##### Unfiltered
*Port accessible but can't determine open or closed*. TCP-ACK scan conducted but results are inconclusive.
##### Open | Filtered
*No response for specific port*. NMAP sets to state, usually indicates firewall or packet filter may be protecting the port. 
##### Closed | Filtered
*Impossible to determine if scanned port is closed or filtered by firewall*. Only occurs in IP ID idle scans. 
#### Discovering Open TCP Ports
*NMAP scans top 1000 ports with [[SYN]] (-sS) by default*. This is only with *sudo* because it requires socket permissions to create TCP packets. If no sudo permissions are provided, then *TCP (-sT)* scan is performed. 

Those are the ports and scanning methods set if not action is taken to set them manually. It is possible to define them:
``` bash
Individually
 -p 22, 25, 80, 139, 445

In a range
-p 22-445

Top ports, defined by most frequent
--top-ports=10

All ports
-p-

Fast port scan, with top 100 ports
-F
```
##### Scanning Top 10 TCP Ports
``` bash
sudo nmap 10.129.2.28 --top-ports=10
```
##### Nmap -Trace the Packets
``` bash
sudo nmap 10.129.2.28 -p 21 --packet-trace -Pn -n --disable-arp-ping
```
###### -Pn
*Disable ICMP echo requests*.
###### -n
*What is this?*
	A flag for *disabling DNS resolution*.
*Why would we use this?*
	It can improve the scanning speed if the hostname is not important. Additionally, it can help in networks where DNS lookups are expensive or unreliable. 
###### SENT (0.0429s) TCP 10.10.14.2:63090 > 10.129.2.28:21 S ...
The flag is apparent at the end of this snippet. *S indicated the packet is trying to establish a connection*. 
###### RCVD (0.0573s) TCP 10.129.2.28:21 > 10.10.14.2:63090 RA ...
The response we can see the flag says *RA, indicating the connection request was refused and the connection reset is being acknowledged*. 
*Why is it RA and not RST?*
	The way the packet is structured, if it were only RST, then the flag would be present as only an *R.* The flag we do see is a combination of RST via R and ACK via A. 
##### Connect Scan
The *TCP Connect Scan (-sT)* uses 3-way handshake to determine if a port is open or closed. 
*Why do we use it?*
	It is a better way of scanning since it does not leave unfinished connections or unsent packets on the host. *Less impactful on the network.* 
	For cases where a firewall drops incoming packets but allows outgoing packets, *it passes.*
*Cons?*
	It is slower since you *have to wait for a response from the target after each packet.*
#### Filtered Ports
When a port is filtered, it can either be *dropped* or *rejected*. 

``` bash
sudo nmap 10.129.2.28 -p 139 --packet-trace -n --disable-arp-ping -Pn
```
To examine how packets are being handled, we disable ICMP, DNS resolution, and ARP. 
##### Comparing outputs
The last scan above, showed a duration of 2.06 seconds to complete the scan, indicating that the packets are being *dropped.* 

*Other scans usually take ~0.05s*. In the case that packets are *rejected* the scan time is still around *0.05s*. 
#### Discovering Open UDP Ports
*UDP does not required 3-way handshake* and *does not receive any acknowledgement*.
*What does this mean for scanning?*
	The timeout is longer. Making *-sU* much slower than TCP scan *-sS*.
##### UDP Port Scan
This is a typical UDP scan on the top 100 ports. 
``` bash
sudo nmap 10.129.2.28 -F -sU
```

NMAP sends *empty* datagrams to UDP ports and we do not receive any response unless it is configured to do so. 
``` bash
sudo nmap 10.129.2.28 -sU -Pn -n --disable-arp-ping --packet-trace -p 137 --reason
```

If we get an ICMP response with *error code 3* (port unreachable), we know the port is *closed*. All other ICMP responses are marked as *open | filtered*.
##### -sV
*What is it?*
	An option for getting additional available information from open ports. To identify *versions, service names, and details*. 
