# Practical 5
## Advanced SELECT Statements



### Objectives

1. If necessary recreate your tables and records from previous Practical task.

2. Against your tables practice using comparison operators.

    Use each of the following comparison operators:

    |Comparison         |Syntax |
    |-------------------|-------|
    |Equal              |=      |
    |Not equal          |!=     |
    |Greater            |>      |
    |Greater or equal   |>=     |
    |Less               |<      |
    |Less or equal      |<=     |

3. Against your tables practice string pattern matching.

    Use each of the following string pattern matching options:

    |Pattern                    |Syntax        |
    |---------------------------|--------------|
    |Strings starting with 'abc'|'abc%'        |
    |Strings ending with 'abc'  |'%abc'        |
    |'abc' within the string    |'%abc%'       |
    |Exactly X characters long  |'___' (3 here)|
    |_ can be any character     |'a_c'         |


4. Use the ORDER BY clause to:
    - Sort your records
    - Sort the results of a query.

5. Use DELETE to remove some records.


Try to use LIKE or NOT LIKE against strings in your tables, along with the following pattern matching clauses:



### Sample Statements

1. (See previous tasks)

2. 
```sql
SELECT * 
FROM products
WHERE product_price < 600;
```
3. 
```sql
SELECT * 
FROM customers
WHERE last_name 
LIKE 'Fo%';
```
4. 
    - 
    ```sql
    SELECT * FROM customers
    ORDER BY first_name;
    ```
    - 
    ```sql
    SELECT * FROM customers
    WHERE age < 10
    ORDER BY first_name;
    ```
5. 
```sql
DELETE FROM customers WHERE first_name LIKE 'John';
```