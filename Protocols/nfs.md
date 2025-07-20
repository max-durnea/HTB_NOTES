# NFS

- It doesn't have an **authentication** mechanism, and relies on the server to handle translating client's user information into the file system's format

- Most common authentication is via UNIX **UID/GID** and **group memberships**. Problem is that client and server don't necessarily have to have the same UID/GID to users and groups.

- config is stored in **/etc/exports**
## Port
**2049**
## Options
- rw	Read and write permissions.
- ro	Read only permissions.
- sync	Synchronous data transfer. (A bit slower)
- async	Asynchronous data transfer. (A bit faster)
- secure	Ports above 1024 will not be used.
- insecure	Ports above 1024 will be used.
- no_subtree_check	This option disables the checking of subdirectory trees.
- root_squash	Assigns all permissions to files of root UID/GID 0 to the UID/GID of anonymous, which prevents root from accessing files on an NFS mount.

## Footprinting

- ports **111 and 2049** are essential
- **rpcinfo** NSE scsript retrieves a list of all running RPC services
- to run NFS scripts in nmap: ```sudo nmap --script nfs* 10.129.14.128 -sV -p111,2049```

## Mounting

- ```showmount -e 10.129.14.128``` - Show avaliable NFS shares
- mkdir target-NFS
```sudo mount -t nfs 10.129.14.128:/ ./target-NFS/ -o nolock```
cd target-NFS
tree . - **mounting**
- There we will have the opportunity to access the rights and the usernames and groups to whom the shown and viewable files belong. Because once we have the usernames, group names, UIDs, and GUIDs, we can create them on our system and adapt them to the NFS share to view and modify the files.
- ```sudo umount ./target-NFS``` - **unmounting**