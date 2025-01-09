# Practical 6
## Working with Multiple Tables

We need to create tables which are joined, and it is unlikely that your sample tables will be suitable for this. They may be, but only if you have one field which contains values from the other's primary key, which they can be joined upon. Although you may be able to tweak your table schemas to accomplish this.

This is a short task for you to either create the sample tables provided, or tweak your own tables to make them suitable for joining.

### Objectives

- Option 1

    - Create joined tables using the sample SQL statements below and practice using SELECT against the tables.

- Option 2

    - Tweak your existing tables so that they have a duplicate field that can link one to another. A couple of examples: 
        - You have a table of pizzas and each pizza type has a unique ID. Another table for orders contains a field which references the ID of pizzas being ordered. 
        - You have one table for students, and another for courses with unique ID's. A field in the students table references the courses they're taking from the other. Or the other way around, each course includes the student IDs of those enrolled.
    
    If using your own tables you'll have to reference the statements below, and adapt them for your table names and fields to create the FOREIGN KEY relationships.

### Sample Tables

Create tables with suitable PRIMARY KEYS, and create FOREIGN KEYS to link the tables.

NOTICE: Not every table needs a FOREIGN KEY, and one table can have multiple FOREIGN KEYs:

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

Populate the tables, but take a moment to ensure that you understand the schema and structure of the data in the new orders table i.e. it contains the customer_id of the person making the order from the customers table, and the product_id of the product being ordered, from the products table.

To ensure that you understand the schema, expand the following examples to add more records to your tables:

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
    (101, 'Ryzen 7 Laptop', 1299.99),
    (102, 'iPhone 14', 799.99),
    (103, '27" Monitor', 199.99);

-- Insert records into the orders table
INSERT INTO orders (order_id, customer_id, product_id, order_date, order_quantity)
VALUES
    (201, 1, 101, '2023-11-22', 2),
    (202, 2, 102, '2023-11-23', 1),
    (203, 3, 103, '2023-11-24', 3);
```

At this point if you have two or three joined tables, with no errors, that's great. If you have any time left practice querying these individual tables, in our next task we'll look at the syntax for querying multiple tables at once.