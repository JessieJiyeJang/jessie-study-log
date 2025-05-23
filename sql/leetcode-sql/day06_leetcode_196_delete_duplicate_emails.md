## 🧠 LeetCode – Delete Duplicate Emails  
🔗 [Problem Link](https://leetcode.com/problems/delete-duplicate-emails)

### 📌 Problem Summary  
You are given a table `Person` with columns `id` and `email`.  
Each row represents an email entry, and some emails are duplicated.  
The goal is to **delete all duplicate emails**, keeping only the one with the **smallest id**.

### 💡 SQL Concepts Used  
- `GROUP BY`: to group duplicate emails  
- `MIN()`: to find the smallest id per email  
- `DELETE`: to remove rows from a table  
- `NOT IN`: to keep only specific ids and delete the rest

### ✅ My Solution  
```sql
DELETE FROM Person
WHERE id NOT IN (
    SELECT MIN(id)
    FROM Person
    GROUP BY email
);

```
### 💬 What I Learned
- You can combine `DELETE` with a subquery to remove specific rows.
- `NOT IN` is useful when you want to exclude a list of values.
- `GROUP BY` + `MIN(id)` lets you find which row to keep among duplicates.
