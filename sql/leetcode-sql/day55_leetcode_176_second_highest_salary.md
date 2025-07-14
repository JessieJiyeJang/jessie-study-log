## 🧠 LeetCode – Second Highest Salary  
🔗 https://leetcode.com/problems/second-highest-salary

### 📌 Problem Summary  
You're given a table `Employee` with each employee's salary.  
Your task is to return the **second highest distinct salary** in the table.  
If no such salary exists (e.g. only one or all salaries are the same), return `NULL`.  

### 💡 SQL Concepts Used  
- `WITH` clause (CTE) to pre-select top N salaries  
- `DISTINCT` to eliminate duplicate salary values  
- `ORDER BY` and `LIMIT` to get the top 2 unique salaries  
- `CASE WHEN` to return the second highest only if it exists  
- `MIN()` to retrieve the lower of the top 2 salaries  

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
    WITH second_highest AS (
        SELECT DISTINCT salary
        FROM Employee
        ORDER BY salary DESC
        LIMIT 2
    )
    
    SELECT 
        CASE 
            WHEN COUNT(salary) = 2 THEN MIN(salary) 
            ELSE NULL
        END AS SecondHighestSalary
    FROM second_highest;
```
### 💬 What I Learned  
- Use `LIMIT` after `ORDER BY` to extract top-N records.  
- When ranking or filtering top results, remember to handle ties with `DISTINCT`.  
- `MIN()` is useful in 2-row subqueries to grab the lower (i.e. second-highest) value cleanly.  

### 🛠️ Room for Improvement  
- Alternatively, a `DENSE_RANK()` window function could be used if row-by-row access is needed.  
- For large datasets, consider using an index on the `salary` column to optimize `ORDER BY`.
