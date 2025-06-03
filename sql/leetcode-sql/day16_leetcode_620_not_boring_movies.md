## 🧠 LeetCode – Not Boring Movies  
🔗 [Problem Link](https://leetcode.com/problems/not-boring-movies)

### 📌 Problem Summary  
You're given a table `Cinema` with movie information.  
Return all movies where:
- The `id` is **odd**, and  
- The `description` is **not** equal to `'boring'`  

The result should be ordered by **rating in descending order**.

### 💡 SQL Concepts Used  
- `WHERE` with modulo (`%`) to filter odd-numbered rows  
- `!=` to exclude rows with a certain text  
- `ORDER BY DESC` to sort from highest to lowest  
- Optional: `LOWER()` can be used for case-insensitive text comparison

### ✅ My Solution (PostgreSQL)
```sql
SELECT id, movie, description, rating
FROM Cinema
WHERE id % 2 != 0 AND description != 'boring'
ORDER BY rating DESC;
```

### 💬 What I Learned  
- `% 2 != 0` is a common way to filter for odd-numbered values.  
- Filtering string values with `!=` is case-sensitive in PostgreSQL.  
- Ordering by `rating DESC` lets us prioritize higher-rated movies first.  
- `MOD()` can also be used instead of `%` for better readability and cross-DB compatibility.
