## 🧠 LeetCode – Employees Earning More Than Their Managers  
🔗 [Problem Link](https://leetcode.com/problems/employees-earning-more-than-their-managers)

### 📌 Problem Summary  
You are given a table `Employee` with the following columns: `id`, `name`, `salary`, and `managerId`.  
The task is to find the names of employees who earn **more than their managers**.

### 💡 SQL Concepts Used  
- `JOIN`: to compare each employee’s salary with their manager's  
- `ON`: to match `managerId` in the employee row with the `id` of another employee (the manager)  
- `WHERE`: to filter only those cases where the employee earns more than their manager

### ✅ My Solution  
```sql
SELECT e.name AS Employee
FROM Employee e
JOIN Employee m ON e.managerId = m.id
WHERE e.salary > m.salary;
```
### 💬 What I Learned
- Self-joins are useful when comparing values within the same table, such as an employee and their manager.
- Using meaningful table aliases (e for employee, m for manager) improves query readability.
- Filtering logic with WHERE lets us target specific conditions after a successful join.

