---
tags:
  - "#type/tech-specific" 
---
# Fundamentals

most databases are relational databases:

- there are many tables, each has rows (each representing a specific item) and columns (each representing a certain property)
- each item has a primary key which it can be found with in all tables

## Implementation Specifics

SQL flavor and DBMS queries differ depending on the database management system:

- [[2 Tech-Specifics/Database/MySQL|MySQL]]
- [[2 Tech-Specifics/Database/MSSQL|MSSQL]]

A set of fundamental queries is supported by most databases, often referred to as standard SQL: [[2 Tech-Specifics/Database/Standard SQL Cheat Sheet|Standard SQL Cheat Sheet]]

# Pentesting

## Generic DB Enumeration

`information_schema` database: holds metadata for all databases on the dbms - Reference: <https://dev.mysql.com/doc/refman/8.4/en/information-schema.html>

**Workflow:**

1. enumerate the available databases
	- this is specific to the database management system
2. select a database: `USE <database>`
3. enumerate all tables within the dbms: `SELECT TABLE_SCHEMA, TABLE_NAME FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_TYPE = 'BASE TABLE';`
4. enumerate the columns of a table: `SELECT COLUMN_NAME, DATA_TYPE FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = '<table>';`

# Hardening
