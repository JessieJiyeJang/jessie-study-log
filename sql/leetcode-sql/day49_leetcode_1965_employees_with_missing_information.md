## 🧠 LeetCode – Employees With Missing Information  
🔗 https://leetcode.com/problems/employees-with-missing-information

### 📌 Problem Summary  
You're given two tables: `Employees` (with names) and `Salaries` (with salaries).  
Your task is to find the `employee_id`s of employees who have missing information.  
- Missing name → exists in `Salaries` but not in `Employees`  
- Missing salary → exists in `Employees` but not in `Salaries`  
Return the result ordered by `employee_id`.

### 💡 SQL Concepts Used  
- `FULL JOIN` to combine both tables and detect missing values on either side  
- `COALESCE()` to ensure `employee_id` is always selected from either table  
- `IS NULL` conditions to detect missing data  
- `ORDER BY` to format final result  

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
    SELECT 
      COALESCE(e.employee_id, s.employee_id) AS employee_id
    FROM Employees e
    FULL JOIN Salaries s ON e.employee_id = s.employee_id
    WHERE e.name IS NULL OR s.salary IS NULL
    ORDER BY employee_id;
```
### 💬 What I Learned  
- `FULL JOIN` is useful when you want to identify unmatched records on both sides of a relationship.  
- `COALESCE()` returns the first non-null value, which is handy when IDs can come from either side.  
- It's crucial to think about nullability when detecting "missing" information in joined data.  

### 🛠️ Room for Improvement  
- If working with very large tables, consider indexes on `employee_id` to optimize the join.  
- Alternatively, use `UNION` of two `LEFT JOIN ... IS NULL` queries for improved portability to SQL engines that don’t support `FULL JOIN`.
