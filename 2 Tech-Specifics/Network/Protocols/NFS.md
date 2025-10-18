**Tags:** #type/tech-specific 

---
# NFS
network file system
a file system or part of a file system can be mounted remotely on a server and then accessed almost like local files
[https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html](https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html)

- configuration info in /etc/exports
- critical option for privesc: no_root_sqash
## Tools
for enumeration: nfs-common:
### showmount
show mounted nfs shares on ip adress
eg. `showmount -e [IP]`

### mount.nfs
`mount.nfs`: mounting nfs shares
### Mounting NFS shares
`sudo mount -t [type] IP:[ip adress and share name] -nolock`
eg: `sudo mount -t nfs IP:share /tmp/mount/ -nolock`

`-t`: type of device to mount, eg. nfs
`-nolock`: do not use nlm locking