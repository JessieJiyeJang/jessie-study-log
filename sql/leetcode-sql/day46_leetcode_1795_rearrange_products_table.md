## 🧠 LeetCode – Rearrange Products Table  
🔗 https://leetcode.com/problems/rearrange-products-table

### 📌 Problem Summary  
You're given a table `Products` that shows prices of each product in 3 different stores (`store1`, `store2`, `store3`).  
If a product is not available in a store, the value is `NULL`.  
Your task is to unpivot this data into a row-wise format, showing one row per product-store-price combination.  
Skip entries where the price is `NULL`.  

### 💡 SQL Concepts Used  
- `UNION ALL` to stack row sets from different columns  
- `IS NOT NULL` to filter out unavailable products  
- String literals to indicate store names  
- Column aliasing (`AS`) for uniform output  
- Optional `ORDER BY` to format results  

### ✅ My Final Solution (PostgreSQL-compatible)
```sql

    SELECT product_id, 'store1' AS store, store1 AS price
    FROM Products
    WHERE store1 IS NOT NULL

    UNION ALL

    SELECT product_id, 'store2' AS store, store2 AS price
    FROM Products
    WHERE store2 IS NOT NULL

    UNION ALL

    SELECT product_id, 'store3' AS store, store3 AS price
    FROM Products
    WHERE store3 IS NOT NULL

    ORDER BY store;
```

### 💬 What I Learned  
- This is a classic “unpivoting” transformation — turning columns into rows.  
- `UNION ALL` is handy for restructuring wide tables into long format.  
- Always filter out `NULL`s to avoid incorrect entries in the result.  

### 🛠️ Room for Improvement  
- If the number of store columns increases, the query becomes repetitive.  
  For a scalable solution, a lateral join or `UNNEST`-style method (in other SQL dialects) would be better.  
- In PostgreSQL 14+, you could explore `UNION ALL` via `VALUES` + `JOIN` for more dynamic pivots.
