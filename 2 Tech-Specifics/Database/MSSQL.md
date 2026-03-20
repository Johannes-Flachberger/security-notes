---
tags:
  - "#type/tech-specific"
---
# Fundamentals

Database management system of the windows ecosystem.

Link: <https://www.microsoft.com/en-us/sql-server/sql-server-2022>

Uses the tabular datastream (TDS) protocol: <https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-tds>

### Manual Connection

From windows use [[3 Tools/database/sqlcmd|sqlcmd]].

From kali use [[3 Tools/network/impacket-scripts|impacket-scripts]]

### Cheat Sheets

- [[2 Tech-Specifics/Database/Standard SQL Cheat Sheet|Standard SQL Cheat Sheet]]
- [MSSQL injection cheat sheet](https://pentestmonkey.net/cheat-sheet/sql-injection/mssql-sql-injection-cheat-sheet)

# Pentesting

### Basic Enumeration

MSSQL provides metadata in form of "[system catalog views](https://learn.microsoft.com/en-us/sql/relational-databases/system-catalog-views/catalog-views-transact-sql?view=sql-server-ver17)", e.g:

- Get the dbms and windows version: `SELECT @@version;`
- show databases: `SELECT name FROM sys.databases;`
- show tables inside a database: `SELECT name FROM sys.tables;`
- list colums of a table - use generic way: `SELECT COLUMN_NAME, DATA_TYPE FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = 'YourTableName';`

### Injection

- Methodology: [[2 Tech-Specifics/Web/Attacks - Web/Injection Attacks/SQL Injection|SQL Injection]]

### Code Execution

the [xp_cmdshell](https://learn.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/xp-cmdshell-transact-sql) function is used to issue system commands

- this is disabled by default!
	- enable by running:
		- `EXECUTE sp_configure 'show advanced options', 1;`
		- `RECONFIGURE;`
		- `EXECUTE sp_configure 'xp_cmdshell', 1;` and
		- `RECONFIGURE;`
- call with `EXECUTE` statement, e.g. `EXECUTE xp_cmdshell 'whoami';`

# Hardening
