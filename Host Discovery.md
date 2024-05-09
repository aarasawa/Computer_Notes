#HostDiscovery #NMAP #NetworkEnumeration 

### Contents
	[[#Scan Network Range]]
		[[#10.129.2.0/24]]
		[[#-sn]]
		[[#-oA tnet]]
		[[#grep for]]
		[[#cut -d" " -f5]]
	[[#Scan IP List]]
		[[#-iL]]
	[[#Scan Single IP]]
		[[#-PE]]
		[[#--packet-trace]]
		[[#--reason]]
		[[#--disable-arp-ping]]
### Questions
	[[#^1093d3]] Implications of -sn
	[[#Why are ICMP Echo requests still not being sent?]]

#### Scan Network Range 
^341fd7
``` bash
sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5
```
##### 10.129.2.0/24

^e74ef0

*Initial impressions*:
	The format of this made it appear as if the [[NMAP]] command was going to scan IPs from 10.129.2.[0-24]. 
*What it actually is*:
	It is a type of notation referred to as [[Classless Inter-Domain Routing (CIDR)]]. For the scan, it means that the *base IP* is 10.129.2.0. */24* is a [[Subnet Mask]] to indicate that the first 24 bits of the 32 bit address are fixed for devices in the network scan. Leaving the last *8* bits to indicate the range of host IPs we are going to scan. 
*What this means*:
	In terms of IP addresses, the range for *8 bits* is going to be *2^8 = 255 values*. Hence, IPs from 10.129.2.[0-255]. 10.129.2.0 is the *network address*. 10.129.2.1 to 10.129.2.254 are the *usable addresses* for devices on the network. 10.129.2.255 is the *broadcast address* for the network. 
##### -sn

^a7aad5

*What is it?*
	Indicates a scanning option for NMAP to *disable port scanning*. [[#^b86b5c]]
*Why would you use it?*
	Typically used for *host discovery* i.e. checking to see which hosts on the network are active without sinking resources into port scanning.
##### -oA tnet
*What is it?*
	Indicates a scanning option to *store results starting with the name 'tnet'*. This is for all major formats *nmap, gnmap, xml* with the base filename tnet, hence the files *tnet.nmap, tnet.gnmap, tnet.xml* will be created. 
##### | grep for 
*What the hell?*
	The *|* symbol is a pipe for *passing output* of the previous command as input to the next command. 
*What does this do?*
	*Grep* is a command for selecting parts of output. The second keyword is the *word we are filtering for*. In total, this segment of the command would *select lines containing the keyword 'for'*. 
##### | cut -d" " -f5
*What does this do?*
	It processes every line passed to it and delimits the line by the delimiter provided. In this case, it is space. Then extracting the 5th field. This segment of the command, *extracts the fifth word of the line fed to it*. 
#### Scan IP List
For an internal penetration test, it is not uncommon to be given a list of IPs for hosts that need testing. Given a list of IP addresses to test in *hosts.txt*:
``` bash
sudo nmap -sn -oA -iL hosts.txt | grep for | cut -d" " -f5
```
##### -iL
*What does this do?*
	Performs defined scans against targets in the list.
*First impression*:
	I am confused about the need for the latter half of the command, since the IPs are already provided. There should not be any strings to parse. However, after reanalyzing, I realized that each IP in the list is pinged and the report is saved, parsed, and reprinted to indicate which ones are active.
#### Scan Single IP
``` bash
sudo nmap 10.129.2.18 -sn -oA host
```
*Implications of disabled port scanning*: ^b86b5c
	If we disable port scans, MAP automatically ping scans with [[ICMP Echo Requests]] (-PE). Usually, if an ICMP request is sent, an ICMP reply is expected if the host is active. However, the example scan above sent [[ARP ping]] and we received ARP replies.  ^1093d3
``` bash
sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace
```
##### -PE
*What does this do?*
	In the previous sections, we show that with *port scan disabled*, NMAP usually sends ICMP echo requests. However, it is preempted by *ARP pings*. 
*Why do we use it?*
	To ensure that ICMP echo requests are sent.
##### --packet-trace
*What does this do?*
	Show all the packets sent and received. 
*Why do we use it?*
	In this example, we are using it to confirm the activity conducted when running nmap. 
##### Output
###### SENT (0.0074s) ARP who-has 10.129.2.18 tell 10.10.14.2
*What am I reading?*
	This is the output to the nmap request above. It shows that *nmap sent an ARP request* to determine the *MAC address associated with 10.129.2.18*. 
###### RCVD (0.0309s) ARP reply 10.129.2.18 is-at DE:AD:00:00:BE:EF
*What am I reading?*
	Indicates that we received an *ARP reply indicating the IP address 10.129.2.18* is associated with *DE:AD:00:00:BE:EF*.

##### Why are ICMP Echo requests still not being sent?
*Why??*
	It should happen, but it doesn't. The output shows it doesn't. *Because nmap tries the fastest and most direct method*. For local networks this is ARP. 
``` bash
sudo nmap 10.129.2.18 -sn -oA host -PE -reason
```
##### --reason
*What is this?*
	It is an option for *displaying the reason for specific results*.
##### Output
###### Host is up, received arp-response (0.028s latency)
*What is this?*
	This is the additional line that is output when --reason is appended to the command.
``` bash
sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace --disable-arp-ping
```
##### --disable-arp-ping
*What does it do?*
	As the name suggests, it is an option for *disabling arp requests*, so we can finally scan the target with *ICMP echo requests*.