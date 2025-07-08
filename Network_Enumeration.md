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
  -D: Decoy, random addresses are inserted into the header, and our address too
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
### Decoy:
```sudo nmap 10.129.2.28 -p 80 -sS -Pn -n --disable-arp-ping --packet-trace -D RND:5```
 - -D RND:5 send 5 packets and insert a packet with our address between them


[More strategies](https://nmap.org/book/host-discovery-strategies.html)

### Evading firewalls:
TCP ACK scan (**-sA**) is much harder to filter for firewalls and IDS/IPS systems then regular SYN (**-sS**) of Connect (**-sT**) scans as they only send a TCP packet with only the **ACK** flag. This way if a port is closed or open, the host must respond with an **RST** flag. It's because the firewall doesn't know if the connection was first established by the internal or the external network.

### Detect IDS/IPS:
- To detect if **IPS**(Intrusion Prevention System)
is present we can try to scan from a single host. If the host gets blocked and has no access to the target

- If the administrators block specific subnets from different regions we can use the **-D** scanning method. Nmap generates various random IP addresses insered into the IP header to disguise the origin of the packet sent

### DNS Proxying
We can use port **53** (DNS) port as a source port, if the administrators set up a trusted DNS. We can also use them by specifying --dns-server
```dig @target_ip version.bind CH TXT +short``` - Determine DNS version
--source-port 53 really helps against some firewalls as they trust port 53 more it being a dns server port!
