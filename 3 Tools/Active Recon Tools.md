---
tags:
  - "#type/tool" 
  - "#attack/reconnaissance/active" 
Link: 
Purpose: Collection of tools used for active recon
---
# Info

# Usage

## Browser

- very unsuspicious
- use devtools to gather information
- useful extensions: Wappalyser, user agent switcher

## Ping

[[3 Tools/scanning/network/ping]]

## Traceroute

- you might want to consider some of the routers on the route, depending on the situation
- many routers don't send TTL exceeded packets, so their IP addresses wont be detected

## Telnet

- can be used to get info about running server
1. connect with[[2 Tech-Specifics/Network/Protocols/TCP 23 Telnet]]
2. send request, type depending on server, eg. `GET / HTTP/1.1` or specify other page
alternative: [[3 Tools/web/cURL]]

## Netcat

- use like telnet
- [[3 Tools/shells/Netcat]]
