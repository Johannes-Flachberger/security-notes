**Type:** #type/theory
**Tags:** #tactic/reconnaissance/active 

---
# Tips and Tricks
- Be aware that portscans can trigger IDS/IPS or might overload network components or target devices. - especially in OT.
- Run partial (quick) port scan first, and then while you investigate further run a full port scan
- Take scans in steps, each time probing for more specific information
# Tools
- **main tool:** [[3_Tools/scanning/network/nmap|nmap]]
- portscanner modules from [[3_Tools/Metasploit framework/msfconsole|msfconsole]]
	- Metaspoit also supports db_nmap
- [[3_Tools/shells/Netcat|Netcat]] can also be used for port scanning
- on Windows: Poershell
- Very fast scanners: masscan and RustScan
	- can use A LOT of bandwidth
# Theory
> [!tip] See [[3_Tools/scanning/network/nmap|nmap]] for more theory
## Live host discovery
various layers/protocols can be used for live host discovery:
nmap chooses the protocol automatically depending on the context
-   ARP from Link Layer
-   ICMP from Network Layer
-   TCP from Transport Layer
-   UDP from Transport Layer
## Port ranges
- **Well-known ports:** 0 to 1023
- **Registered ports:** 1024 to 49151
- **Dynamic/private ports:** 49152 to 65535
## Bandwidth considerations
A full tcp scan generated about 4MB of network traffic
--> scanning a class C subnet (254 hosts) generates about 1GB
## Port states
### without firewall
1.  Open port: some service is listening.
2.  Closed port: no service is listening 
### with firewall
1.  **Open**:  a service is listening
2.  **Closed**: no service is listening on the specified port, although the port is not blocked by the firewall
3.  **Filtered**: means that Nmap cannot determine if the port is open or closed because the port is not accessible. The packets were dropped silently, likely by a firewall, or because of NAT, etc.
4.  **Unfiltered**: means that Nmap cannot determine if the port is open or closed, although the port is accessible. This state is encountered when using an ACK scan `-sA`.
5.  **Open|Filtered**: This means that Nmap cannot determine whether the port is open or filtered.
6.  **Closed|Filtered**: This means that Nmap cannot decide whether a port is closed or filtered.
