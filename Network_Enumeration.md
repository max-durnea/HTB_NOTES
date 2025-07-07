## NMAP
"TCP connect Scan is considered the most accurate scan, but not the stealthiest"
"UDP scans are slower as udp is a stateless protocol"
"xsltproc command is used to transform XML files into HTML files"
### Syntax:
```nmap <scan types> <options> <target>```

SCAN TECHNIQUES:
  -sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Maimon scans
  -sU: UDP Scan
  -sN/sF/sX: TCP Null, FIN, and Xmas scans
  --scanflags <flags>: Customize TCP scan flags
  -sI <zombie host[:probeport]>: Idle scan
  -sY/sZ: SCTP INIT/COOKIE-ECHO scans
  -sO: IP protocol scan
  -b <FTP relay host>: FTP bounce scan
  -sV: Service scan
  ### Other options
- -PE	Performs the ping scan by using 'ICMP Echo requests' against the target.
- --packet-trace	Shows all packets sent and received
- --reason	Displays the reason for specific result.
- --disable-arp-ping Disable ar ping
- -n	Disables DNS resolution.
- --max-retries How many times should it resend a packet
### Host Discovery
```sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5```
- 10.129.2.0/24: Network Range
- -sn: Disables port scanning
- -oA tnet: stores the results in all formats with the name tnet

**Note:** This scanning method works only if the __firewalls__ allow it, **OTHERWISE** other methods are used



[More strategies](https://nmap.org/book/host-discovery-strategies.html)

