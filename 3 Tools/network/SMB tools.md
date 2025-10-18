**Tags:** #type/tool #tactic/reconnaissance/active 
**Link:** 
**Purpose:** Tool collection for SMB

---
## enum4linux
enumerate smb infos, eg. different shares
`-A` for all infos
`enum4linux <options> [ip]`
eg: `enum4linux -a [IP] | tee enum4linux.log` 
if you want to enumerate multiple ips:
	put ips into a file, one each line
	`xargs -n 1 enum4linux -a < targets.txt`
## SMBClient
for connecting to shares (drives/basically data)
`smbclient //[IP]/[SHARE] -options` 
in smb client shell: “help” for available commands 
## smbget
download files on SMB shares
recursively download whole share: `smbget -R smb://<ip>/<sharename>`
## net view
^d4fe5a
smb enumeration on windows
lists domains, resources, and computers belonging to a given host.
e.g. `net view \\dc01 /all`
`/all`: lists administrative shares too
`/all`: Lists all shares, including administrative shares.
`/domain`: Lists all domains/workgroups on the network.
`/domain:<DomainName>`: Lists all computers in the specified domain.
`net view \\SERVER1`: List all shares on the server

