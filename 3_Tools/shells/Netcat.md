**Type:** #type/tool
**Tags:**  #tech/shell
**Link:** 
**Purpose:** simple tool for connect shell and listeners

---
# Info
simple tool to setup shell listeners and connect to shell
windows executables: https://github.com/int0x33/nc.exe/
more sophisticated alternative: [[3_Tools/shells/Socat]]

# Usage

connect to machine: `nc <target-ip> <chosen-port>`
start listener: `nc -lnvp <port>

can also be used for **port scanning**:
- TCP Scan: `nc -nvv -w 1 -z [IP] [START_PORT-END_PORT]`
	- eg. `nc -nvv -w 1 -z 192.168.50.152 3388-3390`
	- `-z` = zero io mode
- UDP  Scan: same as tcp scan, use `-u` additionally
	- if filtered, ports will be listed as open because no "ICMP port unreachable" is received 
## stabilisation: rlwrap
gives better featured shell out of the box
has to be installed`sudo apt install rlwrap`
start special listener: `rlwrap nc -lvnp <port>`
some manual stabilisation may be helpful, eg. step 4 of python method

# Use Cases
### Manual SMTP Connection
connect to port 25, send [[2_Tech-Specifics/Network/Protocols/TCP 25 SMTP|SMTP]] commands manually

``` shell
nc -nv 192.168.50.8 25
VRFY root
```

