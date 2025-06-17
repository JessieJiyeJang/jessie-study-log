## 🚗 LeetCode – Users' Travelled Distances  
🔗 [Problem Link](https://leetcode.com/problems/users-travelled-distance)

### 📌 Problem Summary  
Given a list of users and a list of their rides, report how far each user has traveled.

If a user has no rides, their traveled distance should be 0.  
Sort by `travelled_distance DESC`, and if tied, by `name ASC`.

### ✅ SQL Concepts Used  
- `LEFT JOIN`: to include users with no ride records  
- `COALESCE`: to return 0 if SUM is NULL  
- `GROUP BY`: to aggregate by user  
- `ORDER BY`: to sort results properly

### 💡 Solution (MySQL/PostgreSQL)
```sql
SELECT 
    users.name, 
    COALESCE(SUM(rides.distance), 0) AS travelled_distance
FROM users
LEFT JOIN rides ON users.id = rides.user_id
GROUP BY users.id, users.name
ORDER BY travelled_distance DESC, users.name ASC;
```

### 💬 What I Learned  
- Always use `LEFT JOIN` when we want to include rows with no matches  
- `COALESCE(SUM(...), 0)` is essential to handle NULLs in aggregation  
- Grouping by `id` + `name` is safer than `name` alone due to possible duplicates

