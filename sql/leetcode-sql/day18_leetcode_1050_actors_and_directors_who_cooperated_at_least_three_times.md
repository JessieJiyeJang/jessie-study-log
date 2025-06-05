## 🧠 LeetCode – Actor and Director Cooperation  
🔗 [Problem Link](https://leetcode.com/problems/actor-and-director-cooperation)

### 📌 Problem Summary  
You are given a table `ActorDirector` with actor–director cooperation logs.  
Return the `(actor_id, director_id)` pairs where the actor and director have cooperated **at least three times**.

### 💡 SQL Concepts Used  
- `GROUP BY`: to group records by actor–director pair  
- `COUNT(*)`: to count the number of times each pair has worked together  
- `WHERE` (in outer query): to filter only those pairs with 3 or more cooperations  
- Subquery with alias: used to isolate grouped values

### ✅ My Solution (PostgreSQL)
```sql
SELECT actor_id, director_id
FROM (
  SELECT actor_id, director_id, COUNT(*) AS cooperation_count
  FROM ActorDirector
  GROUP BY actor_id, director_id
) AS grouped
WHERE cooperation_count >= 3;
```

### 💬 What I Learned  
- Always give aliases to aggregated columns if you want to reference them later.  
- A subquery must have a table alias in SQL.  
- Grouping by multiple columns helps summarize pair-based data (like actor–director collaborations).  
- Use `COUNT(*)` instead of `COUNT(column)` when you're simply counting rows.

