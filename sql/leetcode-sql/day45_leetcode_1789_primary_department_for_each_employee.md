## 🧠 LeetCode – Primary Department for Each Employee  
🔗 https://leetcode.com/problems/primary-department-for-each-employee

### 📌 Problem Summary  
You're given a table `Employee` where each employee may belong to multiple departments.  
The column `primary_flag` tells you whether that department is marked as their primary one (`'Y'` or `'N'`).  
If an employee has only one department, it is their default primary even if marked as `'N'`.  
Your task is to return the primary department for each employee.

### 💡 SQL Concepts Used  
- `WITH` clause to count departments per employee  
- `JOIN` to match department count to employee records  
- `UNION` to combine two conditions: single department OR primary marked  
- Conditional filtering using `COUNT()` and `primary_flag`  
- `ORDER BY` for stable output formatting  

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
    WITH department_counts AS (
        SELECT employee_id, COUNT(department_id) AS ds_count
        FROM Employee
        GROUP BY employee_id
    )
    
    SELECT e.employee_id, e.department_id
    FROM Employee e
    JOIN department_counts d ON e.employee_id = d.employee_id
    WHERE d.ds_count = 1
    
    UNION
    
    SELECT e.employee_id, e.department_id
    FROM Employee e
    JOIN department_counts d ON e.employee_id = d.employee_id
    WHERE d.ds_count > 1 AND e.primary_flag = 'Y'
    
    ORDER BY employee_id ASC;
```

### 💬 What I Learned  
- When combining multiple filtering criteria, breaking it into separate queries and `UNION`ing them helps clarity.  
- Using a CTE (`WITH`) allows you to calculate counts once and reuse them cleanly.  
- Just because a flag is `'N'` doesn’t mean it’s not primary — context matters (e.g., when it's the only department).

### 🛠️ Room for Improvement  
- This query is readable and logically structured, but you could also solve it with a `RANK()` or `ROW_NUMBER()` window function instead of `UNION`.  
- Depending on database size, ensuring appropriate indexing on `employee_id` can help performance.
