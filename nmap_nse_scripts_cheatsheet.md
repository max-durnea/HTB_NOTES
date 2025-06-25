# 📜 Useful Nmap NSE Scripts

Nmap's scripting engine (NSE) allows you to automate and extend Nmap for advanced scanning. Use with:

```bash
nmap --script=<script_name> <target>
```

You can combine with `-sV`, `-sC`, `-p <port>`, etc.

---

## 🔍 General Discovery

| Script            | Description                                     |
|------------------|-------------------------------------------------|
| `default`         | Runs a default set of common scripts (`-sC`)   |
| `banner`          | Grabs service banners                          |
| `http-title`      | Gets the title of web pages                    |
| `http-headers`    | Grabs HTTP headers                             |
| `http-methods`    | Lists allowed HTTP methods (e.g., PUT, DELETE) |
| `http-enum`       | Enumerates web paths like gobuster             |
| `http-server-header` | Gets web server type/version                 |
| `http-robots.txt` | Checks for disallowed paths                    |
| `http-generator`  | Identifies CMS or site generator               |

---

## 🧪 Vulnerability Scanning

| Script                 | Description                                           |
|------------------------|-------------------------------------------------------|
| `vuln`                 | Meta script that runs multiple vulnerability checks   |
| `http-vuln-*`          | Includes several HTTP-related vulnerability scripts   |
| `smb-vuln-ms17-010`    | Checks for EternalBlue vulnerability (WannaCry)       |
| `ftp-vsftpd-backdoor`  | Detects VSFTPD backdoor vulnerability                 |
| `ssl-heartbleed`       | Checks for Heartbleed vulnerability                   |

---

## 🔐 Authentication / Brute Forcing

| Script               | Description                                  |
|----------------------|----------------------------------------------|
| `ssh-brute`          | Performs brute force against SSH             |
| `ftp-brute`          | FTP brute force login                        |
| `http-brute`         | Brute forces HTTP basic auth                 |
| `smb-brute`          | Brute forces SMB logins                      |
| `snmp-brute`         | Brute forces SNMP community strings          |

---

## 📁 SMB / Windows Enumeration

| Script                  | Description                                      |
|-------------------------|--------------------------------------------------|
| `smb-enum-shares`       | Lists SMB shares                                 |
| `smb-enum-users`        | Enumerates SMB users                             |
| `smb-os-discovery`      | Gets OS info from SMB                            |
| `smb-security-mode`     | Checks SMB security settings                     |
| `smb-vuln-ms17-010`     | EternalBlue vulnerability                        |

---

## 🧬 Service Enumeration

| Script                 | Description                                    |
|------------------------|------------------------------------------------|
| `ftp-anon`             | Checks for anonymous FTP access               |
| `ssh-hostkey`          | Retrieves SSH host key fingerprints           |
| `mysql-info`           | Gets MySQL server info                        |
| `redis-info`           | Grabs Redis server info                       |
| `mongodb-info`         | Gets MongoDB info                             |
| `rdp-enum-encryption`  | Checks RDP encryption level                   |

---

## 🕵️ Miscellaneous

| Script                | Description                                  |
|-----------------------|----------------------------------------------|
| `whois`               | Performs a WHOIS lookup                      |
| `traceroute-geolocation` | Geolocates traceroute hops                |
| `dns-zone-transfer`   | Attempts DNS zone transfer                   |
| `ntp-info`            | Extracts system info from NTP servers        |