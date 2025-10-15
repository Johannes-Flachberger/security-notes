**Type:** #type/tool
**Tags:**  #goal/exploitation
**Link:** 
**Purpose:** send HTTP requests manually

---
# Info
send HTTP requests manually from the commandline
# Usage
eg. `curl -X GET http://127.0.0.1:5984/`

`-X` request type (verb) eg. `POST`,`GET`
`-H` specify header - e.g.  `-H 'Content-Type: application/json'`
`--data` specify data
`-c` [FILE PATH] to reseve cookies to specified file
`-b` [FILE PATH] to send cookies in specified file
`-i`: include respnse headers in output
`--path-as-is` usually, curl follows RFC 3986 rules for URI path normalization (removing `/../` and `/./` segments) - with this option, paths are interpreted exactly as supplied