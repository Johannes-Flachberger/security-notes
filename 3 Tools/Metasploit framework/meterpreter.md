**Tags:** #type/tool #tactic/command-and-control
**Link:** 
**Purpose:** powerful shell listener and client

---
# Info
runs in memory, does not write files to disc -> hard to detect with antivirus file scanner
- uses TLS encrypted communication to attackers server -> hard to detect by IPS (Intrusion preventoin system) and IDS (intrusion detection System)

available payloads can be listed in [[3 Tools/Metasploit framework/msfconsole]] or using [[3 Tools/Metasploit framework/msfvenom]]
how to decide which payload to use:
- target OS
- components available on target, eg. PHP, python
- available network connection types: eg. tcp, https,...

available platforms:
- Android
-  Apple iOS
-  Java
-  Linux
-  OSX
-  PHP
-  Python
-  Windows
# Usage
available commands vary depending on meterpreter version

3 categories of tools:
-  Built-in commands
-  Meterpreter tools
-  Meterpreter scripting

### Core commands
-  `background`: Backgrounds the current session
-  `exit`: Terminate the Meterpreter session
-  `guid`: Get the session GUID (Globally Unique Identifier) 
-  `help`: Displays the help menu
-  `info`: Displays information about a Post module
-  `irb`: Opens an interactive Ruby shell on the current session
-  `load`: Loads one or more Meterpreter extensions
-  `migrate`: Allows you to migrate Meterpreter to another process, can make session more stable, be careful not to migrate to lower privileged process
-  `run`: Executes a Meterpreter script or Post module
-  `sessions`: Quickly switch to another session

### File system commands
- `edit`: will allow you to edit a file
- `search`: Will search for files
- `upload`: Will upload a file or directory
- `download`: Will download a file or directory

### System commands
- `execute`: Executes a command
- `reboot`: Reboots the remote computer
- `shutdown`: Shuts down the remote computer
- `shell`: Drops into a system command shell
- `sysinfo`: Gets information about the remote system, such as OS
- `getpid`: get process id
- `getuid`: get usder id - gives info about privileges
- `ps`: list processes

### Other commands
very interesting things here, see with `help`
eg. turn on webcam, start keylogger, hashdump,...
- `getsystem`: elevate privileges
- `timestomp`: show and modifz the timestamps of files, eg. after you accessed them

### get hashes with mimikatz
`load kiwi`: load mimikatz module
`lsa_dump_sam`: dump NTLM hashes of all users
`lsa_dump_secrets`: dump LSA login hashes
`change_password`: change password, you have to specify the user and current hash
