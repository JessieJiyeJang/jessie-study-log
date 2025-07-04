## 🧠 LeetCode – Calculate Special Bonus  
🔗 https://leetcode.com/problems/calculate-special-bonus

### 📌 Problem Summary  
You're given a table `Employees` with each employee's ID, name, and salary.  
The bonus rule is:  
- If the `employee_id` is **odd** **and** the `name` does **not start with 'M'**, the bonus is **100% of their salary**  
- Otherwise, the bonus is **0**  
Return a table with each employee's ID and their bonus, ordered by `employee_id`.

### 💡 SQL Concepts Used  
- `CASE WHEN` for conditional logic  
- Regular expression match (`~*`) to check if the name starts with `'M'`  
- Modulo operator (`%`) to check if the ID is odd  
- `ORDER BY` to sort results  

### ✅ My Final Solution (PostgreSQL-compatible)
```sql
    SELECT employee_id,
        CASE 
            WHEN name ~* '^m' OR employee_id % 2 = 0 THEN 0
            ELSE salary
        END AS bonus
    FROM Employees
    ORDER BY employee_id;
```
### 💬 What I Learned  
- PostgreSQL's `~*` allows case-insensitive regex matching.  
- `^m` checks if the string **starts** with 'm' or 'M'.  
- Combining multiple conditions inside a `CASE` lets you control output with precision.  

### 🛠️ Room for Improvement  
- You could use `LEFT(name, 1) != 'M'` instead of regex for better readability in some SQL engines.  
- Adding comments to clarify the logic in long `CASE` expressions can help with code maintenance.
