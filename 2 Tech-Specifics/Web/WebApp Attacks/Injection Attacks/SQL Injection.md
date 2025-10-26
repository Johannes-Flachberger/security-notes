**Tags:** #type/tech-specific #tactic/execution #tactic/exfiltration #tactic/credential-access 

---
# Fundamentals
SQL Basics:  [[2 Tech-Specifics/Database/Databases + SQL basics|Databases + SQL basics]]
## 3 types: In-Band, Blind and Out Of Band
### In-Band SQL Injection
Same communication medium is used for exploit and receiving the results (eg. webpage)
#### Error-Based
- error messages are directly printed to browser screen
- discover: break SQL query until an error message is produced (trick: try single `'` or `"`)
#### Union-Based 
use union operator + select to return additional results
most common way to extract large amounts of data

### Blind SQL Injection
#### authentication bypass
databases often just check if the credentials are a valid pair (can be found in a table) and then return true/false
example request to make the database return true: `select * from users where username='' and password='' OR 1=1;` (in password field the input was `' OR 1=1;-- `, which always returns true)
#### boolean based SQL Injection
find something on the website that changes if the query is true/false.
then you can start enumerating
first check how many colums the current table has `admin123' UNION SELECT 1;--`, add columns (1,2,3) until it shows true
then enumerate 1) database name 2) table name 3) columns 4) rows
eg. `admin123' UNION SELECT 1,2,3 where database() like 's%';--` try different charecters in the like statement to find out which fits
later on looks like `dmin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'a%';`
#### time based SQL Injection
sleep() function is used - it only is executed upon a successful UNION statement -> you can check if you query is true based on if the delay works
eg. find out number of columns: `admin123' UNION SELECT SLEEP(5),2;--`
later on `admin123' UNION SELECT SLEEP(5),2 from users where username='admin' and password like 'a%';`
then enumerate like with the boolean SQLi
### Out of band SQL Injection
medium to send queries and to receive information is not the same
1) An attacker makes a request to a website vulnerable to SQL Injection with an injection payload.
2) The Website makes an SQL query to the database which also passes the hacker's payload.
3) The payload contains a request which forces an HTTP request back to the hacker's machine containing data from the database.
# Pentesting
Bypass filters using [[2 Tech-Specifics/Web/WebApp Attacks/Injection Attacks/Filter Bypassing|Filter Bypassing]]
# Hardening
1) prepared queries: SQL queries are prepared and the use input is just filled in
2) input validation: black/white list on user input characters
3) escaping user input: puts a \ bevor any special characters -> they are interpreted as normal string

