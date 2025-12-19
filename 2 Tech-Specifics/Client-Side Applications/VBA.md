---
tags:
  - "#type/tech-specific"
---
# Fundamentals
- each sub-procedures starts with `Sub Name()` and ends with `End Sub`
- use [ActiveX Objects](https://learn.microsoft.com/en-us/previous-versions/windows/desktop/automat/activex-objects) to issue system commands- e.g. `CreateObject("Wscript.Shell").Run "powershell"`
- VBA has a 255 character limit for literal strings --> build longer strings by concatenating the literals into a variable. [Cyberchef Recipe](https://gchq.github.io/CyberChef/#recipe=Find_/_Replace(%7B'option':'Regex','string':'(.%7B1,50%7D)'%7D,'Cmd%20%3D%20Cmd%20%2B%20%22$1%22%20%5C%5Cn',true,false,true,true)

To execute macro automatically, use the following predefined macros:

```vb
Sub AutoOpen()

  MyMacro
  
End Sub

Sub Document_Open()
  
  MyMacro
  
End Sub
```
# Pentesting
From the macro, e.g. pop a [[1 Methods/Security-Testing/3 Initial Access/Remote Shells|Remote Shell]] or a e.g. using [[3 Tools/shells/powercat|powercat]] or [[2 Tech-Specifics/OS/Windows/PowerShell#Reverse Shell Payloads|PowerShell]]   
## Snippets
Basic VBA macro that auto-starts powershell:
```vb
Sub AutoOpen()

	StartPowershell
  
End Sub

Sub Document_Open()

	StartPowershell
  
End Sub

Sub StartPowershell()

	Dim Cmd As String
	Cmd = "powershell"
	CreateObject("Wscript.Shell").Run Cmd
  
End Sub
```
# Hardening
