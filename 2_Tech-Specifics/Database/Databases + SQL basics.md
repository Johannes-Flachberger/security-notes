tags: #type/theory 

---
# Databases
most databases are relational databases:
- there are many tables, each has rows (each representing a specific item) and columns (each representing a certain property)
- each item has a primary key which it can be found with in all tables

# SQL
cheat sheet: [[2_Tech-Specifics/Database/SQL-cheat-sheet.pdf]]
"statements" are used to make queries
comments: `--`
wildcard: `%`  ...matches everything in queries
## general
- information_schema database: holds information about all the databases and tables the user has access to 
## basic statements
### select
retrieve data
Syntax: `select [argument] from [table name];
- argument can be eg. column names
- eg. `select * from users;`
**LIMIT** clause: limits the number of results (`LIMIT[number of rows to skip],[number of rows to return]` --> LIMIT1,2 skipts 1 row and returns 2 rows)
**where** clause: filter data, eg: `select * from users where username='admin';`
combine with or: `select * from users where username='admin' or username='jon';`
combine with and: `select * from users where username='admin' and password='p4ssword';`
**like** clause: filters for fields that start, contain or end with the specified clause: `select * from users where username like 'a%';` everything that begins with "a", put % to specify location
### UNION
combine two or more select statements, the specified columns have to be in the same order, have the same datatype
eg. `SELECT name,address,city,postcode from customers UNION SELECT company,address,city,postcode from suppliers;`
### INSERT
insert new row to database
Syntax: `insert into [table] ([column1, column2, ...]) values ([value for column1, value for column2, ...]);`
eg: `insert into users (username,password) values ('bob','password123');`
### UPDATE
update one or more rows in the table
Syntax: `update [table] SET column1='[value1]',<column2>='<value2>' <filtering (chose what rows to set);`
eg: `update users SET username='root',password='pass123' where username='admin';`
### DELETE
delete rows
use "where" to specify which rows to delete and "LIMIT" to choose how many to delete
Syntax: `delete from [table] [filtering];`
eg: `delete from users where username='martin';`
to delete everything: `delete from users;`
## useful functions
* `database()`: returns current database
* `group_concat()`:  gets specified column from multiple rows and puts it in one string