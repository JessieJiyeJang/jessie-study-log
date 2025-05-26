## 🧠 LeetCode – Rising Temperature  
🔗 [Problem Link](https://leetcode.com/problems/rising-temperature)

### 📌 Problem Summary  
You are given a table `Weather` that contains temperature data for each day.  
Your goal is to **find the IDs of all dates where the temperature was higher than the previous day**.

### 💡 SQL Concepts Used  
- `JOIN`: to compare each day's temperature with the previous day  
- `INTERVAL '1 day'`: PostgreSQL syntax for subtracting a day from a `DATE` value  
- `WHERE`: to filter only those days where the temperature increased

### ✅ My Solution (PostgreSQL)
```sql
SELECT b.id AS id
FROM weather b
JOIN weather a ON a.recordDate = b.recordDate - INTERVAL '1 day'
WHERE b.temperature > a.temperature;

```

### 💬 What I Learned  
-  In PostgreSQL, use `recordDate - INTERVAL '1 day'` to subtract one day from a date. 
- In MySQL, use `DATE_SUB(recordDate, INTERVAL 1 DAY)` or `recordDate - INTERVAL 1 DAY` for the same effect. 
- Self-joins are useful when comparing data across rows (e.g., today vs. yesterday).
- Date-based comparison is essential for detecting trends in time-series datasets.
