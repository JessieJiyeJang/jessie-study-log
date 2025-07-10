## 🧠 LeetCode – Number of Unique Subjects Taught by Each Teacher
🔗 https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher
### 📌 Problem Summary
You're given a table
`Teacher
` that lists which teacher teaches which subject in which
department.
The combination
`(subject
_
id, dept
_
id)` is unique, meaning the same subject can be taught in
multiple departments.
Your task is to find the **number of unique subjects** each teacher teaches, regardless of
department.
### 💡 SQL Concepts Used
-
`COUNT(DISTINCT ...)` to eliminate duplicate subjects per teacher
-
`GROUP BY` to aggregate per
`teacher
id`
_
-
`ORDER BY` for clean output formatting
### ✅ My Final Solution (PostgreSQL-compatible)
```
sql
SELECT teacher
FROM Teacher
GROUP BY teacher
_
ORDER BY teacher
_
id
id ASC;
_
id, COUNT(DISTINCT subject
_
id) AS cnt
```
### 💬 What I Learned
-
`DISTINCT` inside aggregate functions like
`COUNT()` helps remove logical duplicates.
- Even if a subject is taught in multiple departments, we only count it once per teacher.
-
`GROUP BY`
with aggregates is a common pattern in counting tasks.
### 🛠 Room for Improvement
- You could omit `ORDER BY` if the problem doesn’t require sorted output.
- If subject uniqueness rules change in the schema, the logic here may need adjustment (e.g.,
using
`(teacher
_
id, subject
_
id)`
uniqueness directly).