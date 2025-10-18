**Tags:** #type/tech-specific #tactic/privilege-escalation 

---
# Useful commands:
powershell basics in [[2 Tech-Specifics/OS/Windows/powershell]]
cmd basics in [[2 Tech-Specifics/OS/Windows/cmd cheatsheet]]
## enumerate users
`whoami /priv`: show current users privileges
`net users`: list users
`net user [username]`: list details of user
`qwinsta`: other users logged in simultaneously
`net localgroup`: show user groups defined on the local system
`net localgroup [groupname]`: list groupmembers of group
## system information
`systeminfo`: overview of system, output might be overwhelming -> grep with `systeminfo | findstr /B /C:"OS Name" /C:"OS Version"`
`hostname`: show computers name, might reveal info on its purpose

## searching files
interesting info might be in configuration files of software
`findstr`: eg `findstr /si [keyword] *.txt`
	`/s`: searches in current dir & subdirs
	`/i`: search not case-sensitive
	`*.txt`: cover only txt files useful extensitons: “.txt”, “.xml”, “.ini”, “*.config”, and “.xls”

## check update history
`wmic qfe get Caption,Description,HotFixID,InstalledOn`: list updates

## Antivirus enum
2 options: search for antivirus explicitely or list all running services and checking for antivirus
eg. `sc query windefend`: search for "windefend" service
`sc queryex type=service`: list all active services

view running services
`wmic service get name,displayname,pathname,startmode` filter with `| findstr "[keyword]"`

## installed software
`wmic product`: show info of some installed product, output may be overwhelming ->
`wmic product get name,version,vendor`: show product info, only specific parts
 above commands may not show all software (due to backwards compatibility issues)
 -> enumerate installed software using services
 `wmic service list brief`: list all services
 `wmic service list brief | findstr  "Running"`: list all running services
 `sc qc`: show detailed info of service
-> search online for exploits for the installed software

## Unattend files
file name: Unattend.xml
helps sysadmins to set up the windows system, sometimes is left on teh system
may contain valuable info

