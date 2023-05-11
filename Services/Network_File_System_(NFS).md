# Approaching Network File System (NFS)
### 111, 2049
**What are the common ports for NFS?**  
Port **111** is used by the Network File System (NFS) to allow clients to access files on a remote server. It is also known as the Remote Procedure Call (RPC) Portmapper.

When an NFS client connects to an NFS server, it first contacts the RPC Portmapper on the server via port 111 to get the port number for the NFS service. The Portmapper responds with the port number for the requested service, which the client then uses to connect to the NFS service on the server.

Port 111 uses the TCP and UDP protocols. TCP is a connection-oriented protocol that provides reliable transmission of data, while UDP is a connectionless protocol that provides faster transmission with less overhead. NFS typically uses UDP for its transport protocol, but TCP can be used as well.

It's worth noting that port 111 is a well-known port, meaning it is assigned to a specific protocol or service by the Internet Assigned Numbers Authority (IANA). Therefore, it is generally used exclusively by NFS and should not be used by any other application or service.
#
Port **2049** is also a well-known port used for Network File System (NFS) services. NFS is a distributed file system protocol that allows a client to access files over a network in a manner similar to how local storage is accessed.

Port 2049 is the default port used for the NFS protocol. When a client initiates an NFS request, it sends the request to the server's port 2049. The server then sends the requested data back to the client over the same port.

In addition to NFS, port 2049 may also be used by some other network services and applications, but its primary usage is for NFS. It is important to note that port 2049 should be properly secured to prevent unauthorized access to NFS services and data.  
`Note: Ports can be different.`
#
### Enumeration
```
nfs-ls #List NFS exports and check permissions
nfs-showmount #Like showmount -e
nfs-statfs #Disk statistics and info from NFS share
```
i.e
```bash
┌──(root㉿kali)-[/home/beri]
└─# nmap -sC -sV builder.htb -p111 --script=nfs-showmount,nfs-ls,nfs-statfs
Starting Nmap 7.93 ( https://nmap.org ) at 2023-05-11 11:22 PKT
Nmap scan report for builder.htb (10.10.11.191)
Host is up (0.23s latency).

PORT    STATE SERVICE VERSION
111/tcp open  rpcbind 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3           2049/udp   nfs
|   100003  3           2049/udp6  nfs
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      34907/tcp   mountd
|   100005  1,2,3      35508/udp6  mountd
|   100005  1,2,3      44928/udp   mountd
|   100005  1,2,3      58907/tcp6  mountd
|   100021  1,3,4      42207/tcp   nlockmgr
|   100021  1,3,4      43157/tcp6  nlockmgr
|   100021  1,3,4      51968/udp6  nlockmgr
|   100021  1,3,4      59022/udp   nlockmgr
|   100227  3           2049/tcp   nfs_acl
|   100227  3           2049/tcp6  nfs_acl
|   100227  3           2049/udp   nfs_acl
|_  100227  3           2049/udp6  nfs_acl
| nfs-showmount: 
|   /home/ross *
|_  /var/www/html *
| nfs-ls: Volume /home/ross
|   access: Read Lookup NoModify NoExtend NoDelete NoExecute
| PERMISSION  UID   GID   SIZE  TIME                 FILENAME
| rwxr-xr-x   1001  1001  4096  2023-05-11T05:08:33  .
| ??????????  ?     ?     ?     ?                    ..
| rwx------   1001  1001  4096  2022-10-21T14:57:01  .cache
| rwx------   1001  1001  4096  2022-10-21T14:57:01  .config
| rwx------   1001  1001  4096  2022-10-21T14:57:01  .local
| rw-------   1001  1001  2475  2022-12-27T15:33:41  .xsession-errors.old
| rwxr-xr-x   1001  1001  4096  2022-10-21T14:57:01  Documents
| rwxr-xr-x   1001  1001  4096  2022-10-21T14:57:01  Music
| rwxr-xr-x   1001  1001  4096  2022-10-21T14:57:01  Pictures
| rwxr-xr-x   1001  1001  4096  2022-10-21T14:57:01  Public
| 
| 
| Volume /var/www/html
|   access: Read NoLookup NoModify NoExtend NoDelete NoExecute
| PERMISSION  UID   GID  SIZE  TIME                 FILENAME
| rwxr-xr--   2017  33   4096  2023-05-11T06:20:01  .
| ??????????  ?     ?    ?     ?                    ..
| ??????????  ?     ?    ?     ?                    .htaccess
| ??????????  ?     ?    ?     ?                    css
| ??????????  ?     ?    ?     ?                    images
| ??????????  ?     ?    ?     ?                    index.html
| ??????????  ?     ?    ?     ?                    js
|_
| nfs-statfs: 
|   Filesystem     1K-blocks  Used       Available  Use%  Maxfilesize  Maxlink
|   /home/ross     6071864.0  4505096.0  1487020.0  76%   16.0T        32000
|_  /var/www/html  6071864.0  4505104.0  1487012.0  76%   16.0T        32000

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.17 seconds
```
