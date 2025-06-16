## 🧠 LeetCode – Products Ordered in February 2020  
🔗 [Problem Link](https://leetcode.com/problems/products-ordered-in-february-2020)

### 📌 Problem Summary  
You are given two tables: `Products` and `Orders`.  
Find the `product_name` and total units ordered for **products that had at least 100 units ordered in February 2020**.

### 💡 SQL Concepts Used  
- `WITH` (CTE): to simplify and isolate the filtered & aggregated data  
- `BETWEEN`: for date range filtering  
- `SUM()`, `GROUP BY`: to aggregate units by product  
- `JOIN`: to connect product_id to product_name

### ✅ My Solution (PostgreSQL)
```sql
WITH order_numbers AS (
    SELECT product_id, SUM(unit) AS unit
    FROM orders
    WHERE order_date BETWEEN DATE '2020-02-01' AND DATE '2020-02-29'
    GROUP BY product_id
)
SELECT p.product_name, ord.unit
FROM products p
JOIN order_numbers ord ON p.product_id = ord.product_id
WHERE ord.unit >= 100;
```

### 💬 What I Learned  
- `WITH` helps break down complex queries and improves readability.  
- Filtering by month using `BETWEEN` on `DATE` columns ensures precise targeting.  
- Use `SUM()` and `GROUP BY` to aggregate values before filtering on the result.  
- A `JOIN` brings descriptive columns like `product_name` into the final result.

