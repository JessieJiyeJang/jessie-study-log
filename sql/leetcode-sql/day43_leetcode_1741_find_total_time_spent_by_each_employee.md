## 🧠 LeetCode – Total Time Spent by Each Employee  
🔗 https://leetcode.com/problems/total-time-spent-by-each-employee/

### 📌 Problem Summary  
The `Employees` table tracks each time an employee enters and exits the office.  
Each row represents a single entry and exit with the following columns:  
- `emp_id`: employee identifier  
- `event_day`: date of the entry/exit  
- `in_time` and `out_time`: minutes in a day (1–1440)  
Employees may enter/exit multiple times in a day.  
Return each employee’s total time spent in the office **per day**.

---

### 💡 SQL Concepts Used  
- `SUM()` to add up total minutes spent  
- Simple arithmetic (`out_time - in_time`) to compute session duration  
- `GROUP BY` to aggregate time spent by each employee on each day  
- Column aliasing to rename `event_day` as `day`

---

### ✅ My Final Solution (MySQL)
```sql
# Write your MySQL query statement below
SELECT 
  event_day AS day, 
  emp_id, 
  SUM(out_time - in_time) AS total_time
FROM Employees
GROUP BY event_day, emp_id;
```

---

### 💬 What I Learned  
- Using basic arithmetic and aggregation makes this query simple and efficient.  
- Aliasing column names (e.g., `event_day AS day`) is useful for clarity and matching expected output.  
- Always remember that multiple events per day must be summed correctly.

---

### 🛠️ Room for Improvement  
- This query is already optimal for the current structure.  
- In cases where `in_time` and `out_time` are not guaranteed valid, validation may be required.  
- You could sort the output with `ORDER BY day, emp_id` for consistent ordering if required.

---

### 📈 Time & Space Complexity
- Time Complexity: **O(n log n)** due to `GROUP BY` (assuming index scan on `event_day`, `emp_id`)  
- Space Complexity: **O(n)** to store intermediate grouped results
