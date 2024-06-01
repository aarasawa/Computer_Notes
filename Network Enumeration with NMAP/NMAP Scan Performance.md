#NMAP #NetworkEnumeration #ScanPerformance

Speed, frequency, timeouts of test packets, number of simultaneous packets, and number of retries for scanned ports of the targets. 

### Timeouts
When a packet is sent, **Round-Trip-Time - RTT** is the time to receive a response from the scanned port. NMAP usually starts with high timeout **--min-RTT-timeout** of 100ms. However, sometimes optimized settings can trade scan time and overlook hosts. 
``` bash
# Default Scan
sudo nmap 10.129.2.0/24 -F

# Optimized RTT
sudo nmap 10.129.2.0/24 -F --initial-rtt-timeout 50 ms --max-rtt-timeout 100ms
```

### Max Retries
Default retry rate is 10. If no response is received from a port, it will not send any more packets to it.
``` bash
# Default scan
sudo nmap 10.129.2.0/24 -F | grep "/tcp" | wc -l

# Reduced Retries
sudo nmap 10.129.2.0/24 -F --max-retries 0 | grep "/tcp" | wc -l
```

### Rates
If we know network bandwidth, we can work with *rate of packets sent* to speed up scans. The minimum rate **--min-rate .<number.>** tells NMAP to simultaneously send the specified number of packets.
``` bash
# Default Scan
sudo nmap 10.129.2.0/24 -F -oN tnet.default
<SNIP>
Nmap done: 256 IP addresses (10 hosts up) scanned in 29.83 seconds

# Optimized Scan
sudo nmap 10.129.2.0/24 -F -oN tnet.minrate300 --min-rate 300
<SNIP>
Nmap done: 256 IP addresses (10 hosts up) scanned in 8.67 seconds
```

### Timing
NMAP offers 6 different timing templates on a range of **0-5** in terms of aggressiveness. The default timing is **-T 3**. 

| -T 0 | -T paranoid   |
| ---- | ------------- |
| -T 1 | -T sneaky     |
| -T 2 | -T polite     |
| -T 3 | -T normal     |
| -T 4 | -T aggressive |
| -T 5 | -T insane     |
``` bash
# Default Scan
sudo nmap 10.129.2.0/24 -F -oN tnet.default

# Insane Scan
sudo namp 10.129.2.0/24 -F -oN tnet.T5 -T 5
```