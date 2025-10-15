**Type:** #type/tool
**Tags:**  
**Link:** https://www.kali.org/tools/hping3/
**Purpose:** forge packets, perform network and port scans

---
# Info

# Usage
`-A`: set ACK flag
`-p`: set port
`--flood`: performs tcp flooding

### Examples
`hping3 -A [Target IP Address] -p 80 -c 5`
In this command, **-8** specifies a scan mode, **-p** specifies the range of ports to be scanned (here, **0-100**), and **-V** specifies the verbose mode.

`hping3 -1 [Target IP Address] -p 80 -c 5`
In this command, **-1** specifies ICMP ping scan, **-c** specifies the packet count (here, **5**), and **-p** specifies the port to be scanned (here, **80**).

`hping3 -F -P -U [Target IP Address] -p 80 -c 5`
In this command, **-F** specifies setting the FIN flag, **-P** specifies setting the PUSH flag, **-U** specifies setting the URG flag, **-c** specifies the packet count (here, **5**), and **-p** specifies the port to be scanned (here, **80**).
