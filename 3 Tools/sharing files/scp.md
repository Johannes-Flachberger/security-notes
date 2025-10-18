**Tags:** #type/tool #tactic/exfiltration 
**Link:** 
**Purpose:** transfer files using ssh

---
# Info
**[[2 Tech-Specifics/Network/Protocols/SCP|SCP as a technology]]**
transfer files between two machines using an ssh connection
# Usage

run on attacker: `scp [local file] [user]@[ip]:[path]
eg: `scp ./linpeas.sh jan@10.10.100.180:/tmp/`

or: `scp [user]@[host]:[remote path] [local path]`
eg: `cp example_user@10.10.178.153:/home/example_user/archive.tar.gz ~`