# Practical 2
## Creating Databases and Tables

To summarise the main content so far:
- We use database software such as MySQL to create individual databases. 
- Databases contain tables, and there can be multiple tables in a database.
- A table is comprised of fields, which are strictly defined for their data type, size, and other properties. 
- This definition is known as a Schema.

All of this is done using a language called Structured Query Language (SQL).

In this task you're going to practice creating databases and tables by defining our fields, using SQL commands.

Since your objective is just to practice and build familiarity with the commands and syntax you should just choose your own example DB names, table names, and fields. You're going to drop the tables anyway, so it doesn't matter. 

Here is a reminder of the different commands we've seen so far, you should try to use all of them. If you're not sure about a command go back and review the relevant section, or ask for help: 

### Database Commands
```sql
CREATE DATABASE db_name;

SHOW DATABASES;

USE db_name;

DROP DATABASE db_name;
```

### Table Commands

For these commands think of a realistic scenario to model your table on. It could be a table of students so your fields are the attributes for a person, but it could also be a table for your stock in a shop, or a fantasy football team. This will prompt you to consider the data types in more detail. 

If you're feeling ambitious, you can find many more data types to play around with here <https://www.w3schools.com/sql/sql_datatypes.asp>.

```sql
CREATE TABLE table_name (
	field1_name INT NOT NULL PRIMARY KEY,
	field2_name VARCHAR(30),
	field3_name VARCHAR(30),
	field4_name INT UNSIGNED NOT NULL
);

SHOW tables;

DESCRIBE customers;
```