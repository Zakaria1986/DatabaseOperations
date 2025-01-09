# Practical 7
## Querying Joined Tables

This practical task relies upon the tables and relationships created in the previous one. If you have made changes since that point you may wish to return to it. 

If you're using the provided sample statements, you can try the below sample queries, alternatively you should adapt these to match your own schemas.

```sql
SELECT customers.first_name, customers.last_name
FROM orders
JOIN customers ON orders.customer_id = customers.customer_id
WHERE orders.order_id = 201;
```