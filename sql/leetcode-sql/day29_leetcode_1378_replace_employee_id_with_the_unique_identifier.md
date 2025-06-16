## 🧠 LeetCode – Employee Unique ID Mapping  
🔗 [Problem Link](https://leetcode.com/problems/employees-with-unique-id)

### 📌 Problem Summary  
You're given two tables:
- `Employees`: Contains employee IDs and names  
- `EmployeeUNI`: Contains a mapping between employee IDs and unique IDs  

Return each employee’s `unique_id` and `name`.  
If an employee doesn't have a unique ID, show `null`.

### 💡 SQL Concepts Used  
- `LEFT JOIN`: Ensures all employees are included, even if they have no unique ID  
- Alias for readability  
- Simple projection for desired output columns

### ✅ My Solution (MySQL)
```sql
SELECT u.unique_id, e.name
FROM Employees e
LEFT JOIN EmployeeUNI u ON e.id = u.id;
```

### 💬 What I Learned  
- `LEFT JOIN` is key when the left table is required to be fully preserved  
- Columns not matched on the right table return `NULL`, which is exactly what the problem needs  
- The order of columns in `SELECT` matters when aligning to expected output
