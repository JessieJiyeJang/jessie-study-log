## 🧠 LeetCode – Average Time of Process per Machine  
🔗 https://leetcode.com/problems/average-time-of-process-per-machine

### 📌 Problem Summary  
You're given a table `Activity` containing `start` and `end` timestamps for processes run on machines.  
Return the `machine_id` and average time it takes to complete a process on each machine (rounded to 3 decimals).  

### 💡 SQL Concepts Used  
- `WITH` clause (CTE) for preprocessing time per process  
- `CASE WHEN` to negate start timestamps  
- `SUM()` and `COUNT()` to compute average time  
- `ROUND(..., 3)` for formatting to 3 decimals  
- `GROUP BY` to calculate per-machine stats  

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
WITH Activity_processing_time AS (
  SELECT 
    machine_id, 
    process_id,
    SUM(CASE WHEN activity_type = 'start' THEN timestamp * -1 ELSE timestamp END) AS total_time
  FROM Activity
  GROUP BY machine_id, process_id
)
SELECT 
  machine_id, 
  ROUND(SUM(total_time)::NUMERIC / COUNT(process_id), 3) AS processing_time
FROM Activity_processing_time
GROUP BY machine_id
ORDER BY machine_id;
```

### 💬 What I Learned  
- You can preprocess `start` and `end` times as negatives/positives to calculate differences cleanly.  
- A Common Table Expression (CTE) helps modularize sub-logic before doing aggregation.  
- Using `ROUND(..., 3)` is essential to match result formatting exactly.  

### 🛠️ Room for Improvement  
This query is correct and readable, but in PostgreSQL you can simplify it further by using the `FILTER` clause instead of `CASE WHEN`, which improves both **clarity** and **conciseness**.  
