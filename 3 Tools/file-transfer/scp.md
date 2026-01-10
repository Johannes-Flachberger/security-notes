---
tags:
  - "#type/tool" 
  - "#attack/exfiltration" 
Link: 
Purpose: transfer files using ssh
---
# Info

**[[2 Tech-Specifics/Network/Protocols/TCP 22 SCP|SCP as a technology]]**
transfer files between two machines using an ssh connection

# Usage

`scp <source> <target>`

eg: `scp ./linpeas.sh jan@10.10.100.180:/tmp/`

or: `scp [user]@[host]:[remote path] [local path]`

eg: `cp example_user@10.10.178.153:/home/example_user/archive.tar.gz ~`
