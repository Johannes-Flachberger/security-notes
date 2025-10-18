**Tags:** #type/tech-specific

---
# General
for help menu of each command: `/?`

# Commands
- `hostname`: shows hostname
- `ipconfig`: show network adress settings
- `netstat`: display protocol statistics
- `cls`: clear command prompt
- `net`: manage network resources; help menu: `net help`
- `icacls`: show permissions of a file or folder

![[2_Tech-Specifics/OS/Windows/Command Prompt Cheatsheet.pdf]]

# Useful snippets
`sc queryex type=service state=all`:show all available services
`netsh firewall show state`: show firewall state
`netsh firewall show config`: show firewall config
`wmic /node:"" product get name,version,vendor`: show details of installed software
`wmic useraccount get name,sid`: show login names and SIDs of users
