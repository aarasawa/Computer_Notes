#NMAP #NetworkEnumeration #PortScanning 

### Content
	[[#Different Formats]]
	[[#Style Sheets]]

#### Different Formats
Nmap can save results of a scan in three different formats: 
	*normal output (-oN)* with extension *.nmap*
	*grepable output (-oG)* with extension *.gnmap*
	*xml output (-oX)* with extension *.xml*
To specify that we want to save the results in *all formats* we can use *-oA*.
#### Style Sheets
For the *xml output* we can create readable HTML reports. To convert from xml to HTML we can use *xsltproc*. 
``` bash
xsltproc target.xml -o target.html
```