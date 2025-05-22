## 🧠 LeetCode – Customers Who Never Order  
🔗 [Problem Link](https://leetcode.com/problems/customers-who-never-order)

### 📌 Problem Summary  
You are given two tables: `Customers` and `Orders`.  
Each customer has a unique `id` and may or may not have placed any orders.  
The task is to **find all customers who never placed any orders**.

### 💡 SQL Concepts Used  
- `LEFT JOIN`: to keep all records from the `Customers` table even if there's no match in `Orders`  
- `ON`: to match customer IDs between both tables  
- `WHERE ... IS NULL`: to filter customers with no corresponding records in the `Orders` table

### ✅ My Solution  
```sql
SELECT customers.name AS Customers
FROM customers
LEFT JOIN orders ON customers.id = orders.customerId
WHERE orders.customerId IS NULL;
```
### 💬 What I Learned
- `LEFT JOIN` is useful when you want to include unmatched records from the left table.
- Filtering with `IS NULL` helps identify records without matches in the right table.
- This is a common pattern to find “non-matching” entries across two related tables.
