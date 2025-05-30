## 🧠 LeetCode – Classes More Than 5 Students  
🔗 [Problem Link](https://leetcode.com/problems/classes-more-than-5-students)

### 📌 Problem Summary  
You are given a table `Courses` with columns `student` and `class`.  
Each row represents a student enrolled in a class.  
Return the **names of classes** that have **at least five students** enrolled.

### 💡 SQL Concepts Used  
- `GROUP BY`: to aggregate students by class  
- `COUNT()`: to count the number of students per class  
- `HAVING`: to filter groups based on aggregated results  
- Optional: `WITH` (Common Table Expressions) to improve readability in multi-step queries

### ✅ My Solution (PostgreSQL with CTE)
```sql
WITH courses_table AS (
    SELECT COUNT(student) AS number, class
    FROM Courses
    GROUP BY class
)
SELECT class
FROM courses_table
WHERE number >= 5;
```

### 💬 What I Learned  
- `GROUP BY` is essential when counting grouped values like student enrollments per class.  
- `HAVING` is used to filter aggregated data after grouping.  
- `WITH` (CTE) helps with readability, but I also learned that this problem can be solved more simply **without using CTE**.

### 🔄 Alternative Solution Without CTE
```sql
SELECT class
FROM Courses
GROUP BY class
HAVING COUNT(student) >= 5;
```
