# Practical 4
## Using SELECT Statements

This task introduces the SELECT statement, but you need some tables to query. Hopefully you have your create tables statements saved, so you can quickly recreate them if necessary.

### Objectives 

1. Create tables
2. Add records
3. Write SELECT statements

### Sample code

You may use the following sample code, but try to expand and tweak it.

1. Create tables. 

Create a customers table:

```sql
CREATE TABLE customers (
	customer_ID INT NOT NULL PRIMARY KEY,
	first_name VARCHAR(30),
	last_name VARCHAR(30),
	age INT UNSIGNED NOT NULL
);
```
Create a products table:

```sql
CREATE TABLE products (
    product_id INT NOT NULL PRIMARY KEY,
    product_name VARCHAR(100),
    product_price DECIMAL(10,2)
);
```

2. Add records to each table.

Populate the customers table:

```sql
INSERT INTO customers (customer_id, first_name, last_name, age)
VALUES
    (5, 'Frankie', 'Foy', 5),
	(6, 'Scout', 'Foy', 2),
	(7, 'John', 'McClane', 53);
```

Populate the products table:

```sql
INSERT INTO products (product_id, product_name, product_price)
VALUES
    (101, 'Ryzen 7 Laptop', 999.99),
    (102, 'iPhone 13', 599.99),
	(103, '27" Monitor', 199.99);
```

3. Try running SELECT statements against each table.

```sql
SELECT * 
FROM products
WHERE product_price < 600;
```

```sql
SELECT * 
FROM customers
WHERE last_name = 'Foy';
```