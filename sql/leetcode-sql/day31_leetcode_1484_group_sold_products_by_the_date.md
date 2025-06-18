## 🧠 LeetCode – Number of Sold Products Per Day  
🔗 [Problem Link](https://leetcode.com/problems/sell-different-products)

### 📌 Problem Summary  
Given an `Activities` table with `sell_date` and `product`, return for each date:
- The number of **distinct products** sold  
- A **comma-separated list** of those product names in **lexicographic order**

The result should be sorted by `sell_date`.

### 💡 SQL Concepts Used  
- `WITH` (CTE): to isolate distinct product-date pairs  
- `GROUP BY`: to calculate aggregates per date  
- `STRING_AGG(... ORDER BY ...)`: to combine and sort product names into a single string  
- `COUNT(*)`: to count distinct products per date after duplicates are removed

### ✅ My Solution (PostgreSQL)
```sql
WITH sell_date_products AS (
    SELECT sell_date, product
    FROM Activities 
    GROUP BY sell_date, product
)
SELECT 
    sell_date, 
    COUNT(*) AS num_sold, 
    STRING_AGG(product, ',' ORDER BY product) AS products
FROM sell_date_products
GROUP BY sell_date
ORDER BY sell_date;
```

### 💬 What I Learned  
- Use `GROUP BY` on multiple columns to remove duplicates before aggregation.  
- `STRING_AGG` is perfect for combining strings with custom sort and delimiter.  
- CTEs help keep complex aggregation logic clean and readable.
