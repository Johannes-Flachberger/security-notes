**Tags:** #type/tool #tactic/command-and-control
**Link:** 
**Purpose:** 

---
# Info
## Module types
### auxiliary
- scanners, crawlers and fuzzers
Useful modules:
- `scanner/portscan/`: performing portscans, like nmap
- `scanner/discovery/udp_sweep`: udp service identification
- `scanner/smb_enumshares` and `smb_version`: smb enumeration
### encoders
- encode the exploit and payload, to evade signature based antivirus
### evasion
- try to evade antivirus
### exploits 
### nops
do nothing - used for as bufffer for consistent payload sizes
### payload types
- stageless: all (eg. whole reverse shell) in one, easier to catch
- staged: first a small stager is sent, then the actual payload (stage), the stage can be larger than stageless payloads, stealthier, but a little harder to use

Payload naming:
`<OS>/<arch>/<payload>`
eg: `linux/x86/shell_reverse_tcp`
stageless payloads have a _ in their name: `shell_reverse_tcp`
staged payloads have a / :`shell/reverse_tcp`
### post
post exploitation
## Exploit ranking
exploits are ranked depending on their reliability
https://github.com/rapid7/metasploit-framework/wiki/Exploit-Ranking
## Useful modules
- hashdump: dump hashes on windows systems
# Usage
## Basic process
1. Start postgresql (database) – sometimes you can skip this
2. Start Metasploit (msfconsole)
3. Search for exploit
4. Choose (use) exploit (Ex.: xp_cmdshell enabled)
5. info command – get exploit information and ranking
6. Choose (set) payload (Ex: reverse tcp shell)
7. Set payload options (IP, user, password, port)
8. Execute or run the exploit (launch it!)
9. Interact with target via meterpreter / shell (exploitation, privilege escalation, etc.)
## Commands 
start metasploit console: (-q for quiet mode): `msfconsole`
### general
get help: `help <module or command>` 
treating variables/options: `get/set getg/setg unset/unsetg [name] [value]`
save console output to file `spool`
simple connection to host `connect`
show command history: `history`
save current datastore to use again later `save`
### navigation
search modules: `search`
use module: `use`
leave context (module): `back`
show modules of a type: `show [module type]`
### session handling
show active sessions: `sessions`
background a session: `background` or CTRL+Z
interacct with existing session: `sessions -i`
### module handling
show possible payloads: `show payloads`
show options: `options`
set option: `set [option] [value]`
set rhosts option to hosts from database: `hosts -R`
run module: `run` - add `-j` to run as background job
check if target is exploitable, without exploiting it: `check`
### workspace handling
show existing workspaces: `workspace` (`-h` for help)
add workspace: `workspace -a`
delete workspace `workspace -d`
help: `-h`
change workspace: `workspace [name]`
### database
start & initialize database: `msfdb init` 
get database status: `db_status`
get gathered info about hosts: `hosts` (`-h` for help)
get gathered info about services: `services` (`-h` for help)
`db_import [file]`: import a file to db; e.g. write [[3 Tools/scanning/network/nmap|nmap]] output to file with `-oX [file]` and then import the file

### setup reverse shell listener with multi/handler
in msfconsole use module: `use multi/handler`
set options:
-  `set PAYLOAD <payload>`
-  `set LHOST <listen-address>`
-  `set LPORT <listen-port>`
start exploit: `exploit -j`

foreground reverse shell after connection: `session -i <number>
