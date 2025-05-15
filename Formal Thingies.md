The penetration tester job role goes from signing documents to 
showing the results of our penetration tests.

#Information Gathering

OSINT-Open Source Intelligence: This is a Way to find information about our
target, such as using Github to find ssh keys,tokens,passwords. Looking at
Job roles, social media etc

Service Enumeration: We find the services and their versions and relevant information
about it, plus the reason it can be used to identify potential vulnerabilities.

Host Enumeration: Look through all the available hosts of our target and try to find
any vulnerabilities and services, such as and FTP server that the company uses to
Exchange data between employees, FTP many times allows for anonymous access.

Pillaging: Collecting any relevant and sensitive data from the target. That will
either help us uncover a vulenrability and also used for further steps on escalation
or lateral movement over the network

#Exploitation

Assess the probability of successfully executing a particular attack against the target
You can use <CVSS Scoring> to calculate

You should take into account the Complexity that depends on your experience

Estimate the probability of damage, we generally don't perform DoS attacks, unless The
client requires them. Generally we avoid at all times attacks that can damage the software
or the operating system.

#Preparation for attack

To see the PoC (Proof of Concept) working, we sometimes won't be able to find the necessary Exploitation
code. So we will need to simulate the target machine as similar as possible on a VM and follow the steps 
described in the exploit 

#Post-Exploitation
Evasive Testing: we should go as undetected as possible to identify blind spots in the network environment that
the System Administator might not notice. However it's still a good idea to run commands and tools that their
defenses stop and detect, to show the client that their defenses working

Non-Evasive Testing: It's the reverse of Evasive Testing wehn the client wants us to use any tool to identify the flaws
in their defences.

We go through the Information Gathering and Vulnerability Assessment again to understand what we are working with on
the System.

Pillaging: We examine the role of the host in the corporate network, and analyze the network configurations such as:
Interfaces, ARP, Routing, DNS, VPN, Network Traffic. Also hunt for sensitive data

Persistance: Once we have an overview of the system, our immediate next step is maintaining access to the exploited host.

Privilege Escalation: You know it

Data Exfiltration: Extract sensitive data, better to create your own and exfiltrate to your system

#Lateral movement
We test here what an attacker could do within the entire network. One of the most common examples 
that show us why we should check this is ransomware that can be spread accross the network.

Pivoting or Tunneling: We use a certain host as a proxy to perform all the scans from our attack machine or VM
This way the exploited system represents and routes all our netwrok requests.

Example is a printer at home that is not accessible from the internet but we can send print jobs from our home
network. If one host from the network has been compromised, we can leverage this to send jobs to the printer.

#Privilege Exploitation
We can find ways to crack passwords and hashes to gain higher privileges, then we can try using these on different
systems. Sometimes there can be situations when we do not need to crack a hash and just use them directly. For example 
we can use <Responder> to intercept NTLMv2 hashes. After intercepting we can use <pass-the-hash> technique
to log in as that administrator on multiple hosts and servers

#Proof of Conecpt
We use the proof of concept to prove that a vulnerability exists in a way that the developers or administrators can replicate it
and test their remediation efforts. One of the most common examples used to prove software vulnerabilities is to execute 
<calc.exe> on Windows.