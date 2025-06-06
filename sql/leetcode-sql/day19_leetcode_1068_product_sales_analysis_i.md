## 🧠 LeetCode – Product Sales Analysis I  
🔗 [Problem Link](https://leetcode.com/problems/product-sales-analysis-i)

### 📌 Problem Summary  
You're given two tables: `Sales` and `Product`.  
Return the `product_name`, `year`, and `price` of every sale from the `Sales` table.  
You can obtain the product name by joining with the `Product` table on `product_id`.

### 💡 SQL Concepts Used  
- `JOIN`: to combine sales data with product details using `product_id`  
- Table aliases: used to keep query concise (`s` for `Sales`, `p` for `Product`)  
- Column selection: only relevant fields are returned  
- No sorting required, as per problem statement

### ✅ My Solution (PostgreSQL)
```sql
SELECT 
  p.product_name, 
  s.year, 
  s.price
FROM Sales s
JOIN Product p ON s.product_id = p.product_id;
```

### 💬 What I Learned  
- Foreign keys let us join multiple tables and access meaningful data (like product names).  
- Using table aliases like `s` and `p` can make queries more readable.  
- Always double-check if the problem requires specific sorting — this one doesn’t!

