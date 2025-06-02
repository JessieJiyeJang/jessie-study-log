## 🧠 LeetCode – Largest Unique Number  
🔗 [Problem Link](https://leetcode.com/problems/largest-unique-number)

### 📌 Problem Summary  
You're given a table `MyNumbers` containing integers.  
Some numbers may appear multiple times.  
Return the **largest number that appears only once** in the table.  
If no such number exists, return `null`.

### 💡 SQL Concepts Used  
- `GROUP BY`: to group identical numbers  
- `HAVING COUNT(*) = 1`: to find numbers that appear only once  
- `MAX()`: to return the highest value among filtered results  
- Subquery with alias: used to isolate "single" values before applying aggregation

### ✅ My Solution (PostgreSQL)
```sql
SELECT MAX(num) AS num
FROM (
  SELECT num
  FROM MyNumbers
  GROUP BY num
  HAVING COUNT(*) = 1
) AS singles;
```

### 💬 What I Learned  
- `HAVING` is used for filtering groups after aggregation, unlike `WHERE`.  
- Giving a subquery an alias (e.g., `AS singles`) is required in SQL.  
- Using `COUNT(*)` inside `HAVING` helps filter for truly unique values in a grouped result.  
- This pattern is powerful for extracting "max of unique" or "min of frequent" kinds of logic.

