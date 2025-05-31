## 🧠 LeetCode – Sales Person  
🔗 [Problem Link](https://leetcode.com/problems/sales-person)

### 📌 Problem Summary  
You're given three tables: `SalesPerson`, `Company`, and `Orders`.  
Find the names of all salespeople **who did not have any orders with the company named "RED"**.

### 💡 SQL Concepts Used  
- `LEFT JOIN`: to link salesperson with their orders (if any)  
- `NOT IN`: to exclude salespeople who have sold to the company named 'RED'  
- `JOIN`: to link orders to company names  
- Optional: `COALESCE`, `CTE` for modular query structure

### ✅ My Solution (PostgreSQL with CTE)
```sql
WITH orders_table AS (
    SELECT s.sales_id, s.name, COALESCE(o.com_id,0) AS com_id
    FROM SalesPerson s 
    LEFT JOIN Orders o ON s.sales_id = o.sales_id
),
complete_table AS (
    SELECT ss.sales_id, ss.name, ss.com_id, COALESCE(c.name,'none') AS color
    FROM orders_table ss
    LEFT JOIN Company c ON ss.com_id = c.com_id
)
SELECT name
FROM complete_table
WHERE sales_id NOT IN (
    SELECT sales_id
    FROM complete_table
    WHERE color = 'RED'
)
GROUP BY name;
```

### 💬 What I Learned  
- CTEs (`WITH`) can help break down a complex filtering query into manageable steps.  
- `COALESCE` is useful to handle NULL values, but may not always be needed.  
- I also learned that this problem can be solved in a **simpler way without CTEs** by directly joining `Orders` and `Company`.

### 🔄 Alternative Solution Without CTE
```sql
SELECT name
FROM SalesPerson
WHERE sales_id NOT IN (
    SELECT o.sales_id
    FROM Orders o
    JOIN Company c ON o.com_id = c.com_id
    WHERE c.name = 'RED'
);
```
