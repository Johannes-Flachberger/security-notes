# Standard SQL Cheat Sheet
Basically all SQL flavours support these fundamental statements.
comments: `--`
wildcard: `%` ...matches everything in queries
### SELECT
retrieve data
Syntax: `select [argument] from [table name];
Example:
```sql
select * from users;
```
#### FETCH FIRST:
limit the number of results
```sql
FETCH FIRST 10 ROWS ONLY
```
#### OFFSET ... FETCH NEXT
skip a number of results and then show a limited number of results
```sql
OFFSET 5 ROWS FETCH NEXT 10 ROWS ONLY;
```
#### WHERE:
filter data, eg: 
```sql
select * from users where username='admin';
```

combine with or:
```sql
select * from users where username='admin' or username='jon';
```

combine with and: 
```sql
select * from users where username='admin' and password='p4ssword';
```

#### LIKE:
filters for fields that start, contain or end with the specified clause: 
```sql
select * from users where username like 'a%';
```
 everything that begins with "a", put % to specify location
### UNION
combine two or more select statements, the specified columns have to be in the same order, have the same datatype
eg. 
```sql
SELECT name,address,city,postcode from customers UNION SELECT company,address,city,postcode from suppliers;
```
### INSERT
insert new row to database
Syntax: 
```sql
insert into table_name ([column1, column2, ...]) values (value1, value2, ...);
```

Example:
```sql
insert into users (username,password) values ('bob','password123');
```

### UPDATE
update one or more rows in the table
Syntax: 
```sql
update [table] SET column1='[value1]',<column2>='<value2>' <filtering (chose what rows to set);
```

Example:
```sql
update users SET username='root',password='pass123' where username='admin';
```
### DELETE
delete rows

Syntax: 
```sql
delete from [table] [filtering];
```

Example - use "where" to specify which rows to delete:
```sql
delete from users where username='martin';
```

R.g. to delete everything: 
```sql
delete from users;
```

#### CASE
handle conditions

```sql
SELECT CASE WHEN 2 > 1 THEN 'YES' ELSE 'NO' END;
```