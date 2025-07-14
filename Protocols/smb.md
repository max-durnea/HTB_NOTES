# SMB

- **Connection** - ```smbclient -N -L //10.129.14.128```
- **Inspect Share** - ```smbclient //10.129.14.128/notes```
- **Commands** - ```help```

## Tools

You can use **NMAP** but it won't tell you everything about the server so a good idea is to use different tools and your own research

### RPCclient 
- ```rpcclient -U "" 10.129.14.128```
- get commands with ```man rpcclient```
- **Examples**:
1. srvinfo
2. enumdomains
3. querydominfo
4. netshareenumall
5. netsharegetinfo <name>
6. enumdomusers
7. queryuser <rid> (rid is a number like __0x3e9__)
8. querygroup <rid>

An interesting thing you can do is **Brute Force User RIDs**
```for i in $(seq 500 1100);do rpcclient -N -U "" 10.129.14.128 -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "";done```

### Other Tools
- [samrdump.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/samrdump.py)
- [SMBMap](https://github.com/ShawnDEvans/smbmap)
- [CrackMapExec](https://github.com/byt3bl33d3r/CrackMapExec)
- [enum4linux-ng](https://github.com/cddmp/enum4linux-ng)