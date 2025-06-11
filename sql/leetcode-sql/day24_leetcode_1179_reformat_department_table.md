
## 🧠 LeetCode – Department Monthly Revenue Pivot  
🔗 [Problem Link](https://leetcode.com/problems/reformat-department-table)

### 📌 Problem Summary  
You're given a table `Department` with monthly revenue for each department.  
Reformat the data so that each department has **one row**, with **a column per month** named like `Jan_Revenue`, `Feb_Revenue`, etc.

### 💡 SQL Concepts Used  
- `FILTER (WHERE ...)`: used for conditional aggregation in PostgreSQL  
- `SUM()`: used to aggregate revenue per department per month  
- `GROUP BY`: to pivot data on department ID  
- Pivoting via conditional aggregation

### ✅ My Solution (PostgreSQL)
```sql
SELECT id, 
    SUM(revenue) FILTER (WHERE month = 'Jan') AS Jan_Revenue,
    SUM(revenue) FILTER (WHERE month = 'Feb') AS Feb_Revenue,
    SUM(revenue) FILTER (WHERE month = 'Mar') AS Mar_Revenue,
    SUM(revenue) FILTER (WHERE month = 'Apr') AS Apr_Revenue,
    SUM(revenue) FILTER (WHERE month = 'May') AS May_Revenue,
    SUM(revenue) FILTER (WHERE month = 'Jun') AS Jun_Revenue,
    SUM(revenue) FILTER (WHERE month = 'Jul') AS Jul_Revenue,
    SUM(revenue) FILTER (WHERE month = 'Aug') AS Aug_Revenue,
    SUM(revenue) FILTER (WHERE month = 'Sep') AS Sep_Revenue,
    SUM(revenue) FILTER (WHERE month = 'Oct') AS Oct_Revenue,
    SUM(revenue) FILTER (WHERE month = 'Nov') AS Nov_Revenue,
    SUM(revenue) FILTER (WHERE month = 'Dec') AS Dec_Revenue
FROM Department
GROUP BY id;
```

### 💬 What I Learned  
- `FILTER(WHERE ...)` lets you perform column-level pivots elegantly in PostgreSQL.  
- It's important to use `GROUP BY` to aggregate rows per entity (department in this case).  
- `SUM()` is safe for aggregation when each `(id, month)` pair is unique.  
- Pivoting with SQL is possible even without using `PIVOT` keyword by conditional aggregation.

