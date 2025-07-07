## 🧠 LeetCode – Last Logins in 2020  
🔗 https://leetcode.com/problems/latest-login-in-2020

### 📌 Problem Summary  
You're given a `Logins` table with user login timestamps.  
Your task is to return the **latest login** in the **year 2020** for each user.  
Only include users who logged in at least once in 2020.  

### 💡 SQL Concepts Used  
- `WITH` clause to structure pre-filtered login data  
- `MAX()` with `FILTER` to selectively aggregate within a specific date range  
- `GROUP BY` to find latest login per user  
- `WHERE ... IS NOT NULL` to exclude users who didn’t log in during 2020  

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
    WITH last_logins AS (
        SELECT user_id, 
               MAX(time_stamp) FILTER (
                   WHERE time_stamp >= '2020-01-01' AND time_stamp < '2021-01-01'
               ) AS last_stamp
        FROM Logins
        GROUP BY user_id
    )
    
    SELECT user_id, last_stamp
    FROM last_logins
    WHERE last_stamp IS NOT NULL;
```
### 💬 What I Learned  
- PostgreSQL's `FILTER` clause can simplify conditional aggregation in a clean and readable way.  
- Filtering inside `MAX()` avoids the need for a separate `WHERE` clause or subquery.  
- Always handle NULLs when filtering for partial data — especially in time-sensitive queries.  

### 🛠️ Room for Improvement  
- For compatibility with other SQL engines, you might use a subquery with `WHERE` and `GROUP BY` instead of `FILTER`.  
- Adding `ORDER BY user_id` can improve readability of the result table, though not required by the problem.
