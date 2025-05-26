## 🧠 LeetCode – Employee Bonus  
🔗 [Problem Link](https://leetcode.com/problems/employee-bonus)

### 📌 Problem Summary  
You are given two tables: `Employee` and `Bonus`.  
The task is to report the name and bonus amount of each employee whose bonus is **less than 1000** or **not given at all** (i.e. NULL).

### 💡 SQL Concepts Used  
- `LEFT JOIN`: to include all employees, even if they have no bonus entry  
- `WHERE`: to filter rows based on the bonus value  
- `IS NULL`: to include employees with no bonus data  
- **Alias**: to simplify and clarify table references

### ✅ My Solution (PostgreSQL with Alias)
```sql
SELECT e.name, b.bonus
FROM Employee e
LEFT JOIN Bonus b ON e.empId = b.empId
WHERE b.bonus < 1000 OR b.bonus IS NULL;
```
### 💬 What I Learned  
- Using `LEFT JOIN` ensures that all employees are included, even those with no bonus.  
- Filtering for both `bonus < 1000` and `bonus IS NULL` ensures accurate results. 
- Using table aliases (`e`,` b`) makes the query more readable and concise, especially for longer queries or when using multiple joins.
