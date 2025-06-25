## 🧠 LeetCode – Invalid Tweets  
🔗 https://leetcode.com/problems/invalid-tweets

### 📌 Problem Summary  
You're given a `Tweets` table with `tweet_id` and `content`.  
A tweet is **invalid** if its content exceeds **15 characters**.  
Return the `tweet_id`s of those invalid tweets.

### 💡 SQL Concepts Used  
- `LENGTH()` to measure the number of characters in a string  
- `WHERE` clause to filter based on length condition  
- No `JOIN` or `ORDER BY` needed, since return order is flexible

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
SELECT  
  tweet_id  
FROM Tweets  
WHERE LENGTH(content) > 15;
```

### 💬 What I Learned  
- `LENGTH()` counts all characters including spaces and punctuation.  
- Always read carefully if the condition is "greater than" (`>`) or "greater than or equal to" (`>=`).  
- SQL string functions are essential for validating or filtering content-based rules.

