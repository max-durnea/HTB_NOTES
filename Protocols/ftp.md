# FTP/vsFTPd
## vsFTPd Config file:
/etc/vsftpd.conf
## FTPUSERS
/etc/ftpusers

## Info
FTP servers can have settings for **anonymous** login, this allows us to login to the FTP server without credentials and gain access to more information
- **To connect** ftp <ip.address>
- **FTP Runs** on port 21, but can switch to port 20
- **TLS/SSL** we need to use openssl to be able to handle an FTP server with TLS/SSL
SSL certificate allows us to recognize the **hostname**, also an **email address** in some cases for the company.
- For Anonymous login you put the username "anonymous" and the password is an email address
## Commands
- ```debug``` 
- ```trace``` 
- ```ls -R``` - show the directory structure
- ```get <filename>```
- ```wget -m --no-passive ftp://anonymous:anonymous@10.129.14.136``` - Download all available files
- ```put <filename>``` - upload a file
- ```status``` - see the configuration of the ftp server

## Scanning an ftp port with nmap
```sudo nmap -sV -p21 -sC -A 10.129.14.136```
