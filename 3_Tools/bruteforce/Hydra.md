**Link:**
**Type:** #type/tool
**Tags:**  #goal/cracking 
**Purpose:** brute force tool

---
# Info
more than 50 Protocols, including Telnet, RDP, SSH, FTP, HTTP, HTTPS, SMB
# Usage
`hydra -l [username] -P [wordlist path] [server] [service]`
eg. `hydra -t 4 -l [user] -P /usr/share/wordlists/rockyou.txt -vV 10.10.10.6 ftp`

`-t 4`: Number of parallel connections per target
`-l [user]` specify one user
`-L [userfile]`: specify file of usernames
`-P [path to dictionary]`: file of possible passwords
`-p`: give one specific password
`-vV`: Sets verbose mode to very verbose, shows the login+pass combination for each attempt
`[machine IP]`: The IP address of the target machine
`-s [PORT]`: set port 
`[service]`: Sets the protocol
`-d`: debug - print more info about whats going on