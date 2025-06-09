## 🧠 LeetCode – Daily Active Users  
🔗 [Problem Link](https://leetcode.com/problems/daily-active-users)

### 📌 Problem Summary  
You're given a table `Activity` showing user interactions on a social platform.  
Return the number of **active users per day** during the **30-day period ending 2019-07-27**.  
A user is considered active on a day if they performed **at least one activity** on that date.

### 💡 SQL Concepts Used  
- `BETWEEN` with `INTERVAL`: to filter dates within a 30-day window  
- `COUNT(DISTINCT user_id)`: to count unique users per day  
- `GROUP BY`: to aggregate by day  
- `ORDER BY`: to display results chronologically (optional but useful)

### ✅ My Solution (PostgreSQL)
```sql
SELECT 
  activity_date AS day, 
  COUNT(DISTINCT user_id) AS active_users
FROM Activity
WHERE activity_date BETWEEN DATE '2019-07-27' - INTERVAL '29 days' AND DATE '2019-07-27'
GROUP BY activity_date
ORDER BY day;
```

### 💬 What I Learned  
- You can dynamically define date ranges using `INTERVAL` in PostgreSQL.  
- `COUNT(DISTINCT ...)` is useful to remove duplicate activity entries.  
- Renaming columns (`AS day`) helps match the desired output format.  
- Sorting by day improves readability for time-based reports.

+
## 🧠 PostgreSQL Date Interval – Explained

### 💡 What Does `INTERVAL '29 days'` Mean?

In PostgreSQL, `INTERVAL` is used to represent a **duration or time interval**.

#### 🔍 Breakdown:

| Expression                              | Meaning |
|-----------------------------------------|---------|
| `DATE '2019-07-27'`                     | Casts the string as a DATE type |
| `INTERVAL '29 days'`                    | Represents a time interval of 29 days |
| `DATE '2019-07-27' - INTERVAL '29 days'`| Subtracts 29 days from the given date |
| `BETWEEN ... AND DATE '2019-07-27'`     | Filters the date range between 2019-06-28 and 2019-07-27 |

This makes the query dynamic and easy to maintain for different date ranges.

### 🧪 Common INTERVAL Examples

You can use `INTERVAL` with many units:

| Example                        | Meaning           |
|-------------------------------|--------------------|
| `INTERVAL '1 day'`            | 1 day              |
| `INTERVAL '2 hours'`          | 2 hours            |
| `INTERVAL '30 minutes'`       | 30 minutes         |
| `INTERVAL '1 month'`          | 1 month (not always 30 days) |
| `INTERVAL '1 year'`           | 1 year             |
| `INTERVAL '1 day 3 hours'`    | 1 day and 3 hours  |

### ✅ Summary

Using `INTERVAL` lets you manipulate dates dynamically without hardcoding them, which is especially useful for filtering date ranges in SQL queries.
