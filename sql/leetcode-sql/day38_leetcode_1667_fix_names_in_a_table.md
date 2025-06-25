## 🧠 LeetCode – Capitalize the Title  
🔗 https://leetcode.com/problems/fix-names-in-a-table

### 📌 Problem Summary  
You're given a table `Users` with user names in inconsistent capitalization.  
Return a result where only the **first letter** of each `name` is uppercase and the rest are lowercase.  
Sort the results by `user_id`.

### 💡 SQL Concepts Used  
- `UPPER()` to capitalize the **first character**  
- `LOWER()` to lowercase the rest of the string  
- `LEFT()` and `SUBSTRING()` for string manipulation  
- `||` for string concatenation in PostgreSQL  
- `ORDER BY` to sort results by `user_id`

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
SELECT  
  user_id,  
  UPPER(LEFT(name, 1)) || LOWER(SUBSTRING(name FROM 2)) AS name  
FROM Users  
ORDER BY user_id;
```

### 💬 What I Learned  
- PostgreSQL string functions can be combined to transform text formatting precisely.  
- `||` is used for string concatenation (equivalent to `CONCAT()` in other SQL dialects).  
- Always use `ORDER BY` when the output requires a specific order.

