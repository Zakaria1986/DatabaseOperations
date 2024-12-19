# Intro to Databases

Pretty much every organisation that holds data will have it in a database which makes it easier to store, manage, and retrieve the data. 
There are various different database options available, which are often tailored to specific use cases, however they all fit into one of two categories, SQL and NoSQL.

## Relational Databases (SQL)
### RDBMS

The software that lets you create, manage, and query databases, is called a **relational database management system**. Some popular ones include:
- MySQL
- PostgreSQL
- Microsoft SQL Server

### Practical 1

- Install MySQL
- snapshot VM

### SQL Databases

Structured Query Language (SQL) is a database type which was developed in the 70’s, based on theoretical relational data models proposed in the 60’s. SQL databases are also known as relational databases.
SQL databases store data in tables which are defined by a schema. Each data item entered into the table must adhere to this schema.
You can create multiple tables, and then create relationships between them based on data items they have in common.

We're going to install a database engine (an RDBMS) on our Linux In a momr, but when done we need to create a database, in which we can create our tables to store our data. 

To create a database use the following SQL command.

```sql
CREATE DATABASE test_db;
```

We can then verify it was created with.

```sql
SHOW DATABASES;
```

Once created we need to move into that database so that we can start working with it.

```sql
USE test_db;
```

We can also delete databases with the DROP keyword.

```sql
DROP DATABASE test_db;
```

CREATE and DROP can also be used for tables, which we'll look at shortly. 

### The SQL Language

Although you can interact with SQL databases via a GUI, SQL was developed at a time when GUI’s were not common, and much like Linux, maximum compatibility is still achieved through the use of the standardised command set and syntax.

Many of the different types of SQL databases have their own additional features, such as supporting unique data types, or in some cases restrictions, such as naming conventions, but they should all support the standard SQL features and commands.

The SQL commands can be divided into three groups based on the type of functionality they provide:
- DDL - used to define the structure of the database and its objects such as tables, schemas, and indexes.
- DML - used to manipulate data within the database
- DQL - commands to retrieve data from the database
- DCL - used to manage access to the database by granting or revoking permissions.
- TCL - commands to manage transactions within a database to ensure data integrity.

SQL commands have simple syntax and conventions, compared to say Python or Bash. A basic SQL query looks like this:

```sql
SELECT * FROM Customers WHERE Name = “Company A”;
```

Commonly they’re split over multiple lines for readability. SQL doesn’t care about newlines, it looks for the semi-colon (;) to end the statement.

```sql
SELECT * FROM Customers 
WHERE Name = “Company A”;
```

One convention is that SQL keywords are capitalised, therefore it makes sense that your tables and fields should not be.

### SQL Tables

A database will typically contain multiple tables, but exactly which ones is up to you and your organisation’s needs. 
A common example is to consider a business which needs an employee_table, customer_table, products_table, and an orders_table.

*Instructor prompt: WB*

Tables in SQL are comprised of Fields (columns) and Records (rows), each record is an new entry in the database, and the fields are the data items captured for each record.

Every record in the table needs a unique identifier, known as a ‘Primary Key’, since two entries might have the same name.

When one table has a field for another table’s Primary Key, such as an Orders table referencing a Customer_ID number when they make a purchase, we call this a Foreign Key. 

Linking Primary and Foreign keys is how we create relationships between tables.

### SQL Schema

Here is an example of creating a basic employee table and schema:

```sql
CREATE TABLE customers (
	customer_ID INT NOT NULL PRIMARY KEY,
	first_name VARCHAR(30),
	last_name VARCHAR(30),
	age INT UNSIGNED NOT NULL
);
```

Like with the database, we can verify our table was created with `SHOW tables;`, but to ensure that all of our data types and additional options are configured correctly we can see a more detailed overview with

```sql
DESCRIBE customers;
```

We’re only using two data types, INTs and VARCHARS, but many more area available. However, there are several points worth reviewing…

### SQL Data Types

Although some of the different SQL databases have been developed to support niche data types and features, there are lots of data types supported by all:
- INT = whole numbers, use UNSIGNED to restrict to positive numbers only.
- DECIMAL = decimal numbers to a defined precision e.g. DECIMAL(8, 2) stores up to 8 digits, with 2 after the decimal point. 
- CHAR(number) = a fixed length string
- VARCHAR(number) = a string up to the specified length
- DATE, TIME, DATETIME = yy-mm-dd, hh:mm:ss, YYYY-MM-DD hh:mm:ss
- BOOLEAN = true/false
And many others…

### Practical 2

- Practice creating and dropping databases and tables
- Try to use CREATE, DROP, SHOW, USE, and DESCRIBE.

### Working with Data

Adding records to the database can be done in a number of ways. We are going to use standard SQL commands through the CLI, but this would not be suitable for a non-technical user.

Commonly a GUI can be created which translates user input into the appropriate SQL statements in the back-end.

Alternatively, data can be imported and exported in bulk using a variety of file types, a common option being CSV files.

### Inserting Records

Adding records into a table can be done with the INSERT statement:

```sql
INSERT INTO customers (customer_ID, first_name, last_name, age) 
VALUES (1, 'Alice', 'Smith', 33);
```

As we're just learning, it's good practice to verfiy your data entry. You can do so by running

```sql
SELECT * FROM customers;
```

We'll come back to the SELECT statement shortly.

There are some syntax variations that can improve efficiency if you want to add data to all, or just specific fields in a record, but the basic logic is like the example.

### Updating Records

To make changes to existing records use the UPDATE statement.

```sql
UPDATE customers
SET Age = 31
WHERE customer_ID = 1;
```

Notice the WHERE clause, this allows you to filter the records you retrieve from the database, in this case to make a simple update. But this is the key to retrieving, and gaining insights into your data. 

### Practical 3

- Create customers, and products tables
- Insert records into each table
- Update records

### Selecting Records

Databases allow you to store, manage, and retrieve your data. Retrieval is about providing access to your data quickly and efficiently, for example looking up a customer’s records when then call in for support. 

```sql
SELECT *
FROM customers
WHERE customer_ID = 1;
```

Quick retrieval is one of the primary uses for a database, commonly GUI based applications which are easy for non-technical users to navigate and interact with, have databases in the back-end, such as a CRM system which looks up customer information when they call in for support. Or a web-based storefront, in which all of the product information is recalled from a database as the customer navigates the different items.

### Practical 4

- Practice SELECT statements against created tables

#### Comparison Operators

Similar to Python, Bash, and many other environments, we can use comparison operators in our queries to further refine them, **but only against numeric values**.

```sql
SELECT first_name, last_name 
FROM customers 
WHERE age > 30;
```

The following comparison operators can be used

|Comparison         |Syntax |
|-------------------|-------|
|Equal              |=      |
|Not equal          |= or !=|
|Greater            |>      |
|Greater or equal   |>=     |
|Less               |<      |
|Less or equal      |<=     |

#### String Patterns

We do have the ability to match patterns in strings, but we use the LIKE or NOT LIKE clauses in our SQL statements.  

|Pattern            |Syntax |
|-------------------|-------|
|Strings starting with 'abc'|'abc%'   |
|Strings ending with 'abc'  |'%abc'   |
|'abc' within the string    |'%abc%'  |
|Exactly X characters long  |'___' (3 here)|
|_ can be any character     |'a_c'    |

Example

```sql
SELECT first_name, last_name 
FROM customers 
WHERE first_name LIKE 'Al%';
```

The SELECT statement also allows you to analyse your data to identify patterns, trends, and answer questions. 

You can write queries to identify not only the best selling products, and the biggest spending customers, but also go deeper. What about the best selling products by geography, time of year, or both? Who are the biggest spending customers by age? Or any other summaries, or insights you can think of.

This extra insight might inform decisions for marketing teams, promotion planning, inventory purchasing, future investment, and so on…

### Practical 5

- Practice SELECT statements using comparison operators and pattern matching clauses

### Multiple Tables

We've already made multiple tables, but so far they aren't *related* to each other. Let's change that...

Most databases will require several tables, because for example, the customer table is not suitable for storing data related to the products you have in your inventory. So customers and products will be separate tables, with different schemas according to the type of data to be stored.

Some tables are populated with data from others, for example an orders table might take data from the customers table and the products table to make a new entry.

Ideally when one table references another it should reference the target table’s Primary Key, and we define the field in the destination table as a Foreign key. 

```sql
CREATE TABLE customers (
	customer_ID INT NOT NULL PRIMARY KEY,
	first_name VARCHAR(30),
	last_name VARCHAR(30),
	age INT UNSIGNED NOT NULL
);

CREATE TABLE products (
    product_id INT NOT NULL PRIMARY KEY,
    product_name VARCHAR(100),
    product_price DECIMAL(10,2)
);
```

Hopefully your CREATE TABLE statements look something like the above example, now we're going to create an orders table which references both customers and products by creating FOREIGN KEYS.

```sql
CREATE TABLE orders (
    order_id INT NOT NULL PRIMARY KEY,
    customer_id INT,
    product_id INT,
    order_date DATE,
    order_quantity INT,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
```

It's important that the FOREIGN key and the PRIMARY key it references contain the same data type and attributes or you'll get an error.

Lets add some data to the tables. We'll also update our syntax to add multiple records at once. 

*It is recommended that you copy the following examples to a text editor and extend them so you have more data to work with before running them in MySQL*

```sql
-- Insert records into the customers table
INSERT INTO customers (customer_id, first_name, last_name, age)
VALUES
    (1, 'Alice', 'Smith', 33),
    (2, 'Alan', 'Jones', 28),
    (3, 'Noche', 'Snead', 3);

-- Insert records into the products table
INSERT INTO products (product_id, product_name, product_price)
VALUES
    (101, 'Laptop', 999.99),
    (102, 'Phone', 599.99),
    (103, 'Tablet', 399.99);

-- Insert records into the orders table
INSERT INTO orders (order_id, customer_id, product_id, order_date, order_quantity)
VALUES
    (201, 1, 101, '2023-11-22', 2),
    (202, 2, 102, '2023-11-23', 1),
    (203, 3, 103, '2023-11-24', 3);
```

Now we have records in each table, but the orders table includes two fields which link to unique fields (i.e. primary keys) in neighbouring tables.

We've already retrieved data from individual tables, and we can view orders from the orders table in the same way. Practice this again if you need to, but with this table structure and primary/foreign key relationships, we can retrieve data from related tables together.

Let's say completed orders need to go to the despatch team for packing and postage. They look at the orders table, and know what products to pick and package, *but where do they send it*? 

One option could be to duplicate the customer details from the customer table to the orders table when they place an order. Why would this not be ideal?

The key reasons are:
- Data duplication is inefficient and wastes space on disk.
- If the data changes it needs to be changed in multiple locations. If the data doesn't match in different locations how would you know which one is accurate?

Instead we want to retrieve the current customer contact details from the most up to date source, i.e. the customer table. We can do this because there is a relationship between the tables in our *relational database*.

The following SQL statement will retrieve the customer's first and last name for a particular record in the orders table, even though this data is not stored in the orders table. 

```sql
SELECT customers.first_name, customers.last_name
FROM orders
JOIN customers ON orders.customer_id = customers.customer_id
WHERE orders.order_id = 201;
```

### Joins

JOIN operations combine rows from two or more tables based on a related column. In our example both tables share the customer_id field, so the query:
1. Starts with the orders table and finds the row with order_id 201.
2. It then uses the customer_id from that row to find the corresponding row in the customers table.
3. Finally, it selects the first_name and last_name from the customers table and returns it as the result.

### Aliases

Review the previous SQL statement again, notice how many times the words *customer* and *orders* are used? It's not unusual for SQL statements to become tricky for humans to read accurately, especially as you start to have many similarly named tables, and you spend 8 hours per day staring at them (if you pursue a DB Admin career path)!

Aliases allow you to define a more convenient or readable name for your tables which can be used elsewhere in your statements.

```sql
SELECT c.first_name, c.last_name
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
WHERE o.order_id = 201;
```

### Join Types

There are three common types of joins:

- INNER - An *Inner* join returns results from both tables which match the query condition. Our example above is an Inner join, using JOIN or INNER JOIN will both create this type of query.

- FULL (OUTER) - A Full or Outer join returns results from both tables, even where results from one table doesn't match the condition. E.g.

|Student    |Course |Score  |
|-----------|------ |-------|
|Ant        |AWS    |Null   |
|Jess       |AWS    |90     |
|Richard    |AWS    |92     |
|Ant        |AZ     |89     |
|Jess       |AZ     |Null   |
|Richard    |AZ     |93     |

Let's say we wanted to know the exam scores for three students for the AWS and AZ exams. With an Inner Join we would only get results for Jess because she has done both tests. With an Outer Join we can retrieve results with a NULL value.

- LEFT (OUTER) JOIN - Behaves like the Full Join, but it can only retrieve *none-matching* records from the left table, the table on the right's records must match the query condition.

- RIGHT (OUTER) JOIN - As above, but the table on the right can return unmatched records, and the left must meet the query.

<img src="img/joins.jpg" width="600" />

### Transactions

Another key feature of SQL databases is support for transactions. 
A transaction is a sequence of operations performed as a single logical unit of work.

To understand the concept, consider most common transactions we rely upon each day - electronic payments. Money needs to be deducted from one account, and deposited in another - if either step fails, they should both fail, and be rolled back.

Transactions must adhere to the following ACID properties:
- Atomicity: Ensures that all operations within a transaction are completed successfully. If any operation fails, the entire transaction is rolled back.
- Consistency: Guarantees that a transaction transforms the database from one valid state to another.
- Isolation: Ensures that concurrent transactions do not interfere with each other.
- Durability: Ensures that once a transaction is committed, its changes are permanently stored.

**Don’t worry about the commands or syntax for transactions, at our level just appreciate that these types of operations are traditionally one of the key features, and benefits of SQL databases.**