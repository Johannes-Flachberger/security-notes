**Tags:** #type/tool #tactic/reconnaissance/active #tactic/discovery
**Link:** 
**Purpose:** discovery scanning, port scanning, service detection, OS detection

---
# Info
**GUI tool for building -sn nmap queries: zenmap (preinstalled on kali)**
## general execution steps
1. Enumerate targets 
2. Discover live hosts 
3. Reverse-DNS lookup 
4. Scan ports 
5. Detect versions 
6. Detect OS 
7. Traceroute 
8. Scripts 
9. Write output

# Cheat Sheet: Port ranges
- **Well-known ports:** 0 to 1023
- **Registered ports:** 1024 to 49151
- **Dynamic/private ports:** 49152 to 65535
# Usage
`nmap -options [ip adress]`
enter ip adress as domain names, ip adress, adress ranges `10.10.0-255.0-255` or `10.10.8.149/8` 

## Tips & Tricks
- use multiple output formats at once
- combine SYN and UDP scan
## general options:
`-iL`: file input for list of hosts 
`-v`: verbose mode
`-T<0-5>`: time interval between probes - T4 often used in CTFs T1 used in real world (stealthier)
`--max-parallelism <numprobes>` and `--min-parallelism <numprobes>`: control how much probes are sent in paralell
`-f`: fragment packages for not beeing detected by firewalls or IDSs
`--reason`: show the reason why nmap thinks what it thinks
`--traceroute`: for inbuilt traceroute (many routers block that, so their IP adresses cant be discovered)
`--open`: output only open ports
## output options
`-oN [path]`: write output to file, as it is written out
`-oG [FILENAME]`: greppable output, not easy to read but nice to grep
	see [[#^0d2a5c|nmap grepping cheat sheet]] 
`-oX FILENAME`: xml output, for importing into other toolsexce0
	zusätzlich ```--webxml``` gibt einen xml output den man im browser öffnen kann
`-oA FILENAME`: all output options at once

---
# Discovery scans
if no options are provided for discovery scan:
1. privileged user in local network: ARP requests
2. privileged user outside: ICMP echo, TCP ACK port 80, TCP SYN port 443, ICMP timestamp 
3. unprivileged outside the local network: TCP 3-way handshake by sending SYN packets to ports 80 and 443
**Useful options** 
- `-sn`: no port scanning (however common tcp ports are used for discovery - this can be more accurate than ping)
- `-n`: dont do reverse DNS lookup
- `-R`: also do reverse DNS lookup for offline hosts 
- `-sL` : show list of hosts that will be scanned without actually scanning them
- `--top-ports: scans top 20 ports
- `-O`: guess target OS - take with grain of salt, sometimes firewalls or proxies rewrite packet headers used for OS guessing
#### ARP scan 
`nmap -PR TARGET`
only works if you are on the same subnet
alternative tool: arp-scan
#### ICMP scans
try multiple scan types in case of one beeing blocked
`-PE`: ICMP echo requests often are filtered/blocked!
`-PP`: ICMP timestamp requests
`-PM`: ICMP adress mask request
#### TCP scan
`-PS[port or port list]`: TCP SYN ping (better use priviliged user), reply if port opened
`-PA[port or port list]`: TCP ACK ping, only possible with privileged user, reply if port opened
#### UDP scan
`-PU`: reply if port closed

---
# Port scans
`-p`: specify ports to scan `-p<number>` to scan specified number of ports (supports range, list or - (all))
`-Pn`: do not check if host is online by pinging it
#### Tcp scan (`-ST`)
- default when run without root privileges
full handshake
Information: open, closed, filtered
	What ports respond using tcp:
	open: syn + ack
	closed: reset
	filtered: nothing
-  loud
- sometimes necessary when scanning via a proxy
#### Syn scan (`-sS`)
- default when run with root privileges
scanner sends a RST after SYN/ACK
Information: open, closed, filtered
-  faster than tcp scans
-  sometimes bring unstable services down
- Stealthier: In the application layer, only established connections are logged
	- todays firewalls log SYN scans! 
- **This is basically a DoS attack**, because sessions are not closed
- can be combined with UDP scan (`-sU -sS`)
### UDP scan (`-sU`)
info: closed, opened/filter
- target sends RST or "ICMP port unreachable" if closed, & nothing if open
	- however, firewalls & routers may drop ICMP packets --> false positives
- if no response is given it is unclear if the port is opened or filtered
- the scan can be followed up with probing each port with different protocol packets, to provoke a response - nmap uses fitting protocol packets on well-known ports right away, e.g. a DNS packet on port 53
- a full UDP scan can take several hours
--- 
# Post port scanning
- detect services & versions
- detect os: `-O` or use NSE script (less noisy!)
- use NSE scripts to get more information about each service 

`-A`: Enables OS and version detection, executes in-build scripts for further enumeration
`-sC`: use default nmap scripts
`-O`: guess target OS - take with grain of salt 
`-sV`: determine the running services & versions, full TCP handshake is required -> not possible with SYN scan, `--version-intensity LEVEL` to adjust level, version detection is not a guess
## Scripts

> [!NOTE] Note: some nmap scripts are quite outdated 

scripts path: `/usr/share/nmap/scripts`
multple script catagories exist, eg. discorvery, default....
`--script "SCRIPT-NAME"`: execute script
`--script "SCRIPT-CATEGORY"`: execute scripts from category
`--script-help`: show script information
`-sC`: run script of the "default" category
add further scripts:
- put .nse file in `/usr/share/nmap/scripts/`
- update nmap's script database: `sudo nmap --script-updatedb`
**Ressources:**
- List of scripts: https://nmap.org/nsedoc/scripts/
- NSE usage: https://nmap.org/book/nse-usage.html
## Vulnerability Scanning
^eee943
Also see [[1 Methods/Security-Testing/1 Reconnaissance/Active/Vulnerability Scanning|Vulnerability Scanning]]
Use scripts for vulnerability scanning - script category `vuln`
- e.g. run all scripts from the `vuln` category: `nmap -sV --sript "vuln"`
- e.g. the https://nmap.org/nsedoc/scripts/vulners.html script checks service versions for known vulnerabillities, and also lists Exploit PoCs using the keyword "EXPOIT".
Be careful to know the implications of each script you run
 - category `intrusive` may create an impact on the target
 - category `safe` does not create an impact
If you want to check for a specific vulnerability, just google the cve ID + "nse" 


---
# Firewall detection
## Detect L3/L4 packet filter
#### ACK Scan (`-sA`)
- ACK flag is set
- a non-filtered target responds with ACK regardless of port state
#### Window Scan (`-sW`)
- examines the TCP Window field on response
- similar to ACK scan but might reveal open ports
### Special port scans
helpful when stateless firewall is in place (stateful firewall looks for SYN package)
some firewalls might silently drop traffic, without sending RST packages
#### Null scan (`-sN`)
no flag is set, target sends RST if closed
info: closed, open/filtered
#### FIN scan (`-sF`)
FIN flag is set, target sends RST if closed
info: closed, open/filtered
#### Xmas Scan (`-sX`)
FIN,PSH and URG is set, target send RST,ACK if closed
info: closed, open/filtered
## Detect web application firewalls
`--script http-waf-detect` this uses malicious payloads and checks the response code to detect if a waf blocks the requests
# Firewall evasion
^eb4d21
- `-f`: fragment packages for not beeing detected by firewalls or IDSs
- `-g` or `--source-port` option to perform source port manipulation - set to common port
- `-mtu`: set number of maximum transmission unit
- `-D RND:10`: generate decoy packets using randomly generated IP adresses - makes it more difficult to know which of the source adresses was the actual one
- `--spoof-mac 0`:randomise mac adress

---
## Spoofing
youre only able to both spoof and monitor network traffic in special situations
`-S [spoofed IP adress]`: specify spoofed IP adress to send packets, often you cannot catch the responses --> monitor network traffic with wireshark
`--spoof-mac SPOOFED_MAC`: speficy spoofed mac acress
`-D [decoy adress list]`: makes the attack look as if its coming from multiple (random) adresses eg. `nmap -D 10.10.0.1,10.10.0.2,RND,RND,ME MACHINE_IP` RND = random, ME = my IP adress
## Zombie/idle scan
`nmap -sI ZOMBIE_IP MACHINE_IP`
- similar to spoofing, but is possible more often
- you need an idle host on the network, ie. a host that is not doing anythin right now (eg. an unused printer)
- if the target respons with open port to idle host, the IP ID of the idle host will be incemented -> we can check for this increment
The idle (zombie) scan requires the following three steps to discover whether a port is open:
1. Trigger the idle host to respond so that you can record the current IP ID on the idle host.
2. Send a SYN packet to a TCP port on the target. The packet should be spoofed to appear as if it was coming from the idle host (zombie) IP address.
3. Trigger the idle machine again to respond so that you can compare the new IP ID with the one received earlier.
https://nmap.org/book/idlescan.html
# nmap grepping cheat sheet
^0d2a5c
- grep for active hosts
  - `grep Up [file] | cut -d " " -f 2`
- grep for hosts with specific port open
  - `grep "/<PORT>/open" [file] | awk '{print $2}'`
- grep for hosts with specific port open (IP + hostname)
  - `grep "/<PORT>/open" [file] | awk '{print $2, $3}'`
- grep for any host with open ports
  - `grep "open" [file] | awk '{print $2}'`
- list all open ports per host
  - `grep "Ports:" [file] | awk '{print $2, $4}'` 
- unique IPs with a specific port open
  - `grep "/<PORT>/open" [file] | awk '{print $2}' | sort -u`