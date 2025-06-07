## 🧠 LeetCode – Average Experience Per Project  
🔗 [Problem Link](https://leetcode.com/problems/average-experience-of-each-project)

### 📌 Problem Summary  
You're given two tables: `Project` and `Employee`.  
Each row in `Project` shows that a particular employee is working on a specific project.  
Each row in `Employee` shows the experience (in years) of an employee.  
Return the average experience years (rounded to 2 decimal places) **per project**.

### 💡 SQL Concepts Used  
- `JOIN`: to link employee data with project data using `employee_id`  
- `AVG()`: to calculate the mean value of a group  
- `ROUND(..., 2)`: to round the average to 2 decimal places  
- `GROUP BY`: to calculate average per `project_id`  
- `ORDER BY`: optional, improves result readability

### ✅ My Solution (PostgreSQL)
```sql
SELECT 
  p.project_id, 
  ROUND(AVG(e.experience_years), 2) AS average_years
FROM Project p
JOIN Employee e ON p.employee_id = e.employee_id
GROUP BY p.project_id
ORDER BY p.project_id;
```

### 💬 What I Learned  
- Joining related tables helps enrich the result with more detailed information.  
- `AVG()` can be combined with `ROUND()` to control numeric precision.  
- Grouping by a foreign key like `project_id` allows for per-group aggregations.  
- Clear aliasing (like `p`, `e`) and formatting makes SQL easier to read and debug.
