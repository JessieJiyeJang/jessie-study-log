## 🧠 LeetCode – Employees with Missing Manager  
🔗 https://leetcode.com/problems/employees-with-missing-manager

### 📌 Problem Summary  
You're given a table `Employees` with information on employee salaries and their managers.  
Your task is to return the `employee_id`s of employees who:  
- Have a salary strictly less than `$30000`, **and**  
- Have a `manager_id` that does not exist in the table (i.e., the manager left the company)  
Return the result ordered by `employee_id`.

### 💡 SQL Concepts Used  
- `NOT IN` subquery to detect missing foreign keys  
- `DISTINCT` to ensure uniqueness in the subquery result  
- Simple filtering with `WHERE` clause  
- `ORDER BY` for sorted output  

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
    SELECT employee_id
    FROM employees
    WHERE salary < 30000 
      AND manager_id NOT IN (
          SELECT DISTINCT employee_id 
          FROM employees
      )
    ORDER BY employee_id;
```
### 💬 What I Learned  
- When a foreign key references missing data, `NOT IN (subquery)` can be used to detect orphaned rows.  
- Always use `DISTINCT` in subqueries where the outer query expects uniqueness — though here it's mostly for clarity.  
- A manager "leaving" means their row is deleted — but subordinates retain their `manager_id`, which is the core logic.

### 🛠️ Room for Improvement  
- In some SQL engines, using `NOT EXISTS` is more NULL-safe than `NOT IN` — in this problem, it’s safe, but good to be aware.  
- If the table is large, indexing `employee_id` can help with the subquery performance.

