## 🧠 LeetCode – Student Exam Attendance Count  
🔗 [Problem Link](https://leetcode.com/problems/students-and-examinations)

### 📌 Problem Summary  
You're given:
- A list of students
- A list of subjects
- An exam log of which student attended which subject exam

Your goal is to **report how many times each student attended each subject exam**,  
even if it's 0 (i.e., a student never attended a subject).

### 💡 SQL Concepts Used  
- `CROSS JOIN`: to generate every possible student–subject pair  
- `LEFT JOIN`: to preserve all combinations even if there's no matching exam record  
- `COUNT()`: to count how many times a student attended each subject  
- `GROUP BY`: to group results by student and subject

### ✅ My Solution (PostgreSQL)
```sql
WITH student_examinations AS (
    SELECT s.student_id, s.student_name, j.subject_name
    FROM Students s
    CROSS JOIN Subjects j
)
SELECT 
    se.student_id,
    se.student_name,
    se.subject_name,
    COUNT(e.subject_name) AS attended_exams
FROM student_examinations se
LEFT JOIN Examinations e 
    ON se.student_id = e.student_id AND se.subject_name = e.subject_name
GROUP BY se.student_id, se.student_name, se.subject_name
ORDER BY se.student_id, se.subject_name;
```

### 💬 What I Learned  
- `CROSS JOIN` is perfect for generating all combinations between two tables.  
- `LEFT JOIN` ensures no data is excluded, even when no matches exist.  
- `COUNT(column)` skips NULLs, which is helpful when counting actual matches.  
- Simplifying `GROUP BY` helps with readability and performance.
