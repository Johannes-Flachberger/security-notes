**Tags:** #type/tool #tactic/exfiltration
**Link:** https://github.com/sc0tfree/updog
**Purpose:** upload things to targets

---
# Info
basically works like [[3 Tools/sharing files/simple python webserver|simple python webserver]] but allows http auth and https with self signed certificates - more easy to use
# Usage
`updog [-d DIRECTORY] [-p PORT] [--password PASSWORD] [--ssl]`

|Argument|Description|
|---|---|
|-d DIRECTORY, --directory DIRECTORY|Root directory [Default=.]|
|-p PORT, --port PORT|Port to serve [Default=9090]|
|--password PASSWORD|Use a password to access the page. (No username)|
|--ssl|Enable transport encryption via SSL|
|--version|Show version|
|-h, --help|Show help|
