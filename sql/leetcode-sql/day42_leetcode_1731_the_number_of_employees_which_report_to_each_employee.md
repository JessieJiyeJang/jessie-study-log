## 🧠 LeetCode – The Number of Employees Reporting to Each Manager  
🔗 https://leetcode.com/problems/the-number-of-employees-reporting-to-each-manager/

### 📌 Problem Summary  
Given a table `Employees`, return the list of managers who have at least one direct report.  
For each manager, return:  
- Their `employee_id`  
- Their `name`  
- The number of direct reports they have  
- The average age of those direct reports (rounded to the nearest integer)

Return the result ordered by `employee_id`.

---

### 💡 SQL Concepts Used  
- `JOIN` to relate managers with employees  
- `GROUP BY` on `reports_to` to count and average  
- `ROUND(AVG(...))` to round average age  
- Aliasing to reference manager data in join  
- Filtering only managers who have at least one report (implied by join logic)

---

### ✅ My Final Solution (MySQL)
```sql
SELECT 
  e.reports_to AS employee_id,
  j.name,
  COUNT(e.reports_to) AS reports_count,
  ROUND(AVG(e.age)) AS average_age
FROM Employees e
JOIN Employees j ON e.reports_to = j.employee_id
GROUP BY e.reports_to, j.name
ORDER BY employee_id;
```

---

### 💬 What I Learned  
- Using `JOIN` with the same table (self join) is common for hierarchical structures like employees/managers.  
- Aggregation functions like `COUNT()` and `AVG()` are useful to summarize grouped data.  
- `ROUND()` helps match formatting expectations in the output.  
- Grouping by both `reports_to` and manager `name` ensures consistent results, especially if names are not unique.

---

### 🛠️ Room for Improvement  
- In case there are **managers with no direct reports**, a `LEFT JOIN` with a filter could expose them with zero counts (if required).  
- If names are guaranteed unique, grouping by only `e.reports_to` would suffice.  
- Can create a **view** or CTE if reused frequently in reporting dashboards.

---

### 📈 Time & Space Complexity
- Time Complexity: **O(n log n)** – primarily from grouping and aggregation  
- Space Complexity: **O(n)** – to store intermediate join and aggregation results
