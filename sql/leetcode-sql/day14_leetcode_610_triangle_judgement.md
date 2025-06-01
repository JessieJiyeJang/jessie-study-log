## 🧠 LeetCode – Valid Triangle  
🔗 [Problem Link](https://leetcode.com/problems/valid-triangle-number)

### 📌 Problem Summary  
You're given a table `Triangle` with columns `x`, `y`, and `z`, representing the lengths of three line segments.  
Return whether each set of segments **can form a valid triangle**.  

A set of three lengths can form a triangle **if the sum of any two sides is greater than the third**:  
- `x + y > z`  
- `x + z > y`  
- `y + z > x`

### 💡 SQL Concepts Used  
- `CASE WHEN`: to apply conditional logic and return "Yes" or "No"  
- Logical AND: to combine multiple conditions  
- Alias: to label the result column as `triangle`

### ✅ My Solution (PostgreSQL)
```sql
SELECT 
  x, y, z,
  CASE 
    WHEN x + y > z AND x + z > y AND y + z > x THEN 'Yes'
    ELSE 'No'
  END AS triangle
FROM Triangle;
```

### 💬 What I Learned  
- The triangle inequality theorem can be directly translated into SQL using `CASE WHEN`.  
- `CASE` expressions are powerful tools to apply logic-based labels in result columns.  
- Formatting conditional statements clearly improves readability and maintainability.
