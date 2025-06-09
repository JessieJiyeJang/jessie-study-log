## 🧠 LeetCode – Product Sold in First Quarter  
🔗 [Problem Link](https://leetcode.com/problems/product-sold-in-first-quarter)
### 📌 Problem Summary  
You're given a `Product` table and a `Sales` table.  
Return all products that were sold **only during Q1 2019**  
(i.e., from 2019-01-01 to 2019-03-31 **inclusive**)  
Products that were sold **outside** this time range should be excluded.
### 💡 SQL Concepts Used  
- `JOIN` not needed since only `product_id` link is required  
- `GROUP BY` with `HAVING` for checking all sale dates fall within a range  
- `MIN()` and `MAX()` to check if all sale records for a product are within Q1  
- `DATE 'YYYY-MM-DD'` is a clean and efficient way to express date literals in PostgreSQL
### ✅ My Solution (PostgreSQL)
```sql
SELECT p.product_id, p.product_name
FROM Product p
WHERE p.product_id IN (
    SELECT s.product_id
    FROM Sales s
    GROUP BY s.product_id
    HAVING
        MIN(s.sale_date) >= DATE '2019-01-01' AND
        MAX(s.sale_date) <= DATE '2019-03-31'
);
```
### 💬 What I Learned  
- Using `HAVING MIN(date) >= ... AND MAX(date) <= ...` is a clean trick to filter rows strictly within a range.  
- `NOT IN (...) AND IN (...)` can be refactored more clearly using one subquery with a `HAVING` clause.  
- PostgreSQL allows direct use of `DATE` literals, which improves clarity and avoids `TO_DATE()` noise.