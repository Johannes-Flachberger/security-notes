**Type:** #type/tool
**Tags:**  #tactic/reconnaissance/active 
**Link:** 
**Purpose:** Collection of tools used for active recon

---
# Info
#todo 

# Usage

## Browser
- very unsuspicious
- use devtools to gather information
- useful extensions: Wappalyser, user agent switcher
## ping
[[3_Tools/scanning/network/ping]]
## traceroute
-  you might want to consider some of the routers on the route, depending on the situation
- many routers don't send TTL exceeded packets, so their IP addresses wont be detected
## telnet
- can be used to get info about running server
1. connect with[[2_Tech-Specifics/Network/Protocols/Telnet]]
2. send request, type depending on server, eg. `GET / HTTP/1.1` or specify other page
alternative: [[3_Tools/web/cURL]]
## Netcat
- use like telnet
- [[3_Tools/shells/Netcat]]